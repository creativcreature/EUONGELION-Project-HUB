# Backup Strategy Documentation

**Document:** 72-backup-strategy-documentation.md
**Generated:** 2026-01-19
**Purpose:** Document Supabase backup procedures, automatic vs manual backups, and recovery processes

---

## Overview

EUONGELION uses Supabase as its database provider. This document outlines what backups are automatic, what should be manual, and how to recover from various failure scenarios.

---

## Supabase Automatic Backups

### Free Tier

| Feature | Availability |
|---------|--------------|
| Daily Backups | Yes (7-day retention) |
| Point-in-Time Recovery | No |
| Backup Frequency | Once per day |
| Manual Download | Via Dashboard |

### Pro Tier ($25/month)

| Feature | Availability |
|---------|--------------|
| Daily Backups | Yes (30-day retention) |
| Point-in-Time Recovery | Yes (up to 7 days) |
| Backup Frequency | Continuous (WAL archiving) |
| Manual Download | Via Dashboard + CLI |

### Enterprise Tier

| Feature | Availability |
|---------|--------------|
| Daily Backups | Configurable retention |
| Point-in-Time Recovery | Yes (configurable) |
| Cross-Region Backups | Available |
| Custom RPO/RTO | Negotiable |

---

## What Supabase Backs Up Automatically

### Included in Automatic Backups

1. **All PostgreSQL Data**
   - All tables in `public` schema
   - All user-created schemas
   - Stored procedures and functions
   - Triggers
   - Views
   - Indexes
   - Constraints

2. **Auth Data**
   - `auth.users` table
   - User sessions
   - Authentication settings

3. **Storage Metadata**
   - Storage bucket configurations
   - File metadata
   - Storage policies

### NOT Included in Automatic Backups

1. **Actual Storage Files**
   - Files stored in Supabase Storage are backed up separately
   - Recommend additional backup for critical files

2. **Edge Functions Code**
   - Functions are stored in your repository
   - Supabase does not backup function source code

3. **Environment Variables/Secrets**
   - API keys, secrets stored outside database
   - Maintain separate secure backup

4. **Real-time Subscriptions State**
   - Active connections not preserved
   - Clients must reconnect after recovery

---

## Manual Backup Procedures

### Method 1: Dashboard Export (Simple)

1. Go to Supabase Dashboard
2. Navigate to **Settings > Database**
3. Click **Download backup**
4. Save the `.dump` file securely

**Limitations:**
- Only available for recent backups
- May timeout for large databases

### Method 2: pg_dump (Recommended for Production)

```bash
# Full database backup
pg_dump -h db.[project-ref].supabase.co \
        -U postgres \
        -d postgres \
        -F c \
        -f backup_$(date +%Y%m%d_%H%M%S).dump

# Schema only (no data)
pg_dump -h db.[project-ref].supabase.co \
        -U postgres \
        -d postgres \
        --schema-only \
        -f schema_$(date +%Y%m%d).sql

# Data only (for specific tables)
pg_dump -h db.[project-ref].supabase.co \
        -U postgres \
        -d postgres \
        --data-only \
        -t public.devotionals \
        -t public.series \
        -f content_$(date +%Y%m%d).sql
```

**Connection String:**
```
postgresql://postgres:[YOUR-PASSWORD]@db.[PROJECT-REF].supabase.co:5432/postgres
```

### Method 3: Supabase CLI

```bash
# Dump local database
supabase db dump -f backup.sql

# Dump remote database
supabase db dump -f backup.sql --linked
```

### Method 4: Automated Backup Script

Create a backup script for scheduled execution:

```bash
#!/bin/bash
# backup_euongelion.sh

# Configuration
SUPABASE_HOST="db.[project-ref].supabase.co"
SUPABASE_USER="postgres"
SUPABASE_DB="postgres"
BACKUP_DIR="/path/to/backups"
RETENTION_DAYS=30

# Create backup directory if needed
mkdir -p "$BACKUP_DIR"

# Create timestamped backup
TIMESTAMP=$(date +%Y%m%d_%H%M%S)
BACKUP_FILE="$BACKUP_DIR/euongelion_$TIMESTAMP.dump"

# Perform backup
PGPASSWORD="$SUPABASE_PASSWORD" pg_dump \
    -h "$SUPABASE_HOST" \
    -U "$SUPABASE_USER" \
    -d "$SUPABASE_DB" \
    -F c \
    -f "$BACKUP_FILE"

# Check if backup succeeded
if [ $? -eq 0 ]; then
    echo "Backup completed: $BACKUP_FILE"

    # Compress backup
    gzip "$BACKUP_FILE"

    # Upload to cloud storage (optional)
    # aws s3 cp "$BACKUP_FILE.gz" s3://your-bucket/backups/
    # gsutil cp "$BACKUP_FILE.gz" gs://your-bucket/backups/

    # Remove old backups
    find "$BACKUP_DIR" -name "euongelion_*.dump.gz" -mtime +$RETENTION_DAYS -delete

    echo "Backup process complete"
else
    echo "ERROR: Backup failed!"
    exit 1
fi
```

Schedule with cron:
```bash
# Run backup daily at 2 AM
0 2 * * * /path/to/backup_euongelion.sh >> /var/log/euongelion_backup.log 2>&1
```

---

## EUONGELION Backup Strategy

### Recommended Backup Schedule

| Data Type | Frequency | Retention | Method |
|-----------|-----------|-----------|--------|
| Full Database | Daily | 30 days | Automatic (Supabase) |
| Content (series, devotionals) | After changes | Indefinite | Manual pg_dump |
| User Data | Daily | 30 days | Automatic (Supabase) |
| Soul Audit Questions | After changes | Indefinite | Version control |
| Schema | After migrations | Indefinite | Version control |

### Backup Categories

#### 1. Content Backup (High Value, Low Change)

```bash
# Backup content tables specifically
pg_dump -h db.[ref].supabase.co \
        -U postgres \
        -d postgres \
        --data-only \
        -t public.series \
        -t public.devotionals \
        -t public.soul_audit_questions \
        -f content_backup_$(date +%Y%m%d).sql
```

**When:** After any content changes, before deployments
**Why:** Devotional content represents significant creative investment

#### 2. User Data Backup (High Value, High Change)

Covered by Supabase automatic daily backups. For additional protection:

```bash
# Backup user-related tables
pg_dump -h db.[ref].supabase.co \
        -U postgres \
        -d postgres \
        --data-only \
        -t public.users \
        -t public.user_progress \
        -t public.bookmarks \
        -t public.soul_audit_responses \
        -t public.soul_audit_sessions \
        -f user_data_$(date +%Y%m%d).sql
```

**When:** Daily (covered by Supabase), weekly manual for extra safety
**Why:** User spiritual journey data is irreplaceable

#### 3. Schema Backup (Critical, Low Change)

```bash
# Backup schema only
pg_dump -h db.[ref].supabase.co \
        -U postgres \
        -d postgres \
        --schema-only \
        -f schema_$(date +%Y%m%d).sql
```

**When:** After every migration
**Why:** Schema changes must be reproducible

---

## Recovery Procedures

### Scenario 1: Accidental Data Deletion

**Symptoms:** Users report missing progress, bookmarks, etc.

**Recovery Steps:**

1. **Identify the scope**
   ```sql
   -- Check what's missing
   SELECT COUNT(*) FROM public.user_progress;
   SELECT MAX(created_at) FROM public.bookmarks;
   ```

2. **Check if Point-in-Time Recovery is available (Pro tier)**
   - Contact Supabase support
   - Specify the target recovery time

3. **Restore from backup (if no PITR)**
   ```bash
   # Create temporary restore database
   createdb euongelion_restore

   # Restore backup to temp database
   pg_restore -d euongelion_restore backup_file.dump

   # Extract missing data
   pg_dump -t public.user_progress euongelion_restore | \
       psql -d postgres
   ```

### Scenario 2: Corrupted Migration

**Symptoms:** Application errors after schema change

**Recovery Steps:**

1. **Immediate: Apply rollback script**
   ```bash
   psql -f rollback_migration.sql
   ```

2. **If rollback fails: Restore from backup**
   ```bash
   # Point-in-time recovery (Pro tier)
   # Contact Supabase with timestamp before migration

   # Or restore from dump
   pg_restore -c -d postgres backup_pre_migration.dump
   ```

3. **Re-deploy previous application version**

### Scenario 3: Complete Database Loss

**Symptoms:** All data inaccessible

**Recovery Steps:**

1. **Contact Supabase Support immediately**
   - They have additional backup systems

2. **Restore from latest backup**
   ```bash
   pg_restore -c -d postgres latest_backup.dump
   ```

3. **Re-apply migrations if schema-only restore**
   ```bash
   supabase db push
   ```

4. **Restore data from separate backup**
   ```bash
   psql -f content_backup.sql
   psql -f user_data_backup.sql
   ```

### Scenario 4: Restoring Specific User Data

**Symptoms:** Single user requests data recovery

**Recovery Steps:**

1. **Restore backup to temporary database**
   ```bash
   createdb temp_restore
   pg_restore -d temp_restore backup.dump
   ```

2. **Extract user's data**
   ```sql
   -- Connect to temp_restore
   \c temp_restore

   -- Export user's data
   \copy (SELECT * FROM user_progress WHERE user_id = 'xxx') TO 'user_progress.csv' CSV HEADER;
   \copy (SELECT * FROM bookmarks WHERE user_id = 'xxx') TO 'bookmarks.csv' CSV HEADER;
   \copy (SELECT * FROM soul_audit_responses WHERE user_id = 'xxx') TO 'audit_responses.csv' CSV HEADER;
   ```

3. **Import into production**
   ```sql
   -- Carefully merge data, avoiding duplicates
   INSERT INTO user_progress
   SELECT * FROM temp_table
   ON CONFLICT (user_id, devotional_id) DO NOTHING;
   ```

4. **Cleanup**
   ```bash
   dropdb temp_restore
   ```

---

## Backup Verification

### Monthly Backup Test Procedure

1. **Select a recent backup**
2. **Restore to test environment**
   ```bash
   createdb euongelion_test
   pg_restore -d euongelion_test backup.dump
   ```

3. **Verify data integrity**
   ```sql
   -- Check record counts
   SELECT 'users' as table_name, COUNT(*) FROM users
   UNION ALL
   SELECT 'series', COUNT(*) FROM series
   UNION ALL
   SELECT 'devotionals', COUNT(*) FROM devotionals
   UNION ALL
   SELECT 'user_progress', COUNT(*) FROM user_progress;

   -- Check for orphaned records
   SELECT COUNT(*) FROM user_progress
   WHERE user_id NOT IN (SELECT id FROM users);

   -- Check constraint integrity
   SELECT COUNT(*) FROM devotionals
   WHERE series_id IS NOT NULL
   AND series_id NOT IN (SELECT id FROM series);
   ```

4. **Test application against restored database**
5. **Document results**
6. **Cleanup test environment**

### Backup Integrity Checklist

- [ ] Backup file is not corrupted (can be read)
- [ ] All tables are present
- [ ] Record counts match expected values
- [ ] Foreign key relationships intact
- [ ] RLS policies functional
- [ ] Views return correct data
- [ ] Functions execute properly

---

## Disaster Recovery Plan

### Recovery Time Objective (RTO)

| Scenario | Target RTO |
|----------|------------|
| Minor data loss | 1 hour |
| Major data corruption | 4 hours |
| Complete database loss | 8 hours |
| Regional outage | 24 hours |

### Recovery Point Objective (RPO)

| Plan | RPO |
|------|-----|
| Free Tier | 24 hours (daily backup) |
| Pro Tier | Minutes (PITR) |

### Emergency Contacts

- **Supabase Support:** support@supabase.io
- **Status Page:** https://status.supabase.com
- **Emergency Hotline (Pro):** Available in dashboard

---

## Cloud Storage Backup Integration

### AWS S3 Backup

```bash
# Upload backup to S3
aws s3 cp backup.dump.gz s3://euongelion-backups/database/

# Set lifecycle policy for automatic archival
aws s3api put-bucket-lifecycle-configuration \
    --bucket euongelion-backups \
    --lifecycle-configuration file://lifecycle.json
```

### Google Cloud Storage

```bash
# Upload to GCS
gsutil cp backup.dump.gz gs://euongelion-backups/database/

# Set retention policy
gsutil retention set 30d gs://euongelion-backups/
```

### Backup Encryption

```bash
# Encrypt backup before upload
gpg --symmetric --cipher-algo AES256 backup.dump

# Decrypt when needed
gpg --decrypt backup.dump.gpg > backup.dump
```

---

## Backup Monitoring

### Alerts to Configure

1. **Backup failure alert**
   - Notify if daily backup doesn't complete

2. **Backup size anomaly**
   - Alert if backup is significantly smaller (possible data loss)
   - Alert if backup is significantly larger (possible issue)

3. **Backup age alert**
   - Alert if latest backup is more than 48 hours old

### Monitoring Script

```bash
#!/bin/bash
# check_backup_health.sh

BACKUP_DIR="/path/to/backups"
MAX_AGE_HOURS=48
MIN_SIZE_MB=10

# Check latest backup age
LATEST_BACKUP=$(ls -t "$BACKUP_DIR"/*.dump.gz 2>/dev/null | head -1)

if [ -z "$LATEST_BACKUP" ]; then
    echo "CRITICAL: No backup files found!"
    exit 2
fi

# Check age
AGE_HOURS=$(( ($(date +%s) - $(stat -f %m "$LATEST_BACKUP")) / 3600 ))
if [ $AGE_HOURS -gt $MAX_AGE_HOURS ]; then
    echo "WARNING: Latest backup is $AGE_HOURS hours old"
    exit 1
fi

# Check size
SIZE_MB=$(( $(stat -f %z "$LATEST_BACKUP") / 1048576 ))
if [ $SIZE_MB -lt $MIN_SIZE_MB ]; then
    echo "WARNING: Backup size ($SIZE_MB MB) is unusually small"
    exit 1
fi

echo "OK: Backup is $AGE_HOURS hours old, $SIZE_MB MB"
exit 0
```

---

## Summary

### Automatic (Supabase Handles)
- Daily database backups
- Point-in-time recovery (Pro tier)
- Infrastructure redundancy

### Manual (Team Responsibility)
- Content backups after changes
- Pre-migration backups
- Backup verification testing
- Off-site backup copies
- Environment variables/secrets

### Key Recommendations

1. **Upgrade to Pro tier** for point-in-time recovery
2. **Automate weekly off-site backups** to cloud storage
3. **Test backup restoration monthly**
4. **Document recovery procedures** for the team
5. **Monitor backup health** with alerts

---

*This backup strategy was generated as part of the EUONGELION overnight database documentation process.*

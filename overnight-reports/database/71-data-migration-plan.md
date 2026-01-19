# Data Migration Plan

**Document:** 71-data-migration-plan.md
**Generated:** 2026-01-19
**Purpose:** Document safe database migration procedures for schema changes

---

## Overview

This document provides procedures for safely modifying the EUONGELION database schema in Supabase. It covers adding columns, changing data types, migrating data, and handling common schema evolution scenarios.

---

## Migration Philosophy

### Principles

1. **Non-destructive First** - Always prefer additive changes over destructive ones
2. **Backwards Compatible** - New schema should work with existing application code
3. **Test in Staging** - Always test migrations in a staging environment first
4. **Backup Before Migrating** - Take a backup before any production migration
5. **Atomic Migrations** - Keep migrations small and focused
6. **Document Everything** - Record what changed and why

### Migration Workflow

```
1. Design change
2. Write migration SQL
3. Test in development
4. Backup staging database
5. Apply to staging
6. Test application against staging
7. Backup production database
8. Apply to production
9. Verify application functionality
10. Update TypeScript types
```

---

## Supabase Migration Tools

### Option 1: Supabase CLI (Recommended)

```bash
# Create a new migration
supabase migration new migration_name

# Apply migrations locally
supabase db push

# Check migration status
supabase db diff

# Reset local database
supabase db reset
```

### Option 2: Dashboard SQL Editor

1. Go to Supabase Dashboard
2. Navigate to SQL Editor
3. Write and execute SQL
4. Note: Does not track migration history automatically

### Option 3: Direct Connection

```bash
# Connect via psql
psql postgresql://postgres:[password]@db.[project-ref].supabase.co:5432/postgres

# Run migration file
\i path/to/migration.sql
```

---

## Common Migration Scenarios

### 1. Adding a New Column

**Scenario:** Add a `timezone` column to the `users` table

**Safe Migration:**

```sql
-- Migration: add_user_timezone
-- Description: Add timezone preference to users table
-- Date: 2026-XX-XX

-- Step 1: Add column with default value (non-blocking)
ALTER TABLE public.users
ADD COLUMN IF NOT EXISTS timezone TEXT DEFAULT 'UTC';

-- Step 2: Add check constraint if needed
ALTER TABLE public.users
ADD CONSTRAINT check_valid_timezone
CHECK (timezone ~ '^[A-Za-z]+/[A-Za-z_]+$' OR timezone = 'UTC');

-- Step 3: Update TypeScript types (separate file)
-- Add: timezone: string; to User interface
```

**Rollback:**

```sql
-- Rollback: remove_user_timezone
ALTER TABLE public.users
DROP CONSTRAINT IF EXISTS check_valid_timezone;

ALTER TABLE public.users
DROP COLUMN IF EXISTS timezone;
```

---

### 2. Changing Column Data Type

**Scenario:** Change `rating` from INTEGER to DECIMAL for finer granularity

**Safe Migration (with data preservation):**

```sql
-- Migration: change_rating_to_decimal
-- Description: Change rating from INTEGER to DECIMAL(3,1) for half-star ratings

-- Step 1: Create new column
ALTER TABLE public.user_progress
ADD COLUMN rating_new DECIMAL(3,1);

-- Step 2: Migrate data
UPDATE public.user_progress
SET rating_new = rating::DECIMAL(3,1)
WHERE rating IS NOT NULL;

-- Step 3: Add constraint to new column
ALTER TABLE public.user_progress
ADD CONSTRAINT check_rating_range_new
CHECK (rating_new >= 1.0 AND rating_new <= 5.0);

-- Step 4: Swap columns (requires brief downtime or careful timing)
-- Option A: Rename columns (requires app code update simultaneously)
ALTER TABLE public.user_progress
RENAME COLUMN rating TO rating_old;

ALTER TABLE public.user_progress
RENAME COLUMN rating_new TO rating;

-- Option B: Drop old column after app is updated
-- ALTER TABLE public.user_progress DROP COLUMN rating_old;

-- Step 5: Drop old constraint
ALTER TABLE public.user_progress
DROP CONSTRAINT IF EXISTS user_progress_rating_check;
```

**Rollback:**

```sql
-- Rollback: revert_rating_to_integer
ALTER TABLE public.user_progress
RENAME COLUMN rating TO rating_decimal;

ALTER TABLE public.user_progress
RENAME COLUMN rating_old TO rating;

ALTER TABLE public.user_progress
DROP COLUMN rating_decimal;
```

---

### 3. Adding a New Table

**Scenario:** Add a `notifications` table

**Safe Migration:**

```sql
-- Migration: create_notifications_table
-- Description: Add notifications system for user alerts

CREATE TABLE IF NOT EXISTS public.notifications (
    id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    user_id UUID NOT NULL REFERENCES public.users(id) ON DELETE CASCADE,
    type TEXT NOT NULL CHECK (type IN ('devotional_reminder', 'streak_milestone', 'series_complete', 'system')),
    title TEXT NOT NULL,
    body TEXT,
    data JSONB DEFAULT '{}',
    read_at TIMESTAMPTZ,
    created_at TIMESTAMPTZ DEFAULT NOW()
);

-- Create indexes
CREATE INDEX IF NOT EXISTS idx_notifications_user ON public.notifications(user_id);
CREATE INDEX IF NOT EXISTS idx_notifications_unread ON public.notifications(user_id) WHERE read_at IS NULL;
CREATE INDEX IF NOT EXISTS idx_notifications_created ON public.notifications(user_id, created_at DESC);

-- Enable RLS
ALTER TABLE public.notifications ENABLE ROW LEVEL SECURITY;

-- RLS Policies
CREATE POLICY "Users can view own notifications"
    ON public.notifications FOR SELECT USING (auth.uid() = user_id);

CREATE POLICY "Users can update own notifications"
    ON public.notifications FOR UPDATE USING (auth.uid() = user_id);

CREATE POLICY "Users can delete own notifications"
    ON public.notifications FOR DELETE USING (auth.uid() = user_id);

-- System can insert notifications (via service role)
-- No INSERT policy needed for user role

-- Grant permissions
GRANT SELECT, UPDATE, DELETE ON public.notifications TO authenticated;
```

**Rollback:**

```sql
-- Rollback: drop_notifications_table
DROP TABLE IF EXISTS public.notifications;
```

---

### 4. Adding a Foreign Key Relationship

**Scenario:** Link devotionals to recommended follow-up series

**Safe Migration:**

```sql
-- Migration: add_recommended_next_series
-- Description: Add optional link to a recommended follow-up series for devotionals

-- Step 1: Add the foreign key column
ALTER TABLE public.devotionals
ADD COLUMN recommended_next_series_id UUID REFERENCES public.series(id) ON DELETE SET NULL;

-- Step 2: Create index for joins
CREATE INDEX IF NOT EXISTS idx_devotionals_recommended_series
ON public.devotionals(recommended_next_series_id);

-- Step 3: No RLS changes needed (inherits from table policy)
```

**Rollback:**

```sql
-- Rollback: remove_recommended_next_series
DROP INDEX IF EXISTS idx_devotionals_recommended_series;
ALTER TABLE public.devotionals DROP COLUMN recommended_next_series_id;
```

---

### 5. Renaming a Column

**Scenario:** Rename `full_name` to `display_name` in users table

**Safe Migration (requires code update coordination):**

```sql
-- Migration: rename_fullname_to_displayname
-- IMPORTANT: This requires simultaneous application code update
-- Plan a maintenance window or use the two-column approach below

-- Option A: Direct rename (brief disruption)
ALTER TABLE public.users
RENAME COLUMN full_name TO display_name;

-- Option B: Zero-downtime approach
-- Step 1: Add new column
ALTER TABLE public.users ADD COLUMN display_name TEXT;

-- Step 2: Copy data
UPDATE public.users SET display_name = full_name;

-- Step 3: Create trigger to sync during transition
CREATE OR REPLACE FUNCTION sync_name_columns()
RETURNS TRIGGER AS $$
BEGIN
    IF TG_OP = 'INSERT' OR TG_OP = 'UPDATE' THEN
        IF NEW.display_name IS NULL AND NEW.full_name IS NOT NULL THEN
            NEW.display_name = NEW.full_name;
        ELSIF NEW.full_name IS NULL AND NEW.display_name IS NOT NULL THEN
            NEW.full_name = NEW.display_name;
        END IF;
    END IF;
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER sync_names_trigger
BEFORE INSERT OR UPDATE ON public.users
FOR EACH ROW EXECUTE FUNCTION sync_name_columns();

-- Step 4: After app is updated to use display_name only:
-- DROP TRIGGER sync_names_trigger ON public.users;
-- DROP FUNCTION sync_name_columns();
-- ALTER TABLE public.users DROP COLUMN full_name;
```

---

### 6. Adding an Enum Value

**Scenario:** Add 'trial' to subscription_tier

**Safe Migration:**

```sql
-- Migration: add_trial_subscription_tier
-- Description: Add 'trial' tier for 7-day free trial users

-- Note: PostgreSQL enums are tricky to modify
-- Since subscription_tier is a CHECK constraint, not an enum, this is easier:

-- Step 1: Drop the existing constraint
ALTER TABLE public.users
DROP CONSTRAINT IF EXISTS users_subscription_tier_check;

-- Step 2: Add new constraint with additional value
ALTER TABLE public.users
ADD CONSTRAINT users_subscription_tier_check
CHECK (subscription_tier IN ('free', 'premium', 'lifetime', 'trial'));
```

**For actual ENUM types (question_category, question_type):**

```sql
-- Adding to PostgreSQL enum type
ALTER TYPE question_category ADD VALUE 'worship' AFTER 'life_integration';

-- Note: Cannot remove enum values or reorder in PostgreSQL
-- To remove a value, you must recreate the type and migrate data
```

---

### 7. Data Migration (Backfill)

**Scenario:** Populate a new column from existing data

**Safe Migration:**

```sql
-- Migration: backfill_reading_time
-- Description: Calculate reading_time_minutes from content length

-- Step 1: Add column if not exists
ALTER TABLE public.devotionals
ADD COLUMN IF NOT EXISTS reading_time_minutes INTEGER DEFAULT 5;

-- Step 2: Update based on content (assuming ~200 words per minute)
UPDATE public.devotionals
SET reading_time_minutes = GREATEST(
    1,
    CEIL(
        (LENGTH(content) - LENGTH(REPLACE(content, ' ', '')) + 1) / 200.0
    )
)
WHERE reading_time_minutes = 5 OR reading_time_minutes IS NULL;

-- Step 3: Verify
SELECT title, LENGTH(content) as chars, reading_time_minutes
FROM public.devotionals
ORDER BY reading_time_minutes DESC;
```

---

### 8. Modifying RLS Policies

**Scenario:** Allow admins to view all user progress

**Safe Migration:**

```sql
-- Migration: add_admin_progress_policy
-- Description: Allow admin users to view all user progress for analytics

-- Step 1: Create admin check function
CREATE OR REPLACE FUNCTION public.is_admin()
RETURNS BOOLEAN AS $$
BEGIN
    RETURN EXISTS (
        SELECT 1 FROM public.users
        WHERE id = auth.uid()
        AND email LIKE '%@euongelion.com'  -- Or use a role column
    );
END;
$$ LANGUAGE plpgsql SECURITY DEFINER;

-- Step 2: Add admin policy (does not replace user policy)
CREATE POLICY "Admins can view all progress"
    ON public.user_progress
    FOR SELECT
    USING (public.is_admin());

-- Note: Multiple SELECT policies use OR logic
-- Users can view their own OR admins can view all
```

**Rollback:**

```sql
-- Rollback: remove_admin_progress_policy
DROP POLICY IF EXISTS "Admins can view all progress" ON public.user_progress;
DROP FUNCTION IF EXISTS public.is_admin();
```

---

## Migration Best Practices

### Pre-Migration Checklist

- [ ] Migration tested in development
- [ ] Migration tested in staging with production-like data
- [ ] Rollback script prepared and tested
- [ ] Backup completed
- [ ] Application code updated (if required)
- [ ] TypeScript types updated
- [ ] Team notified of migration window
- [ ] Monitoring in place

### During Migration

1. **Set maintenance mode** if migration causes downtime
2. **Monitor error rates** during migration
3. **Check query performance** after migration
4. **Verify RLS policies** still work correctly

### Post-Migration Checklist

- [ ] Application functions correctly
- [ ] All queries return expected results
- [ ] No increase in error rates
- [ ] Performance metrics stable
- [ ] Types match new schema
- [ ] Documentation updated

---

## Handling Large Data Migrations

For tables with millions of rows, use batched updates:

```sql
-- Batched update example
DO $$
DECLARE
    batch_size INT := 10000;
    rows_updated INT;
BEGIN
    LOOP
        WITH batch AS (
            SELECT id FROM public.user_progress
            WHERE new_column IS NULL
            LIMIT batch_size
            FOR UPDATE SKIP LOCKED
        )
        UPDATE public.user_progress up
        SET new_column = calculated_value
        FROM batch
        WHERE up.id = batch.id;

        GET DIAGNOSTICS rows_updated = ROW_COUNT;

        IF rows_updated = 0 THEN
            EXIT;
        END IF;

        RAISE NOTICE 'Updated % rows', rows_updated;
        PERFORM pg_sleep(0.1);  -- Prevent overwhelming the database
    END LOOP;
END $$;
```

---

## Emergency Rollback Procedure

If a migration causes critical issues:

### 1. Assess the Situation
- Is the application down?
- Is data being corrupted?
- Can users still access the service?

### 2. Quick Rollback Steps

```bash
# If using Supabase point-in-time recovery (Pro plan)
# Contact Supabase support for recovery

# If you have a pre-migration backup
pg_restore -d postgres backup_pre_migration.dump

# If you have a rollback script
psql -f rollback_migration.sql
```

### 3. Communicate
- Notify team of rollback
- Update status page
- Document what went wrong

---

## Version Control for Migrations

### File Naming Convention

```
database/migrations/
├── 20260118000001_create_users.sql
├── 20260118000002_create_series.sql
├── 20260118000003_create_devotionals.sql
├── 20260119000001_add_user_timezone.sql
├── 20260119000002_add_notifications.sql
└── ...
```

Format: `YYYYMMDDHHMMSS_description.sql`

### Migration File Template

```sql
-- Migration: YYYYMMDDHHMMSS_description
-- Description: Brief description of what this migration does
-- Author: Name
-- Date: YYYY-MM-DD
--
-- Pre-requisites:
--   - List any required prior migrations
--   - List any required application changes
--
-- Rollback:
--   - See rollback section at bottom of file
--   - Or reference separate rollback file

-- ============================================
-- UP MIGRATION
-- ============================================

-- Your migration SQL here

-- ============================================
-- DOWN MIGRATION (ROLLBACK)
-- ============================================
-- Uncomment and run if rollback needed

-- Your rollback SQL here (commented out)
```

---

## EUONGELION-Specific Migration Considerations

### Tables with User Data
- `users`, `user_progress`, `bookmarks`, `soul_audit_*`
- Always maintain CASCADE DELETE relationships
- Test RLS policies after changes

### Content Tables
- `series`, `devotionals`, `soul_audit_questions`
- Consider SEO impact of slug changes
- Maintain full-text search index on devotionals

### Premium Content
- Any changes to `is_premium` logic require RLS policy review
- Test access for all subscription tiers

### Views
- `user_streaks`, `bookmarks_with_devotionals`, `soul_audit_results`
- Views must be recreated if underlying columns change
- Use `CREATE OR REPLACE VIEW` when possible

---

## Conclusion

Database migrations require careful planning and execution. Always:

1. Test thoroughly before production
2. Have a rollback plan
3. Backup before migrating
4. Coordinate with application code changes
5. Monitor after deployment

For the EUONGELION project, remember that user spiritual data is sensitive - ensure data integrity is maintained throughout any migration process.

---

*This migration plan was generated as part of the EUONGELION overnight database documentation process.*

# Data Retention Policy

**Document:** 73-data-retention-policy.md
**Generated:** 2026-01-19
**Purpose:** Define what user data is stored, retention periods, deletion procedures, and GDPR/privacy considerations

---

## Overview

EUONGELION is a Christian devotional application that collects and processes user data to provide personalized spiritual growth experiences. This policy outlines our data retention practices, user rights, and compliance with privacy regulations including GDPR (EU), CCPA (California), and general privacy best practices.

---

## Data Categories and Retention Periods

### 1. User Account Data

**Table:** `public.users`

| Data Field | Purpose | Retention Period | Legal Basis |
|------------|---------|------------------|-------------|
| `id` | User identification | Account lifetime + 30 days | Contract |
| `email` | Authentication, communication | Account lifetime + 30 days | Contract |
| `full_name` | Personalization | Account lifetime + 30 days | Contract |
| `avatar_url` | Profile display | Account lifetime + 30 days | Contract |
| `subscription_tier` | Access control | Account lifetime + 30 days | Contract |
| `onboarding_completed` | UX flow | Account lifetime | Contract |
| `preferences` | Personalization | Account lifetime | Consent |
| `created_at` | Account management | Account lifetime + 30 days | Legitimate Interest |
| `updated_at` | Audit trail | Account lifetime + 30 days | Legitimate Interest |

**Retention Notes:**
- Account data retained for 30 days after deletion request to allow for recovery
- After 30-day grace period, data is permanently deleted
- Anonymized analytics may be retained indefinitely

---

### 2. User Progress Data

**Table:** `public.user_progress`

| Data Field | Purpose | Retention Period | Legal Basis |
|------------|---------|------------------|-------------|
| `user_id` | Link to user | Account lifetime | Contract |
| `devotional_id` | Track completion | Account lifetime | Contract |
| `completed_at` | Streak calculation | Account lifetime | Contract |
| `notes` | Personal reflection | Account lifetime | Consent |
| `rating` | Feedback, recommendations | Account lifetime | Consent |
| `time_spent_seconds` | Analytics, improvement | Account lifetime | Legitimate Interest |

**Retention Notes:**
- Progress data is considered part of the core service
- Users may export all progress data before deletion
- Aggregate/anonymized progress data may be retained for analytics

---

### 3. Bookmarks Data

**Table:** `public.bookmarks`

| Data Field | Purpose | Retention Period | Legal Basis |
|------------|---------|------------------|-------------|
| `user_id` | Link to user | Account lifetime | Contract |
| `devotional_id` | Saved content | Account lifetime | Contract |
| `collection_name` | Organization | Account lifetime | Contract |
| `notes` | Personal notes | Account lifetime | Consent |

**Retention Notes:**
- Bookmarks are user-curated content
- Exported with user data upon request
- Deleted with account deletion

---

### 4. Soul Audit Data

**Tables:** `public.soul_audit_responses`, `public.soul_audit_sessions`

| Data Field | Purpose | Retention Period | Legal Basis |
|------------|---------|------------------|-------------|
| `response_value` | Assessment answers | Account lifetime | Consent |
| `response_text` | Open-ended responses | Account lifetime | Consent |
| `category_scores` | Personalization | Account lifetime | Consent |
| `recommendations` | Content suggestions | Account lifetime | Consent |
| `session_id` | Group responses | Account lifetime | Contract |

**Special Sensitivity:**
- Soul Audit data reveals spiritual and potentially sensitive personal beliefs
- Treated as **sensitive personal data** under GDPR Article 9
- Explicit consent required before collection
- Additional encryption recommended for this data

**Retention Notes:**
- Users may delete Soul Audit history independently of account
- Historical sessions retained to show spiritual growth over time
- Option to "reset" Soul Audit while keeping account

---

### 5. Authentication Data

**Table:** `auth.users` (Supabase managed)

| Data Field | Purpose | Retention Period | Legal Basis |
|------------|---------|------------------|-------------|
| Email | Authentication | Account lifetime | Contract |
| Password hash | Authentication | Account lifetime | Contract |
| Auth tokens | Session management | Session duration | Contract |
| Last sign in | Security | Account lifetime | Legitimate Interest |

**Retention Notes:**
- Managed by Supabase Auth
- Cascading delete removes `public.users` entry
- Auth logs retained per Supabase policy

---

### 6. Content Data (Non-Personal)

**Tables:** `public.series`, `public.devotionals`, `public.soul_audit_questions`

| Data Type | Retention Period | Notes |
|-----------|------------------|-------|
| Series metadata | Indefinite | Platform content |
| Devotional content | Indefinite | Platform content |
| Assessment questions | Indefinite | Platform content |

**Notes:**
- Not personal data
- Owned by EUONGELION
- Not subject to user deletion requests

---

## User Rights and Procedures

### Right to Access (GDPR Article 15)

**User Action:** Request a copy of all personal data

**Procedure:**

```sql
-- Generate user data export
SELECT
    u.*,
    (SELECT json_agg(up) FROM user_progress up WHERE up.user_id = u.id) as progress,
    (SELECT json_agg(b) FROM bookmarks b WHERE b.user_id = u.id) as bookmarks,
    (SELECT json_agg(s) FROM soul_audit_sessions s WHERE s.user_id = u.id) as audit_sessions,
    (SELECT json_agg(r) FROM soul_audit_responses r WHERE r.user_id = u.id) as audit_responses
FROM users u
WHERE u.id = 'user-uuid-here';
```

**Response Time:** Within 30 days
**Format:** JSON export or PDF report

---

### Right to Rectification (GDPR Article 16)

**User Action:** Correct inaccurate personal data

**Procedure:**
1. User updates profile in app settings
2. For data not editable in app, contact support
3. Support verifies identity and makes corrections

**Fields Editable by User:**
- Full name
- Avatar
- Preferences (theme, notifications, etc.)
- Notes on progress and bookmarks

**Fields Requiring Support:**
- Email (with verification)
- Subscription tier (with payment verification)

---

### Right to Erasure (GDPR Article 17) - "Right to be Forgotten"

**User Action:** Request deletion of all personal data

**Procedure:**

1. **User initiates deletion** (in-app or support request)

2. **Immediate actions:**
   - Revoke all active sessions
   - Mark account for deletion
   - Send confirmation email

3. **Grace period (30 days):**
   - Account disabled but data retained
   - User can cancel deletion and recover account
   - No new data collected

4. **Final deletion:**
   ```sql
   -- This cascades to all user-related tables due to ON DELETE CASCADE
   DELETE FROM auth.users WHERE id = 'user-uuid-here';

   -- Verify deletion
   SELECT EXISTS (SELECT 1 FROM public.users WHERE id = 'user-uuid-here');
   ```

5. **Post-deletion:**
   - Confirmation email sent (to email on file)
   - Log deletion event (anonymized) for compliance

**Exceptions:**
- Legal obligations may require retention
- Anonymized aggregate data may be retained

---

### Right to Data Portability (GDPR Article 20)

**User Action:** Export data in machine-readable format

**Export Format:** JSON

**Data Included:**
```json
{
  "user": {
    "email": "user@example.com",
    "full_name": "John Doe",
    "subscription_tier": "premium",
    "preferences": {...},
    "created_at": "2024-01-01T00:00:00Z"
  },
  "progress": [
    {
      "devotional_title": "You Are Chosen",
      "completed_at": "2024-06-15T08:30:00Z",
      "rating": 5,
      "notes": "This really spoke to me..."
    }
  ],
  "bookmarks": [...],
  "soul_audit_history": [...]
}
```

**Procedure:**
1. User requests export in settings
2. System generates JSON file
3. User downloads within 7 days
4. Link expires after download or 7 days

---

### Right to Restrict Processing (GDPR Article 18)

**User Action:** Request limitation of data processing

**Implementation:**
- Account placed in "restricted" state
- Data retained but not processed
- User cannot use app features
- Data not used for recommendations or analytics

---

### Right to Object (GDPR Article 21)

**User Action:** Object to specific processing activities

**Applicable To:**
- Marketing communications
- Analytics tracking
- Personalized recommendations

**Implementation:**
- User preferences updated
- Processing stopped for objected purposes
- Core service functionality maintained

---

## GDPR Compliance Checklist

### Lawful Basis Documentation

| Processing Activity | Lawful Basis | Documentation |
|--------------------|--------------|---------------|
| Account creation | Contract | Terms of Service |
| Progress tracking | Contract | Terms of Service |
| Email communication | Consent | Opt-in during signup |
| Analytics | Legitimate Interest | Privacy Policy |
| Soul Audit | Explicit Consent | Separate consent screen |
| Marketing | Consent | Opt-in preference |

### Required Documentation

- [x] Privacy Policy (user-facing)
- [x] Data Processing Agreement (if applicable)
- [ ] Records of Processing Activities (Article 30)
- [ ] Data Protection Impact Assessment (for Soul Audit)
- [ ] Consent management system
- [ ] Data breach response procedure

### Technical Measures

- [x] Row Level Security (RLS) on all user tables
- [x] Encrypted database connections (TLS)
- [x] Cascading deletes for data cleanup
- [ ] Data encryption at rest (Supabase handles)
- [ ] Audit logging for data access
- [ ] Automated data retention enforcement

---

## CCPA Compliance (California)

### Categories of Personal Information Collected

1. **Identifiers** - Email, name
2. **Internet Activity** - Progress, preferences
3. **Sensitive Personal Information** - Soul Audit responses (religious beliefs)

### Consumer Rights

| Right | Implementation |
|-------|----------------|
| Right to Know | Data export feature |
| Right to Delete | Account deletion |
| Right to Opt-Out of Sale | We do not sell data |
| Right to Non-Discrimination | No price differences |

### Required Disclosures

- Privacy policy must state: "We do not sell personal information"
- Collection notice at point of collection
- Retention periods disclosed

---

## Data Retention Implementation

### Automated Retention Enforcement

```sql
-- Create scheduled job for data cleanup (example)
-- Run daily to enforce retention policies

-- Delete accounts past grace period
DELETE FROM auth.users
WHERE id IN (
    SELECT id FROM public.users
    WHERE marked_for_deletion = true
    AND deletion_requested_at < NOW() - INTERVAL '30 days'
);

-- Archive old Soul Audit sessions (optional)
-- Move to archive table after 2 years if not accessed
INSERT INTO soul_audit_sessions_archive
SELECT * FROM soul_audit_sessions
WHERE completed_at < NOW() - INTERVAL '2 years'
AND user_id IN (
    SELECT id FROM users WHERE last_active < NOW() - INTERVAL '1 year'
);
```

### Retention Schedule Monitoring

| Check | Frequency | Action |
|-------|-----------|--------|
| Pending deletions | Daily | Process accounts past grace period |
| Inactive accounts | Monthly | Send re-engagement or deletion notice |
| Data export requests | Daily | Generate and send exports |
| Consent expiry | Monthly | Re-request expired consents |

---

## Data Breach Procedures

### Detection

1. Monitor for unauthorized access
2. Audit logs reviewed regularly
3. User reports of suspicious activity

### Response Timeline (GDPR)

| Action | Deadline |
|--------|----------|
| Internal assessment | 24 hours |
| Notify supervisory authority | 72 hours |
| Notify affected users | Without undue delay |
| Document incident | Ongoing |

### Notification Template

```
Subject: Important Security Notice from EUONGELION

Dear [User],

We are writing to inform you of a security incident that may have affected your personal data.

What happened: [Description]
When: [Date/time]
What data was affected: [Specific data types]
What we're doing: [Actions taken]
What you can do: [Recommended actions]

For questions, contact: privacy@euongelion.com

Sincerely,
EUONGELION Team
```

---

## Special Considerations for Religious Data

### GDPR Article 9 - Sensitive Personal Data

Soul Audit data reveals religious beliefs and is classified as sensitive personal data.

**Additional Requirements:**

1. **Explicit Consent Required**
   - Separate consent screen before Soul Audit
   - Cannot be bundled with general terms
   - Must be freely withdrawable

2. **Enhanced Security**
   - Additional encryption layer recommended
   - Limited access to this data
   - Regular security audits

3. **Purpose Limitation**
   - Only used for spiritual growth features
   - Not used for marketing segmentation
   - Not shared with third parties

### Consent Language Example

```
SOUL AUDIT CONSENT

The Soul Audit collects information about your spiritual beliefs and practices.
This is sensitive personal data protected under privacy laws.

By proceeding, you consent to:
- Collection of your responses to spiritual assessment questions
- Storage of your assessment results and scores
- Use of this data to provide personalized content recommendations

You can withdraw this consent at any time by deleting your Soul Audit history
in the app settings. This will not affect your account or other features.

[ ] I consent to the collection and processing of my Soul Audit data

[CONTINUE] [CANCEL]
```

---

## Third-Party Data Sharing

### Current Third Parties

| Service | Data Shared | Purpose | DPA Status |
|---------|-------------|---------|------------|
| Supabase | All data | Database hosting | DPA in place |
| (Payment processor) | Email, name | Subscriptions | DPA required |
| (Email service) | Email | Communications | DPA required |

### Data Sharing Principles

1. **Minimum necessary** - Only share what's required
2. **Contractual protection** - DPA with all processors
3. **User notification** - Disclose in privacy policy
4. **No selling** - We never sell personal data

---

## Policy Review and Updates

| Review Type | Frequency | Responsibility |
|-------------|-----------|----------------|
| Full policy review | Annual | Legal/Privacy team |
| Compliance check | Quarterly | Development team |
| Incident-triggered review | As needed | All stakeholders |

### Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-01-19 | Initial policy |

---

## Summary

### Key Retention Periods

| Data Type | Retention |
|-----------|-----------|
| Account data | Account lifetime + 30 days |
| Progress/bookmarks | Account lifetime |
| Soul Audit data | Account lifetime (explicit consent) |
| Content | Indefinite (not personal data) |

### User Rights

- Access: 30-day response
- Correction: Immediate (in-app) or support
- Deletion: 30-day grace period, then permanent
- Export: JSON format, 7-day download window

### Compliance

- GDPR: Full compliance with enhanced protection for Soul Audit
- CCPA: Full compliance, no sale of personal data
- General: Privacy by design, data minimization

---

*This data retention policy was generated as part of the EUONGELION overnight database documentation process. This document should be reviewed by legal counsel before implementation.*

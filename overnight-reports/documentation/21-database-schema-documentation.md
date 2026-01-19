# EUONGELION Database Schema Documentation

## Overview

EUONGELION uses Supabase (PostgreSQL) as its database, leveraging Row Level Security (RLS) for data protection. The database schema is designed to support a devotional application with user profiles, devotional content, reading progress tracking, bookmarks, and a spiritual assessment feature called "Soul Audit."

---

## Database Tables

### 1. `users` Table

**Purpose:** Stores user profile data that extends Supabase Auth. Automatically populated when a user signs up.

**Location:** `public.users`

| Column | Type | Nullable | Default | Description |
|--------|------|----------|---------|-------------|
| `id` | UUID | NOT NULL | - | Primary key, references `auth.users(id)` |
| `email` | TEXT | NOT NULL | - | User's email address (unique) |
| `full_name` | TEXT | YES | NULL | User's display name |
| `avatar_url` | TEXT | YES | NULL | Profile picture URL |
| `subscription_tier` | TEXT | YES | 'free' | One of: 'free', 'premium', 'lifetime' |
| `onboarding_completed` | BOOLEAN | YES | FALSE | Whether user completed onboarding |
| `preferences` | JSONB | YES | '{}' | User preferences (theme, notifications, etc.) |
| `created_at` | TIMESTAMPTZ | YES | NOW() | Account creation timestamp |
| `updated_at` | TIMESTAMPTZ | YES | NOW() | Last update timestamp |

**Indexes:**
- `idx_users_email` - Email lookups
- `idx_users_subscription` - Subscription tier filtering

**Triggers:**
- `on_auth_user_created` - Auto-creates user profile when auth.users record is inserted
- `update_users_updated_at` - Auto-updates `updated_at` on record changes

**Relationships:**
- References `auth.users(id)` with CASCADE delete

---

### 2. `series` Table

**Purpose:** Stores devotional series (collections of related devotionals).

**Location:** `public.series`

| Column | Type | Nullable | Default | Description |
|--------|------|----------|---------|-------------|
| `id` | UUID | NOT NULL | uuid_generate_v4() | Primary key |
| `name` | TEXT | NOT NULL | - | Series title |
| `slug` | TEXT | NOT NULL | - | URL-friendly identifier (unique) |
| `description` | TEXT | YES | NULL | Full description |
| `short_description` | TEXT | YES | NULL | Brief summary for cards |
| `image_url` | TEXT | YES | NULL | Cover image URL |
| `thumbnail_url` | TEXT | YES | NULL | Thumbnail image URL |
| `devotional_count` | INTEGER | YES | 0 | Number of published devotionals |
| `duration_days` | INTEGER | YES | NULL | Expected completion duration |
| `difficulty_level` | TEXT | YES | 'beginner' | One of: 'beginner', 'intermediate', 'advanced' |
| `tags` | TEXT[] | YES | '{}' | Array of tags for filtering |
| `is_premium` | BOOLEAN | YES | FALSE | Requires premium subscription |
| `is_published` | BOOLEAN | YES | FALSE | Visible to users |
| `is_featured` | BOOLEAN | YES | FALSE | Featured on home page |
| `sort_order` | INTEGER | YES | 0 | Display order |
| `author` | TEXT | YES | NULL | Series author name |
| `created_at` | TIMESTAMPTZ | YES | NOW() | Creation timestamp |
| `updated_at` | TIMESTAMPTZ | YES | NOW() | Last update timestamp |

**Indexes:**
- `idx_series_slug` - Slug lookups
- `idx_series_published` - Published filtering
- `idx_series_featured` - Featured filtering
- `idx_series_premium` - Premium filtering
- `idx_series_sort_order` - Ordering

**Triggers:**
- `update_series_updated_at` - Auto-updates `updated_at`

---

### 3. `devotionals` Table

**Purpose:** Stores individual devotional content.

**Location:** `public.devotionals`

| Column | Type | Nullable | Default | Description |
|--------|------|----------|---------|-------------|
| `id` | UUID | NOT NULL | uuid_generate_v4() | Primary key |
| `series_id` | UUID | YES | NULL | Foreign key to series |
| `title` | TEXT | NOT NULL | - | Devotional title |
| `slug` | TEXT | NOT NULL | - | URL-friendly identifier |
| `subtitle` | TEXT | YES | NULL | Optional subtitle |
| `content` | TEXT | NOT NULL | - | Main content (markdown/plain text) |
| `content_html` | TEXT | YES | NULL | Pre-rendered HTML content |
| `scripture_ref` | TEXT | NOT NULL | - | Scripture reference (e.g., "John 3:16") |
| `scripture_text` | TEXT | YES | NULL | Full scripture passage text |
| `scripture_version` | TEXT | YES | 'ESV' | Bible translation used |
| `day_number` | INTEGER | YES | NULL | Day number within series |
| `reading_time_minutes` | INTEGER | YES | 5 | Estimated reading time |
| `prayer` | TEXT | YES | NULL | Closing prayer text |
| `reflection_questions` | TEXT[] | YES | NULL | Array of reflection questions |
| `action_step` | TEXT | YES | NULL | Practical application step |
| `audio_url` | TEXT | YES | NULL | Audio version URL |
| `image_url` | TEXT | YES | NULL | Featured image URL |
| `tags` | TEXT[] | YES | '{}' | Array of tags |
| `is_premium` | BOOLEAN | YES | FALSE | Requires premium subscription |
| `is_published` | BOOLEAN | YES | FALSE | Visible to users |
| `is_featured` | BOOLEAN | YES | FALSE | Featured on home page |
| `author` | TEXT | YES | NULL | Author name |
| `published_at` | TIMESTAMPTZ | YES | NULL | Publication date |
| `created_at` | TIMESTAMPTZ | YES | NOW() | Creation timestamp |
| `updated_at` | TIMESTAMPTZ | YES | NOW() | Last update timestamp |

**Constraints:**
- `unique_series_day` - Unique combination of `series_id` and `day_number`

**Indexes:**
- `idx_devotionals_series` - Series filtering
- `idx_devotionals_slug` - Slug lookups
- `idx_devotionals_published` - Published filtering
- `idx_devotionals_featured` - Featured filtering
- `idx_devotionals_premium` - Premium filtering
- `idx_devotionals_day_number` - Day number within series
- `idx_devotionals_published_at` - Publication date ordering
- `idx_devotionals_fts` - Full-text search on title and content

**Triggers:**
- `update_devotionals_updated_at` - Auto-updates `updated_at`
- `update_series_count_on_devotional_change` - Updates series `devotional_count` on insert/update/delete

**Relationships:**
- References `series(id)` with SET NULL on delete

---

### 4. `user_progress` Table

**Purpose:** Tracks which devotionals users have completed.

**Location:** `public.user_progress`

| Column | Type | Nullable | Default | Description |
|--------|------|----------|---------|-------------|
| `id` | UUID | NOT NULL | uuid_generate_v4() | Primary key |
| `user_id` | UUID | NOT NULL | - | Foreign key to users |
| `devotional_id` | UUID | NOT NULL | - | Foreign key to devotionals |
| `series_id` | UUID | YES | NULL | Foreign key to series (cached) |
| `completed_at` | TIMESTAMPTZ | YES | NOW() | Completion timestamp |
| `notes` | TEXT | YES | NULL | User's personal notes |
| `rating` | INTEGER | YES | NULL | User rating (1-5) |
| `time_spent_seconds` | INTEGER | YES | NULL | Actual time spent reading |
| `created_at` | TIMESTAMPTZ | YES | NOW() | Creation timestamp |
| `updated_at` | TIMESTAMPTZ | YES | NOW() | Last update timestamp |

**Constraints:**
- `unique_user_devotional` - One progress record per user per devotional

**Indexes:**
- `idx_user_progress_user` - User filtering
- `idx_user_progress_devotional` - Devotional filtering
- `idx_user_progress_series` - Series filtering
- `idx_user_progress_completed` - Completion date ordering

**Triggers:**
- `update_user_progress_updated_at` - Auto-updates `updated_at`

**Relationships:**
- References `users(id)` with CASCADE delete
- References `devotionals(id)` with CASCADE delete
- References `series(id)` with SET NULL on delete

---

### 5. `bookmarks` Table

**Purpose:** Stores user-saved devotionals for quick access.

**Location:** `public.bookmarks`

| Column | Type | Nullable | Default | Description |
|--------|------|----------|---------|-------------|
| `id` | UUID | NOT NULL | uuid_generate_v4() | Primary key |
| `user_id` | UUID | NOT NULL | - | Foreign key to users |
| `devotional_id` | UUID | NOT NULL | - | Foreign key to devotionals |
| `collection_name` | TEXT | YES | 'default' | Folder/collection name |
| `notes` | TEXT | YES | NULL | User's notes about bookmark |
| `created_at` | TIMESTAMPTZ | YES | NOW() | Bookmark creation timestamp |

**Constraints:**
- `unique_user_devotional_bookmark` - One bookmark per user per devotional

**Indexes:**
- `idx_bookmarks_user` - User filtering
- `idx_bookmarks_devotional` - Devotional filtering
- `idx_bookmarks_collection` - Collection filtering
- `idx_bookmarks_created` - Creation date ordering

**Relationships:**
- References `users(id)` with CASCADE delete
- References `devotionals(id)` with CASCADE delete

---

### 6. `soul_audit_questions` Table

**Purpose:** Stores questions for the spiritual assessment feature.

**Location:** `public.soul_audit_questions`

| Column | Type | Nullable | Default | Description |
|--------|------|----------|---------|-------------|
| `id` | UUID | NOT NULL | uuid_generate_v4() | Primary key |
| `question_text` | TEXT | NOT NULL | - | Question content |
| `question_description` | TEXT | YES | NULL | Additional context |
| `category` | question_category | NOT NULL | - | Question category enum |
| `question_type` | question_type | YES | 'scale' | Response type enum |
| `options` | JSONB | YES | NULL | Options for multiple choice |
| `min_value` | INTEGER | YES | 1 | Minimum scale value |
| `max_value` | INTEGER | YES | 10 | Maximum scale value |
| `min_label` | TEXT | YES | 'Strongly Disagree' | Label for minimum |
| `max_label` | TEXT | YES | 'Strongly Agree' | Label for maximum |
| `weight` | DECIMAL(3,2) | YES | 1.0 | Scoring weight |
| `sort_order` | INTEGER | NOT NULL | - | Display order |
| `is_required` | BOOLEAN | YES | TRUE | Whether answer is required |
| `is_active` | BOOLEAN | YES | TRUE | Whether question is active |
| `help_text` | TEXT | YES | NULL | Additional help text |
| `scripture_reference` | TEXT | YES | NULL | Related scripture |
| `created_at` | TIMESTAMPTZ | YES | NOW() | Creation timestamp |
| `updated_at` | TIMESTAMPTZ | YES | NOW() | Last update timestamp |

**Indexes:**
- `idx_soul_audit_questions_category` - Category filtering
- `idx_soul_audit_questions_order` - Ordering
- `idx_soul_audit_questions_active` - Active filtering

**Triggers:**
- `update_soul_audit_questions_updated_at` - Auto-updates `updated_at`

---

### 7. `soul_audit_responses` Table

**Purpose:** Stores user responses to soul audit questions.

**Location:** `public.soul_audit_responses`

| Column | Type | Nullable | Default | Description |
|--------|------|----------|---------|-------------|
| `id` | UUID | NOT NULL | uuid_generate_v4() | Primary key |
| `user_id` | UUID | NOT NULL | - | Foreign key to users |
| `question_id` | UUID | NOT NULL | - | Foreign key to questions |
| `session_id` | UUID | NOT NULL | - | Groups responses in a session |
| `response_value` | INTEGER | YES | NULL | Numeric response |
| `response_text` | TEXT | YES | NULL | Text response |
| `response_json` | JSONB | YES | NULL | Complex response data |
| `created_at` | TIMESTAMPTZ | YES | NOW() | Creation timestamp |
| `updated_at` | TIMESTAMPTZ | YES | NOW() | Last update timestamp |

**Indexes:**
- `idx_soul_audit_responses_user` - User filtering
- `idx_soul_audit_responses_question` - Question filtering
- `idx_soul_audit_responses_session` - Session filtering
- `idx_soul_audit_responses_created` - Creation date ordering

**Triggers:**
- `update_soul_audit_responses_updated_at` - Auto-updates `updated_at`

**Relationships:**
- References `users(id)` with CASCADE delete
- References `soul_audit_questions(id)` with CASCADE delete

---

### 8. `soul_audit_sessions` Table

**Purpose:** Stores soul audit assessment sessions and results.

**Location:** `public.soul_audit_sessions`

| Column | Type | Nullable | Default | Description |
|--------|------|----------|---------|-------------|
| `id` | UUID | NOT NULL | uuid_generate_v4() | Primary key |
| `user_id` | UUID | NOT NULL | - | Foreign key to users |
| `started_at` | TIMESTAMPTZ | YES | NOW() | Session start time |
| `completed_at` | TIMESTAMPTZ | YES | NULL | Session completion time |
| `total_score` | DECIMAL(5,2) | YES | NULL | Overall assessment score |
| `category_scores` | JSONB | YES | NULL | Scores by category |
| `recommendations` | JSONB | YES | NULL | Personalized recommendations |
| `created_at` | TIMESTAMPTZ | YES | NOW() | Creation timestamp |

**Indexes:**
- `idx_soul_audit_sessions_user` - User filtering
- `idx_soul_audit_sessions_completed` - Completion date ordering

**Relationships:**
- References `users(id)` with CASCADE delete

---

## Custom Enums

### `question_category`

Categories for soul audit questions:
- `faith_foundation`
- `prayer_life`
- `scripture_engagement`
- `community`
- `service`
- `spiritual_disciplines`
- `heart_condition`
- `life_integration`

### `question_type`

Response types for questions:
- `scale` - Numeric rating (typically 1-10)
- `multiple_choice` - Select from options
- `text` - Free text response
- `yes_no` - Binary choice
- `frequency` - Never/Rarely/Sometimes/Often/Always

---

## Database Views

### `user_streaks`

**Purpose:** Calculates consecutive day streaks for users.

**Columns:**
- `user_id` - User identifier
- `streak_start` - Start date of streak
- `streak_end` - End date of streak
- `streak_length` - Number of consecutive days

### `bookmarks_with_devotionals`

**Purpose:** Joins bookmarks with devotional details for easy retrieval.

**Columns:**
- `id` - Bookmark ID
- `user_id` - User identifier
- `devotional_id` - Devotional identifier
- `collection_name` - Bookmark collection
- `bookmark_notes` - User's notes
- `bookmarked_at` - Bookmark creation time
- `title` - Devotional title
- `subtitle` - Devotional subtitle
- `scripture_ref` - Scripture reference
- `image_url` - Devotional image
- `reading_time_minutes` - Reading time
- `series_name` - Series name
- `series_slug` - Series slug

### `soul_audit_results`

**Purpose:** Aggregates soul audit session data with responses.

**Columns:**
- `session_id` - Session identifier
- `user_id` - User identifier
- `completed_at` - Completion timestamp
- `total_score` - Overall score
- `category_scores` - Scores by category (JSONB)
- `recommendations` - Recommendations (JSONB)
- `total_responses` - Number of responses
- `responses` - Detailed responses (JSON array)

---

## Database Functions

### `handle_new_user()`

**Purpose:** Automatically creates a user profile when a new auth user is created.

**Trigger:** `on_auth_user_created` on `auth.users`

**Logic:**
1. Extracts user metadata from auth record
2. Creates corresponding `public.users` record
3. Copies email, full_name, and avatar_url from auth metadata

### `update_updated_at_column()`

**Purpose:** Generic function to set `updated_at` to current timestamp.

**Used by:** Multiple triggers across tables

### `update_series_devotional_count()`

**Purpose:** Keeps series `devotional_count` in sync with actual published devotionals.

**Trigger:** `update_series_count_on_devotional_change` on `devotionals`

**Logic:**
- On INSERT/UPDATE: Counts published devotionals for the series
- On DELETE: Recalculates count for the affected series

---

## Entity Relationship Diagram

```
+------------------+      +------------------+      +------------------+
|   auth.users     |      |      users       |      |     series       |
+------------------+      +------------------+      +------------------+
| id (PK)          |<---->| id (PK, FK)      |      | id (PK)          |
| email            |      | email            |      | name             |
| ...              |      | full_name        |      | slug (UNIQUE)    |
+------------------+      | subscription_tier|      | description      |
                          | preferences      |      | devotional_count |
                          +------------------+      | is_published     |
                                 |                  +------------------+
                                 |                         |
          +----------------------+----------------------+  |
          |                      |                      |  |
          v                      v                      v  v
+------------------+   +------------------+   +------------------+
|  user_progress   |   |    bookmarks     |   |   devotionals    |
+------------------+   +------------------+   +------------------+
| id (PK)          |   | id (PK)          |   | id (PK)          |
| user_id (FK)     |   | user_id (FK)     |   | series_id (FK)   |
| devotional_id(FK)|   | devotional_id(FK)|   | title            |
| series_id (FK)   |   | collection_name  |   | content          |
| completed_at     |   | notes            |   | scripture_ref    |
| notes            |   | created_at       |   | is_published     |
| rating           |   +------------------+   +------------------+
+------------------+

+------------------+   +------------------+   +------------------+
| soul_audit_      |   | soul_audit_      |   | soul_audit_      |
| questions        |   | responses        |   | sessions         |
+------------------+   +------------------+   +------------------+
| id (PK)          |<--| question_id (FK) |   | id (PK)          |
| category         |   | user_id (FK)     |-->| user_id (FK)     |
| question_text    |   | session_id       |-->| total_score      |
| question_type    |   | response_value   |   | category_scores  |
| weight           |   +------------------+   | recommendations  |
+------------------+                          +------------------+
```

---

## TypeScript Type Definitions

The database types are defined in `/database/types.ts` and provide full TypeScript support:

```typescript
// Example usage with Supabase client
import type { Database } from '@/database/types';

const supabase = createClient<Database>(url, key);

// Fully typed queries
const { data, error } = await supabase
  .from('devotionals')
  .select('*')
  .eq('is_published', true);

// Type inference
type Devotional = Database['public']['Tables']['devotionals']['Row'];
type UserInsert = Database['public']['Tables']['users']['Insert'];
```

---

## Best Practices

1. **Always use RLS**: Never bypass RLS unless using service_role key for admin operations
2. **Use transactions**: For operations that modify multiple tables
3. **Index foreign keys**: All foreign key columns have indexes
4. **Use JSONB for flexible data**: Preferences, scores, and recommendations use JSONB
5. **Soft deletes for content**: Consider archiving instead of hard deleting devotionals/series
6. **Timestamp tracking**: All tables have `created_at` and most have `updated_at`

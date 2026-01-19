# Seed Data Review

**Document:** 70-seed-data-review.md
**Generated:** 2026-01-19
**Purpose:** Review existing seed data for completeness, realism, and testing coverage

---

## Overview

The EUONGELION project has seed data defined in two locations:
- `/database/seed-data.sql` - Primary SQL seed file
- `/database/seeds/series.json` - JSON format series data (10 series)

The seed data is designed to populate the database for development and testing purposes.

---

## Current Seed Data Summary

### Series Data

| Table | Records | Status |
|-------|---------|--------|
| `series` | 4 (SQL) / 10 (JSON) | Partial |
| `devotionals` | 3 | Minimal |
| `soul_audit_questions` | 24 | Complete |
| `users` | 0 | Missing |
| `user_progress` | 0 | Missing |
| `bookmarks` | 0 | Missing |
| `soul_audit_responses` | 0 | Missing |
| `soul_audit_sessions` | 0 | Missing |

---

## Detailed Review by Table

### 1. Series Table

**Current State:** 4 series in SQL seed, 10 in JSON seed (discrepancy)

**Series Seeded (SQL):**
1. Finding Your Identity in Christ (7 days, beginner, free, featured)
2. The Power of Daily Prayer (14 days, intermediate, free)
3. Walking Through Trials (10 days, intermediate, premium)
4. Foundations of Faith (21 days, beginner, free, featured)

**Additional Series (JSON only):**
5. The Nature of Belief (6 days, intermediate, free)
6. What Is the Gospel? (7 days, beginner, free, featured)
7. Hearing God in the Noise (10 days, intermediate, premium)
8. The Lord Is My Shepherd (6 days, beginner, free)
9. Too Busy for God (7 days, intermediate, free)
10. What Is Carrying a Cross? (10 days, advanced, premium)

**Assessment:**
- GOOD: Variety of difficulty levels (beginner, intermediate, advanced)
- GOOD: Mix of free and premium content
- GOOD: Featured series for homepage testing
- ISSUE: SQL and JSON seeds are out of sync
- ISSUE: No image_url or thumbnail_url provided (all null)
- MISSING: Advanced difficulty series in SQL seed
- MISSING: Series with 0 devotionals for edge case testing

**Recommendations:**
1. Sync SQL seed with JSON seed (use all 10 series)
2. Add sample image URLs for visual testing
3. Add a series with `is_published = false` to test unpublished filtering
4. Add a series with no devotionals to test empty state handling

---

### 2. Devotionals Table

**Current State:** Only 3 devotionals seeded (all in "Identity in Christ" series)

**Devotionals Seeded:**
1. You Are Chosen (Day 1)
2. You Are Forgiven (Day 2)
3. You Are a New Creation (Day 3)

**Assessment:**
- GOOD: Rich content with all fields populated
- GOOD: Realistic scripture references and prayer texts
- GOOD: Reflection questions as arrays
- ISSUE: Only covers 3 of 7 days in one series
- ISSUE: No devotionals for other 9 series
- ISSUE: No premium devotionals to test paywall
- MISSING: Devotionals with audio_url for accessibility testing
- MISSING: Devotionals with content_html for HTML rendering testing
- MISSING: Featured devotionals for homepage
- MISSING: Unpublished devotionals for admin testing

**Recommendations:**
1. Complete Day 4-7 for "Identity in Christ" series
2. Add at least 2-3 devotionals per series
3. Include premium devotionals in "Walking Through Trials" and "Hearing God in the Noise"
4. Add devotionals with audio_url populated
5. Add devotionals with is_featured = true
6. Add unpublished devotionals for CMS testing
7. Add devotionals without a series (standalone) for edge case testing

---

### 3. Soul Audit Questions Table

**Current State:** 24 questions across 8 categories - COMPLETE

**Category Distribution:**
| Category | Questions | Weight Range |
|----------|-----------|--------------|
| faith_foundation | 3 | 1.0 - 1.2 |
| prayer_life | 3 | 0.8 - 1.0 |
| scripture_engagement | 3 | 0.9 - 1.0 |
| community | 3 | 0.9 - 1.0 |
| service | 3 | 0.8 - 1.0 |
| spiritual_disciplines | 2 | 0.7 - 0.8 |
| heart_condition | 3 | 1.0 |
| life_integration | 4 | 0.8 - 1.2 |

**Assessment:**
- EXCELLENT: All 8 categories covered
- EXCELLENT: Weighted scoring implemented
- EXCELLENT: Scripture references for each question
- EXCELLENT: Question descriptions provided
- GOOD: Mix of scale and frequency question types
- ISSUE: Only scale and frequency types used (no multiple_choice, text, yes_no)
- MISSING: Inactive questions for testing is_active filter
- MISSING: Questions with options JSONB populated
- MISSING: Questions with help_text populated

**Recommendations:**
1. Add 1-2 questions using multiple_choice type with options JSONB
2. Add 1 text-type question for qualitative feedback
3. Add 1 yes_no question for binary assessment
4. Add 1 inactive question to test filtering
5. Populate help_text on a few questions

---

### 4. Users Table (NOT SEEDED)

**Current State:** No seed data

**Issue:** Cannot test user-related features without user data

**Recommendations:**
1. Create test users with different subscription tiers:
   - Free user (default tier)
   - Premium subscriber
   - Lifetime subscriber
2. Create users with various onboarding states:
   - Onboarding completed
   - Onboarding incomplete
3. Create users with different preferences:
   - Light theme, dark theme, system
   - Various font sizes
   - Notifications enabled/disabled
4. Note: User creation requires corresponding auth.users entries in Supabase

**Sample Seed Structure:**
```sql
-- Note: Requires auth.users entries first
INSERT INTO public.users (id, email, full_name, subscription_tier, onboarding_completed, preferences) VALUES
('test-user-free', 'free@test.com', 'Free User', 'free', true, '{"theme": "light"}'),
('test-user-premium', 'premium@test.com', 'Premium User', 'premium', true, '{"theme": "dark"}'),
('test-user-lifetime', 'lifetime@test.com', 'Lifetime User', 'lifetime', true, '{}'),
('test-user-new', 'new@test.com', 'New User', 'free', false, '{}');
```

---

### 5. User Progress Table (NOT SEEDED)

**Current State:** No seed data

**Issue:** Cannot test streak calculations, progress tracking, or completion states

**Recommendations:**
1. Create progress entries for a test user showing:
   - Multi-day streak (consecutive days)
   - Broken streak (gap in days)
   - Series completion progress (partial and full)
2. Include entries with:
   - Notes populated
   - Ratings (1-5 range, plus edge cases)
   - Time spent tracking
3. Create entries across multiple dates for streak view testing

**Sample Seed Structure:**
```sql
INSERT INTO public.user_progress (user_id, devotional_id, series_id, completed_at, notes, rating, time_spent_seconds) VALUES
-- Streak testing (consecutive days)
('test-user-id', 'devotional-1', 'series-1', NOW() - INTERVAL '6 days', NULL, 5, 300),
('test-user-id', 'devotional-2', 'series-1', NOW() - INTERVAL '5 days', 'Great insight!', 4, 420),
('test-user-id', 'devotional-3', 'series-1', NOW() - INTERVAL '4 days', NULL, NULL, 180),
-- Gap in streak
('test-user-id', 'devotional-4', 'series-1', NOW() - INTERVAL '1 day', NULL, 3, 600),
('test-user-id', 'devotional-5', 'series-1', NOW(), 'Powerful message', 5, 540);
```

---

### 6. Bookmarks Table (NOT SEEDED)

**Current State:** No seed data

**Issue:** Cannot test bookmark functionality, collections, or the bookmarks_with_devotionals view

**Recommendations:**
1. Create bookmarks for test users:
   - Default collection bookmarks
   - Custom collection bookmarks ("Favorites", "To Revisit", etc.)
   - Bookmarks with notes
   - Bookmarks without notes
2. Create bookmarks across multiple series

**Sample Seed Structure:**
```sql
INSERT INTO public.bookmarks (user_id, devotional_id, collection_name, notes) VALUES
('test-user-id', 'devotional-1', 'default', NULL),
('test-user-id', 'devotional-2', 'Favorites', 'Must share with small group'),
('test-user-id', 'devotional-3', 'To Revisit', NULL);
```

---

### 7. Soul Audit Responses & Sessions (NOT SEEDED)

**Current State:** No seed data

**Issue:** Cannot test Soul Audit results, category scores, or recommendations

**Recommendations:**
1. Create completed sessions with:
   - High scores (strong spiritual health)
   - Low scores (areas needing growth)
   - Mixed scores (realistic scenario)
2. Create in-progress sessions (completed_at = NULL)
3. Populate category_scores JSONB correctly
4. Include sample recommendations

**Sample Seed Structure:**
```sql
-- Session with results
INSERT INTO public.soul_audit_sessions (id, user_id, completed_at, total_score, category_scores, recommendations) VALUES
('session-1', 'test-user-id', NOW(), 72.5,
 '{"faith_foundation": 85, "prayer_life": 70, "scripture_engagement": 65, "community": 80, "service": 60, "spiritual_disciplines": 55, "heart_condition": 75, "life_integration": 70}',
 '[{"category": "spiritual_disciplines", "title": "Grow in Disciplines", "description": "Consider starting a journaling practice", "priority": 1}]');

-- Responses for session
INSERT INTO public.soul_audit_responses (user_id, question_id, session_id, response_value) VALUES
('test-user-id', 'question-1', 'session-1', 8),
('test-user-id', 'question-2', 'session-1', 9);
-- ... continue for all 24 questions
```

---

## Edge Cases Not Covered

The current seed data does not cover these important edge cases:

### Schema Edge Cases
1. **NULL handling** - No entries test nullable fields
2. **Empty arrays** - No devotionals with empty tags[] or reflection_questions[]
3. **Maximum lengths** - No content testing text field limits
4. **Special characters** - No content with quotes, apostrophes, Unicode
5. **Constraint boundaries** - No ratings at boundaries (1 and 5)

### Business Logic Edge Cases
1. **Premium access** - No premium users accessing premium content
2. **Unpublished content** - No unpublished series/devotionals
3. **Inactive questions** - No deactivated Soul Audit questions
4. **User without progress** - No users with zero completions
5. **Orphaned data** - What happens when a series is deleted?

### View Testing
1. **user_streaks** - No data to test streak calculation
2. **bookmarks_with_devotionals** - No bookmarks to test join
3. **soul_audit_results** - No sessions to test aggregation

---

## Realism Assessment

### Strengths
- Devotional content is high-quality and spiritually meaningful
- Scripture references are accurate (ESV)
- Series descriptions are compelling and realistic
- Question text reflects genuine spiritual assessment

### Weaknesses
- All content from "EUONGELION Team" (no variety in authors)
- No date variety in published_at timestamps
- No realistic user engagement data
- Missing media (images, audio, thumbnails)

---

## Recommended Seed Data Improvements

### Priority 1: Critical for Development
1. Sync SQL seed with JSON seed (all 10 series)
2. Add more devotionals (at least 50% of each series)
3. Add test users across subscription tiers
4. Add user_progress for streak testing

### Priority 2: Important for Testing
1. Add bookmarks data
2. Add Soul Audit responses and sessions
3. Add inactive/unpublished content
4. Include edge case data (nulls, boundaries)

### Priority 3: Polish
1. Add sample image URLs
2. Add audio URLs for some devotionals
3. Vary author names
4. Add realistic timestamps over date ranges

---

## Conclusion

The current seed data provides a foundation but is **incomplete for comprehensive development and testing**. The Soul Audit questions are well-seeded, but user-related tables have no data, making it impossible to test key features like progress tracking, streaks, bookmarks, and premium access.

**Completeness Score: 35%**

The SQL seed file should be expanded to include:
- All 10 series from the JSON file
- Complete devotionals for at least 2-3 series
- Test users with varying subscription tiers
- User progress, bookmarks, and Soul Audit response data
- Edge cases for robust testing

---

*This review was generated as part of the EUONGELION overnight database documentation process.*

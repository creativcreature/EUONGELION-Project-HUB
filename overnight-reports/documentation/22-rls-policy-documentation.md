# EUONGELION Row Level Security (RLS) Policy Documentation

## Overview

EUONGELION uses Supabase's Row Level Security (RLS) to enforce data access controls at the database level. RLS ensures that users can only access data they're authorized to see, regardless of how the application queries the database.

---

## How RLS Works in EUONGELION

### Supabase Client Types

1. **Anonymous Client (anon key)**: Used by the frontend; all queries go through RLS policies
2. **Service Role Client**: Bypasses RLS; used only for admin operations on the server
3. **User Client**: Authenticated user context; RLS policies use `auth.uid()` to identify the user

### Key Functions Used in Policies

- `auth.uid()` - Returns the current authenticated user's ID
- `auth.jwt()` - Returns the current user's JWT claims
- `auth.role()` - Returns 'authenticated' or 'anon'

---

## Table Policies

### 1. `users` Table Policies

**Policy: `users_select_own`**
```sql
CREATE POLICY "users_select_own" ON public.users
  FOR SELECT
  USING (auth.uid() = id);
```
- **Operation**: SELECT
- **Who can access**: Only the user themselves
- **Purpose**: Users can only read their own profile data
- **Why**: Protects user privacy; prevents enumeration of user data

**Policy: `users_update_own`**
```sql
CREATE POLICY "users_update_own" ON public.users
  FOR UPDATE
  USING (auth.uid() = id)
  WITH CHECK (auth.uid() = id);
```
- **Operation**: UPDATE
- **Who can access**: Only the user themselves
- **Purpose**: Users can only modify their own profile
- **Why**: Prevents unauthorized profile modifications

**Policy: `users_insert_own`**
```sql
CREATE POLICY "users_insert_own" ON public.users
  FOR INSERT
  WITH CHECK (auth.uid() = id);
```
- **Operation**: INSERT
- **Who can access**: Only when creating own record
- **Purpose**: Allows user profile creation during signup
- **Why**: Works with the `handle_new_user()` trigger

**Note**: DELETE is not allowed via RLS; account deletion must go through service role.

---

### 2. `series` Table Policies

**Policy: `series_public_read`**
```sql
CREATE POLICY "series_public_read" ON public.series
  FOR SELECT
  USING (is_published = true);
```
- **Operation**: SELECT
- **Who can access**: Everyone (authenticated and anonymous)
- **Purpose**: Published series are publicly readable
- **Why**: Content discovery doesn't require authentication

**Policy: `series_premium_read`**
```sql
CREATE POLICY "series_premium_read" ON public.series
  FOR SELECT
  USING (
    is_published = true
    AND (
      is_premium = false
      OR EXISTS (
        SELECT 1 FROM public.users
        WHERE id = auth.uid()
        AND subscription_tier IN ('premium', 'lifetime')
      )
    )
  );
```
- **Operation**: SELECT
- **Who can access**: Everyone for free content; premium subscribers for premium content
- **Purpose**: Gate premium content behind subscription
- **Why**: Enforces business model at database level

**Note**: INSERT, UPDATE, DELETE are restricted to service role (admin operations only).

---

### 3. `devotionals` Table Policies

**Policy: `devotionals_public_read`**
```sql
CREATE POLICY "devotionals_public_read" ON public.devotionals
  FOR SELECT
  USING (is_published = true);
```
- **Operation**: SELECT
- **Who can access**: Everyone
- **Purpose**: Published devotionals are publicly readable
- **Why**: Allows content discovery and reading

**Policy: `devotionals_full_access_for_premium`**
```sql
CREATE POLICY "devotionals_full_access_for_premium" ON public.devotionals
  FOR SELECT
  USING (
    is_published = true
    AND (
      is_premium = false
      OR EXISTS (
        SELECT 1 FROM public.users
        WHERE id = auth.uid()
        AND subscription_tier IN ('premium', 'lifetime')
      )
    )
  );
```
- **Operation**: SELECT
- **Who can access**: Everyone for free content; premium subscribers for all content
- **Purpose**: Enforces premium content access
- **Why**: Premium devotionals require subscription

**Policy: `devotionals_series_access`**
```sql
CREATE POLICY "devotionals_series_access" ON public.devotionals
  FOR SELECT
  USING (
    is_published = true
    AND (
      series_id IS NULL
      OR EXISTS (
        SELECT 1 FROM public.series
        WHERE id = devotionals.series_id
        AND is_published = true
      )
    )
  );
```
- **Operation**: SELECT
- **Who can access**: Everyone for published devotionals in published series
- **Purpose**: Ensures devotionals inherit series visibility
- **Why**: Unpublished series should hide their devotionals

**Note**: INSERT, UPDATE, DELETE are restricted to service role (content management).

---

### 4. `user_progress` Table Policies

**Policy: `user_progress_select_own`**
```sql
CREATE POLICY "user_progress_select_own" ON public.user_progress
  FOR SELECT
  USING (auth.uid() = user_id);
```
- **Operation**: SELECT
- **Who can access**: Only the user who owns the progress
- **Purpose**: Users can view their reading history
- **Why**: Progress data is private

**Policy: `user_progress_insert_own`**
```sql
CREATE POLICY "user_progress_insert_own" ON public.user_progress
  FOR INSERT
  WITH CHECK (auth.uid() = user_id);
```
- **Operation**: INSERT
- **Who can access**: Only for own records
- **Purpose**: Users can record their progress
- **Why**: Prevents recording progress for other users

**Policy: `user_progress_update_own`**
```sql
CREATE POLICY "user_progress_update_own" ON public.user_progress
  FOR UPDATE
  USING (auth.uid() = user_id)
  WITH CHECK (auth.uid() = user_id);
```
- **Operation**: UPDATE
- **Who can access**: Only the owner
- **Purpose**: Users can update their notes/ratings
- **Why**: Progress belongs to the user

**Policy: `user_progress_delete_own`**
```sql
CREATE POLICY "user_progress_delete_own" ON public.user_progress
  FOR DELETE
  USING (auth.uid() = user_id);
```
- **Operation**: DELETE
- **Who can access**: Only the owner
- **Purpose**: Users can reset their progress
- **Why**: Data ownership

---

### 5. `bookmarks` Table Policies

**Policy: `bookmarks_select_own`**
```sql
CREATE POLICY "bookmarks_select_own" ON public.bookmarks
  FOR SELECT
  USING (auth.uid() = user_id);
```
- **Operation**: SELECT
- **Who can access**: Only the bookmark owner
- **Purpose**: Users see only their bookmarks
- **Why**: Bookmarks are personal

**Policy: `bookmarks_insert_own`**
```sql
CREATE POLICY "bookmarks_insert_own" ON public.bookmarks
  FOR INSERT
  WITH CHECK (auth.uid() = user_id);
```
- **Operation**: INSERT
- **Who can access**: Only for own records
- **Purpose**: Users can create bookmarks
- **Why**: Prevents creating bookmarks for others

**Policy: `bookmarks_update_own`**
```sql
CREATE POLICY "bookmarks_update_own" ON public.bookmarks
  FOR UPDATE
  USING (auth.uid() = user_id)
  WITH CHECK (auth.uid() = user_id);
```
- **Operation**: UPDATE
- **Who can access**: Only the owner
- **Purpose**: Users can update bookmark notes/collection
- **Why**: Bookmark ownership

**Policy: `bookmarks_delete_own`**
```sql
CREATE POLICY "bookmarks_delete_own" ON public.bookmarks
  FOR DELETE
  USING (auth.uid() = user_id);
```
- **Operation**: DELETE
- **Who can access**: Only the owner
- **Purpose**: Users can remove bookmarks
- **Why**: User data control

---

### 6. `soul_audit_questions` Table Policies

**Policy: `soul_audit_questions_public_read`**
```sql
CREATE POLICY "soul_audit_questions_public_read" ON public.soul_audit_questions
  FOR SELECT
  USING (is_active = true);
```
- **Operation**: SELECT
- **Who can access**: Everyone (authenticated users)
- **Purpose**: Questions are readable by all authenticated users
- **Why**: Questions are content, not user data

**Note**: INSERT, UPDATE, DELETE are restricted to service role (admin only).

---

### 7. `soul_audit_responses` Table Policies

**Policy: `soul_audit_responses_select_own`**
```sql
CREATE POLICY "soul_audit_responses_select_own" ON public.soul_audit_responses
  FOR SELECT
  USING (auth.uid() = user_id);
```
- **Operation**: SELECT
- **Who can access**: Only the respondent
- **Purpose**: Users view only their own responses
- **Why**: Assessment data is sensitive and private

**Policy: `soul_audit_responses_insert_own`**
```sql
CREATE POLICY "soul_audit_responses_insert_own" ON public.soul_audit_responses
  FOR INSERT
  WITH CHECK (auth.uid() = user_id);
```
- **Operation**: INSERT
- **Who can access**: Only for own records
- **Purpose**: Users can submit responses
- **Why**: Prevents submitting responses as other users

**Policy: `soul_audit_responses_update_own`**
```sql
CREATE POLICY "soul_audit_responses_update_own" ON public.soul_audit_responses
  FOR UPDATE
  USING (auth.uid() = user_id)
  WITH CHECK (auth.uid() = user_id);
```
- **Operation**: UPDATE
- **Who can access**: Only the owner
- **Purpose**: Users can update responses within a session
- **Why**: Allows answer changes before submission

**Policy: `soul_audit_responses_delete_own`**
```sql
CREATE POLICY "soul_audit_responses_delete_own" ON public.soul_audit_responses
  FOR DELETE
  USING (auth.uid() = user_id);
```
- **Operation**: DELETE
- **Who can access**: Only the owner
- **Purpose**: Users can clear their assessment data
- **Why**: Data ownership and privacy

---

### 8. `soul_audit_sessions` Table Policies

**Policy: `soul_audit_sessions_select_own`**
```sql
CREATE POLICY "soul_audit_sessions_select_own" ON public.soul_audit_sessions
  FOR SELECT
  USING (auth.uid() = user_id);
```
- **Operation**: SELECT
- **Who can access**: Only the session owner
- **Purpose**: Users view their assessment history
- **Why**: Session results are private

**Policy: `soul_audit_sessions_insert_own`**
```sql
CREATE POLICY "soul_audit_sessions_insert_own" ON public.soul_audit_sessions
  FOR INSERT
  WITH CHECK (auth.uid() = user_id);
```
- **Operation**: INSERT
- **Who can access**: Only for own records
- **Purpose**: Users can start new sessions
- **Why**: Session ownership

**Policy: `soul_audit_sessions_update_own`**
```sql
CREATE POLICY "soul_audit_sessions_update_own" ON public.soul_audit_sessions
  FOR UPDATE
  USING (auth.uid() = user_id)
  WITH CHECK (auth.uid() = user_id);
```
- **Operation**: UPDATE
- **Who can access**: Only the owner
- **Purpose**: Update session with scores upon completion
- **Why**: Session belongs to user

---

## Policy Summary Matrix

| Table | SELECT | INSERT | UPDATE | DELETE |
|-------|--------|--------|--------|--------|
| `users` | Own only | Own only | Own only | Service role |
| `series` | Published (public) | Service role | Service role | Service role |
| `devotionals` | Published (public) | Service role | Service role | Service role |
| `user_progress` | Own only | Own only | Own only | Own only |
| `bookmarks` | Own only | Own only | Own only | Own only |
| `soul_audit_questions` | Active (public) | Service role | Service role | Service role |
| `soul_audit_responses` | Own only | Own only | Own only | Own only |
| `soul_audit_sessions` | Own only | Own only | Own only | Service role |

---

## Security Considerations

### 1. Premium Content Protection

Premium content is protected at the database level:
- Users cannot access premium devotionals without subscription
- The check is done via a subquery on the `users` table
- Even if frontend code is bypassed, RLS prevents unauthorized access

### 2. User Data Isolation

All user-specific data (progress, bookmarks, responses) is isolated:
- `user_id = auth.uid()` ensures complete isolation
- No cross-user data leakage is possible
- Even SQL injection attempts are blocked by RLS

### 3. Content Management

Content tables (series, devotionals, questions) are read-only for users:
- Only service role can modify content
- Prevents malicious content injection
- Content moderation happens through admin tools

### 4. Anonymous Access

Anonymous users (not logged in) can:
- Read published, non-premium series and devotionals
- View active soul audit questions (for preview)

Anonymous users cannot:
- Access premium content
- Record progress
- Create bookmarks
- Submit soul audit responses

---

## Enabling/Disabling RLS

### Enable RLS on a Table
```sql
ALTER TABLE public.table_name ENABLE ROW LEVEL SECURITY;
```

### Disable RLS (not recommended for production)
```sql
ALTER TABLE public.table_name DISABLE ROW LEVEL SECURITY;
```

### Force RLS for Table Owner
```sql
ALTER TABLE public.table_name FORCE ROW LEVEL SECURITY;
```

---

## Debugging RLS Issues

### Check Current User
```sql
SELECT auth.uid(), auth.role();
```

### Test Policy Manually
```sql
-- Temporarily become a specific user
SET LOCAL ROLE authenticated;
SET LOCAL request.jwt.claim.sub = 'user-uuid-here';

-- Run your query
SELECT * FROM public.devotionals WHERE is_published = true;
```

### View All Policies
```sql
SELECT schemaname, tablename, policyname, permissive, roles, cmd, qual, with_check
FROM pg_policies
WHERE schemaname = 'public';
```

---

## Best Practices

1. **Always use RLS**: Never disable RLS in production
2. **Test policies**: Write tests that verify access controls
3. **Minimize service role usage**: Only use for admin operations
4. **Audit policy changes**: Log all RLS policy modifications
5. **Keep policies simple**: Complex policies can have performance implications
6. **Use indexes**: Ensure columns used in policies are indexed
7. **Document changes**: Update this documentation when policies change

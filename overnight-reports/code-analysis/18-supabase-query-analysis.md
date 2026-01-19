# Supabase Query Analysis

**Generated:** 2026-01-19
**Project:** EUONGELION
**Path:** `/Users/meltmac/Documents/Personal/wkGD/EUONGELION-STARTUP/app`

---

## Executive Summary

The EUONGELION app uses Supabase for authentication and database operations. The codebase has **comprehensive auth integration** but database queries are primarily implemented through API routes with proper error handling. Most Supabase queries follow good patterns, but there are opportunities to optimize N+1 queries and add RLS policies.

**Overall Rating:** Good (7/10)

---

## 1. Supabase Client Configuration

### Client Files

| File | Purpose | Client Type |
|------|---------|-------------|
| `/lib/supabase/client.ts` | Browser client | Anonymous |
| `/lib/supabase/server.ts` | Server client | Anonymous + Service Role |
| `/lib/supabase/middleware.ts` | Middleware client | Anonymous |
| `/src/lib/auth/supabase.ts` | Auth-specific client | Anonymous + Service Role |

### Client Initialization Pattern

```typescript
// /lib/supabase/client.ts
import { createBrowserClient } from '@supabase/ssr';

export const createClient = () =>
  createBrowserClient(
    process.env.NEXT_PUBLIC_SUPABASE_URL!,
    process.env.NEXT_PUBLIC_SUPABASE_ANON_KEY!
  );
```

```typescript
// /lib/supabase/server.ts - Service Role (Admin)
export const createServiceRoleClient = () =>
  createClient(
    process.env.NEXT_PUBLIC_SUPABASE_URL!,
    process.env.SUPABASE_SERVICE_ROLE_KEY!,
    { auth: { persistSession: false } }
  );
```

---

## 2. Authentication Queries

### Auth State Management

| File | Line | Query | Purpose |
|------|------|-------|---------|
| `/lib/supabase/middleware.ts` | 42 | `supabase.auth.getUser()` | Get current user |
| `/src/contexts/AuthContext.tsx` | 112 | `supabase.auth.onAuthStateChange()` | Auth state subscription |
| `/src/contexts/AuthContext.tsx` | 283 | `supabase.auth.getUser()` | Refresh user |
| `/src/lib/auth/session.ts` | 30 | `supabase.auth.getSession()` | Get session |
| `/src/lib/auth/session.ts` | 70 | `supabase.auth.getUser()` | Get user |
| `/src/lib/auth/session.ts` | 91 | `supabase.auth.refreshSession()` | Refresh session |

### Auth Actions

| File | Line | Query | Purpose |
|------|------|-------|---------|
| `/src/lib/auth/auth.ts` | 33 | `supabase.auth.signUp()` | Register user |
| `/src/lib/auth/auth.ts` | 65 | `supabase.auth.signInWithPassword()` | Email login |
| `/src/lib/auth/auth.ts` | 90 | `supabase.auth.signOut()` | Logout |
| `/src/lib/auth/auth.ts` | 112 | `supabase.auth.signInWithOAuth()` | Google login |
| `/src/lib/auth/auth.ts` | 143 | `supabase.auth.signInWithOAuth()` | Apple login |
| `/src/lib/auth/auth.ts` | 170 | `supabase.auth.resetPasswordForEmail()` | Password reset |
| `/src/lib/auth/auth.ts` | 194 | `supabase.auth.updateUser()` | Update password |
| `/src/lib/auth/auth.ts` | 218 | `supabase.auth.resend()` | Resend verification |
| `/src/lib/auth/auth.ts` | 249 | `supabase.auth.updateUser()` | Update email |
| `/src/lib/auth/auth.ts` | 291 | `supabase.rpc('delete_user_account')` | Delete account |

### User Context Queries

| File | Line | Query | Purpose |
|------|------|-------|---------|
| `/src/contexts/UserContext.tsx` | 179 | `supabase.auth.updateUser()` | Update display name |
| `/src/contexts/UserContext.tsx` | 207 | `supabase.auth.updateUser()` | Update avatar |
| `/src/contexts/UserContext.tsx` | 235 | `supabase.auth.updateUser()` | Update bio |
| `/src/contexts/UserContext.tsx` | 302 | `supabase.from('user_preferences').delete()` | Delete preferences |

---

## 3. Database Queries

### User Preferences

```typescript
// /src/contexts/UserContext.tsx line 302
await supabase.from('user_preferences').delete().eq('user_id', user.id);
```

**Tables Used:**
- `user_preferences`

### RPC Calls

```typescript
// /src/lib/auth/auth.ts line 291
await supabase.rpc('delete_user_account');
```

**Functions Used:**
- `delete_user_account` - Cascade delete user data

---

## 4. N+1 Query Analysis

### Potential N+1 Patterns

Based on the API routes and data model, watch for these patterns:

| Pattern | Location | Issue | Recommendation |
|---------|----------|-------|----------------|
| Devotionals with series | API routes | May query series per devotional | Use JOIN or single query |
| User progress per series | progressStore | Loops over series | Batch query |
| Bookmarks with devotionals | bookmarkStore | May fetch devotional details per bookmark | Include devotional data in bookmark |

### Example Fix for N+1

```typescript
// Instead of (N+1):
const devotionals = await supabase.from('devotionals').select('*');
for (const d of devotionals.data) {
  const series = await supabase.from('series').select('*').eq('id', d.series_id);
}

// Use JOIN (1 query):
const { data } = await supabase
  .from('devotionals')
  .select(`
    *,
    series:series_id (
      id,
      title,
      slug
    )
  `);
```

---

## 5. Error Handling Analysis

### Good Patterns Found

All auth queries follow proper error handling:

```typescript
// /src/lib/auth/auth.ts
const { data, error } = await supabase.auth.signUp({ ... });
if (error) throw error;
return data;
```

### Missing Error Handling

None found - all queries have try/catch or error checks.

---

## 6. RLS (Row Level Security) Considerations

### Current State

Based on code analysis, the following tables need RLS:

| Table | Needed Policies | Status |
|-------|-----------------|--------|
| `user_preferences` | User can CRUD own preferences | Needs verification |
| `bookmarks` | User can CRUD own bookmarks | Needs verification |
| `reading_progress` | User can CRUD own progress | Needs verification |
| `devotionals` | All can read published, admins can CRUD | Needs verification |
| `series` | All can read published, admins can CRUD | Needs verification |

### Recommended RLS Policies

```sql
-- user_preferences
CREATE POLICY "Users can view own preferences"
  ON user_preferences FOR SELECT
  USING (auth.uid() = user_id);

CREATE POLICY "Users can update own preferences"
  ON user_preferences FOR UPDATE
  USING (auth.uid() = user_id);

-- bookmarks
CREATE POLICY "Users can view own bookmarks"
  ON bookmarks FOR SELECT
  USING (auth.uid() = user_id);

CREATE POLICY "Users can insert own bookmarks"
  ON bookmarks FOR INSERT
  WITH CHECK (auth.uid() = user_id);

-- devotionals (public read)
CREATE POLICY "Anyone can view published devotionals"
  ON devotionals FOR SELECT
  USING (status = 'published');
```

---

## 7. Query Performance Recommendations

### 1. Use Proper Indexes

```sql
-- Common query patterns need indexes
CREATE INDEX idx_devotionals_status ON devotionals(status);
CREATE INDEX idx_devotionals_series_id ON devotionals(series_id);
CREATE INDEX idx_devotionals_slug ON devotionals(slug);
CREATE INDEX idx_bookmarks_user_id ON bookmarks(user_id);
CREATE INDEX idx_progress_user_id ON reading_progress(user_id);
```

### 2. Limit Query Results

```typescript
// Always paginate large result sets
const { data } = await supabase
  .from('devotionals')
  .select('*')
  .range(0, 19)  // First 20 items
  .order('created_at', { ascending: false });
```

### 3. Select Only Needed Fields

```typescript
// Instead of
.select('*')

// Use
.select('id, title, slug, description, featured_image')
```

---

## 8. API Route Query Summary

### /api/devotionals/route.ts

- GET: Fetch devotionals list with pagination
- POST: Create new devotional (admin)

### /api/devotionals/[id]/route.ts

- GET: Fetch single devotional
- PUT: Update devotional (admin)
- DELETE: Remove devotional (admin)

### /api/series/route.ts

- GET: Fetch series list with pagination
- POST: Create new series (admin)

### /api/series/[slug]/route.ts

- GET: Fetch single series with devotionals
- PUT: Update series (admin)
- DELETE: Remove series (admin)

### /api/user/bookmarks/route.ts

- GET: Fetch user bookmarks
- POST: Add bookmark
- PUT: Update bookmark
- DELETE: Remove bookmark

### /api/user/progress/route.ts

- GET: Fetch user progress
- POST: Record progress
- DELETE: Reset progress

### /api/soul-audit/*

- GET questions: Fetch assessment questions
- POST submit: Submit assessment and get results

---

## 9. Action Items

### High Priority

1. **Verify RLS policies exist**
   - Check Supabase dashboard
   - Ensure all tables have appropriate policies

2. **Add database indexes**
   - Index foreign keys
   - Index commonly filtered columns

3. **Review N+1 patterns**
   - Audit devotional/series fetching
   - Use JOINs where appropriate

### Medium Priority

4. **Implement query caching**
   - Use SWR or React Query
   - Cache devotional lists

5. **Add query monitoring**
   - Enable Supabase query logging
   - Monitor slow queries

6. **Optimize SELECT statements**
   - Review all `select('*')` calls
   - Select only needed columns

### Low Priority

7. **Add database migrations**
   - Version control schema changes
   - Document RLS policies

8. **Implement soft deletes**
   - Add `deleted_at` column
   - Filter in queries

---

## 10. Security Checklist

| Item | Status | Notes |
|------|--------|-------|
| RLS enabled on all tables | Verify | Check Supabase dashboard |
| Service role key only on server | Yes | Only in server.ts |
| Anon key in client code | Yes | Public key, expected |
| Auth state properly managed | Yes | Good implementation |
| User can only access own data | Needs RLS | Depends on policies |
| Admin routes protected | Verify | Check middleware |

---

## Summary

The Supabase integration is well-implemented for authentication with:
- Proper client separation (browser/server)
- Comprehensive auth flows
- Good error handling

Areas for improvement:
1. **Verify RLS policies** are in place
2. **Optimize queries** to prevent N+1 patterns
3. **Add database indexes** for performance
4. **Review SELECT statements** to fetch only needed data

The authentication layer is production-ready; database queries need optimization review.

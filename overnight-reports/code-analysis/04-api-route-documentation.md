# API Route Documentation

**Generated:** 2026-01-19
**Project:** EUONGELION
**Path:** /Users/meltmac/Documents/Personal/wkGD/EUONGELION-STARTUP/app/api

---

## Executive Summary

EUONGELION has 10 API routes implementing CRUD operations for devotionals, series, user progress, bookmarks, soul audit, feedback, and health check. All routes return consistent error responses and are well-typed. However, database integration is pending (TODO placeholders throughout).

---

## API Routes Overview

| Route | Methods | Authentication | Database Integration |
|-------|---------|----------------|---------------------|
| `/api/devotionals` | GET, POST | Admin for POST | TODO |
| `/api/devotionals/[id]` | GET, PUT, DELETE | Admin for PUT/DELETE | TODO |
| `/api/series` | GET, POST | Admin for POST | TODO |
| `/api/series/[slug]` | GET, PUT, DELETE | Admin for PUT/DELETE | TODO |
| `/api/user/progress` | GET, POST, DELETE | Required | TODO |
| `/api/user/bookmarks` | GET, POST, PUT, DELETE | Required | TODO |
| `/api/soul-audit/questions` | GET | None | Static data |
| `/api/soul-audit/submit` | GET, POST | Required | TODO |
| `/api/feedback` | POST | None | TODO |
| `/api/health` | GET | None | N/A |

**Note:** Currently using 10 of 12 allowed serverless functions (Vercel Hobby plan limit).

---

## Detailed Route Documentation

### 1. `/api/devotionals`

**File:** `/Users/meltmac/Documents/Personal/wkGD/EUONGELION-STARTUP/app/api/devotionals/route.ts`

#### GET /api/devotionals

**Purpose:** Fetch paginated list of devotionals with filtering and sorting.

**Query Parameters:**
| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `page` | number | 1 | Page number |
| `limit` | number | 10 | Items per page (max: 100) |
| `seriesId` | string | - | Filter by series ID |
| `status` | DevotionalStatus | - | Filter by status |
| `tags` | string | - | Comma-separated tags |
| `search` | string | - | Search in title/description |
| `sortBy` | string | publishedAt | Sort field: publishedAt, title, dayNumber |
| `sortOrder` | string | desc | asc or desc |

**Response Shape:**
```typescript
interface DevotionalsResponse {
  devotionals: DevotionalCard[];
  pagination: {
    page: number;
    limit: number;
    total: number;
    totalPages: number;
    hasNextPage: boolean;
    hasPreviousPage: boolean;
  };
  filters: {
    seriesId?: string;
    status?: DevotionalStatus;
    tags?: string[];
    search?: string;
  };
}
```

**Error Handling:**
- 500: Internal server error (logged)

---

#### POST /api/devotionals

**Purpose:** Create a new devotional (admin only).

**Request Body:**
```typescript
{
  title: string;          // Required
  subtitle?: string;
  slug?: string;          // Auto-generated if not provided
  description?: string;
  seriesId?: string;
  dayNumber?: number;
  weekNumber?: number;
  primaryScripture: ScriptureReference; // Required
  additionalScriptures?: ScriptureReference[];
  immersionSections?: ImmersionSection[];
  wordStudies?: WordStudy[];
  reflectionQuestions?: ReflectionQuestion[];
  tags?: string[];
}
```

**Response Shape:**
```typescript
{ devotional: Devotional }
```

**Error Handling:**
- 400: Validation error (missing title or primaryScripture)
- 401: Unauthorized (TODO - not implemented)
- 500: Internal server error

---

### 2. `/api/devotionals/[id]`

**File:** `/Users/meltmac/Documents/Personal/wkGD/EUONGELION-STARTUP/app/api/devotionals/[id]/route.ts`

#### GET /api/devotionals/[id]

**Purpose:** Fetch single devotional by ID or slug.

**Path Parameters:**
| Parameter | Description |
|-----------|-------------|
| `id` | Devotional ID (dev_xxx) or slug |

**Query Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| `include` | string | Comma-separated: series, navigation, wordStudies |

**Response Shape:**
```typescript
interface DevotionalResponse {
  devotional: Devotional;
  related?: {
    previousDevotional?: { id, title, slug };
    nextDevotional?: { id, title, slug };
    seriesInfo?: { id, title, slug, totalDays, currentDay };
  };
}
```

**Error Handling:**
- 400: Invalid ID format
- 404: Devotional not found
- 500: Internal server error

**Caching:** `Cache-Control: public, s-maxage=3600, stale-while-revalidate=86400`

---

#### PUT /api/devotionals/[id]

**Purpose:** Update a devotional (admin only).

**Request Body:** Partial Devotional object

**Status Transitions:**
| From | Allowed To |
|------|------------|
| draft | review, archived |
| review | draft, scheduled, published, archived |
| scheduled | review, published, archived |
| published | archived |
| archived | draft |

**Error Handling:**
- 400: Invalid ID or invalid status transition
- 404: Devotional not found
- 401: Unauthorized (TODO)
- 500: Internal server error

---

#### DELETE /api/devotionals/[id]

**Purpose:** Delete or archive a devotional.

**Query Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| `hard` | boolean | If true, permanently delete; otherwise archive |

**Response Shape:**
```typescript
{ success: boolean; message: string }
```

---

### 3. `/api/series`

**File:** `/Users/meltmac/Documents/Personal/wkGD/EUONGELION-STARTUP/app/api/series/route.ts`

#### GET /api/series

**Purpose:** Fetch paginated list of series.

**Query Parameters:**
| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `page` | number | 1 | Page number |
| `limit` | number | 10 | Items per page (max: 50) |
| `category` | SeriesCategory | - | Filter by category |
| `depth` | SeriesDepth | - | Filter by depth level |
| `status` | SeriesStatus | published | Filter by status |
| `featured` | boolean | - | Filter featured series |
| `tags` | string | - | Comma-separated tags |
| `search` | string | - | Search query |
| `sortBy` | string | displayOrder | Sort field |
| `sortOrder` | string | asc | asc or desc |

**Response Shape:**
```typescript
interface SeriesListResponse {
  series: SeriesCard[];
  pagination: { ... };
  filters: { ... };
}
```

**Caching:** `Cache-Control: public, s-maxage=300, stale-while-revalidate=600`

---

#### POST /api/series

**Purpose:** Create a new series (admin only).

**Required Fields:** title, description, shortDescription, category

**Valid Categories:**
- onboarding, foundations, book-study, topical
- character-study, seasonal, prayer, worship
- discipleship, evangelism, apologetics, theology
- practical-living

---

### 4. `/api/series/[slug]`

**File:** `/Users/meltmac/Documents/Personal/wkGD/EUONGELION-STARTUP/app/api/series/[slug]/route.ts`

#### GET /api/series/[slug]

**Purpose:** Fetch series with devotionals.

**Query Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| `include` | string | Comma-separated: progress, navigation, related |

**Response Shape:**
```typescript
interface SeriesWithDevotionalsResponse {
  series: Series;
  devotionals: DevotionalCard[];
  userProgress?: {
    completedDevotionalIds: string[];
    currentDay: number;
    completionPercentage: number;
    isCompleted: boolean;
    currentStreak: number;
    longestStreak: number;
    startedAt?: Date;
    lastActivityAt?: Date;
  };
  navigation?: {
    previousSeries?: { id, title, slug };
    nextSeries?: { id, title, slug };
    relatedSeries?: Array<{ id, title, slug, shortDescription }>;
  };
}
```

**Caching:** `Cache-Control: public, s-maxage=1800, stale-while-revalidate=3600`

---

### 5. `/api/user/progress`

**File:** `/Users/meltmac/Documents/Personal/wkGD/EUONGELION-STARTUP/app/api/user/progress/route.ts`

#### GET /api/user/progress

**Purpose:** Get user's reading progress across all series.

**Query Parameters:**
| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `seriesId` | string | - | Filter to specific series |
| `limit` | number | 10 | Limit recent activity (max: 50) |

**Response Shape:**
```typescript
interface UserProgressResponse {
  seriesProgress: SeriesProgress[];
  recentActivity: DailyProgress[];
  stats: {
    totalDevotionalsCompleted: number;
    totalSeriesCompleted: number;
    currentStreak: number;
    longestStreak: number;
    totalReadingTimeMinutes: number;
    favoriteImmersionLevel?: ImmersionLevel;
  };
}
```

---

#### POST /api/user/progress

**Purpose:** Record reading progress for a devotional.

**Request Body:**
```typescript
interface RecordProgressRequest {
  devotionalId: string;        // Required
  seriesId?: string;
  immersionLevel?: ImmersionLevel;  // "1-minute" | "5-minute" | "15-minute"
  timeSpentMinutes?: number;
  completedReflection?: boolean;
  completedPrayer?: boolean;
  notes?: string;
}
```

**Response includes achievements earned:**
```typescript
interface Achievement {
  id: string;
  name: string;
  description: string;
  earnedAt: Date;
  type: 'streak' | 'completion' | 'milestone' | 'special';
}
```

**Streak Milestones:** 3, 7, 14, 21, 30, 40, 60, 90, 100, 365 days
**Devotional Milestones:** 1, 10, 25, 50, 100, 250, 500, 1000

---

#### DELETE /api/user/progress

**Purpose:** Reset progress for a series or all progress.

**Query Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| `seriesId` | string | Reset specific series |
| `all` | boolean | Reset ALL progress (dangerous) |

---

### 6. `/api/user/bookmarks`

**File:** `/Users/meltmac/Documents/Personal/wkGD/EUONGELION-STARTUP/app/api/user/bookmarks/route.ts`

#### GET /api/user/bookmarks

**Query Parameters:**
| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `type` | BookmarkType | - | devotional, series, word-study, scripture |
| `folderId` | string | - | Filter by folder |
| `page` | number | 1 | Page number |
| `limit` | number | 20 | Items per page (max: 100) |
| `search` | string | - | Search query |
| `sortBy` | string | createdAt | Sort field |
| `sortOrder` | string | desc | Sort direction |

**Response Shape:**
```typescript
interface BookmarksListResponse {
  bookmarks: Bookmark[];
  folders: BookmarkFolder[];
  pagination: {
    page: number;
    limit: number;
    total: number;
    hasMore: boolean;
  };
}
```

---

#### POST /api/user/bookmarks

**Request Body:**
```typescript
interface CreateBookmarkRequest {
  type: BookmarkType;      // Required
  targetId: string;        // Required
  title: string;           // Required
  description?: string;
  thumbnail?: string;
  tags?: string[];
  notes?: string;
  folderId?: string;
}
```

---

#### PUT /api/user/bookmarks

**Purpose:** Update bookmark (notes, folder, tags).

**Request Body:** Partial bookmark with required `id`.

---

#### DELETE /api/user/bookmarks

**Query Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| `id` | string | Bookmark ID |
| `targetId` | string | Target ID (requires `type`) |
| `type` | BookmarkType | Required when using targetId |

---

### 7. `/api/soul-audit/questions`

**File:** `/Users/meltmac/Documents/Personal/wkGD/EUONGELION-STARTUP/app/api/soul-audit/questions/route.ts`

#### GET /api/soul-audit/questions

**Purpose:** Get soul audit questions.

**Query Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| `category` | SoulAuditCategory | Filter by category |
| `required` | boolean | Only required questions |

**Categories:**
- faith-foundation, prayer-life, scripture-engagement
- community, spiritual-disciplines, witness
- character, stewardship, worship, rest-sabbath

**Response Shape:**
```typescript
interface QuestionsResponse {
  questions: SoulAuditQuestion[];
  categories: CategoryInfo[];
  metadata: {
    totalQuestions: number;
    estimatedTimeMinutes: number;
    version: string;
    lastUpdated: Date;
  };
}
```

**Question Count:** 26 questions across 10 categories
**Estimated Time:** ~13 minutes

**Caching:** `Cache-Control: public, s-maxage=86400, stale-while-revalidate=604800`

---

### 8. `/api/soul-audit/submit`

**File:** `/Users/meltmac/Documents/Personal/wkGD/EUONGELION-STARTUP/app/api/soul-audit/submit/route.ts`

#### POST /api/soul-audit/submit

**Purpose:** Submit responses and get results.

**Request Body:**
```typescript
interface SubmitSoulAuditRequest {
  responses: Array<{
    questionId: string;
    value: string | number;
    responseType: QuestionResponseType;
  }>;
  completedAt?: Date;
  notes?: string;
}
```

**Response Shape:**
```typescript
interface SubmitResponse {
  success: boolean;
  result: {
    id: string;
    overallScore: number;
    overallMaxScore: number;
    overallPercentage: number;
    categoryScores: CategoryScore[];
    topStrengths: Array<{ category, description }>;
    topGrowthAreas: Array<{ category, description, suggestedSeries }>;
    recommendedSeriesIds: string[];
    recommendedDevotionalIds: string[];
    completedAt: Date;
    responses: QuestionResponse[];
  };
  message: string;
}
```

---

#### GET /api/soul-audit/submit

**Purpose:** Get previous audit submissions.

**Query Parameters:**
| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `limit` | number | 5 | Number of submissions (max: 20) |
| `compare` | boolean | false | Include comparison |

---

### 9. `/api/feedback`

**File:** `/Users/meltmac/Documents/Personal/wkGD/EUONGELION-STARTUP/app/api/feedback/route.ts`

#### POST /api/feedback

**Purpose:** Submit user feedback.

**Request Body:** Feedback data (structure TBD)

**Error Handling:** Standard error response

---

### 10. `/api/health`

**File:** `/Users/meltmac/Documents/Personal/wkGD/EUONGELION-STARTUP/app/api/health/route.ts`

#### GET /api/health

**Purpose:** Health check endpoint.

**Response:** Health status object

---

## Common Error Response Structure

All API routes return errors in this format:

```typescript
interface ApiError {
  error: string;        // Error code (e.g., "NOT_FOUND", "VALIDATION_ERROR")
  message: string;      // Human-readable message
  statusCode: number;   // HTTP status code
}
```

**Common Error Codes:**
| Code | HTTP Status | Description |
|------|-------------|-------------|
| INVALID_ID | 400 | Invalid ID format |
| INVALID_SLUG | 400 | Invalid slug format |
| VALIDATION_ERROR | 400 | Missing or invalid fields |
| UNAUTHORIZED | 401 | Authentication required |
| NOT_FOUND | 404 | Resource not found |
| DUPLICATE | 409 | Resource already exists |
| INTERNAL_ERROR | 500 | Server error |

---

## Implementation Status

| Feature | Status |
|---------|--------|
| Route handlers | Complete |
| TypeScript types | Complete |
| Input validation | Complete |
| Error handling | Complete |
| Database integration | TODO |
| Authentication | TODO |
| Caching headers | Complete |
| Rate limiting | TODO |

---

## Recommendations

### Critical
1. **Implement database integration** - All routes currently return empty/mock data
2. **Add authentication** - All commented-out auth checks need implementation
3. **Connect to Supabase** - Database client exists but not used in routes

### High Priority
4. **Add rate limiting** - Prevent abuse of public endpoints
5. **Add request logging** - Track API usage
6. **Implement validation middleware** - Centralize input validation

### Medium Priority
7. **Add API versioning** - Prepare for future changes
8. **Create API documentation page** - User-facing docs
9. **Add OpenAPI spec** - Machine-readable API docs

---

*Report generated by overnight autonomous analysis*

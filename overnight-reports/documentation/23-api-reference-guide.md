# EUONGELION API Reference Guide

## Overview

EUONGELION uses Next.js 15 App Router API routes built on serverless functions. The API follows RESTful conventions and is designed to work within Vercel's Hobby plan constraints (maximum 12 serverless functions).

**Base URL**: `https://euongelion.app/api` (production) or `http://localhost:3333/api` (development)

---

## Authentication

All authenticated endpoints require a valid Supabase session cookie. The middleware automatically handles session refresh and validation.

### Headers
```http
Cookie: sb-[project-ref]-auth-token=[jwt-token]
```

### Error Response (401 Unauthorized)
```json
{
  "error": "UNAUTHORIZED",
  "message": "Authentication required",
  "statusCode": 401
}
```

---

## Error Response Format

All errors follow a consistent format:

```json
{
  "error": "ERROR_CODE",
  "message": "Human-readable error message",
  "statusCode": 400
}
```

### Common Error Codes

| Code | Status | Description |
|------|--------|-------------|
| `UNAUTHORIZED` | 401 | Authentication required |
| `FORBIDDEN` | 403 | Insufficient permissions |
| `NOT_FOUND` | 404 | Resource not found |
| `VALIDATION_ERROR` | 400 | Invalid request data |
| `DUPLICATE` | 409 | Resource already exists |
| `INTERNAL_ERROR` | 500 | Server error |

---

## Endpoints

### Devotionals

#### GET /api/devotionals

Retrieve a list of devotionals with optional filtering and pagination.

**Authentication**: Optional (premium content filtered for unauthenticated users)

**Query Parameters**:

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `page` | number | 1 | Page number |
| `limit` | number | 10 | Items per page (max: 50) |
| `seriesId` | string | - | Filter by series ID |
| `featured` | boolean | - | Filter featured devotionals |
| `premium` | boolean | - | Filter premium devotionals |
| `search` | string | - | Search in title/content |
| `sortBy` | string | `publishedAt` | Sort field |
| `sortOrder` | string | `desc` | Sort direction (asc/desc) |

**Response (200 OK)**:
```json
{
  "devotionals": [
    {
      "id": "uuid",
      "title": "Finding Peace in Chaos",
      "subtitle": "Day 1 of 7",
      "slug": "finding-peace-in-chaos",
      "scriptureRef": "Philippians 4:6-7",
      "scriptureText": "Do not be anxious about anything...",
      "readingTimeMinutes": 5,
      "imageUrl": "https://...",
      "seriesId": "uuid",
      "seriesName": "Peace Series",
      "dayNumber": 1,
      "isPremium": false,
      "isFeatured": true,
      "publishedAt": "2024-01-15T00:00:00Z"
    }
  ],
  "pagination": {
    "page": 1,
    "limit": 10,
    "total": 42,
    "totalPages": 5,
    "hasNext": true,
    "hasPrevious": false
  }
}
```

---

#### GET /api/devotionals/[id]

Retrieve a single devotional by ID.

**Authentication**: Optional (premium content requires authentication)

**Path Parameters**:
- `id` (string, required): Devotional UUID

**Response (200 OK)**:
```json
{
  "id": "uuid",
  "title": "Finding Peace in Chaos",
  "subtitle": "Day 1 of 7",
  "slug": "finding-peace-in-chaos",
  "content": "Full markdown content...",
  "contentHtml": "<p>Pre-rendered HTML...</p>",
  "scriptureRef": "Philippians 4:6-7",
  "scriptureText": "Do not be anxious about anything...",
  "scriptureVersion": "ESV",
  "readingTimeMinutes": 5,
  "prayer": "Lord, help us find peace...",
  "reflectionQuestions": [
    "What causes you anxiety today?",
    "How can you apply this scripture?"
  ],
  "actionStep": "Take 5 minutes to meditate on this passage",
  "imageUrl": "https://...",
  "audioUrl": "https://...",
  "tags": ["peace", "anxiety", "prayer"],
  "author": "John Smith",
  "series": {
    "id": "uuid",
    "name": "Peace Series",
    "slug": "peace-series"
  },
  "dayNumber": 1,
  "isPremium": false,
  "publishedAt": "2024-01-15T00:00:00Z"
}
```

**Error Response (404)**:
```json
{
  "error": "NOT_FOUND",
  "message": "Devotional not found",
  "statusCode": 404
}
```

---

### Series

#### GET /api/series

Retrieve all published series.

**Authentication**: Optional

**Query Parameters**:

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `featured` | boolean | - | Filter featured series |
| `premium` | boolean | - | Filter by premium status |
| `difficulty` | string | - | Filter by difficulty level |
| `sortBy` | string | `sortOrder` | Sort field |
| `sortOrder` | string | `asc` | Sort direction |

**Response (200 OK)**:
```json
{
  "series": [
    {
      "id": "uuid",
      "name": "Foundations of Faith",
      "slug": "foundations-of-faith",
      "description": "A comprehensive introduction to Christian faith...",
      "shortDescription": "Build your faith foundation",
      "imageUrl": "https://...",
      "thumbnailUrl": "https://...",
      "devotionalCount": 7,
      "durationDays": 7,
      "difficultyLevel": "beginner",
      "tags": ["foundation", "basics", "new believers"],
      "isPremium": false,
      "isFeatured": true,
      "author": "EUONGELION Team"
    }
  ]
}
```

---

#### GET /api/series/[slug]

Retrieve a single series with its devotionals.

**Authentication**: Optional

**Path Parameters**:
- `slug` (string, required): Series slug

**Response (200 OK)**:
```json
{
  "id": "uuid",
  "name": "Foundations of Faith",
  "slug": "foundations-of-faith",
  "description": "Full description...",
  "shortDescription": "Build your faith foundation",
  "imageUrl": "https://...",
  "thumbnailUrl": "https://...",
  "devotionalCount": 7,
  "durationDays": 7,
  "difficultyLevel": "beginner",
  "tags": ["foundation", "basics"],
  "isPremium": false,
  "isFeatured": true,
  "author": "EUONGELION Team",
  "devotionals": [
    {
      "id": "uuid",
      "title": "Day 1: Who is God?",
      "slug": "day-1-who-is-god",
      "dayNumber": 1,
      "readingTimeMinutes": 5,
      "scriptureRef": "Genesis 1:1",
      "isPremium": false
    }
  ]
}
```

---

### User Progress

#### GET /api/user/progress

Retrieve the authenticated user's reading progress.

**Authentication**: Required

**Query Parameters**:

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `seriesId` | string | - | Filter by series |
| `limit` | number | 10 | Recent activity limit (max: 50) |

**Response (200 OK)**:
```json
{
  "seriesProgress": [
    {
      "seriesId": "uuid",
      "seriesName": "Foundations of Faith",
      "totalDevotionals": 7,
      "completedDevotionals": 3,
      "percentComplete": 43,
      "lastReadAt": "2024-01-20T10:30:00Z",
      "isCompleted": false
    }
  ],
  "recentActivity": [
    {
      "devotionalId": "uuid",
      "devotionalTitle": "Day 3: The Trinity",
      "seriesId": "uuid",
      "completedAt": "2024-01-20T10:30:00Z",
      "timeSpentMinutes": 7,
      "immersionLevel": "5-minute"
    }
  ],
  "stats": {
    "totalDevotionalsCompleted": 15,
    "totalSeriesCompleted": 2,
    "currentStreak": 5,
    "longestStreak": 12,
    "totalReadingTimeMinutes": 120,
    "favoriteImmersionLevel": "5-minute"
  }
}
```

---

#### POST /api/user/progress

Record reading progress for a devotional.

**Authentication**: Required

**Request Body**:
```json
{
  "devotionalId": "uuid",
  "seriesId": "uuid",
  "immersionLevel": "5-minute",
  "timeSpentMinutes": 7,
  "completedReflection": true,
  "completedPrayer": true,
  "notes": "This really spoke to me..."
}
```

**Fields**:

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `devotionalId` | string | Yes | Devotional UUID |
| `seriesId` | string | No | Series UUID (for tracking) |
| `immersionLevel` | string | No | `1-minute`, `5-minute`, or `15-minute` |
| `timeSpentMinutes` | number | No | Actual reading time |
| `completedReflection` | boolean | No | Completed reflection questions |
| `completedPrayer` | boolean | No | Read/prayed the prayer |
| `notes` | string | No | Personal notes |

**Response (201 Created)**:
```json
{
  "success": true,
  "progress": {
    "devotionalId": "uuid",
    "completedAt": "2024-01-20T10:30:00Z",
    "timeSpentMinutes": 7,
    "immersionLevel": "5-minute"
  },
  "seriesProgress": {
    "seriesId": "uuid",
    "completedDevotionals": 4,
    "percentComplete": 57,
    "isCompleted": false
  },
  "achievements": [
    {
      "id": "streak_7",
      "name": "7-Day Streak",
      "description": "Completed devotionals for 7 consecutive days",
      "earnedAt": "2024-01-20T10:30:00Z",
      "type": "streak"
    }
  ]
}
```

---

#### DELETE /api/user/progress

Reset reading progress.

**Authentication**: Required

**Query Parameters**:

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `seriesId` | string | No* | Reset progress for specific series |
| `all` | boolean | No* | Reset all progress if `true` |

*Either `seriesId` or `all=true` must be provided.

**Response (200 OK)**:
```json
{
  "success": true,
  "message": "Progress for series \"Foundations of Faith\" has been reset"
}
```

---

### Bookmarks

#### GET /api/user/bookmarks

Retrieve the user's bookmarks.

**Authentication**: Required

**Query Parameters**:

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `type` | string | - | Filter by type (devotional, series, etc.) |
| `folderId` | string | - | Filter by folder |
| `page` | number | 1 | Page number |
| `limit` | number | 20 | Items per page (max: 100) |
| `search` | string | - | Search in title/description |
| `sortBy` | string | `createdAt` | Sort field |
| `sortOrder` | string | `desc` | Sort direction |

**Response (200 OK)**:
```json
{
  "bookmarks": [
    {
      "id": "bm_xxx",
      "type": "devotional",
      "targetId": "uuid",
      "title": "Finding Peace in Chaos",
      "description": "Day 1 of Peace Series",
      "thumbnail": "https://...",
      "tags": ["peace", "favorite"],
      "notes": "Great for morning devotion",
      "folderId": null,
      "createdAt": "2024-01-15T08:00:00Z",
      "updatedAt": "2024-01-15T08:00:00Z"
    }
  ],
  "folders": [
    {
      "id": "folder_xxx",
      "name": "Morning Devotions",
      "color": "#C19A6B",
      "icon": "sun",
      "sortOrder": 1,
      "createdAt": "2024-01-10T00:00:00Z"
    }
  ],
  "pagination": {
    "page": 1,
    "limit": 20,
    "total": 8,
    "hasMore": false
  }
}
```

---

#### POST /api/user/bookmarks

Create a new bookmark.

**Authentication**: Required

**Request Body**:
```json
{
  "type": "devotional",
  "targetId": "uuid",
  "title": "Finding Peace in Chaos",
  "description": "Day 1 of Peace Series",
  "thumbnail": "https://...",
  "tags": ["favorite"],
  "notes": "Great for morning devotion",
  "folderId": "folder_xxx"
}
```

**Response (201 Created)**:
```json
{
  "success": true,
  "bookmark": {
    "id": "bm_xxx",
    "type": "devotional",
    "targetId": "uuid",
    "title": "Finding Peace in Chaos",
    "createdAt": "2024-01-20T10:30:00Z"
  },
  "message": "Bookmark created successfully"
}
```

---

#### PUT /api/user/bookmarks

Update an existing bookmark.

**Authentication**: Required

**Request Body**:
```json
{
  "id": "bm_xxx",
  "notes": "Updated notes",
  "folderId": "folder_yyy",
  "tags": ["favorite", "peace"]
}
```

**Response (200 OK)**:
```json
{
  "success": true,
  "bookmark": { ... },
  "message": "Bookmark updated successfully"
}
```

---

#### DELETE /api/user/bookmarks

Remove a bookmark.

**Authentication**: Required

**Query Parameters**:

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `id` | string | No* | Bookmark ID |
| `targetId` | string | No* | Target resource ID |
| `type` | string | No | Required with `targetId` |

*Either `id` or `targetId` (with `type`) must be provided.

**Response (200 OK)**:
```json
{
  "success": true,
  "message": "Bookmark removed successfully"
}
```

---

### Soul Audit

#### GET /api/soul-audit/questions

Retrieve soul audit assessment questions.

**Authentication**: Required

**Query Parameters**:

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `category` | string | - | Filter by category |
| `required` | boolean | - | Filter required questions only |

**Response (200 OK)**:
```json
{
  "questions": [
    {
      "id": "ff-1",
      "category": "faith-foundation",
      "question": "I have a clear understanding of the Gospel message...",
      "description": null,
      "responseType": "scale",
      "options": null,
      "scriptureReference": "Romans 10:9-10",
      "order": 1,
      "required": true,
      "weight": 2
    },
    {
      "id": "pl-1",
      "category": "prayer-life",
      "question": "How often do you spend dedicated time in prayer?",
      "responseType": "frequency",
      "options": [
        { "value": "never", "label": "Never", "score": 0 },
        { "value": "rarely", "label": "Rarely", "score": 1 },
        { "value": "sometimes", "label": "Sometimes", "score": 2 },
        { "value": "often", "label": "Often", "score": 3 },
        { "value": "always", "label": "Always", "score": 4 }
      ],
      "scriptureReference": "1 Thessalonians 5:17",
      "order": 1,
      "required": true,
      "weight": 1
    }
  ],
  "categories": [
    {
      "id": "faith-foundation",
      "name": "Faith Foundation",
      "description": "Core beliefs and understanding of the Gospel",
      "icon": "cross",
      "color": "#8B5CF6",
      "order": 1
    }
  ],
  "metadata": {
    "totalQuestions": 26,
    "estimatedTimeMinutes": 13,
    "version": "1.0.0",
    "lastUpdated": "2024-01-01T00:00:00Z"
  }
}
```

**Categories**:
- `faith-foundation` - Core beliefs
- `prayer-life` - Communication with God
- `scripture-engagement` - Bible study habits
- `community` - Fellowship and church
- `spiritual-disciplines` - Fasting, silence, etc.
- `witness` - Evangelism and testimony
- `character` - Fruit of the Spirit
- `stewardship` - Time, talents, treasure
- `worship` - Personal and corporate worship
- `rest-sabbath` - Rhythms of rest

---

#### POST /api/soul-audit/submit

Submit soul audit responses and receive results.

**Authentication**: Required

**Request Body**:
```json
{
  "responses": [
    {
      "questionId": "ff-1",
      "value": 8,
      "responseType": "scale"
    },
    {
      "questionId": "pl-1",
      "value": "often",
      "responseType": "frequency"
    }
  ],
  "notes": "Optional personal notes"
}
```

**Response (201 Created)**:
```json
{
  "success": true,
  "result": {
    "id": "sa_xxx",
    "userId": "uuid",
    "overallScore": 65.5,
    "overallMaxScore": 100,
    "overallPercentage": 66,
    "categoryScores": [
      {
        "category": "faith-foundation",
        "categoryName": "Faith Foundation",
        "score": 9.2,
        "maxScore": 12,
        "percentage": 77,
        "questionsAnswered": 3,
        "totalQuestions": 3,
        "strengthAreas": ["Strong faith foundation practices"],
        "growthAreas": []
      },
      {
        "category": "prayer-life",
        "categoryName": "Prayer Life",
        "score": 5.5,
        "maxScore": 12,
        "percentage": 46,
        "questionsAnswered": 3,
        "totalQuestions": 3,
        "strengthAreas": [],
        "growthAreas": ["Develop a more consistent and intimate prayer life"]
      }
    ],
    "topStrengths": [
      {
        "category": "Faith Foundation",
        "description": "Strong foundation in faith foundation"
      }
    ],
    "topGrowthAreas": [
      {
        "category": "Prayer Life",
        "description": "Develop a more consistent and intimate prayer life",
        "suggestedSeries": "learning-to-pray"
      }
    ],
    "recommendedSeriesIds": ["learning-to-pray", "spiritual-disciplines"],
    "recommendedDevotionalIds": [],
    "completedAt": "2024-01-20T10:30:00Z"
  },
  "message": "Soul audit completed successfully"
}
```

---

#### GET /api/soul-audit/submit

Retrieve previous soul audit submissions.

**Authentication**: Required

**Query Parameters**:

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `limit` | number | 5 | Number of submissions (max: 20) |
| `compare` | boolean | false | Include comparison with previous |

**Response (200 OK)**:
```json
{
  "submissions": [
    {
      "id": "sa_xxx",
      "userId": "uuid",
      "overallPercentage": 66,
      "categoryScores": [...],
      "completedAt": "2024-01-20T10:30:00Z"
    }
  ],
  "comparison": {
    "previousResult": { ... },
    "changes": [
      {
        "category": "prayer-life",
        "previousPercentage": 40,
        "currentPercentage": 46,
        "change": 6
      }
    ]
  }
}
```

---

## Rate Limiting

The API implements rate limiting to prevent abuse:

| Endpoint Type | Limit | Window |
|---------------|-------|--------|
| General API | 30 requests | 1 minute |
| Authentication | 10 requests | 1 minute |
| File uploads | 5 requests | 1 minute |

**Rate Limit Headers**:
```http
X-RateLimit-Limit: 30
X-RateLimit-Remaining: 25
X-RateLimit-Reset: 1705750800
```

**Response (429 Too Many Requests)**:
```json
{
  "error": "RATE_LIMIT_EXCEEDED",
  "message": "Too many requests. Please try again later.",
  "statusCode": 429
}
```

---

## Caching

Certain endpoints return cache control headers:

| Endpoint | Cache Strategy |
|----------|----------------|
| `GET /api/devotionals` | `public, s-maxage=60, stale-while-revalidate=300` |
| `GET /api/series` | `public, s-maxage=60, stale-while-revalidate=300` |
| `GET /api/soul-audit/questions` | `public, s-maxage=86400, stale-while-revalidate=604800` |
| User endpoints | `no-store, no-cache, must-revalidate` |

---

## Vercel Constraints

EUONGELION runs on Vercel's Hobby plan with these constraints:

- **Maximum 12 serverless functions**
- **10-second function timeout**
- **50MB deployment size**
- **100GB bandwidth/month**

Current function count: 10/12

---

## TypeScript Types

The API uses TypeScript for type safety. Import types from:

```typescript
import type {
  Devotional,
  DevotionalCard,
  ImmersionLevel,
  Series,
  SeriesCard,
  SeriesProgress,
  DailyProgress
} from '@/types';
```

---

## SDK Usage Examples

### Fetch Devotionals
```typescript
const response = await fetch('/api/devotionals?featured=true&limit=5');
const { devotionals } = await response.json();
```

### Record Progress
```typescript
const response = await fetch('/api/user/progress', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    devotionalId: 'uuid-here',
    immersionLevel: '5-minute',
    timeSpentMinutes: 7
  })
});
const { success, achievements } = await response.json();
```

### Toggle Bookmark
```typescript
// Add bookmark
await fetch('/api/user/bookmarks', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    type: 'devotional',
    targetId: 'uuid-here',
    title: 'Devotional Title'
  })
});

// Remove bookmark
await fetch('/api/user/bookmarks?targetId=uuid-here&type=devotional', {
  method: 'DELETE'
});
```

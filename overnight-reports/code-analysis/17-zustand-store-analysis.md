# Zustand Store Analysis

**Generated:** 2026-01-19
**Project:** EUONGELION
**Path:** `/Users/meltmac/Documents/Personal/wkGD/EUONGELION-STARTUP/app/stores`

---

## Executive Summary

The EUONGELION app uses **5 Zustand stores** with comprehensive middleware setup including persistence, logging, devtools, and subscriptions. The stores are well-architected with clear separation of concerns, typed selectors, and action helpers. Some TODO placeholders indicate incomplete API integration.

**Overall Rating:** Excellent (8.5/10)

---

## 1. Store Overview

| Store | File | Purpose | Lines |
|-------|------|---------|-------|
| `useAuthStore` | `authStore.ts` | Authentication & sessions | 415 |
| `useBookmarkStore` | `bookmarkStore.ts` | Saved devotionals & folders | 554 |
| `useDevotionalStore` | `devotionalStore.ts` | Current devotional & reading | 458 |
| `useProgressStore` | `progressStore.ts` | Streaks, stats, progress | 560 |
| `useUserStore` | `userStore.ts` | Profile & preferences | 346 |

**Total:** ~2,333 lines of well-structured state management

---

## 2. Common Middleware Stack

All stores use the same middleware pattern:

```typescript
create<StoreState>()(
  devtools(
    subscribeWithSelector(
      persist(
        logger<StoreState>({ prefix: '[StoreName]', diffOnly: true })(
          (set, get) => ({
            // state and actions
          })
        ),
        {
          name: 'euongelion-store-name',
          storage: { getItem, setItem, removeItem },
          partialize: (state) => ({ /* persisted fields */ }),
        }
      )
    ),
    { name: 'StoreName' }
  )
);
```

### Middleware Benefits

| Middleware | Purpose | Status |
|------------|---------|--------|
| `devtools` | Redux DevTools integration | Active |
| `subscribeWithSelector` | Selective subscriptions | Active |
| `persist` | localStorage persistence | Active |
| `logger` | Development logging | Dev-only |

### Custom Middleware (from middleware.ts)

- `createSSRStorage()` - SSR-safe localStorage wrapper
- `createIndexedDBStorage()` - Large data storage
- `logger()` - State change logging
- `createSelector()` - Memoized selectors
- `shallowEqual()` - Equality helper

---

## 3. Store: useAuthStore

**File:** `/stores/authStore.ts` (415 lines)

### State Shape

```typescript
interface AuthStoreState {
  session: UserSession | null;
  status: AuthStatus;  // 'idle' | 'loading' | 'authenticated' | 'unauthenticated' | 'error'
  error: string | null;
  isInitialized: boolean;
}

interface UserSession {
  id: string;
  email: string | null;
  displayName: string;
  photoUrl: string | null;
  provider: AuthProvider;  // 'email' | 'google' | 'apple' | 'anonymous'
  emailVerified: boolean;
  accessToken: string;
  expiresAt: number;
  createdAt: number;
}
```

### Actions

| Action | Description | Status |
|--------|-------------|--------|
| `setSession` | Set current session | Complete |
| `setStatus` | Update auth status | Complete |
| `setError` | Set error message | Complete |
| `clearError` | Clear error | Complete |
| `initialize` | Check existing session | Complete |
| `signIn` | Authenticate with provider | Mock |
| `signUp` | Register new user | Mock |
| `signOut` | End session | Mock |
| `refreshToken` | Refresh access token | Mock |
| `resetPassword` | Request password reset | Mock |

### Selectors

```typescript
authSelectors.session
authSelectors.isAuthenticated
authSelectors.isLoading
authSelectors.userId
authSelectors.isPremium
authSelectors.error
authSelectors.isInitialized
authSelectors.status
```

### Side Effects

- **Token refresh timer** - Automatically refreshes token 5 minutes before expiration (line 390-413)

### Issues

1. **Mock implementations** - All auth methods use mock data (TODO comments)
2. **Missing Supabase integration** - Should integrate with existing Supabase auth

---

## 4. Store: useBookmarkStore

**File:** `/stores/bookmarkStore.ts` (554 lines)

### State Shape

```typescript
interface BookmarkStoreState {
  bookmarks: Bookmark[];
  folders: BookmarkFolder[];
  isLoading: boolean;
  error: string | null;
}

interface Bookmark {
  id: string;
  devotionalId: string;
  devotionalTitle: string;
  scriptureReference: string;
  sectionId?: string;
  folderId?: string;
  notes?: string;
  tags: string[];
  createdAt: Date;
}

interface BookmarkFolder {
  id: string;
  name: string;
  description?: string;
  color?: string;
  bookmarkCount: number;
  createdAt: Date;
  updatedAt: Date;
}
```

### Actions

| Action | Description | Status |
|--------|-------------|--------|
| `clearError` | Clear error | Complete |
| `addBookmark` | Add new bookmark | Complete |
| `removeBookmark` | Delete bookmark | Complete |
| `updateBookmark` | Modify bookmark | Complete |
| `createFolder` | Create new folder | Complete |
| `deleteFolder` | Remove folder | Complete |
| `moveToFolder` | Move bookmark to folder | Complete |
| `loadBookmarks` | Fetch from API | Mock |
| `syncBookmarks` | Sync to server | Mock |
| `isBookmarked` | Check if bookmarked | Complete |

### Selectors & Derived Selectors

```typescript
// Basic selectors
bookmarkSelectors.bookmarks
bookmarkSelectors.folders
bookmarkSelectors.isLoading
bookmarkSelectors.error
bookmarkSelectors.bookmarkCount
bookmarkSelectors.folderCount
bookmarkSelectors.uncategorizedBookmarks

// Derived selectors (parameterized)
bookmarkDerivedSelectors.getBookmarkById(id)
bookmarkDerivedSelectors.getDevotionalBookmarks(devotionalId)
bookmarkDerivedSelectors.getFolderBookmarks(folderId)
bookmarkDerivedSelectors.getFolderById(folderId)
bookmarkDerivedSelectors.getBookmarksByTag(tag)
bookmarkDerivedSelectors.getAllTags
bookmarkDerivedSelectors.sortedByDate
bookmarkDerivedSelectors.recentBookmarks(limit)
bookmarkDerivedSelectors.isSectionBookmarked(devotionalId, sectionId)
bookmarkDerivedSelectors.searchBookmarks(query)
```

### Helper Functions

- `toggleBookmark()` - Toggle bookmark on/off
- `addTagToBookmark()` - Add tag
- `removeTagFromBookmark()` - Remove tag
- `renameFolder()` - Rename folder
- `updateFolderColor()` - Change folder color

### Limits

- `MAX_BOOKMARKS = 500`
- `MAX_FOLDERS = 20`

---

## 5. Store: useDevotionalStore

**File:** `/stores/devotionalStore.ts` (458 lines)

### State Shape

```typescript
interface DevotionalStoreState {
  currentDevotional: Devotional | null;
  readingState: ReadingState | null;
  readingHistory: ReadingHistoryEntry[];
  isLoading: boolean;
  error: string | null;
}

interface ReadingState {
  devotionalId: string;
  currentImmersionLevel: ImmersionLevel;
  scrollPosition: number;
  timeSpent: number;
  startedAt: number;
  lastReadAt: number;
  completedSections: string[];
  isComplete: boolean;
}

interface ReadingHistoryEntry {
  devotionalId: string;
  seriesId?: string;
  readAt: Date;
  immersionLevel: ImmersionLevel;
  timeSpentMinutes: number;
  notes?: string;
}
```

### Actions

| Action | Description | Status |
|--------|-------------|--------|
| `setCurrentDevotional` | Set active devotional | Complete |
| `clearCurrentDevotional` | Clear current | Complete |
| `clearError` | Clear error | Complete |
| `loadDevotional` | Fetch devotional | Mock |
| `startReading` | Begin reading session | Complete |
| `updateReadingProgress` | Update progress | Complete |
| `completeReading` | Mark as complete | Complete |
| `addToHistory` | Add to history | Complete |

### Selectors

```typescript
devotionalSelectors.currentDevotional
devotionalSelectors.readingState
devotionalSelectors.readingHistory
devotionalSelectors.isReading
devotionalSelectors.currentImmersionLevel
devotionalSelectors.timeSpent
devotionalSelectors.scrollPosition
devotionalSelectors.isLoading
devotionalSelectors.error
devotionalSelectors.completedSections
devotionalSelectors.isComplete

// Derived
devotionalDerivedSelectors.todaysReadings
devotionalDerivedSelectors.recentHistory
devotionalDerivedSelectors.wasReadToday(devotionalId)
devotionalDerivedSelectors.sessionStats
```

### Helper Functions

- `startReadingTimer()` - Start time tracking
- `stopReadingTimer()` - Stop time tracking
- `updateScrollPosition()` - Update scroll progress
- `markSectionComplete()` - Mark section done
- `changeImmersionLevel()` - Switch immersion level

### Constants

- `MAX_HISTORY_ENTRIES = 100`
- `READING_STATE_EXPIRY = 24 hours`

---

## 6. Store: useProgressStore

**File:** `/stores/progressStore.ts` (560 lines)

### State Shape

```typescript
interface ProgressStoreState {
  streak: StreakInfo;
  stats: ReadingStats;
  seriesProgress: Record<string, SeriesProgress>;
  dailyProgress: DailyProgress[];
  isLoading: boolean;
  error: string | null;
}

interface StreakInfo {
  currentStreak: number;
  longestStreak: number;
  lastActivityDate: string;
  streakStartDate: string;
  streakDates: string[];
}

interface ReadingStats {
  totalDevotionalsCompleted: number;
  totalSeriesCompleted: number;
  totalTimeSpentMinutes: number;
  totalWordStudies: number;
  totalReflectionsAnswered: number;
  immersionLevelStats: Record<ImmersionLevel, number>;
  weeklyTrend: DailyReadingCount[];
  monthlyTrend: DailyReadingCount[];
}
```

### Actions

| Action | Description | Status |
|--------|-------------|--------|
| `clearError` | Clear error | Complete |
| `updateStreak` | Update streak count | Complete |
| `recordProgress` | Record daily progress | Complete |
| `updateSeriesProgress` | Update series progress | Complete |
| `loadProgress` | Load from API | Mock |
| `syncProgress` | Sync to server | Mock |
| `calculateStats` | Recalculate stats | Complete |

### Streak Logic

- Consecutive days extend streak
- 48-hour grace period (can miss one day)
- Longer gaps reset streak to 1

### Helper Functions

- `recordDevotionalCompletion()` - Record completion
- `startSeries()` - Begin new series
- `completeSeries()` - Mark series done

### Constants

- `MAX_DAILY_PROGRESS_ENTRIES = 365`
- `STREAK_GRACE_PERIOD_HOURS = 48`

---

## 7. Store: useUserStore

**File:** `/stores/userStore.ts` (346 lines)

### State Shape

```typescript
interface UserStoreState {
  profile: UserProfile | null;
  preferences: UserPreferences;
  isLoading: boolean;
  error: string | null;
}

interface UserProfile {
  id: string;
  displayName: string;
  email: string;
  avatarUrl?: string;
  bio?: string;
  createdAt: Date;
  lastLoginAt: Date;
  isPremium: boolean;
  premiumExpiresAt?: Date;
  churchAffiliation?: string;
  timezone: string;
  locale: string;
}

interface UserPreferences {
  preferredTranslation: string;
  defaultImmersionLevel: ImmersionLevel;
  dailyReminderEnabled: boolean;
  dailyReminderTime: string;
  pushNotificationsEnabled: boolean;
  emailNotificationsEnabled: boolean;
  theme: 'light' | 'dark' | 'system';
  fontSize: 'small' | 'medium' | 'large';
  showOriginalLanguage: boolean;
  autoPlayAudio: boolean;
  offlineModeEnabled: boolean;
  privacy: PrivacySettings;
}
```

### Actions

| Action | Description | Status |
|--------|-------------|--------|
| `setProfile` | Set profile | Complete |
| `setPreferences` | Update preferences | Complete |
| `clearError` | Clear error | Complete |
| `loadProfile` | Fetch profile | Mock |
| `updateProfile` | Update profile | Mock |
| `savePreferences` | Save to server | Mock |
| `resetPreferences` | Reset to defaults | Complete |

### Helper Functions

- `updatePreference(key, value)` - Update single preference
- `togglePreference(key)` - Toggle boolean preference
- `updatePrivacy(updates)` - Update privacy settings

### Default Preferences

```typescript
{
  preferredTranslation: 'ESV',
  defaultImmersionLevel: '5-minute',
  dailyReminderEnabled: true,
  dailyReminderTime: '07:00',
  pushNotificationsEnabled: true,
  emailNotificationsEnabled: true,
  theme: 'system',
  fontSize: 'medium',
  showOriginalLanguage: true,
  autoPlayAudio: false,
  offlineModeEnabled: false,
}
```

---

## 8. Persistence Configuration

| Store | Persisted Fields | Storage Key |
|-------|------------------|-------------|
| Auth | `session` | `euongelion-auth-store` |
| Bookmark | `bookmarks`, `folders` | `euongelion-bookmark-store` |
| Devotional | `readingState`, `readingHistory` | `euongelion-devotional-store` |
| Progress | `streak`, `stats`, `seriesProgress`, `dailyProgress` | `euongelion-progress-store` |
| User | `preferences` | `euongelion-user-store` |

### Rehydration Handlers

- **Auth:** Marks `isInitialized = true`
- **Devotional:** Clears stale reading state (>24 hours)

---

## 9. Potential Issues

### 1. Mock Implementations (High Priority)

All stores have TODO comments for API integration:
- `signIn`, `signUp`, `signOut` (authStore)
- `loadBookmarks`, `syncBookmarks` (bookmarkStore)
- `loadDevotional` (devotionalStore)
- `loadProgress`, `syncProgress` (progressStore)
- `loadProfile`, `updateProfile`, `savePreferences` (userStore)

### 2. Relative Imports (Medium Priority)

```typescript
// devotionalStore.ts line 11
import type { Devotional, ImmersionLevel } from '../types/devotional';

// progressStore.ts line 11
import type { SeriesProgress, DailyProgress } from '../types/series';
```

Should use `@/types/*` path aliases.

### 3. No Offline Sync Queue (Medium Priority)

When offline, mutations are lost. Consider:
- Queue failed API calls
- Sync when back online
- Conflict resolution

### 4. LocalStorage Size Limits (Low Priority)

Progress store persists up to 365 daily entries. Monitor size.

### 5. Missing Type Export (Low Priority)

`stores/types.ts` should be verified to export all referenced types.

---

## 10. Action Items

### High Priority

1. **Integrate Supabase Auth**
   - Replace mock auth methods
   - Use existing `/lib/supabase/*` clients

2. **Connect API endpoints**
   - Implement all `loadX` and `syncX` methods
   - Use existing API routes

3. **Add optimistic updates**
   - Update UI immediately
   - Rollback on error

### Medium Priority

4. **Fix relative imports**
   ```typescript
   // Change from
   import type { Devotional } from '../types/devotional';
   // To
   import type { Devotional } from '@/types/devotional';
   ```

5. **Add offline sync queue**
   - Use IndexedDB storage helper
   - Implement background sync

6. **Add error recovery**
   - Retry failed operations
   - User-friendly error messages

### Low Priority

7. **Monitor localStorage usage**
   - Add size tracking
   - Implement cleanup for old data

8. **Add store documentation**
   - JSDoc for all actions
   - Usage examples

---

## 11. Best Practices Observed

1. **Separation of Concerns** - Each store has single responsibility
2. **Typed Selectors** - All selectors are typed
3. **Derived Selectors** - Computed values separated
4. **Action Helpers** - Common operations extracted
5. **Constants** - Limits and timeouts extracted
6. **SSR Safety** - Storage wrapper handles server rendering
7. **DevTools Integration** - All stores named for debugging
8. **Logging** - Development logging with diff-only option

---

## Summary

The Zustand store architecture is well-designed with:
- Clear separation between 5 domain stores
- Comprehensive middleware stack
- Typed state and selectors
- Helper functions for common operations
- Persistence with SSR safety

Key gaps:
1. **Mock implementations need real API integration**
2. **Relative imports should use path aliases**
3. **No offline sync strategy**

The stores provide a solid foundation; completing the API integration will make them production-ready.

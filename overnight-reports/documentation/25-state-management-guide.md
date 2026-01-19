# EUONGELION State Management Guide

## Overview

EUONGELION uses **Zustand** for client-side state management. Zustand provides a minimal, unopinionated state management solution that integrates well with React's hooks and Next.js's server components.

**Store Location**: `/app/stores/`

---

## Why Zustand?

| Feature | Zustand | Redux | Context API |
|---------|---------|-------|-------------|
| Bundle size | ~1KB | ~7KB+ | 0 (built-in) |
| Boilerplate | Minimal | Extensive | Moderate |
| DevTools | Yes | Yes | Limited |
| SSR support | Yes | Yes | Yes |
| Learning curve | Low | High | Low |
| Middleware | Yes | Yes | Manual |
| Selectors | Built-in | Required | Manual |

Zustand was chosen for its simplicity, small bundle size, and excellent TypeScript support.

---

## Store Architecture

```
/app/stores/
  ├── authStore.ts       # Authentication state
  ├── userStore.ts       # User profile & preferences
  ├── devotionalStore.ts # Current devotional & reading state
  ├── progressStore.ts   # Reading progress & streaks
  ├── bookmarkStore.ts   # Bookmarks management
  └── types.ts           # Shared type definitions
```

---

## Store Implementations

### 1. Auth Store

**Purpose**: Manages authentication state, session, and auth operations.

**Location**: `/app/stores/authStore.ts`

```typescript
interface AuthStoreState {
  // State
  session: UserSession | null;
  status: AuthStatus;  // 'idle' | 'loading' | 'authenticated' | 'unauthenticated' | 'error'
  error: string | null;
  isInitialized: boolean;

  // Actions
  setSession: (session: UserSession | null) => void;
  setStatus: (status: AuthStatus) => void;
  setError: (error: string | null) => void;
  initialize: () => Promise<void>;
  signIn: (provider: AuthProvider, credentials?: { email: string; password: string }) => Promise<void>;
  signUp: (email: string, password: string, displayName: string) => Promise<void>;
  signOut: () => Promise<void>;
  refreshToken: () => Promise<void>;
  resetPassword: (email: string) => Promise<void>;
  clearError: () => void;
}
```

**Usage**:
```typescript
import { useAuthStore } from '@/stores/authStore';

function LoginButton() {
  const { status, signIn, error } = useAuthStore();

  const handleLogin = async () => {
    await signIn('email', { email: 'user@example.com', password: 'password' });
  };

  if (status === 'loading') return <Spinner />;
  if (status === 'authenticated') return <ProfileButton />;

  return (
    <>
      <Button onClick={handleLogin}>Sign In</Button>
      {error && <ErrorMessage>{error}</ErrorMessage>}
    </>
  );
}
```

**State Flow**:
```
idle -> loading -> authenticated | unauthenticated | error
```

---

### 2. User Store

**Purpose**: Manages user profile data and preferences.

**Location**: `/app/stores/userStore.ts`

```typescript
interface UserStoreState {
  // State
  profile: UserProfile | null;
  preferences: UserPreferences;
  isLoading: boolean;
  error: string | null;

  // Actions
  setProfile: (profile: UserProfile | null) => void;
  updateProfile: (updates: Partial<UserProfile>) => Promise<void>;
  setPreferences: (preferences: Partial<UserPreferences>) => void;
  loadProfile: (userId: string) => Promise<void>;
  savePreferences: () => Promise<void>;
  resetPreferences: () => void;
  clearError: () => void;
}
```

**Default Preferences**:
```typescript
const defaultPreferences: UserPreferences = {
  preferredTranslation: 'ESV',
  defaultImmersionLevel: '5-minute',
  dailyReminderEnabled: true,
  dailyReminderTime: '07:00',
  pushNotificationsEnabled: false,
  emailNotificationsEnabled: true,
  theme: 'system',
  fontSize: 'medium',
  showOriginalLanguage: false,
  autoPlayAudio: false,
  offlineModeEnabled: true,
  privacy: {
    profileVisibility: 'private',
    showProgress: false,
    allowFriendRequests: true,
    showInLeaderboards: false,
  },
};
```

**Usage**:
```typescript
import { useUserStore } from '@/stores/userStore';

function SettingsPage() {
  const { preferences, setPreferences, savePreferences } = useUserStore();

  const toggleDarkMode = () => {
    setPreferences({ theme: preferences.theme === 'dark' ? 'light' : 'dark' });
    savePreferences();
  };

  return (
    <Toggle
      checked={preferences.theme === 'dark'}
      onChange={toggleDarkMode}
    />
  );
}
```

---

### 3. Devotional Store

**Purpose**: Manages current devotional content and reading session state.

**Location**: `/app/stores/devotionalStore.ts`

```typescript
interface DevotionalStoreState {
  // State
  currentDevotional: Devotional | null;
  readingState: ReadingState | null;
  readingHistory: ReadingHistoryEntry[];
  isLoading: boolean;
  error: string | null;

  // Actions
  setCurrentDevotional: (devotional: Devotional | null) => void;
  loadDevotional: (id: string) => Promise<void>;
  startReading: (devotionalId: string, immersionLevel: ImmersionLevel) => void;
  updateReadingProgress: (updates: Partial<ReadingState>) => void;
  completeReading: () => void;
  addToHistory: (entry: ReadingHistoryEntry) => void;
  clearCurrentDevotional: () => void;
  clearError: () => void;
}
```

**ReadingState Structure**:
```typescript
interface ReadingState {
  devotionalId: string;
  currentImmersionLevel: ImmersionLevel;
  scrollPosition: number;  // 0-100 percentage
  timeSpent: number;       // seconds
  startedAt: number;       // timestamp
  lastReadAt: number;      // timestamp
  completedSections: string[];
  isComplete: boolean;
}
```

**Usage**:
```typescript
import { useDevotionalStore } from '@/stores/devotionalStore';

function DevotionalPage({ id }: { id: string }) {
  const {
    currentDevotional,
    readingState,
    loadDevotional,
    startReading,
    updateReadingProgress,
    completeReading
  } = useDevotionalStore();

  useEffect(() => {
    loadDevotional(id);
  }, [id]);

  useEffect(() => {
    if (currentDevotional) {
      startReading(currentDevotional.id, '5-minute');
    }
  }, [currentDevotional]);

  const handleScroll = (position: number) => {
    updateReadingProgress({ scrollPosition: position });

    if (position >= 90 && !readingState?.isComplete) {
      completeReading();
    }
  };

  return <DevotionalReader devotional={currentDevotional} onScroll={handleScroll} />;
}
```

---

### 4. Progress Store

**Purpose**: Tracks reading progress, streaks, and statistics.

**Location**: `/app/stores/progressStore.ts`

```typescript
interface ProgressStoreState {
  // State
  streak: StreakInfo;
  stats: ReadingStats;
  seriesProgress: Record<string, SeriesProgress>;
  dailyProgress: DailyProgress[];
  isLoading: boolean;
  error: string | null;

  // Actions
  updateStreak: (activityDate: string) => void;
  recordProgress: (progress: DailyProgress) => void;
  updateSeriesProgress: (seriesId: string, progress: Partial<SeriesProgress>) => void;
  loadProgress: (userId: string) => Promise<void>;
  syncProgress: () => Promise<void>;
  calculateStats: () => void;
  clearError: () => void;
}
```

**StreakInfo Structure**:
```typescript
interface StreakInfo {
  currentStreak: number;
  longestStreak: number;
  lastActivityDate: string;  // YYYY-MM-DD
  streakStartDate: string;
  streakDates: string[];
}
```

**ReadingStats Structure**:
```typescript
interface ReadingStats {
  totalDevotionalsCompleted: number;
  totalSeriesCompleted: number;
  totalTimeSpentMinutes: number;
  totalWordStudies: number;
  totalReflectionsAnswered: number;
  immersionLevelStats: {
    '1-minute': number;
    '5-minute': number;
    '15-minute': number;
  };
  weeklyTrend: DailyReadingCount[];
  monthlyTrend: DailyReadingCount[];
}
```

**Usage**:
```typescript
import { useProgressStore } from '@/stores/progressStore';

function StreakDisplay() {
  const { streak, stats } = useProgressStore();

  return (
    <div>
      <FireIcon />
      <span>{streak.currentStreak} day streak</span>
      <span>Best: {streak.longestStreak} days</span>
      <span>{stats.totalDevotionalsCompleted} devotionals read</span>
    </div>
  );
}
```

---

### 5. Bookmark Store

**Purpose**: Manages user bookmarks and folders.

**Location**: `/app/stores/bookmarkStore.ts`

```typescript
interface BookmarkStoreState {
  // State
  bookmarks: Bookmark[];
  folders: BookmarkFolder[];
  isLoading: boolean;
  error: string | null;

  // Actions
  addBookmark: (bookmark: Omit<Bookmark, 'id' | 'createdAt'>) => void;
  removeBookmark: (bookmarkId: string) => void;
  updateBookmark: (bookmarkId: string, updates: Partial<Bookmark>) => void;
  createFolder: (folder: Omit<BookmarkFolder, 'id' | 'createdAt' | 'updatedAt' | 'bookmarkCount'>) => void;
  deleteFolder: (folderId: string) => void;
  moveToFolder: (bookmarkId: string, folderId: string | null) => void;
  loadBookmarks: (userId: string) => Promise<void>;
  syncBookmarks: () => Promise<void>;
  isBookmarked: (devotionalId: string) => boolean;
  clearError: () => void;
}
```

**Usage**:
```typescript
import { useBookmarkStore } from '@/stores/bookmarkStore';

function BookmarkButton({ devotionalId, title }: Props) {
  const { isBookmarked, addBookmark, removeBookmark } = useBookmarkStore();
  const bookmarked = isBookmarked(devotionalId);

  const toggleBookmark = () => {
    if (bookmarked) {
      removeBookmark(devotionalId);
    } else {
      addBookmark({
        devotionalId,
        devotionalTitle: title,
        scriptureReference: '',
        tags: [],
      });
    }
  };

  return (
    <Button onClick={toggleBookmark}>
      <BookmarkIcon filled={bookmarked} />
    </Button>
  );
}
```

---

## Data Flow Architecture

### API to UI Flow

```
┌─────────────────────────────────────────────────────────────────┐
│                         API Layer                                │
│  /api/devotionals  /api/user/progress  /api/user/bookmarks      │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                       Zustand Stores                             │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐           │
│  │ authStore│ │userStore │ │devotional│ │progress  │           │
│  │          │ │          │ │  Store   │ │  Store   │           │
│  └──────────┘ └──────────┘ └──────────┘ └──────────┘           │
│                                                                  │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │                    bookmarkStore                          │   │
│  └──────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                      React Components                            │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐           │
│  │  Header  │ │Devotional│ │ Progress │ │ Bookmark │           │
│  │          │ │  Reader  │ │ Display  │ │  Button  │           │
│  └──────────┘ └──────────┘ └──────────┘ └──────────┘           │
└─────────────────────────────────────────────────────────────────┘
```

### Store Interactions

```
┌──────────────┐       ┌──────────────┐
│   authStore  │──────▶│   userStore  │
│ (session)    │ loads │ (profile)    │
└──────────────┘       └──────────────┘
       │                      │
       │                      │
       ▼                      ▼
┌──────────────┐       ┌──────────────┐
│progressStore │◀──────│devotionalStore│
│ (tracks)     │records│ (content)    │
└──────────────┘       └──────────────┘
       │                      │
       │                      │
       ▼                      ▼
┌──────────────────────────────────────┐
│           bookmarkStore              │
│    (bookmarks across devotionals)    │
└──────────────────────────────────────┘
```

---

## Persistence & Synchronization

### Local Storage Persistence

Zustand supports persistence middleware for offline capability:

```typescript
import { create } from 'zustand';
import { persist } from 'zustand/middleware';

export const useProgressStore = create<ProgressStoreState>()(
  persist(
    (set, get) => ({
      // ... state and actions
    }),
    {
      name: 'euongelion-progress',
      partialize: (state) => ({
        streak: state.streak,
        dailyProgress: state.dailyProgress,
        seriesProgress: state.seriesProgress,
      }),
    }
  )
);
```

### Synchronization Strategy

1. **On Mount**: Load from local storage (instant)
2. **On Auth**: Fetch from API, merge with local
3. **On Action**: Update local immediately, sync to API
4. **On Reconnect**: Sync pending changes to API

```typescript
// Sync pending changes when back online
const syncOnReconnect = () => {
  window.addEventListener('online', () => {
    useProgressStore.getState().syncProgress();
    useBookmarkStore.getState().syncBookmarks();
  });
};
```

---

## Selectors and Derived State

Zustand supports selectors for performance optimization:

```typescript
// Select only what you need
const streak = useProgressStore((state) => state.streak);
const isAuthenticated = useAuthStore((state) => state.status === 'authenticated');

// Computed selectors with shallow comparison
import { shallow } from 'zustand/shallow';

const { streak, stats } = useProgressStore(
  (state) => ({
    streak: state.streak,
    stats: state.stats,
  }),
  shallow
);

// Derived state
const isOnStreak = useProgressStore((state) => state.streak.currentStreak > 0);
const completionPercentage = useProgressStore((state) => {
  const progress = state.seriesProgress['series-id'];
  return progress ? (progress.completedDevotionals / progress.totalDevotionals) * 100 : 0;
});
```

---

## Best Practices

### 1. Use Selectors
```typescript
// Good - only re-renders when streak changes
const streak = useProgressStore((state) => state.streak);

// Bad - re-renders on any state change
const store = useProgressStore();
const streak = store.streak;
```

### 2. Separate Concerns
```typescript
// Good - focused stores
const { session } = useAuthStore();
const { profile } = useUserStore();

// Bad - monolithic store
const { session, profile, devotionals, bookmarks } = useAppStore();
```

### 3. Handle Loading States
```typescript
function Component() {
  const { data, isLoading, error } = useStore();

  if (isLoading) return <Skeleton />;
  if (error) return <ErrorDisplay error={error} />;
  if (!data) return null;

  return <Content data={data} />;
}
```

### 4. Optimistic Updates
```typescript
const toggleBookmark = async (id: string) => {
  // Update UI immediately
  set({ bookmarks: [...bookmarks, newBookmark] });

  try {
    // Sync to server
    await api.addBookmark(newBookmark);
  } catch (error) {
    // Revert on failure
    set({ bookmarks: originalBookmarks, error: error.message });
  }
};
```

### 5. Type Safety
```typescript
// Always define store types
interface StoreState {
  data: Data | null;
  isLoading: boolean;
  error: string | null;
  fetchData: () => Promise<void>;
}

export const useStore = create<StoreState>()((set) => ({
  // Implementation
}));
```

---

## Testing Stores

```typescript
import { renderHook, act } from '@testing-library/react-hooks';
import { useProgressStore } from '@/stores/progressStore';

describe('progressStore', () => {
  beforeEach(() => {
    // Reset store before each test
    useProgressStore.setState({
      streak: { currentStreak: 0, longestStreak: 0, ... },
      dailyProgress: [],
    });
  });

  it('should update streak on activity', () => {
    const { result } = renderHook(() => useProgressStore());

    act(() => {
      result.current.updateStreak('2024-01-20');
    });

    expect(result.current.streak.currentStreak).toBe(1);
  });
});
```

---

## DevTools Integration

Zustand integrates with Redux DevTools for debugging:

```typescript
import { devtools } from 'zustand/middleware';

export const useStore = create<StoreState>()(
  devtools(
    (set, get) => ({
      // ... implementation
    }),
    { name: 'euongelion-store' }
  )
);
```

Enable in browser:
1. Install Redux DevTools extension
2. Open DevTools
3. Navigate to "Redux" tab
4. Select "euongelion-store" instance

# Codebase Architecture Map

**Generated:** 2026-01-19
**Project:** EUONGELION
**Path:** /Users/meltmac/Documents/Personal/wkGD/EUONGELION-STARTUP/app

---

## Executive Summary

EUONGELION follows a Next.js 15 App Router architecture with a hybrid structure containing both `/app` and `/src` directories. The codebase is well-organized with clear separation of concerns between API routes, components, stores, and utility libraries.

---

## Directory Structure Overview

```
/app
├── __tests__/                 # Test files
├── api/                       # API route handlers
├── components/                # Shared React components
├── hooks/                     # Custom React hooks
├── lib/                       # Utility libraries
├── providers/                 # React context providers
├── src/                       # Main application source
│   ├── app/                   # Next.js App Router pages
│   ├── components/            # Additional components
│   ├── contexts/              # React contexts
│   ├── hooks/                 # Additional hooks
│   ├── lib/                   # Additional utilities
│   └── styles/                # Global styles
├── stores/                    # Zustand state stores
├── types/                     # TypeScript type definitions
├── public/                    # Static assets
├── settings/                  # Settings pages
├── onboarding/                # Onboarding pages
├── feedback/                  # Feedback pages
└── help/                      # Help pages
```

---

## Core Application Files

### Entry Points

| File | Purpose | Imports | Imported By |
|------|---------|---------|-------------|
| `/app/src/app/layout.tsx` | Root layout with fonts, metadata | Inter, Crimson_Pro fonts, globals.css | All pages |
| `/app/src/app/page.tsx` | Home page | Header, BottomNav | None (entry) |
| `/app/layout.tsx` | Alternative root layout | Fonts, ThemeProvider, globals.css | Pages |
| `/app/middleware.ts` | Request middleware | Security headers, CSP | All routes |

### Configuration Files

| File | Purpose |
|------|---------|
| `/app/next.config.js` | Next.js configuration with PWA, headers, images |
| `/app/tailwind.config.ts` | Tailwind CSS with EUONGELION brand colors |
| `/app/globals.css` | Global CSS with design tokens |
| `/app/tsconfig.json` | TypeScript configuration |
| `/app/package.json` | Dependencies and scripts |
| `/app/vitest.config.ts` | Test configuration |

---

## Pages (App Router)

### `/app/src/app/` - Main Pages

| File | Route | Purpose | Key Imports |
|------|-------|---------|-------------|
| `page.tsx` | `/` | Home/Today's devotional | Header, BottomNav |
| `layout.tsx` | Root | Layout wrapper | Fonts, globals.css |
| `devotional/[id]/page.tsx` | `/devotional/:id` | Devotional reader | Header, BottomNav |
| `series/page.tsx` | `/series` | Series listing | Header, BottomNav |
| `series/[slug]/page.tsx` | `/series/:slug` | Series detail | Header, BottomNav |
| `settings/page.tsx` | `/settings` | User settings | Header, BottomNav |
| `soul-audit/page.tsx` | `/soul-audit` | Soul audit quiz | Header, BottomNav |
| `discovery/page.tsx` | `/discovery` | Content discovery | Custom layout |

---

## API Routes

### Location: `/app/api/`

| Route | Methods | Purpose | Response Types |
|-------|---------|---------|----------------|
| `/api/devotionals/route.ts` | GET, POST | List/Create devotionals | DevotionalsResponse, ApiError |
| `/api/devotionals/[id]/route.ts` | GET, PUT, DELETE | CRUD single devotional | Devotional, ApiError |
| `/api/series/route.ts` | GET, POST | List/Create series | SeriesListResponse, ApiError |
| `/api/series/[slug]/route.ts` | GET, PUT, DELETE | CRUD single series | Series, ApiError |
| `/api/user/progress/route.ts` | GET, POST, DELETE | User reading progress | UserProgressResponse, ApiError |
| `/api/user/bookmarks/route.ts` | GET, POST, PUT, DELETE | User bookmarks | BookmarksListResponse, ApiError |
| `/api/soul-audit/questions/route.ts` | GET | Soul audit questions | Questions array |
| `/api/soul-audit/submit/route.ts` | POST, GET | Submit/Get audit results | SoulAuditResult, ApiError |
| `/api/feedback/route.ts` | POST | Submit feedback | Success response |
| `/api/health/route.ts` | GET | Health check | Health status |

---

## State Management (Zustand Stores)

### Location: `/app/stores/`

| Store | File | Purpose | Key State |
|-------|------|---------|-----------|
| **AuthStore** | `authStore.ts` | Authentication state | user, isAuthenticated, token |
| **DevotionalStore** | `devotionalStore.ts` | Current reading state | currentDevotional, readingState, history |
| **ProgressStore** | `progressStore.ts` | Reading progress tracking | seriesProgress, streaks |
| **BookmarkStore** | `bookmarkStore.ts` | User bookmarks | bookmarks, folders |
| **UserStore** | `userStore.ts` | User profile/preferences | profile, preferences |

### Store Middleware

| File | Purpose |
|------|---------|
| `middleware.ts` | Logging, persistence (localStorage, IndexedDB) |
| `types.ts` | Store type definitions |

---

## Component Architecture

### UI Components (`/app/components/ui/`)

| Component | Purpose | Variants/Props |
|-----------|---------|----------------|
| `Button.tsx` | Primary button | primary, secondary, ghost, outline, danger, link |
| `Card.tsx` | Content card | default, elevated, outlined, ghost, glass |
| `Modal.tsx` | Modal dialog | title, description, onClose |
| `Drawer.tsx` | Slide-out drawer | side, title, onClose |
| `Toast.tsx` | Toast notifications | success, error, warning, info |
| `Skeleton.tsx` | Loading placeholder | Various sizes |

### Devotional Components (`/app/components/devotional/`)

| Component | Purpose | Used By |
|-----------|---------|---------|
| `DevotionalCard.tsx` | Card for devotional preview | Series page, Discovery |
| `DevotionalReader.tsx` | Full devotional reading view | Devotional page |
| `ProgressIndicator.tsx` | Reading progress display | Reader |
| `ReflectionPrompt.tsx` | Reflection question UI | Reader |
| `ScriptureBlock.tsx` | Scripture text display | Reader |

### Layout Components (`/app/components/layout/`, `/app/src/components/layout/`)

| Component | Purpose | Used By |
|-----------|---------|---------|
| `Header.tsx` | Top navigation header | All pages |
| `BottomNav.tsx` | Mobile bottom navigation | All pages |
| `Layout.tsx` | Page layout wrapper | Various |
| `Sidebar.tsx` | Desktop sidebar navigation | Settings |

### Feature Components

| Directory | Components | Purpose |
|-----------|------------|---------|
| `/app/components/animated/` | FadeIn, SlideIn, Collapse, etc. | Animation wrappers |
| `/app/components/icons/` | Organized icon sets | SVG icons |
| `/app/components/images/` | Avatar, OptimizedImage, etc. | Image handling |
| `/app/components/loading/` | Spinner, Skeleton, ProgressBar | Loading states |
| `/app/components/navigation/` | BackButton, Breadcrumbs, Pagination | Navigation UI |
| `/app/components/notifications/` | Toast, NotificationCenter | Notifications |
| `/app/components/offline/` | OfflinePage, CachedContent | Offline support |
| `/app/components/settings/` | ProfileEditor, SettingsNav | Settings UI |
| `/app/components/seo/` | JsonLd, CanonicalUrl | SEO metadata |
| `/app/src/components/a11y/` | SkipLink, FocusTrap, LiveRegion | Accessibility |
| `/app/src/components/auth/` | LoginForm, SignupForm | Authentication |
| `/app/src/components/error/` | ErrorBoundary, GlobalErrorBoundary | Error handling |
| `/app/src/components/share/` | ShareButton, ShareModal, QuoteCard | Social sharing |
| `/app/src/components/soul-audit/` | QuestionCard, AnswerOptions | Soul audit UI |

---

## Utility Libraries

### Location: `/app/lib/`

| Module | Purpose | Key Exports |
|--------|---------|-------------|
| `analytics/` | Analytics tracking | analytics.ts, consent.ts, events.ts |
| `animations/` | Animation utilities | gestures.ts, transitions.ts, variants.ts |
| `content/` | Content processing | loader.ts, parser.ts, mdx.ts, validator.ts |
| `cron/` | Scheduled tasks | scheduler.ts, notifications.ts, cleanup.ts |
| `features/` | Feature flags | context.ts, flags.ts, provider.ts |
| `feedback/` | Feedback submission | submit.ts, categories.ts |
| `feeds/` | RSS feed generation | rss.ts, utils.ts |
| `images/` | Image optimization | cdn.ts, blur.ts, optimize.ts, resize.ts |
| `monitoring/` | Performance monitoring | health.ts, metrics.ts, performance.ts |
| `notes/` | User notes | storage.ts, sync.ts, types.ts |
| `notifications/` | Push notifications | push.ts, permissions.ts, subscription.ts |
| `onboarding/` | Onboarding flow | steps.ts, progress.ts, defaults.ts |
| `reading/` | Reading experience | highlight.ts, notes.ts, position.ts |
| `security/` | Security utilities | csrf.ts, headers.ts, rateLimit.ts, sanitize.ts |
| `seo/` | SEO utilities | metadata.ts |
| `settings/` | Settings management | defaults.ts, sync.ts, validation.ts |
| `supabase/` | Supabase client | client.ts, server.ts, middleware.ts |
| `theme/` | Theme management | colors.ts, themes.ts, utils.ts |
| `validation/` | Input validation | schemas.ts, validators.ts, messages.ts |

### Location: `/app/src/lib/`

| Module | Purpose | Key Exports |
|--------|---------|-------------|
| `a11y/` | Accessibility utilities | ariaLabels.ts, focusRing.ts, keyboardShortcuts.ts |
| `auth/` | Authentication | auth.ts, session.ts, supabase.ts |
| `error/` | Error handling | errorHandler.ts, errors.ts, logger.ts, sentry.ts |
| `progress/` | Progress tracking | achievements.ts, milestones.ts, stats.ts, streak.ts |
| `search/` | Search functionality | filters.ts, highlight.ts, query.ts, rank.ts |
| `share/` | Sharing utilities | clipboard.ts, images.ts, platforms.ts, urls.ts |
| `soul-audit/` | Soul audit logic | categories.ts, questions.ts, scoring.ts |

---

## Custom Hooks

### Location: `/app/hooks/`

| Hook | Purpose | Dependencies |
|------|---------|--------------|
| `useAnalytics.ts` | Analytics tracking | lib/analytics |
| `useFeatureFlag.ts` | Feature flag access | lib/features |
| `useForm.ts` | Form state management | React |
| `useNotifications.ts` | Notification management | lib/notifications |
| `useOfflineDevotionals.ts` | Offline caching | IndexedDB |
| `useOnboarding.ts` | Onboarding state | lib/onboarding |
| `useOnlineStatus.ts` | Network status | Browser APIs |
| `usePushNotifications.ts` | Push notification | lib/notifications |
| `useServiceWorker.ts` | Service worker | PWA |
| `useTheme.ts` | Theme switching | lib/theme |
| `useToast.ts` | Toast notifications | components/Toast |

### Location: `/app/src/hooks/`

| Hook | Purpose | Dependencies |
|------|---------|--------------|
| `useAnnounce.ts` | Screen reader announcements | a11y |
| `useCanShare.ts` | Web Share API detection | Browser APIs |
| `useClipboard.ts` | Clipboard operations | Browser APIs |
| `useFocusManagement.ts` | Focus control | a11y |
| `useFocusVisible.ts` | Focus visibility | a11y |
| `useKeyboardNavigation.ts` | Keyboard handling | a11y |
| `useReducedMotion.ts` | Motion preferences | a11y |
| `useShare.ts` | Share functionality | lib/share |

---

## Type Definitions

### Location: `/app/types/`

| File | Defines |
|------|---------|
| `index.ts` | Central type exports (re-exports all) |
| `devotional.ts` | Devotional, ImmersionLevel, Scripture types |
| `series.ts` | Series, SeriesProgress, SeriesCard types |
| `user.ts` | User, UserProfile, Preferences types |
| `soul-audit.ts` | SoulAuditQuestion, Response, Result types |
| `navigation.ts` | AppRoute, NavigationItem types |
| `api.ts` | ApiResponse, ApiError, endpoint types |
| `content.ts` | ContentSection, SearchDocument types |
| `progress.ts` | StreakData, Milestone, Achievement types |
| `reading.ts` | ReadingPosition, Highlight, FontConfig types |
| `database.ts` | Database schema types |

---

## Data Flow Diagram

```
┌─────────────────────────────────────────────────────────────────┐
│                         User Interface                          │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────────┐    │
│  │   Pages  │  │Components│  │  Hooks   │  │   Contexts   │    │
│  └────┬─────┘  └────┬─────┘  └────┬─────┘  └──────┬───────┘    │
└───────┼─────────────┼─────────────┼───────────────┼────────────┘
        │             │             │               │
        ▼             ▼             ▼               ▼
┌─────────────────────────────────────────────────────────────────┐
│                      State Management                            │
│  ┌───────────┐  ┌─────────────┐  ┌────────────┐  ┌───────────┐ │
│  │ AuthStore │  │DevotionalSt.│  │ProgressSt. │  │ UserStore │ │
│  └─────┬─────┘  └──────┬──────┘  └──────┬─────┘  └─────┬─────┘ │
└────────┼───────────────┼────────────────┼──────────────┼───────┘
         │               │                │              │
         ▼               ▼                ▼              ▼
┌─────────────────────────────────────────────────────────────────┐
│                        API Layer                                 │
│  ┌────────────────┐  ┌─────────────────┐  ┌──────────────────┐ │
│  │ /api/devotionals│  │   /api/series   │  │  /api/user/*     │ │
│  └────────┬───────┘  └────────┬────────┘  └────────┬─────────┘ │
└───────────┼───────────────────┼────────────────────┼───────────┘
            │                   │                    │
            ▼                   ▼                    ▼
┌─────────────────────────────────────────────────────────────────┐
│                      Data Layer                                  │
│  ┌──────────────────┐  ┌─────────────────┐  ┌────────────────┐ │
│  │  Supabase DB     │  │  localStorage   │  │   IndexedDB    │ │
│  │  (PostgreSQL)    │  │  (Persistence)  │  │ (Offline Cache)│ │
│  └──────────────────┘  └─────────────────┘  └────────────────┘ │
└─────────────────────────────────────────────────────────────────┘
```

---

## Import/Export Relationships

### Most Imported Files

1. **`/app/types/index.ts`** - Central type exports
2. **`/app/components/ui/Button.tsx`** - Primary button component
3. **`/app/components/layout/Header.tsx`** - Header component
4. **`/app/components/layout/BottomNav.tsx`** - Bottom navigation
5. **`/app/lib/supabase/client.ts`** - Database client

### Import Patterns

- Types: `import type { X } from '@/types'`
- Components: `import { Button } from '@/components/ui/Button'`
- Hooks: `import { useTheme } from '@/hooks/useTheme'`
- Stores: `import { useAuthStore } from '@/stores/authStore'`
- Libraries: `import { sanitizeHtml } from '@/lib/security/sanitize'`

---

## Architecture Observations

### Strengths
1. Clear separation between UI, state, and data layers
2. Comprehensive type definitions
3. Good use of custom hooks for shared logic
4. Organized component hierarchy
5. Security utilities are well-implemented

### Areas for Improvement
1. Duplicate structure between `/app/` and `/app/src/` needs consolidation
2. API routes lack database integration (TODO placeholders)
3. Some components exist in both locations
4. Missing integration between stores and API layer

### Recommended Consolidation
Consider merging:
- `/app/components/layout/` and `/app/src/components/layout/`
- `/app/hooks/` and `/app/src/hooks/`
- `/app/lib/` and `/app/src/lib/`

---

*Report generated by overnight autonomous analysis*

# EUONGELION Component Documentation

## Overview

EUONGELION uses a modular component architecture organized by feature domain. Components are built with React 19, TypeScript, and Tailwind CSS, following the "Sacred Minimalism" design philosophy.

**Component Location**: `/app/components/`

---

## Component Categories

| Category | Purpose | Count |
|----------|---------|-------|
| `animated/` | Animation wrappers and motion components | 8 |
| `devotional/` | Devotional content display | 5 |
| `features/` | Feature flags and gates | 2 |
| `feedback/` | User feedback forms | 3 |
| `icons/` | Icon components | 1 |
| `images/` | Image components with optimization | 6 |
| `layout/` | Layout structure components | 4 |
| `loading/` | Loading states and skeletons | 9 |
| `navigation/` | Navigation components | 8 |
| `notifications/` | Toasts and notifications | 5 |
| `offline/` | PWA offline support | 3 |
| `performance/` | Performance monitoring | 2 |
| `seo/` | SEO helpers | 3 |

---

## Devotional Components

### DevotionalCard

**Purpose**: Displays a devotional preview card for lists and grids.

**Location**: `/app/components/devotional/DevotionalCard.tsx`

**Props Interface**:
```typescript
interface DevotionalCardProps {
  id: string;
  title: string;
  subtitle?: string;
  slug: string;
  scriptureRef: string;
  imageUrl?: string;
  readingTimeMinutes: number;
  seriesName?: string;
  seriesSlug?: string;
  dayNumber?: number;
  isPremium?: boolean;
  isFeatured?: boolean;
  isCompleted?: boolean;
  isBookmarked?: boolean;
  onBookmarkToggle?: (id: string) => void;
  variant?: 'default' | 'compact' | 'featured';
  className?: string;
}
```

**Usage Example**:
```tsx
<DevotionalCard
  id="uuid-here"
  title="Finding Peace in Chaos"
  subtitle="Day 1 of 7"
  slug="finding-peace-in-chaos"
  scriptureRef="Philippians 4:6-7"
  imageUrl="/images/peace.jpg"
  readingTimeMinutes={5}
  seriesName="Peace Series"
  seriesSlug="peace-series"
  dayNumber={1}
  isPremium={false}
  isCompleted={true}
  isBookmarked={false}
  onBookmarkToggle={(id) => toggleBookmark(id)}
  variant="default"
/>
```

**Dependencies**:
- `next/link`
- `ImageWithFallback`
- `Icon`
- Tailwind CSS classes

---

### DevotionalReader

**Purpose**: Full devotional content display with immersion levels and reading tracking.

**Location**: `/app/components/devotional/DevotionalReader.tsx`

**Props Interface**:
```typescript
interface DevotionalReaderProps {
  devotional: Devotional;
  initialImmersionLevel?: ImmersionLevel;
  onProgressUpdate?: (progress: DailyProgress) => void;
  onComplete?: () => void;
  showReflectionPrompts?: boolean;
  showPrayer?: boolean;
  className?: string;
}

type ImmersionLevel = '1-minute' | '5-minute' | '15-minute';
```

**Usage Example**:
```tsx
<DevotionalReader
  devotional={devotionalData}
  initialImmersionLevel="5-minute"
  onProgressUpdate={(progress) => recordProgress(progress)}
  onComplete={() => showCompletionModal()}
  showReflectionPrompts={true}
  showPrayer={true}
/>
```

**Features**:
- Immersion level selector (1, 5, or 15 minute versions)
- Reading time tracking
- Scroll position persistence
- Reflection question prompts
- Prayer section
- Progress auto-save

**Dependencies**:
- `ScriptureBlock`
- `ReflectionPrompt`
- `ProgressIndicator`
- `useDevotionalStore`

---

### ScriptureBlock

**Purpose**: Beautifully formatted scripture passage display.

**Location**: `/app/components/devotional/ScriptureBlock.tsx`

**Props Interface**:
```typescript
interface ScriptureBlockProps {
  reference: string;
  text: string;
  version?: BibleTranslation;
  showReference?: boolean;
  showVersion?: boolean;
  highlight?: boolean;
  size?: 'sm' | 'md' | 'lg' | 'xl';
  className?: string;
}
```

**Usage Example**:
```tsx
<ScriptureBlock
  reference="John 3:16"
  text="For God so loved the world..."
  version="ESV"
  showReference={true}
  showVersion={true}
  highlight={true}
  size="lg"
/>
```

**Dependencies**:
- Crimson Pro font (via Tailwind)
- Custom verse typography classes

---

### ReflectionPrompt

**Purpose**: Interactive reflection question with optional text input.

**Location**: `/app/components/devotional/ReflectionPrompt.tsx`

**Props Interface**:
```typescript
interface ReflectionPromptProps {
  questions: string[];
  onAnswerSave?: (questionIndex: number, answer: string) => void;
  savedAnswers?: Record<number, string>;
  showTextInput?: boolean;
  expandedByDefault?: boolean;
  className?: string;
}
```

**Usage Example**:
```tsx
<ReflectionPrompt
  questions={[
    "What stood out to you in this passage?",
    "How can you apply this today?"
  ]}
  onAnswerSave={(index, answer) => saveReflection(index, answer)}
  savedAnswers={{ 0: "The idea of peace..." }}
  showTextInput={true}
  expandedByDefault={false}
/>
```

---

### ProgressIndicator

**Purpose**: Visual reading progress indicator.

**Location**: `/app/components/devotional/ProgressIndicator.tsx`

**Props Interface**:
```typescript
interface ProgressIndicatorProps {
  current: number;
  total: number;
  showLabel?: boolean;
  showPercentage?: boolean;
  variant?: 'bar' | 'circle' | 'dots';
  size?: 'sm' | 'md' | 'lg';
  color?: 'gold' | 'olive' | 'default';
  className?: string;
}
```

**Usage Example**:
```tsx
<ProgressIndicator
  current={3}
  total={7}
  showLabel={true}
  showPercentage={true}
  variant="bar"
  size="md"
  color="gold"
/>
```

---

## Layout Components

### Layout

**Purpose**: Main application layout wrapper with header, sidebar, and content area.

**Location**: `/app/components/layout/Layout.tsx`

**Props Interface**:
```typescript
interface LayoutProps {
  children: React.ReactNode;
  showHeader?: boolean;
  showSidebar?: boolean;
  showBottomNav?: boolean;
  headerTitle?: string;
  headerAction?: React.ReactNode;
  className?: string;
}
```

**Usage Example**:
```tsx
<Layout
  showHeader={true}
  showSidebar={true}
  showBottomNav={true}
  headerTitle="Daily Devotional"
>
  <DevotionalReader devotional={data} />
</Layout>
```

---

### Header

**Purpose**: Top navigation header with title and actions.

**Location**: `/app/components/layout/Header.tsx`

**Props Interface**:
```typescript
interface HeaderProps {
  title?: string;
  showBackButton?: boolean;
  showMenuButton?: boolean;
  leftAction?: React.ReactNode;
  rightAction?: React.ReactNode;
  transparent?: boolean;
  sticky?: boolean;
  className?: string;
}
```

---

### Sidebar

**Purpose**: Desktop sidebar navigation.

**Location**: `/app/components/layout/Sidebar.tsx`

**Props Interface**:
```typescript
interface SidebarProps {
  isOpen: boolean;
  onClose: () => void;
  className?: string;
}
```

---

### BottomNav

**Purpose**: Mobile bottom navigation bar.

**Location**: `/app/components/layout/BottomNav.tsx`

**Props Interface**:
```typescript
interface BottomNavProps {
  activeItem?: string;
  className?: string;
}
```

---

## Animation Components

### FadeIn

**Purpose**: Fade-in animation wrapper.

**Location**: `/app/components/animated/FadeIn.tsx`

**Props Interface**:
```typescript
interface FadeInProps {
  children: React.ReactNode;
  delay?: number;
  duration?: number;
  direction?: 'up' | 'down' | 'left' | 'right' | 'none';
  className?: string;
}
```

**Usage Example**:
```tsx
<FadeIn delay={200} duration={500} direction="up">
  <DevotionalCard {...props} />
</FadeIn>
```

---

### SlideIn

**Purpose**: Slide-in animation wrapper.

**Location**: `/app/components/animated/SlideIn.tsx`

**Props Interface**:
```typescript
interface SlideInProps {
  children: React.ReactNode;
  direction: 'left' | 'right' | 'top' | 'bottom';
  delay?: number;
  duration?: number;
  distance?: number;
  className?: string;
}
```

---

### Stagger

**Purpose**: Stagger child animations sequentially.

**Location**: `/app/components/animated/Stagger.tsx`

**Props Interface**:
```typescript
interface StaggerProps {
  children: React.ReactNode;
  delayBetween?: number;
  initialDelay?: number;
  className?: string;
}
```

**Usage Example**:
```tsx
<Stagger delayBetween={100} initialDelay={200}>
  {devotionals.map((d) => (
    <DevotionalCard key={d.id} {...d} />
  ))}
</Stagger>
```

---

### PageTransition

**Purpose**: Page-level transition wrapper.

**Location**: `/app/components/animated/PageTransition.tsx`

**Props Interface**:
```typescript
interface PageTransitionProps {
  children: React.ReactNode;
  className?: string;
}
```

---

### Collapse

**Purpose**: Collapsible content section with animation.

**Location**: `/app/components/animated/Collapse.tsx`

**Props Interface**:
```typescript
interface CollapseProps {
  children: React.ReactNode;
  isOpen: boolean;
  duration?: number;
  className?: string;
}
```

---

### SwipeableCard

**Purpose**: Card with swipe gestures for mobile.

**Location**: `/app/components/animated/SwipeableCard.tsx`

**Props Interface**:
```typescript
interface SwipeableCardProps {
  children: React.ReactNode;
  onSwipeLeft?: () => void;
  onSwipeRight?: () => void;
  leftAction?: React.ReactNode;
  rightAction?: React.ReactNode;
  threshold?: number;
  className?: string;
}
```

---

### PullToRefresh

**Purpose**: Pull-to-refresh gesture for mobile lists.

**Location**: `/app/components/animated/PullToRefresh.tsx`

**Props Interface**:
```typescript
interface PullToRefreshProps {
  children: React.ReactNode;
  onRefresh: () => Promise<void>;
  disabled?: boolean;
  threshold?: number;
  className?: string;
}
```

---

## Loading Components

### Skeleton

**Purpose**: Base skeleton loading placeholder.

**Location**: `/app/components/loading/Skeleton.tsx`

**Props Interface**:
```typescript
interface SkeletonProps {
  width?: string | number;
  height?: string | number;
  variant?: 'text' | 'circular' | 'rectangular' | 'rounded';
  animation?: 'pulse' | 'wave' | 'none';
  className?: string;
}
```

**Usage Example**:
```tsx
<Skeleton width="100%" height={200} variant="rounded" animation="pulse" />
```

---

### SkeletonCard

**Purpose**: Skeleton placeholder for devotional cards.

**Location**: `/app/components/loading/SkeletonCard.tsx`

**Props Interface**:
```typescript
interface SkeletonCardProps {
  variant?: 'default' | 'compact' | 'featured';
  count?: number;
  className?: string;
}
```

**Usage Example**:
```tsx
// Show 3 skeleton cards while loading
<SkeletonCard variant="default" count={3} />
```

---

### Spinner

**Purpose**: Loading spinner indicator.

**Location**: `/app/components/loading/Spinner.tsx`

**Props Interface**:
```typescript
interface SpinnerProps {
  size?: 'sm' | 'md' | 'lg' | 'xl';
  color?: 'gold' | 'white' | 'dark' | 'current';
  label?: string;
  className?: string;
}
```

---

### LoadingOverlay

**Purpose**: Full-screen loading overlay.

**Location**: `/app/components/loading/LoadingOverlay.tsx`

**Props Interface**:
```typescript
interface LoadingOverlayProps {
  isLoading: boolean;
  message?: string;
  transparent?: boolean;
  className?: string;
}
```

---

### ProgressBar

**Purpose**: Linear progress indicator.

**Location**: `/app/components/loading/ProgressBar.tsx`

**Props Interface**:
```typescript
interface ProgressBarProps {
  value: number;
  max?: number;
  showLabel?: boolean;
  labelPosition?: 'inside' | 'outside' | 'none';
  color?: 'gold' | 'olive' | 'burgundy' | 'default';
  size?: 'sm' | 'md' | 'lg';
  animated?: boolean;
  className?: string;
}
```

---

## Image Components

### OptimizedImage

**Purpose**: Next.js Image component with lazy loading and blur placeholder.

**Location**: `/app/components/images/OptimizedImage.tsx`

**Props Interface**:
```typescript
interface OptimizedImageProps {
  src: string;
  alt: string;
  width?: number;
  height?: number;
  fill?: boolean;
  priority?: boolean;
  quality?: number;
  placeholder?: 'blur' | 'empty';
  blurDataURL?: string;
  sizes?: string;
  className?: string;
  objectFit?: 'contain' | 'cover' | 'fill' | 'none';
}
```

---

### ImageWithFallback

**Purpose**: Image component with fallback for broken images.

**Location**: `/app/components/images/ImageWithFallback.tsx`

**Props Interface**:
```typescript
interface ImageWithFallbackProps extends OptimizedImageProps {
  fallbackSrc?: string;
  fallbackComponent?: React.ReactNode;
  onError?: () => void;
}
```

---

### Avatar

**Purpose**: User avatar with fallback initials.

**Location**: `/app/components/images/Avatar.tsx`

**Props Interface**:
```typescript
interface AvatarProps {
  src?: string;
  alt?: string;
  name?: string;
  size?: 'xs' | 'sm' | 'md' | 'lg' | 'xl';
  status?: 'online' | 'offline' | 'away';
  showStatus?: boolean;
  className?: string;
}
```

---

## Navigation Components

### NavLink

**Purpose**: Navigation link with active state.

**Location**: `/app/components/navigation/NavLink.tsx`

**Props Interface**:
```typescript
interface NavLinkProps {
  href: string;
  children: React.ReactNode;
  icon?: React.ReactNode;
  activeClassName?: string;
  exact?: boolean;
  className?: string;
}
```

---

### BackButton

**Purpose**: Navigation back button.

**Location**: `/app/components/navigation/BackButton.tsx`

**Props Interface**:
```typescript
interface BackButtonProps {
  fallbackHref?: string;
  label?: string;
  showLabel?: boolean;
  className?: string;
}
```

---

### Breadcrumbs

**Purpose**: Breadcrumb navigation trail.

**Location**: `/app/components/navigation/Breadcrumbs.tsx`

**Props Interface**:
```typescript
interface BreadcrumbsProps {
  items: Array<{
    label: string;
    href?: string;
  }>;
  separator?: React.ReactNode;
  className?: string;
}
```

---

### Pagination

**Purpose**: Page navigation controls.

**Location**: `/app/components/navigation/Pagination.tsx`

**Props Interface**:
```typescript
interface PaginationProps {
  currentPage: number;
  totalPages: number;
  onPageChange: (page: number) => void;
  showFirstLast?: boolean;
  siblingCount?: number;
  className?: string;
}
```

---

### TabNav

**Purpose**: Tab navigation component.

**Location**: `/app/components/navigation/TabNav.tsx`

**Props Interface**:
```typescript
interface TabNavProps {
  tabs: Array<{
    id: string;
    label: string;
    icon?: React.ReactNode;
    badge?: number;
  }>;
  activeTab: string;
  onTabChange: (tabId: string) => void;
  variant?: 'default' | 'pills' | 'underline';
  className?: string;
}
```

---

## Notification Components

### Toast

**Purpose**: Toast notification message.

**Location**: `/app/components/notifications/Toast.tsx`

**Props Interface**:
```typescript
interface ToastProps {
  id: string;
  type: 'success' | 'error' | 'warning' | 'info';
  title: string;
  message?: string;
  duration?: number;
  action?: {
    label: string;
    onClick: () => void;
  };
  onDismiss: (id: string) => void;
}
```

---

### ToastContainer

**Purpose**: Container for positioning toasts.

**Location**: `/app/components/notifications/ToastContainer.tsx`

**Props Interface**:
```typescript
interface ToastContainerProps {
  position?: 'top-right' | 'top-left' | 'bottom-right' | 'bottom-left' | 'top-center' | 'bottom-center';
  className?: string;
}
```

---

### NotificationBadge

**Purpose**: Badge indicator for unread notifications.

**Location**: `/app/components/notifications/NotificationBadge.tsx`

**Props Interface**:
```typescript
interface NotificationBadgeProps {
  count: number;
  max?: number;
  showZero?: boolean;
  size?: 'sm' | 'md' | 'lg';
  color?: 'red' | 'gold' | 'default';
  className?: string;
}
```

---

## Offline Components

### OfflineIndicator

**Purpose**: Shows when the app is offline.

**Location**: `/app/components/offline/OfflineIndicator.tsx`

**Props Interface**:
```typescript
interface OfflineIndicatorProps {
  show?: boolean;
  message?: string;
  position?: 'top' | 'bottom';
  className?: string;
}
```

---

### OfflinePage

**Purpose**: Full offline fallback page.

**Location**: `/app/components/offline/OfflinePage.tsx`

**Props Interface**:
```typescript
interface OfflinePageProps {
  title?: string;
  message?: string;
  showRetry?: boolean;
  onRetry?: () => void;
}
```

---

### CachedContent

**Purpose**: Display cached content when offline.

**Location**: `/app/components/offline/CachedContent.tsx`

**Props Interface**:
```typescript
interface CachedContentProps {
  children: React.ReactNode;
  fallback?: React.ReactNode;
  cacheKey: string;
  maxAge?: number;
}
```

---

## Feature Flag Components

### FeatureFlag

**Purpose**: Conditionally render based on feature flag.

**Location**: `/app/components/features/FeatureFlag.tsx`

**Props Interface**:
```typescript
interface FeatureFlagProps {
  flag: string;
  children: React.ReactNode;
  fallback?: React.ReactNode;
}
```

**Usage Example**:
```tsx
<FeatureFlag flag="premium-features" fallback={<UpgradePrompt />}>
  <PremiumContent />
</FeatureFlag>
```

---

### FeatureGate

**Purpose**: Gate feature access with subscription check.

**Location**: `/app/components/features/FeatureGate.tsx`

**Props Interface**:
```typescript
interface FeatureGateProps {
  requiredTier: 'free' | 'premium' | 'lifetime';
  children: React.ReactNode;
  fallback?: React.ReactNode;
  showUpgradePrompt?: boolean;
}
```

---

## Design System Integration

### Color Tokens

All components use the EUONGELION color palette:
- `tehom` - Primary dark (backgrounds)
- `scroll` - Light backgrounds (parchment)
- `gold` - Accent (CTAs, highlights)
- `burgundy` - Passion, emphasis
- `olive` - Growth, wisdom
- `shalom-blue` - Peace, depth

### Typography

- `font-crimson` - Headings and scripture
- `font-sans` - Body text and UI
- Custom verse sizing: `text-verse-sm`, `text-verse`, `text-verse-lg`, `text-verse-xl`

### Spacing

- `reading-sm`, `reading`, `reading-lg`, `reading-xl` - Reading content
- `page-sm`, `page`, `page-lg`, `page-xl` - Page margins
- `section`, `section-lg`, `section-xl` - Section spacing

### Accessibility

All components follow WCAG 2.1 AA standards:
- Minimum touch targets of 44px
- Proper ARIA labels
- Keyboard navigation support
- Focus indicators
- Color contrast ratios

---

## Best Practices

1. **Use TypeScript strictly**: All props must be typed
2. **Prefer composition**: Build complex components from simple ones
3. **Keep components focused**: One responsibility per component
4. **Use design tokens**: Never use arbitrary values
5. **Mobile-first**: Design for mobile, enhance for desktop
6. **Dark mode support**: All components support both themes
7. **Accessibility first**: ARIA labels, keyboard support, contrast

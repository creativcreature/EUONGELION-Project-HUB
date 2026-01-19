# EUONGELION Component API Documentation

**Document:** 63-component-api-documentation.md
**Generated:** 2026-01-19
**Status:** Design System Reference

---

## Overview

This document provides comprehensive API documentation for all reusable components in the EUONGELION design system. Each component includes props, variants, default values, and usage examples.

---

## Table of Contents

1. [UI Components](#ui-components)
   - [Button](#button)
   - [Card](#card)
   - [Modal](#modal)
   - [Toast](#toast)
   - [Skeleton](#skeleton)
2. [Layout Components](#layout-components)
   - [Header](#header)
   - [BottomNav](#bottomnav)
3. [Accessibility Components](#accessibility-components)
   - [SkipLink](#skiplink)
   - [VisuallyHidden](#visuallyhidden)
   - [FocusTrap](#focustrap)
   - [LiveRegion](#liveregion)
   - [ReducedMotion](#reducedmotion)
4. [Soul Audit Components](#soul-audit-components)
   - [QuestionCard](#questioncard)
   - [ProgressBar](#progressbar)
5. [Share Components](#share-components)
   - [ShareButton](#sharebutton)
   - [ShareModal](#sharemodal)
   - [QuoteCard](#quotecard)
6. [Error Components](#error-components)
   - [ErrorBoundary](#errorboundary)
7. [Auth Components](#auth-components)
   - [LoginForm](#loginform)
8. [Icon System](#icon-system)

---

## UI Components

### Button

**Location:** `/app/components/ui/Button.tsx`

A flexible button component with multiple variants and sizes.

#### Props

```typescript
interface ButtonProps extends ButtonHTMLAttributes<HTMLButtonElement> {
  /** Visual style variant */
  variant?: 'primary' | 'secondary' | 'ghost' | 'outline' | 'danger' | 'link';

  /** Button size */
  size?: 'sm' | 'md' | 'lg' | 'icon' | 'iconSm' | 'iconLg';

  /** Make button full width */
  fullWidth?: boolean;

  /** Icon to display before text */
  leftIcon?: ReactNode;

  /** Icon to display after text */
  rightIcon?: ReactNode;

  /** Show loading state */
  isLoading?: boolean;

  /** Text to show while loading */
  loadingText?: string;

  /** Button content */
  children: ReactNode;
}
```

#### Variants

| Variant | Description | Usage |
|---------|-------------|-------|
| `primary` | Gold background, dark text | Primary CTAs |
| `secondary` | Subtle background with border | Secondary actions |
| `ghost` | No background, text only | Tertiary actions |
| `outline` | Gold border, transparent background | Alternative CTA |
| `danger` | Burgundy background | Destructive actions |
| `link` | Underlined text | Inline links |

#### Sizes

| Size | Height | Padding | Usage |
|------|--------|---------|-------|
| `sm` | 36px (h-9) | 16px | Compact buttons |
| `md` | 48px (h-12) | 24px | **Default** |
| `lg` | 56px (h-14) | 32px | Prominent buttons |
| `icon` | 44px | - | Icon-only button |
| `iconSm` | 36px | - | Small icon button |
| `iconLg` | 56px | - | Large icon button |

#### Usage Examples

```jsx
import { Button } from '@/components/ui/Button';

// Primary button
<Button variant="primary">Continue</Button>

// With icon
<Button leftIcon={<ShareIcon />}>Share</Button>

// Loading state
<Button isLoading loadingText="Saving...">Save</Button>

// Full width
<Button fullWidth>Sign In</Button>

// Icon button
<Button variant="ghost" size="icon">
  <SettingsIcon />
</Button>

// Danger action
<Button variant="danger">Delete</Button>
```

---

### Card

**Location:** `/app/components/ui/Card.tsx`

Container component for grouping related content.

#### Props

```typescript
interface CardProps extends HTMLAttributes<HTMLDivElement> {
  /** Visual style variant */
  variant?: 'default' | 'elevated' | 'outlined' | 'ghost' | 'glass';

  /** Internal padding */
  padding?: 'none' | 'sm' | 'md' | 'lg';

  /** Make card interactive (clickable) */
  interactive?: boolean;

  /** Card content */
  children: ReactNode;
}
```

#### Variants

| Variant | Description |
|---------|-------------|
| `default` | Subtle background (`bg-scroll/5`) |
| `elevated` | With shadow, hover lift effect |
| `outlined` | Transparent with visible border |
| `ghost` | Transparent, no border |
| `glass` | Frosted glass effect (backdrop-blur) |

#### Padding

| Padding | Value |
|---------|-------|
| `none` | 0 |
| `sm` | 16px (p-4) |
| `md` | 24px (p-6) - **Default** |
| `lg` | 32px (p-8) |

#### Sub-Components

```typescript
// Card header with bottom border
<CardHeader>Title Area</CardHeader>

// Card title (heading)
<CardTitle as="h3">Card Title</CardTitle>

// Card description (subtitle)
<CardDescription>Brief description</CardDescription>

// Card content area
<CardContent>Main content</CardContent>

// Card footer with top border
<CardFooter>Actions</CardFooter>
```

#### Usage Examples

```jsx
import { Card, CardHeader, CardTitle, CardContent, CardFooter } from '@/components/ui/Card';

// Simple card
<Card>
  <p>Card content</p>
</Card>

// Elevated interactive card
<Card variant="elevated" interactive onClick={handleClick}>
  <CardTitle>Click Me</CardTitle>
</Card>

// Structured card
<Card>
  <CardHeader>
    <CardTitle>Devotional</CardTitle>
    <CardDescription>5 min read</CardDescription>
  </CardHeader>
  <CardContent>
    Content here...
  </CardContent>
  <CardFooter>
    <Button>Read</Button>
  </CardFooter>
</Card>
```

---

### Modal

**Location:** `/app/components/ui/Modal.tsx`

Overlay dialog for focused interactions.

#### Props

```typescript
interface ModalProps extends HTMLAttributes<HTMLDivElement> {
  /** Whether modal is visible */
  isOpen: boolean;

  /** Callback when modal should close */
  onClose: () => void;

  /** Modal title (optional) */
  title?: string;

  /** Modal description (optional) */
  description?: string;

  /** Modal width */
  size?: 'sm' | 'md' | 'lg' | 'xl' | 'full';

  /** Close when clicking backdrop */
  closeOnOverlayClick?: boolean;

  /** Close on Escape key */
  closeOnEscape?: boolean;

  /** Show close button */
  showCloseButton?: boolean;

  /** Modal content */
  children: ReactNode;
}
```

#### Sizes

| Size | Max Width |
|------|-----------|
| `sm` | 384px (max-w-sm) |
| `md` | 448px (max-w-md) - **Default** |
| `lg` | 512px (max-w-lg) |
| `xl` | 576px (max-w-xl) |
| `full` | calc(100vw - 2rem) |

#### Sub-Components

```typescript
// Modal action buttons area
<ModalActions>
  <Button variant="ghost" onClick={onClose}>Cancel</Button>
  <Button onClick={onConfirm}>Confirm</Button>
</ModalActions>
```

#### Usage Examples

```jsx
import { Modal, ModalActions } from '@/components/ui/Modal';

function MyComponent() {
  const [isOpen, setIsOpen] = useState(false);

  return (
    <>
      <Button onClick={() => setIsOpen(true)}>Open Modal</Button>

      <Modal
        isOpen={isOpen}
        onClose={() => setIsOpen(false)}
        title="Confirm Action"
        description="Are you sure you want to proceed?"
      >
        <p>Modal content goes here.</p>

        <ModalActions>
          <Button variant="ghost" onClick={() => setIsOpen(false)}>
            Cancel
          </Button>
          <Button onClick={handleConfirm}>
            Confirm
          </Button>
        </ModalActions>
      </Modal>
    </>
  );
}
```

---

### Toast

**Location:** `/app/components/ui/Toast.tsx`

Notification system for feedback messages.

#### ToastProvider Props

```typescript
interface ToastProviderProps {
  /** Child components */
  children: ReactNode;

  /** Toast position on screen */
  position?: 'top-right' | 'top-left' | 'bottom-right' | 'bottom-left' | 'top-center' | 'bottom-center';

  /** Maximum toasts shown at once */
  maxToasts?: number;
}
```

#### Toast Object

```typescript
interface Toast {
  id: string;
  title?: string;
  description?: string;
  variant?: 'default' | 'success' | 'error' | 'warning' | 'info';
  duration?: number;  // ms, default 5000
  action?: {
    label: string;
    onClick: () => void;
  };
}
```

#### useToast Hook

```typescript
const { toasts, addToast, removeToast, clearToasts } = useToast();

// Add a toast
const id = addToast({
  title: 'Success',
  description: 'Your changes were saved.',
  variant: 'success',
});

// Remove a toast
removeToast(id);

// Clear all toasts
clearToasts();
```

#### Usage Examples

```jsx
// In your app root
import { ToastProvider } from '@/components/ui/Toast';

function App() {
  return (
    <ToastProvider position="bottom-right" maxToasts={3}>
      <YourApp />
    </ToastProvider>
  );
}

// In any component
import { useToast } from '@/components/ui/Toast';

function MyComponent() {
  const { addToast } = useToast();

  const handleSave = () => {
    // ... save logic
    addToast({
      title: 'Saved!',
      description: 'Your devotional has been bookmarked.',
      variant: 'success',
    });
  };

  const handleError = () => {
    addToast({
      title: 'Error',
      description: 'Something went wrong.',
      variant: 'error',
      action: {
        label: 'Retry',
        onClick: () => handleSave(),
      },
    });
  };
}
```

---

### Skeleton

**Location:** `/app/components/ui/Skeleton.tsx`

Loading placeholder components.

#### Props

```typescript
interface SkeletonProps extends HTMLAttributes<HTMLDivElement> {
  /** Shape variant */
  variant?: 'default' | 'circle' | 'text' | 'title' | 'avatar' | 'card' | 'button' | 'image';

  /** Custom width */
  width?: string | number;

  /** Custom height */
  height?: string | number;
}
```

#### Preset Components

```typescript
// Multiple lines of text
<SkeletonText lines={3} />

// Card placeholder with optional image
<SkeletonCard showImage={true} />

// Avatar placeholder
<SkeletonAvatar size="md" />  // sm | md | lg

// Devotional card placeholder
<SkeletonDevotionalCard />

// Series card placeholder
<SkeletonSeriesCard />
```

#### Usage Examples

```jsx
import { Skeleton, SkeletonText, SkeletonCard } from '@/components/ui/Skeleton';

// Simple placeholder
<Skeleton width={200} height={20} />

// Text block
<SkeletonText lines={3} />

// Loading card
{isLoading ? <SkeletonCard /> : <ActualCard />}

// Avatar with text
<div className="flex items-center gap-3">
  <Skeleton variant="avatar" width={48} height={48} />
  <div>
    <Skeleton variant="title" width={120} />
    <Skeleton variant="text" width={80} />
  </div>
</div>
```

---

## Layout Components

### Header

**Location:** `/app/src/components/layout/Header.tsx`

Application header with navigation and actions.

#### Props

```typescript
interface HeaderProps {
  /** Show back button instead of logo */
  showBackButton?: boolean;

  /** Page title (replaces logo when set) */
  title?: string;
}
```

#### Usage Examples

```jsx
import { Header } from '@/components/layout/Header';

// Default header with logo
<Header />

// With back button
<Header showBackButton />

// With page title
<Header showBackButton title="Settings" />
```

---

### BottomNav

**Location:** `/app/src/components/layout/BottomNav.tsx`

Mobile bottom navigation bar.

#### Props

None - self-contained component with predefined navigation items.

#### Navigation Items

| Item | Path | Icon |
|------|------|------|
| Today | `/` | Sun icon |
| Series | `/series` | Book icon |
| Soul Audit | `/soul-audit` | Shield icon |
| Settings | `/settings` | Gear icon |

#### Usage Examples

```jsx
import { BottomNav } from '@/components/layout/BottomNav';

// In your layout
<main className="pb-16">
  {children}
</main>
<BottomNav />
```

---

## Accessibility Components

### SkipLink

**Location:** `/app/src/components/a11y/SkipLink.tsx`

Skip navigation link for keyboard users.

#### Props

```typescript
interface SkipLinkProps {
  /** ID of target element */
  targetId?: string;  // default: 'main-content'

  /** Link text */
  children?: ReactNode;  // default: 'Skip to main content'

  /** Additional CSS classes */
  className?: string;
}

// Multiple skip links
interface SkipLinksProps {
  links: Array<{
    targetId: string;
    label: string;
  }>;
  className?: string;
}
```

#### Usage Examples

```jsx
import { SkipLink, SkipLinks } from '@/components/a11y/SkipLink';

// Single skip link
<SkipLink targetId="main-content" />

// Multiple skip links
<SkipLinks
  links={[
    { targetId: 'main-content', label: 'Skip to content' },
    { targetId: 'navigation', label: 'Skip to navigation' },
  ]}
/>

// Target element
<main id="main-content" tabIndex={-1}>
  Content...
</main>
```

---

### VisuallyHidden

**Location:** `/app/src/components/a11y/VisuallyHidden.tsx`

Hide content visually while keeping it accessible to screen readers.

#### Props

```typescript
interface VisuallyHiddenProps<E extends ElementType = 'span'> {
  /** Element to render */
  as?: E;

  /** Make visible (for debugging) */
  visible?: boolean;

  /** Become visible on focus */
  focusable?: boolean;

  /** Additional CSS classes */
  className?: string;

  /** Content to hide */
  children: ReactNode;
}
```

#### Usage Examples

```jsx
import { VisuallyHidden } from '@/components/a11y/VisuallyHidden';

// Hidden label for icon button
<button>
  <ShareIcon />
  <VisuallyHidden>Share this devotional</VisuallyHidden>
</button>

// Hidden heading for screen readers
<VisuallyHidden as="h2">Navigation</VisuallyHidden>

// Focusable skip link
<VisuallyHidden as="a" href="#main" focusable>
  Skip to main content
</VisuallyHidden>
```

---

### FocusTrap

**Location:** `/app/src/components/a11y/FocusTrap.tsx`

Trap keyboard focus within a container (for modals/dialogs).

#### Props

```typescript
interface FocusTrapProps {
  /** Whether trap is active */
  active?: boolean;

  /** Auto-focus first element on mount */
  autoFocus?: boolean;

  /** Restore focus on unmount */
  restoreFocus?: boolean;

  /** Initial element to focus */
  initialFocus?: string | React.RefObject<HTMLElement>;

  /** Element to focus when closing */
  finalFocus?: string | React.RefObject<HTMLElement>;

  /** Escape key callback */
  onEscapeKey?: () => void;

  /** Click outside callback */
  onClickOutside?: () => void;

  /** Additional CSS classes */
  className?: string;

  /** Trapped content */
  children: ReactNode;
}

// Ref interface
interface FocusTrapRef {
  focusFirst: () => void;
  focusLast: () => void;
  getFocusableElements: () => HTMLElement[];
}
```

#### Usage Examples

```jsx
import { FocusTrap } from '@/components/a11y/FocusTrap';

function Modal({ isOpen, onClose }) {
  return (
    <FocusTrap
      active={isOpen}
      onEscapeKey={onClose}
      restoreFocus
    >
      <div role="dialog" aria-modal="true">
        <h2>Modal Title</h2>
        <button onClick={onClose}>Close</button>
      </div>
    </FocusTrap>
  );
}
```

---

### LiveRegion

**Location:** `/app/src/components/a11y/LiveRegion.tsx`

ARIA live region for screen reader announcements.

#### Props

```typescript
interface LiveRegionProps {
  /** Politeness level */
  politeness?: 'polite' | 'assertive' | 'off';

  /** Announce entire region or just changes */
  atomic?: boolean;

  /** What changes to announce */
  relevant?: 'additions' | 'removals' | 'text' | 'all' | 'additions text';

  /** Clear announcement after milliseconds */
  clearAfter?: number;

  /** Additional CSS classes */
  className?: string;

  /** Content to announce */
  children?: ReactNode;
}
```

#### Preset Components

```typescript
// Assertive (urgent) announcements
<AlertRegion>Error: {message}</AlertRegion>

// Polite (non-urgent) announcements
<StatusRegion>Saved successfully</StatusRegion>

// Global announcer for hooks
<Announcer id="a11y-announcer" />
```

#### Usage Examples

```jsx
import { LiveRegion, AlertRegion, StatusRegion } from '@/components/a11y/LiveRegion';

// Polite status update
<LiveRegion>
  {status && `Form submitted: ${status}`}
</LiveRegion>

// Urgent error message
<AlertRegion>
  {error && `Error: ${error}`}
</AlertRegion>

// Auto-clearing status
<StatusRegion clearAfter={3000}>
  Changes saved
</StatusRegion>
```

---

### ReducedMotion

**Location:** `/app/src/components/a11y/ReducedMotion.tsx`

Components for respecting reduced motion preferences.

#### Components

```typescript
// Show animated content with static fallback
<Motion fallback={<StaticImage />}>
  <AnimatedImage />
</Motion>

// Show static content with animated fallback
<NoMotion fallback={<AnimatedSpinner />}>
  <StaticText>Loading...</StaticText>
</NoMotion>

// Apply different classes based on preference
<MotionSafe
  motionClassName="animate-fade-in duration-300"
  reducedMotionClassName="opacity-100"
>
  <Card />
</MotionSafe>
```

#### Provider

```jsx
import { ReducedMotionProvider } from '@/components/a11y/ReducedMotion';

// Wrap app to provide context
<ReducedMotionProvider>
  <App />
</ReducedMotionProvider>
```

---

## Soul Audit Components

### QuestionCard

**Location:** `/app/src/components/soul-audit/QuestionCard.tsx`

Primary question display with textarea input.

#### Props

```typescript
interface QuestionCardProps {
  /** Callback when response is submitted */
  onSubmit: (response: string) => void;

  /** Callback when validation state changes */
  onValidationChange?: (result: ValidationResult) => void;

  /** Disable input */
  disabled?: boolean;

  /** Initial textarea value */
  initialValue?: string;
}
```

#### Usage Examples

```jsx
import { QuestionCard } from '@/components/soul-audit/QuestionCard';

<QuestionCard
  onSubmit={(response) => handleSubmit(response)}
  onValidationChange={(result) => setIsValid(result.isValid)}
/>
```

---

### ProgressBar

**Location:** `/app/src/components/soul-audit/ProgressBar.tsx`

Progress indicator for multi-step flows.

#### Props

```typescript
type AuditStep = 'intro' | 'question' | 'processing' | 'results' | 'series-selection';

interface ProgressBarProps {
  /** Current step */
  currentStep: AuditStep;

  /** Show step labels */
  showLabels?: boolean;
}

// Dot indicator for mobile
interface DotIndicatorProps {
  totalSteps: number;
  currentStep: number;  // 0-indexed
}
```

#### Related Components

```typescript
// Loading indicator
<ProcessingIndicator />

// Breathing animation for contemplative loading
<BreathIndicator />
```

#### Usage Examples

```jsx
import { ProgressBar, DotIndicator, ProcessingIndicator } from '@/components/soul-audit/ProgressBar';

// Simple progress bar
<ProgressBar currentStep="question" />

// With labels
<ProgressBar currentStep="results" showLabels />

// Mobile dots
<DotIndicator totalSteps={4} currentStep={1} />

// Processing state
{isProcessing && <ProcessingIndicator />}
```

---

## Share Components

### ShareButton

**Location:** `/app/src/components/share/ShareButton.tsx`

Main share button with native share and modal fallback.

#### Props

```typescript
interface ShareButtonProps {
  /** Devotional ID */
  devotionalId: string;

  /** Devotional title */
  title: string;

  /** Scripture reference */
  scriptureReference: string;

  /** Optional scripture text for quote sharing */
  scriptureText?: string;

  /** Button variant */
  variant?: 'primary' | 'secondary' | 'ghost' | 'icon';

  /** Button size */
  size?: 'sm' | 'md' | 'lg';

  /** Custom class names */
  className?: string;

  /** Show label text */
  showLabel?: boolean;

  /** Custom label */
  label?: string;
}
```

#### Usage Examples

```jsx
import { ShareButton } from '@/components/share/ShareButton';

// Full share button
<ShareButton
  devotionalId="abc123"
  title="Finding Peace"
  scriptureReference="John 14:27"
  scriptureText="Peace I leave with you..."
/>

// Icon only
<ShareButton
  devotionalId="abc123"
  title="Finding Peace"
  scriptureReference="John 14:27"
  variant="icon"
/>
```

---

### ShareModal

**Location:** `/app/src/components/share/ShareModal.tsx`

Modal with share options and quote card.

#### Props

```typescript
interface ShareModalProps {
  /** Whether modal is open */
  isOpen: boolean;

  /** Close callback */
  onClose: () => void;

  /** Devotional ID */
  devotionalId: string;

  /** Devotional title */
  title: string;

  /** Scripture reference */
  scriptureReference: string;

  /** Optional scripture text */
  scriptureText?: string;
}
```

---

### QuoteCard

**Location:** `/app/src/components/share/QuoteCard.tsx`

Beautiful shareable quote card with preview.

#### Props

```typescript
interface QuoteCardProps {
  /** Quote text */
  quote: string;

  /** Scripture reference */
  reference: string;

  /** Translation (optional) */
  translation?: string;

  /** Devotional title */
  title?: string;

  /** Devotional ID for linking */
  devotionalId: string;

  /** Show share options */
  showShareOptions?: boolean;

  /** Custom class names */
  className?: string;
}
```

---

## Error Components

### ErrorBoundary

**Location:** `/app/src/components/error/ErrorBoundary.tsx`

React error boundary with fallback UI.

#### Props

```typescript
interface ErrorBoundaryProps {
  /** Child components */
  children: ReactNode;

  /** Custom fallback component */
  fallback?: ReactNode | ((props: ErrorFallbackProps) => ReactNode);

  /** Error callback */
  onError?: (error: AppError, errorInfo: ErrorInfo) => void;

  /** Reset callback */
  onReset?: () => void;

  /** Component name for logging */
  componentName?: string;

  /** Show technical details in dev */
  showDetails?: boolean;

  /** Custom recovery actions */
  recoveryActions?: Array<{
    label: string;
    action: () => void;
  }>;
}
```

#### Related Components/Hooks

```typescript
// Error boundary with context provider
<ErrorBoundaryWithContext>
  <App />
</ErrorBoundaryWithContext>

// Hook to trigger reset
const { resetError } = useErrorBoundary();

// HOC wrapper
const SafeComponent = withErrorBoundary(Component, {
  componentName: 'Component',
});
```

#### Usage Examples

```jsx
import { ErrorBoundary, withErrorBoundary } from '@/components/error/ErrorBoundary';

// Basic usage
<ErrorBoundary>
  <RiskyComponent />
</ErrorBoundary>

// With custom fallback
<ErrorBoundary
  fallback={<CustomErrorPage />}
  onError={(error) => logError(error)}
>
  <App />
</ErrorBoundary>

// HOC usage
const SafeDevotional = withErrorBoundary(DevotionalCard, {
  componentName: 'DevotionalCard',
});
```

---

## Auth Components

### LoginForm

**Location:** `/app/src/components/auth/LoginForm.tsx`

Login form with validation and social auth.

#### Features

- Email/password validation
- Show/hide password toggle
- Error message display
- Loading states
- Social login buttons
- Link to forgot password
- Link to signup

#### Usage Examples

```jsx
import { LoginForm } from '@/components/auth/LoginForm';

// In login page
function LoginPage() {
  return (
    <div className="max-w-md mx-auto p-4">
      <LoginForm />
    </div>
  );
}
```

---

## Icon System

**Location:** `/app/components/icons/`

### Base Icon Component

```typescript
interface IconProps extends React.SVGProps<SVGSVGElement> {
  /** Size: xs(12), sm(16), md(20), lg(24), xl(32), 2xl(48) */
  size?: 'xs' | 'sm' | 'md' | 'lg' | 'xl' | '2xl';

  /** Additional CSS classes */
  className?: string;

  /** Accessible label (makes icon non-decorative) */
  label?: string;

  /** Color override */
  color?: string;
}
```

### Available Icons

```typescript
// Navigation
import { Home, Search, Settings, Menu, Close, Back, Forward } from '@/components/icons/navigation';

// Actions
import { Share, Bookmark, BookmarkFilled, Copy, Download, Edit, Delete } from '@/components/icons/actions';

// Reading
import { Book, Chapter, Verse, Quote, Highlight } from '@/components/icons/reading';

// Progress
import { Check, CheckCircle, Circle, Clock, Calendar, Streak } from '@/components/icons/progress';

// User
import { User, UserCircle, Login, Logout } from '@/components/icons/user';

// Social
import { Twitter, Facebook, Link, Email } from '@/components/icons/social';

// UI
import { ChevronUp, ChevronDown, ChevronLeft, ChevronRight, Plus, Minus } from '@/components/icons/ui';

// Status
import { Info, Warning, Error, Success } from '@/components/icons/status';
```

### Usage Examples

```jsx
import { Share } from '@/components/icons/actions/Share';
import { Icon } from '@/components/icons/Icon';

// Basic usage
<Share size="md" />

// With accessible label
<Share label="Share this devotional" />

// Custom color
<Share color="#C19A6B" />

// Inheriting color
<button className="text-gold">
  <Share /> {/* Inherits gold color */}
</button>
```

---

## Component Import Paths

### Recommended Imports

```typescript
// UI Components
import { Button } from '@/components/ui/Button';
import { Card, CardHeader, CardTitle, CardContent, CardFooter } from '@/components/ui/Card';
import { Modal, ModalActions } from '@/components/ui/Modal';
import { ToastProvider, useToast } from '@/components/ui/Toast';
import { Skeleton, SkeletonText, SkeletonCard } from '@/components/ui/Skeleton';

// Layout
import { Header } from '@/components/layout/Header';
import { BottomNav } from '@/components/layout/BottomNav';

// Accessibility
import { SkipLink } from '@/components/a11y/SkipLink';
import { VisuallyHidden } from '@/components/a11y/VisuallyHidden';
import { FocusTrap } from '@/components/a11y/FocusTrap';
import { LiveRegion } from '@/components/a11y/LiveRegion';
import { Motion, NoMotion, MotionSafe } from '@/components/a11y/ReducedMotion';

// Soul Audit
import { QuestionCard } from '@/components/soul-audit/QuestionCard';
import { ProgressBar, DotIndicator, ProcessingIndicator } from '@/components/soul-audit/ProgressBar';

// Share
import { ShareButton } from '@/components/share/ShareButton';
import { ShareModal } from '@/components/share/ShareModal';
import { QuoteCard } from '@/components/share/QuoteCard';

// Error
import { ErrorBoundary } from '@/components/error/ErrorBoundary';

// Auth
import { LoginForm } from '@/components/auth/LoginForm';

// Icons
import { Icon } from '@/components/icons/Icon';
import { Share } from '@/components/icons/actions/Share';
// ... etc
```

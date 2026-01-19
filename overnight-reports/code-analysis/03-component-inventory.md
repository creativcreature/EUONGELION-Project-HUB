# Component Inventory Report

**Generated:** 2026-01-19
**Project:** EUONGELION
**Path:** /Users/meltmac/Documents/Personal/wkGD/EUONGELION-STARTUP/app

---

## Executive Summary

The EUONGELION codebase contains approximately 120 React components distributed across two main component directories. This report catalogs all components, their usage, and identifies orphaned components that may be candidates for removal.

---

## Component Locations

| Location | Component Count | Purpose |
|----------|-----------------|---------|
| `/app/components/` | ~95 | Shared/UI components |
| `/app/src/components/` | ~23 | Feature-specific components |

---

## Actively Used Components

### Layout Components (Used by Pages)

| Component | File Path | Used In |
|-----------|-----------|---------|
| **Header** | `/app/src/components/layout/Header.tsx` | All main pages |
| **BottomNav** | `/app/src/components/layout/BottomNav.tsx` | All main pages |
| **Header** (duplicate) | `/app/components/layout/Header.tsx` | Legacy/alternative |
| **BottomNav** (duplicate) | `/app/components/layout/BottomNav.tsx` | Legacy/alternative |
| **Layout** | `/app/components/layout/Layout.tsx` | Page wrapper |
| **Sidebar** | `/app/components/layout/Sidebar.tsx` | Desktop sidebar |

**Usage Evidence:**
- `/app/src/app/page.tsx:2` - imports Header, BottomNav
- `/app/src/app/series/page.tsx:2-3` - imports Header, BottomNav
- `/app/src/app/devotional/[id]/page.tsx:3` - imports Header
- `/app/src/app/settings/page.tsx:2-3` - imports Header, BottomNav
- `/app/src/app/soul-audit/page.tsx:1-2` - imports Header, BottomNav

---

### UI Components (Core Design System)

| Component | File Path | Purpose | Status |
|-----------|-----------|---------|--------|
| **Button** | `/app/components/ui/Button.tsx` | Primary button | ACTIVE |
| **Card** | `/app/components/ui/Card.tsx` | Content card | ACTIVE |
| **Modal** | `/app/components/ui/Modal.tsx` | Dialog modal | ACTIVE |
| **Drawer** | `/app/components/ui/Drawer.tsx` | Side drawer | ACTIVE |
| **Skeleton** | `/app/components/ui/Skeleton.tsx` | Loading placeholder | ACTIVE |
| **Toast** | `/app/components/ui/Toast.tsx` | Notifications | ACTIVE |

**Subcomponents exported:**
- Card: CardHeader, CardTitle, CardDescription, CardContent, CardFooter
- Modal: ModalActions
- Drawer: DrawerFooter

---

### Devotional Components

| Component | File Path | Purpose | Status |
|-----------|-----------|---------|--------|
| **DevotionalCard** | `/app/components/devotional/DevotionalCard.tsx` | Card display | ACTIVE |
| **DevotionalReader** | `/app/components/devotional/DevotionalReader.tsx` | Full reader | ACTIVE |
| **ProgressIndicator** | `/app/components/devotional/ProgressIndicator.tsx` | Progress display | ACTIVE |
| **ReflectionPrompt** | `/app/components/devotional/ReflectionPrompt.tsx` | Reflection UI | ACTIVE |
| **ScriptureBlock** | `/app/components/devotional/ScriptureBlock.tsx` | Scripture display | ACTIVE |
| **WordStudy** | `/app/components/devotional/WordStudy.tsx` | Word study UI | ACTIVE |
| **ActionBar** | `/app/components/devotional/ActionBar.tsx` | Actions toolbar | ACTIVE |
| **ReadingTimer** | `/app/components/devotional/ReadingTimer.tsx` | Timer display | ACTIVE |

---

### Soul Audit Components

| Component | File Path | Purpose | Status |
|-----------|-----------|---------|--------|
| **QuestionCard** | `/app/src/components/soul-audit/QuestionCard.tsx` | Question display | ACTIVE |
| **AnswerOptions** | `/app/src/components/soul-audit/AnswerOptions.tsx` | Answer choices | ACTIVE |
| **ProgressBar** | `/app/src/components/soul-audit/ProgressBar.tsx` | Progress bar | ACTIVE |
| **ResultsChart** | `/app/src/components/soul-audit/ResultsChart.tsx` | Results viz | ACTIVE |

---

### Authentication Components

| Component | File Path | Purpose | Status |
|-----------|-----------|---------|--------|
| **LoginForm** | `/app/src/components/auth/LoginForm.tsx` | Login form | ACTIVE |
| **SignupForm** | `/app/src/components/auth/SignupForm.tsx` | Registration | ACTIVE |
| **ForgotPasswordForm** | `/app/src/components/auth/ForgotPasswordForm.tsx` | Password reset | ACTIVE |

---

### Share Components

| Component | File Path | Purpose | Status |
|-----------|-----------|---------|--------|
| **ShareButton** | `/app/src/components/share/ShareButton.tsx` | Share trigger | ACTIVE |
| **ShareModal** | `/app/src/components/share/ShareModal.tsx` | Share dialog | ACTIVE |
| **ShareOptions** | `/app/src/components/share/ShareOptions.tsx` | Platform options | ACTIVE |
| **CopyLinkButton** | `/app/src/components/share/CopyLinkButton.tsx` | Copy URL | ACTIVE |
| **ShareImage** | `/app/src/components/share/ShareImage.tsx` | Image generator | ACTIVE |
| **QuoteCard** | `/app/src/components/share/QuoteCard.tsx` | Quote image | ACTIVE |

---

### Accessibility Components

| Component | File Path | Purpose | Status |
|-----------|-----------|---------|--------|
| **SkipLink** | `/app/src/components/a11y/SkipLink.tsx` | Skip navigation | ACTIVE |
| **VisuallyHidden** | `/app/src/components/a11y/VisuallyHidden.tsx` | SR-only content | ACTIVE |
| **FocusTrap** | `/app/src/components/a11y/FocusTrap.tsx` | Focus management | ACTIVE |
| **LiveRegion** | `/app/src/components/a11y/LiveRegion.tsx` | ARIA live region | ACTIVE |
| **ReducedMotion** | `/app/src/components/a11y/ReducedMotion.tsx` | Motion preference | ACTIVE |

---

### Error Handling Components

| Component | File Path | Purpose | Status |
|-----------|-----------|---------|--------|
| **ErrorBoundary** | `/app/src/components/error/ErrorBoundary.tsx` | Error boundary | ACTIVE |
| **GlobalErrorBoundary** | `/app/src/components/error/GlobalErrorBoundary.tsx` | App-level error | ACTIVE |
| **DevotionalErrorBoundary** | `/app/src/components/error/DevotionalErrorBoundary.tsx` | Devotional error | ACTIVE |

---

## Potentially Orphaned Components

The following components exist but may not be used in current pages. These should be verified before removal.

### Icon Components (Large Collection)

**Location:** `/app/components/icons/`

| Category | Components | Notes |
|----------|------------|-------|
| navigation/ | Home, Search, Settings, Menu, Close, Back, Forward | May be used in BottomNav |
| actions/ | Share, Bookmark, BookmarkFilled, Copy, Download, Edit, Delete | Used in action bars |
| reading/ | Book, Chapter, Verse, Quote, Highlight | Used in reader |
| progress/ | Check, CheckCircle, Circle, Clock, Calendar, Streak | Used in progress UI |
| social/ | Twitter, Facebook, Link, Email | Used in ShareOptions |
| status/ | Info, Warning, Error, Success | Used in Toast |
| user/ | User, UserCircle, Login, Logout | Used in auth/header |
| ui/ | ChevronUp, ChevronDown, ChevronLeft, ChevronRight, Plus, Minus | General UI |

**Recommendation:** Keep - These are likely used throughout the application even if not directly imported by pages.

---

### Animation Components (Possibly Underutilized)

| Component | File Path | Status |
|-----------|-----------|--------|
| **PageTransition** | `/app/components/animated/PageTransition.tsx` | VERIFY |
| **FadeIn** | `/app/components/animated/FadeIn.tsx` | VERIFY |
| **SlideIn** | `/app/components/animated/SlideIn.tsx` | VERIFY |
| **Stagger** | `/app/components/animated/Stagger.tsx` | VERIFY |
| **Collapse** | `/app/components/animated/Collapse.tsx` | VERIFY |
| **ScaleOnHover** | `/app/components/animated/ScaleOnHover.tsx` | VERIFY |
| **SwipeableCard** | `/app/components/animated/SwipeableCard.tsx` | VERIFY |
| **PullToRefresh** | `/app/components/animated/PullToRefresh.tsx` | VERIFY |

**Recommendation:** Verify usage - These animation wrappers may be intended for future use or may be orphaned.

---

### Loading Components

| Component | File Path | Status |
|-----------|-----------|--------|
| **Skeleton** | `/app/components/loading/Skeleton.tsx` | DUPLICATE (ui/Skeleton) |
| **SkeletonText** | `/app/components/loading/SkeletonText.tsx` | VERIFY |
| **SkeletonAvatar** | `/app/components/loading/SkeletonAvatar.tsx` | VERIFY |
| **SkeletonImage** | `/app/components/loading/SkeletonImage.tsx` | VERIFY |
| **SkeletonCard** | `/app/components/loading/SkeletonCard.tsx` | VERIFY |
| **SkeletonList** | `/app/components/loading/SkeletonList.tsx` | VERIFY |

**Recommendation:** Consolidate - `/app/components/ui/Skeleton.tsx` and `/app/components/loading/Skeleton.tsx` should be merged.

---

### Settings Components

| Component | File Path | Status |
|-----------|-----------|--------|
| **SettingsNav** | `/app/components/settings/SettingsNav.tsx` | ACTIVE |
| **SettingsLayout** | `/app/components/settings/SettingsLayout.tsx` | ACTIVE |
| **SettingsSection** | `/app/components/settings/SettingsSection.tsx` | ACTIVE |
| **SettingsRow** | `/app/components/settings/SettingsRow.tsx` | ACTIVE |
| **ProfileEditor** | `/app/components/settings/ProfileEditor.tsx` | VERIFY |

---

### Static Content Components

| Component | File Path | Status |
|-----------|-----------|--------|
| **StaticPageLayout** | `/app/components/static/StaticPageLayout.tsx` | VERIFY |
| **LegalDocument** | `/app/components/static/LegalDocument.tsx` | VERIFY |
| **LastUpdated** | `/app/components/static/LastUpdated.tsx` | VERIFY |
| **TableOfContents** | `/app/components/static/TableOfContents.tsx` | VERIFY |

**Recommendation:** Verify - These may be used for Terms/Privacy pages that need to be checked.

---

### Offline Components

| Component | File Path | Status |
|-----------|-----------|--------|
| **OfflinePage** | `/app/components/offline/OfflinePage.tsx` | ACTIVE (PWA) |
| **OfflineIndicator** | `/app/components/offline/OfflineIndicator.tsx` | ACTIVE (PWA) |
| **CachedContent** | `/app/components/offline/CachedContent.tsx` | VERIFY |

---

### Feedback Components

| Component | File Path | Status |
|-----------|-----------|--------|
| **FeedbackForm** | `/app/components/feedback/FeedbackForm.tsx` | ACTIVE |
| **BugReportForm** | `/app/components/feedback/BugReportForm.tsx` | ACTIVE |
| **RatingWidget** | `/app/components/feedback/RatingWidget.tsx` | VERIFY |

---

### SEO Components

| Component | File Path | Status |
|-----------|-----------|--------|
| **JsonLd** | `/app/components/seo/JsonLd.tsx` | ACTIVE |
| **CanonicalUrl** | `/app/components/seo/CanonicalUrl.tsx` | VERIFY |
| **Breadcrumbs** | `/app/components/seo/Breadcrumbs.tsx` | VERIFY |

---

### Image Components

| Component | File Path | Status |
|-----------|-----------|--------|
| **OptimizedImage** | `/app/components/images/OptimizedImage.tsx` | ACTIVE |
| **DevotionalImage** | `/app/components/images/DevotionalImage.tsx` | ACTIVE |
| **SeriesImage** | `/app/components/images/SeriesImage.tsx` | ACTIVE |
| **Avatar** | `/app/components/images/Avatar.tsx` | ACTIVE |
| **PlaceholderImage** | `/app/components/images/PlaceholderImage.tsx` | VERIFY |
| **ImageWithFallback** | `/app/components/images/ImageWithFallback.tsx` | ACTIVE |

---

### Feature Flag Components

| Component | File Path | Status |
|-----------|-----------|--------|
| **FeatureFlag** | `/app/components/features/FeatureFlag.tsx` | ACTIVE |
| **FeatureGate** | `/app/components/features/FeatureGate.tsx` | ACTIVE |

---

### Notification Components

| Component | File Path | Status |
|-----------|-----------|--------|
| **Toast** | `/app/components/notifications/Toast.tsx` | DUPLICATE (ui/Toast) |
| **ToastContainer** | `/app/components/notifications/ToastContainer.tsx` | VERIFY |
| **NotificationBadge** | `/app/components/notifications/NotificationBadge.tsx` | VERIFY |
| **NotificationItem** | `/app/components/notifications/NotificationItem.tsx` | VERIFY |
| **NotificationCenter** | `/app/components/notifications/NotificationCenter.tsx` | VERIFY |

**Recommendation:** Consolidate - Toast exists in both `/ui/` and `/notifications/`. Pick one.

---

## Duplicate Component Analysis

| Component Name | Location 1 | Location 2 | Recommendation |
|----------------|------------|------------|----------------|
| **Header** | `/app/components/layout/Header.tsx` | `/app/src/components/layout/Header.tsx` | Consolidate to src |
| **BottomNav** | `/app/components/layout/BottomNav.tsx` | `/app/src/components/layout/BottomNav.tsx` | Consolidate to src |
| **Skeleton** | `/app/components/ui/Skeleton.tsx` | `/app/components/loading/Skeleton.tsx` | Keep ui, remove loading |
| **Toast** | `/app/components/ui/Toast.tsx` | `/app/components/notifications/Toast.tsx` | Keep ui, remove notifications |

---

## Component Health Summary

| Category | Count | Active | Verify | Duplicate |
|----------|-------|--------|--------|-----------|
| Layout | 6 | 4 | 0 | 2 |
| UI Core | 6 | 6 | 0 | 0 |
| Devotional | 8 | 8 | 0 | 0 |
| Soul Audit | 4 | 4 | 0 | 0 |
| Auth | 3 | 3 | 0 | 0 |
| Share | 6 | 6 | 0 | 0 |
| A11y | 5 | 5 | 0 | 0 |
| Error | 3 | 3 | 0 | 0 |
| Icons | ~30 | ~30 | 0 | 0 |
| Animated | 8 | 0 | 8 | 0 |
| Loading | 6 | 1 | 5 | 1 |
| Settings | 5 | 4 | 1 | 0 |
| Static | 4 | 0 | 4 | 0 |
| Offline | 3 | 2 | 1 | 0 |
| Feedback | 3 | 2 | 1 | 0 |
| SEO | 3 | 1 | 2 | 0 |
| Images | 6 | 5 | 1 | 0 |
| Features | 2 | 2 | 0 | 0 |
| Notifications | 5 | 1 | 4 | 1 |
| **Total** | ~120 | ~87 | ~27 | ~4 |

---

## Recommendations

### Immediate Actions
1. **Consolidate duplicates** - Remove duplicate Header, BottomNav, Skeleton, Toast
2. **Verify orphaned** - Check 27 components marked VERIFY for actual usage
3. **Update imports** - After consolidation, update all import paths

### Short-term Actions
4. **Add barrel exports** - Create index.ts files for each component directory
5. **Document components** - Add JSDoc to all components
6. **Create Storybook** - Visual component documentation

### Long-term Actions
7. **Remove unused** - Delete components confirmed as unused
8. **Establish naming convention** - Consistent naming across all components
9. **Component testing** - Add unit tests for all components

---

*Report generated by overnight autonomous analysis*

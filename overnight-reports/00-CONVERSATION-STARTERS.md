# EUONGELION Conversation Starters

**Purpose:** Ready-to-copy prompts for continuing work on the EUONGELION project
**Generated:** 2026-01-19

Copy any prompt below and paste it directly into Claude Code to continue work.

---

## Quick Fix Prompts

### Fix TypeScript Build Errors
```
Read the tech debt audit at tools/overnight-reports/code-analysis/01-tech-debt-audit.md. Then remove `ignoreBuildErrors: true` and `ignoreDuringBuilds: true` from next.config.js (around lines 161-166). Run `npx tsc --noEmit` to see all TypeScript errors and fix them systematically, starting with the most critical files.
```

### Remove Debug Console Logs
```
Read the console.log cleanup list at tools/overnight-reports/code-analysis/20-console-log-cleanup-list.md. Remove the debug console.log statements marked for removal in these hooks:
- /app/hooks/useOfflineDevotionals.ts (lines 155, 214, 248, 283, 299, 313)
- /app/hooks/usePushNotifications.ts (lines 138, 172)
- /app/hooks/useServiceWorker.ts (lines 86, 98, 116, 120, 140, 168, 184, 212)
Keep console.error statements in catch blocks. Replace success logs with proper logger if needed.
```

### Fix LoadingSpinner Accessibility
```
Read the accessibility audit at tools/overnight-reports/code-analysis/05-accessibility-audit.md. In /app/components/ui/Button.tsx around lines 76-97, add `aria-hidden="true"` to the LoadingSpinner SVG element since it's decorative and the button already has loading text. This is flagged as a critical accessibility issue.
```

### Fix Small Button Touch Targets
```
Per the accessibility audit at tools/overnight-reports/code-analysis/05-accessibility-audit.md, the small button variants (sm and iconSm) are 36px which is below the 44px minimum touch target. In /app/components/ui/Button.tsx, update the size variants:
- Change `sm: 'h-9 px-4'` to `sm: 'h-11 px-4'`
- Change `iconSm: 'h-9 w-9'` to `iconSm: 'h-11 w-11'`
```

### Sanitize dangerouslySetInnerHTML
```
The security scan at tools/overnight-reports/code-analysis/09-security-scan.md flags XSS risks with dangerouslySetInnerHTML. Install DOMPurify and sanitize content in:
1. /app/components/devotional/DevotionalReader.tsx line 227
2. /app/src/app/devotional/[id]/page.tsx line 237

Use: `dangerouslySetInnerHTML={{ __html: DOMPurify.sanitize(content) }}`
```

---

## Feature Implementation Prompts

### Implement Push Notifications
```
Based on the feature prioritization matrix at tools/overnight-reports/planning/44-feature-prioritization-matrix.md, push notifications are Priority 1.67 (Sprint 1). The hooks already exist at /app/hooks/usePushNotifications.ts but have TODOs. Implement the actual Web Push API integration:
1. Complete the subscription flow
2. Add server-side endpoint for storing subscriptions
3. Create Supabase Edge Function for sending scheduled notifications
4. Add user preference controls in settings
Reference the push notification copy at tools/overnight-reports/content/38-push-notification-copy.md for notification text.
```

### Implement Search Functionality
```
Per the feature prioritization at tools/overnight-reports/planning/44-feature-prioritization-matrix.md, search is a Sprint 2 priority (Impact: 4, Effort: 3). Create a search feature that:
1. Uses Supabase full-text search on devotionals table
2. Searches by title, content, Scripture references
3. Filters by series/category
4. Works offline for cached content
Add search bar to main navigation. See the API route documentation at tools/overnight-reports/code-analysis/04-api-route-documentation.md for route patterns.
```

### Implement Daily Reminder System
```
The feature prioritization matrix (tools/overnight-reports/planning/44-feature-prioritization-matrix.md) rates daily reminders as Priority 2.50 - the highest priority feature. Implement:
1. Time picker for preferred reminder time in settings
2. Store preference in user profile
3. Connect to push notification system
4. Use the gentle notification copy from tools/overnight-reports/content/38-push-notification-copy.md
Acceptance criteria: User can set time, receive notification at that time, notification leads to today's content.
```

### Implement Progress Statistics Page
```
Create a /stats or /progress page showing user reading statistics (Priority 2.00 per tools/overnight-reports/planning/44-feature-prioritization-matrix.md):
- Total devotionals read
- Current streak with visual display
- Series completed count
- Time spent reading
- Historical view (weekly/monthly chart)
Use data from progressStore.ts. Reference the design system documentation at tools/overnight-reports/design-system/ for styling.
```

### Add Reading Time Estimates
```
Per the feature prioritization (tools/overnight-reports/planning/44-feature-prioritization-matrix.md), reading time estimates are Priority 3.00 - a quick win. Add estimated reading time to DevotionalCard and DevotionalReader components:
1. Calculate based on word count (~200 words per minute)
2. Display for each depth level (1-min, 5-min, 15-min)
3. Show in UI with appropriate formatting
Use the formatDuration() function from lib/date.ts if available, or create it.
```

---

## Code Cleanup Prompts

### Add Dynamic Imports for Modals
```
The performance analysis at tools/overnight-reports/code-analysis/08-performance-analysis.md identifies missing code splitting as critical. Add dynamic imports for:
- /app/components/ui/Modal.tsx
- /app/components/ui/Drawer.tsx
- /app/components/share/ShareModal.tsx
- /app/components/forms/FeedbackForm.tsx

Example pattern:
const Modal = dynamic(() => import('@/components/ui/Modal'), { ssr: false });

This will reduce initial bundle size and improve FCP.
```

### Add React.memo to List Components
```
Per the performance analysis at tools/overnight-reports/code-analysis/08-performance-analysis.md, list item components need memoization. Add React.memo to:
- /app/components/devotional/DevotionalCard.tsx (used in lists)
- /app/components/notifications/NotificationItem.tsx (if exists)
- /app/components/series/SeriesCard.tsx (if exists)

Wrap the existing forwardRef pattern: `export const DevotionalCard = memo(forwardRef<...>(...));`
```

### Implement Content Security Policy
```
The security scan at tools/overnight-reports/code-analysis/09-security-scan.md notes CSP is not implemented despite nonce generation. In /app/middleware.ts, add the CSP header:

const csp = `
  default-src 'self';
  script-src 'self' 'nonce-${nonce}';
  style-src 'self' 'unsafe-inline';
  img-src 'self' data: https:;
  connect-src 'self' https://*.supabase.co;
`;
response.headers.set('Content-Security-Policy', csp);
```

### Implement Rate Limiting
```
The security scan (tools/overnight-reports/code-analysis/09-security-scan.md) identifies that rate limiting is headers-only with no actual tracking. In /app/middleware.ts, implement actual rate limiting:
1. Consider using Upstash Rate Limit or Redis
2. Track requests per IP
3. Block requests exceeding limits
4. Return 429 status with Retry-After header
Priority: High - this is a security gap.
```

### Add Error Boundary to Root Layout
```
Per the error handling audit at tools/overnight-reports/code-analysis/11-error-handling-audit.md, the root layout lacks an error boundary. In /app/layout.tsx, wrap children with GlobalErrorBoundary:

import { GlobalErrorBoundary } from '@/components/error/GlobalErrorBoundary';

export default function RootLayout({ children }) {
  return (
    <html>
      <body>
        <GlobalErrorBoundary>
          {children}
        </GlobalErrorBoundary>
      </body>
    </html>
  );
}
```

### Replace Console.error with Sentry in API Routes
```
The error handling audit (tools/overnight-reports/code-analysis/11-error-handling-audit.md) recommends replacing console.error with Sentry in API routes. Update all files in /app/api/ to use:

import { captureException } from '@/lib/error/sentry';

catch (error) {
  captureException(error, { tags: { route: 'route-name' } });
  return NextResponse.json({ error: 'User-friendly message' }, { status: 500 });
}

Start with the most used routes: /api/devotionals, /api/series, /api/user/progress.
```

---

## Content Creation Prompts

### Create Devotional from Outline
```
Read the devotional outlines at tools/overnight-reports/content/32-devotional-outlines.md. Take outline #1 "The Invitation to Rest" (Matthew 11:28-30) and create the full devotional with:
- 1-minute version (focus on Central Point C with Hebrew/Greek word)
- 5-minute version (cover A through A' with story illustration)
- 15-minute version (full development with deep dives into original languages)

Follow the chiastic structure A-B-C-B'-A' exactly. Save to the appropriate content directory.
```

### Write Empty State Copy
```
Read tools/overnight-reports/content/35-empty-state-copy.md for the voice and tone guidelines. The following empty states need implementation in their respective components:
1. No reading history (Reading Progress page)
2. No bookmarks yet (Bookmarks page)
3. No search results (Search page)
4. No Soul Audit taken (Soul Audit page)

Create React components that match the copy and include appropriate CTAs. Follow the "quiet invitation, not scolding parent" tone.
```

### Implement Onboarding Flow
```
Using the welcome and onboarding copy at tools/overnight-reports/content/34-welcome-onboarding-copy.md, implement the 7-screen onboarding flow:
1. Welcome screen
2. Sacred Minimalism explanation
3. Three Depths explanation
4. Soul Audit introduction
5. Personalization questions
6. Notification setup
7. Ready to start

Create an OnboardingFlow component that steps through these screens. Store completion in user preferences. Follow the voice guidelines - calm confidence, no guilt or gamification.
```

### Create Error Message Components
```
Read tools/overnight-reports/content/36-error-message-copy.md (if exists) and the error handling audit at tools/overnight-reports/code-analysis/11-error-handling-audit.md. Create user-friendly error components for:
1. Network errors
2. Authentication failures
3. Content not found
4. Session expired

Each should include: thoughtful messaging, Scripture quote where appropriate, clear next action, and match the brand tone.
```

### Write App Store Description
```
Read tools/overnight-reports/content/39-app-store-description.md and create the finalized App Store and Google Play descriptions including:
- Title and subtitle
- Full description with feature highlights
- Keywords/tags
- Screenshots captions
- What's New section template

Follow ASO best practices from tools/overnight-reports/research/53-app-store-optimization-research.md.
```

---

## Investigation Prompts

### Audit Authentication TODOs
```
The tech debt audit at tools/overnight-reports/code-analysis/01-tech-debt-audit.md identifies 6 authentication TODOs as critical. Read /app/stores/authStore.ts and document:
1. What's currently implemented vs placeholder
2. What Supabase Auth methods need to be called
3. Required environment variables
4. Token refresh flow requirements
5. Password reset flow requirements

Create a checklist of exactly what needs to be implemented to complete authentication.
```

### Analyze Database Integration Gaps
```
Per tools/overnight-reports/code-analysis/01-tech-debt-audit.md, there are 35+ TODOs for database integration. Read the database schema documentation at tools/overnight-reports/documentation/21-database-schema-documentation.md and the API routes at /app/api/. Create a mapping of:
1. Each API route that needs database integration
2. The corresponding Supabase table/query needed
3. RLS policies required (see tools/overnight-reports/documentation/22-rls-policy-documentation.md)
4. Priority order for implementation
```

### Review Zustand Store Architecture
```
Read tools/overnight-reports/code-analysis/17-zustand-store-analysis.md and examine the stores in /app/stores/. Analyze:
1. Are selectors being used properly to prevent re-renders?
2. Is there state duplication across stores?
3. Are async actions handled consistently?
4. Is middleware (persist, devtools) configured correctly?

Document any architectural issues or improvements needed.
```

### Investigate PWA Offline Behavior
```
Read the PWA audit at tools/overnight-reports/code-analysis/13-pwa-audit.md and examine:
- /app/hooks/useServiceWorker.ts
- /app/hooks/useOfflineDevotionals.ts
- /app/hooks/useOnlineStatus.ts

Test and document:
1. What content is cached and when
2. How the app behaves fully offline
3. How sync works when coming back online
4. What user feedback is provided during offline state
5. Any gaps in the offline experience
```

### Audit Component Accessibility
```
Using the accessibility audit at tools/overnight-reports/code-analysis/05-accessibility-audit.md as a guide, manually test these components for keyboard navigation and screen reader compatibility:
1. /app/components/navigation/TabNav.tsx
2. /app/components/ui/Drawer.tsx
3. /app/components/settings/ThemeSelect.tsx

Document any issues found and propose fixes. Test with VoiceOver on macOS.
```

### Review Test Coverage Gaps
```
Read the unit test plan at tools/overnight-reports/testing/80-unit-test-plan.md. Current coverage is ~5% with only Button and DevotionalCard tests. Analyze the Phase 1 priority items:
1. lib/date.ts - streak functionality
2. lib/scripture.ts - devotional functionality
3. lib/validation/validators.ts - form validation
4. stores/authStore.ts - authentication
5. stores/progressStore.ts - progress tracking

For each, identify the most critical test cases that should be written first.
```

---

## How to Use These Prompts

1. **Copy the entire prompt** including the code blocks
2. **Paste directly into Claude Code** - no modifications needed
3. **Review Claude's plan** before approving file changes
4. **Run tests/builds** after changes to verify

### Prompt Categories by Time Available

**15 minutes:** Quick Fix Prompts
**1-2 hours:** Code Cleanup Prompts, Investigation Prompts
**Half day:** Feature Implementation Prompts, Content Creation Prompts

### Recommended Starting Points

1. **If builds are failing:** Start with "Fix TypeScript Build Errors"
2. **If launching soon:** Start with security fixes (CSP, XSS sanitization)
3. **If adding features:** Start with "Daily Reminder System" (highest priority)
4. **If improving quality:** Start with "Add Error Boundary to Root Layout"

---

*Generated from overnight reports analysis. See individual reports in /tools/overnight-reports/ for full context.*

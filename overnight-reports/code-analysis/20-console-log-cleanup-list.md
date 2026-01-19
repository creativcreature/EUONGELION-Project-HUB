# Console.log Cleanup List

**Generated:** 2026-01-19
**Project:** EUONGELION
**Path:** `/Users/meltmac/Documents/Personal/wkGD/EUONGELION-STARTUP/app`

---

## Executive Summary

The EUONGELION codebase contains **196 console statements** across 57 files. Most are appropriate error logging or development-only debugging. This report categorizes each statement to help prioritize cleanup before production deployment.

**Total Console Statements:** 196
- `console.log`: 62
- `console.error`: 78
- `console.warn`: 43
- `console.info`: 10
- `console.debug`: 3

---

## 1. Priority Categories

### Keep (Production-appropriate)

Error logging that aids debugging:
- `console.error` in catch blocks
- `console.warn` for deprecations/issues
- Dev-only conditional logging

### Review (May need removal)

- `console.log` for general debugging
- Verbose logging in hooks
- Success messages

### Remove (Should be removed)

- Debugging `console.log` statements
- Temporary development logging
- Sensitive data logging

---

## 2. Files with Console Statements (Sorted by Count)

| File | Total | log | error | warn | info | debug |
|------|-------|-----|-------|------|------|-------|
| `/lib/analytics/analytics.ts` | 24 | 23 | 1 | 0 | 0 | 0 |
| `/hooks/useOfflineDevotionals.ts` | 12 | 6 | 6 | 0 | 0 | 0 |
| `/hooks/usePushNotifications.ts` | 11 | 2 | 4 | 5 | 0 | 0 |
| `/hooks/useServiceWorker.ts` | 12 | 10 | 2 | 0 | 0 | 0 |
| `/src/lib/error/sentry.ts` | 14 | 0 | 1 | 0 | 10 | 3 |
| `/lib/cron/scheduler.ts` | 9 | 0 | 3 | 2 | 2 | 2 |
| `/stores/middleware.ts` | 6 | 2 | 1 | 3 | 0 | 0 |
| `/lib/notes/sync.ts` | 7 | 0 | 7 | 0 | 0 | 0 |
| `/lib/notifications/subscription.ts` | 6 | 0 | 5 | 1 | 0 | 0 |
| `/lib/onboarding/progress.ts` | 5 | 0 | 5 | 0 | 0 | 0 |
| `/src/contexts/UserContext.tsx` | 5 | 0 | 5 | 0 | 0 | 0 |

---

## 3. Complete File:Line List

### API Routes (Keep - Error Logging)

```
/api/devotionals/route.ts:244        console.error('Error fetching devotionals:', error);
/api/devotionals/route.ts:302        console.error('Error creating devotional:', error);
/api/devotionals/[id]/route.ts:171   console.error('Error fetching devotional:', error);
/api/devotionals/[id]/route.ts:256   console.error('Error updating devotional:', error);
/api/devotionals/[id]/route.ts:323   console.error('Error deleting devotional:', error);
/api/feedback/route.ts:96            console.log('[Feedback Received]', { ... });  // REMOVE
/api/feedback/route.ts:114           console.error('[Feedback API Error]', error);
/api/health/route.ts:66              console.error('Health check failed:', error);
/api/series/route.ts:306             console.error('Error fetching series:', error);
/api/series/route.ts:396             console.error('Error creating series:', error);
/api/series/[slug]/route.ts:195      console.error('Error fetching series:', error);
/api/series/[slug]/route.ts:268      console.warn('...');  // Keep - Warning
/api/series/[slug]/route.ts:288      console.error('Error updating series:', error);
/api/series/[slug]/route.ts:366      console.error('Error deleting series:', error);
/api/user/bookmarks/route.ts:230     console.error('Error fetching bookmarks:', error);
/api/user/bookmarks/route.ts:319     console.error('Error creating bookmark:', error);
/api/user/bookmarks/route.ts:391     console.error('Error updating bookmark:', error);
/api/user/bookmarks/route.ts:472     console.error('Error removing bookmark:', error);
/api/user/progress/route.ts:305      console.error('Error fetching user progress:', error);
/api/user/progress/route.ts:402      console.error('Error recording progress:', error);
/api/user/progress/route.ts:467      console.error('Error resetting progress:', error);
/api/soul-audit/questions/route.ts:596  console.error('Error fetching soul audit questions:', error);
/api/soul-audit/submit/route.ts:431  console.error('Error submitting soul audit:', error);
/api/soul-audit/submit/route.ts:499  console.error('Error fetching soul audit history:', error);
```

### Stores (Review - Dev Logging)

```
/stores/middleware.ts:26             logger?: typeof console.log;  // Type definition - Keep
/stores/middleware.ts:54             logger: customLogger = console.log,  // Default - Keep
/stores/middleware.ts:146            console.warn('Failed to get item from localStorage');
/stores/middleware.ts:155            console.warn('Failed to set item in localStorage');
/stores/middleware.ts:163            console.warn('Failed to remove item from localStorage');
/stores/middleware.ts:213            console.warn('Failed to get item from IndexedDB');
/stores/middleware.ts:230            console.warn('Failed to set item in IndexedDB');
/stores/middleware.ts:246            console.warn('Failed to remove item from IndexedDB');
/stores/middleware.ts:358            console.log('...');  // Dev logging - Conditional
/stores/middleware.ts:366            console.error('...');  // Error logging - Keep
/stores/authStore.ts:408             useAuthStore.getState().refreshToken().catch(console.error);  // Keep
```

### Hooks (Review - Verbose Logging)

```
/hooks/useOfflineDevotionals.ts:102  console.error('[Offline] Failed to refresh cache:', err);
/hooks/useOfflineDevotionals.ts:155  console.log('[Offline] Cached devotional:', devotional.slug);  // REMOVE
/hooks/useOfflineDevotionals.ts:158  console.error('[Offline] Failed to cache devotional:', err);
/hooks/useOfflineDevotionals.ts:214  console.log('[Offline] Cached', devotionals.length, 'devotionals');  // REMOVE
/hooks/useOfflineDevotionals.ts:217  console.error('[Offline] Failed to cache multiple devotionals:', err);
/hooks/useOfflineDevotionals.ts:248  console.log('[Offline] Removed cached devotional:', id);  // REMOVE
/hooks/useOfflineDevotionals.ts:251  console.error('[Offline] Failed to remove cached devotional:', err);
/hooks/useOfflineDevotionals.ts:283  console.log('[Offline] Cleared all cached devotionals');  // REMOVE
/hooks/useOfflineDevotionals.ts:286  console.error('[Offline] Failed to clear cache:', err);
/hooks/useOfflineDevotionals.ts:299  console.log('[Offline] Prefetching week', weekNumber);  // REMOVE
/hooks/useOfflineDevotionals.ts:313  console.log('[Offline] Prefetched week', weekNumber, ...);  // REMOVE
/hooks/useOfflineDevotionals.ts:316  console.error('[Offline] Failed to prefetch week:', err);

/hooks/usePushNotifications.ts:82    console.error('[Push] Failed to request permission:', err);
/hooks/usePushNotifications.ts:138   console.log('[Push] Successfully subscribed');  // REMOVE
/hooks/usePushNotifications.ts:142   console.error('[Push] Subscription failed:', err);
/hooks/usePushNotifications.ts:172   console.log('[Push] Successfully unsubscribed');  // REMOVE
/hooks/usePushNotifications.ts:177   console.error('[Push] Unsubscribe failed:', err);
/hooks/usePushNotifications.ts:186   console.warn('[Push] Cannot send test notification');
/hooks/usePushNotifications.ts:212   console.warn('[Push] Failed to check existing subscription:', err);
/hooks/usePushNotifications.ts:289   console.warn('[Push] Failed to save subscription to server:', err);
/hooks/usePushNotifications.ts:307   console.warn('[Push] Failed to remove subscription from server:', err);

/hooks/useServiceWorker.ts:81        console.warn('[SW] Service workers not supported');
/hooks/useServiceWorker.ts:86        console.log('[SW] Registering service worker...');  // REMOVE
/hooks/useServiceWorker.ts:98        console.log('[SW] Service worker registered:', reg.scope);  // REMOVE
/hooks/useServiceWorker.ts:116       console.log('[SW] Service worker installed');  // REMOVE
/hooks/useServiceWorker.ts:120       console.log('[SW] Service worker activated');  // REMOVE
/hooks/useServiceWorker.ts:140       console.log('[SW] Update found');  // REMOVE
/hooks/useServiceWorker.ts:151       console.error('[SW] Registration failed:', err);
/hooks/useServiceWorker.ts:168       console.log('[SW] Service worker unregistered');  // REMOVE
/hooks/useServiceWorker.ts:172       console.error('[SW] Unregistration failed:', err);
/hooks/useServiceWorker.ts:184       console.log('[SW] Checking for updates...');  // REMOVE
/hooks/useServiceWorker.ts:187       console.error('[SW] Update check failed:', err);
/hooks/useServiceWorker.ts:212       console.log('[SW] Controller changed');  // REMOVE

/hooks/useNotifications.ts:89        console.error('Error loading notifications:', error);
/hooks/useNotifications.ts:104       console.error('Error saving notifications:', error);
/hooks/useNotifications.ts:144       console.error('Error polling notifications:', error);
```

### Components (Mixed)

```
/components/ui/Toast.tsx:235                   console.warn('toast() function requires ToastProvider');  // Keep
/components/settings/ProfileEditor.tsx:74     console.error('Failed to save profile:', error);
/components/performance/WebVitals.tsx:91      console.log('...');  // Dev-only conditional - Keep
/components/performance/WebVitals.tsx:114     console.warn('Failed to load web vitals:', error);
/components/performance/WebVitals.tsx:309     console.warn('Failed to send web vital to analytics:', error);
/components/animated/PullToRefresh.tsx:122    console.error('Refresh failed:', error);

/src/components/error/ErrorBoundary.tsx:191   console.warn('useErrorBoundary called outside');  // Keep
/src/components/share/QuoteCard.tsx:92        console.error('Failed to generate quote image:', err);
/src/components/share/ShareButton.tsx:65      console.error('Share error:', error);
```

### Library Functions (Mixed)

```
/lib/reading/highlight.ts:65         console.error('Failed to save highlights:', error);
/lib/reading/position.ts:172         console.error('Failed to save reading position:', error);
/lib/reading/position.ts:190         console.error('Failed to remove reading position:', error);
/lib/reading/position.ts:203         console.error('Failed to clear reading positions:', error);
/lib/reading/notes.ts:61             console.error('Failed to save notes:', error);

/lib/settings/sync.ts:469            console.error('Settings change listener error:', error);

/lib/features/context.ts:20          console.warn('FeatureFlagProvider not found');
/lib/features/context.ts:23          console.warn('FeatureFlagProvider not found');
/lib/features/provider.ts:76         console.warn('Failed to load user feature overrides:', error);
/lib/features/provider.ts:155        console.warn('Flag overrides are only available in dev');
/lib/features/provider.ts:174        console.warn('Flag overrides are only available in dev');

/lib/content/transformer.ts:150      console.error('Failed to fetch scripture:', error);
/lib/content/transformer.ts:165      console.error('Failed to fetch scripture batch:', error);
/lib/content/loader.ts:98            console.error('Error reading directory:', error);
/lib/content/loader.ts:243           console.error('Error loading file:', error);

/lib/feedback/submit.ts:135          console.error('Feedback submission error:', error);
/lib/feedback/submit.ts:182          console.error('Bug report submission error:', error);
/lib/feedback/submit.ts:248          console.error('Contact form submission error:', error);
/lib/feedback/submit.ts:306          console.error('Failed to save feedback draft:', error);
/lib/feedback/submit.ts:317          console.error('Failed to load feedback draft:', error);
/lib/feedback/submit.ts:328          console.error('Failed to clear feedback draft:', error);

/lib/notes/storage.ts:190            console.error('Failed to save to localStorage:', error);
/lib/notes/sync.ts:161               console.error('Failed to sync note to server:', error);
/lib/notes/sync.ts:186               console.error('Failed to sync note update:', error);
/lib/notes/sync.ts:204               console.error('Failed to sync note deletion:', error);
/lib/notes/sync.ts:292               console.error('Failed to sync highlight:', error);
/lib/notes/sync.ts:316               console.error('Failed to sync highlight update:', error);
/lib/notes/sync.ts:334               console.error('Failed to sync highlight deletion:', error);
/lib/notes/sync.ts:437               console.error('Failed to pull server data:', error);

/lib/theme/utils.ts:78               console.warn('Unable to save theme preference');
/lib/theme/utils.ts:320              console.error('Failed to sync theme preference:', error);
/lib/theme/utils.ts:353              console.error('Failed to fetch theme preference:', error);

/lib/monitoring/uptime.ts:138        console.warn('[DOWNTIME START]...');  // Keep
/lib/monitoring/uptime.ts:157        console.info('[DOWNTIME END]...');  // Keep
/lib/monitoring/performance.ts:81    console.log('Web Vital...');  // Dev-only - Keep

/lib/notifications/permissions.ts:140  console.error('Error requesting notification permission:', error);
/lib/notifications/permissions.ts:159  console.warn('Cannot show notification');
/lib/notifications/permissions.ts:172  console.error('Error showing notification:', error);
/lib/notifications/subscription.ts:99  console.error('Error getting current subscription:', error);
/lib/notifications/subscription.ts:171 console.error('Error subscribing to push:', error);
/lib/notifications/subscription.ts:208 console.warn('Failed to notify server of unsubscription');
/lib/notifications/subscription.ts:216 console.error('Error unsubscribing from push:', error);
/lib/notifications/subscription.ts:263 console.error('Error updating preferences:', error);
/lib/notifications/subscription.ts:281 console.error('Error reading preferences:', error);

/lib/onboarding/progress.ts:73       console.error('Failed to load onboarding progress');
/lib/onboarding/progress.ts:92       console.error('Failed to save onboarding progress');
/lib/onboarding/progress.ts:121      console.error('Failed to clear onboarding progress');
/lib/onboarding/progress.ts:232      console.error('Failed to load onboarding data');
/lib/onboarding/progress.ts:249      console.error('Failed to save onboarding data');
/lib/onboarding/progress.ts:268      console.error('Failed to complete onboarding');

/lib/cron/scheduler.ts:166           console.warn('[Cron] Running without secret...');
/lib/cron/scheduler.ts:171           console.error('[Cron] CRON_SECRET not set');
/lib/cron/scheduler.ts:297           console.debug('...');  // Dev-only
/lib/cron/scheduler.ts:301           console.info('...');
/lib/cron/scheduler.ts:304           console.warn('...');
/lib/cron/scheduler.ts:307           console.error('...');
/lib/cron/scheduler.ts:337           console.error('[Cron] Failed to send log');

/lib/analytics/consent.ts:137        console.warn('Unable to persist consent');
/lib/analytics/consent.ts:319        console.info('Local analytics data cleared');
```

### Analytics (All console.log - Development Only)

```
/lib/analytics/analytics.ts:135      console.log('[GA4] Would initialize...');
/lib/analytics/analytics.ts:150      console.log('[GA4] Would track:', event);
/lib/analytics/analytics.ts:165      console.log('[GA4] Would track page view:', pageData);
/lib/analytics/analytics.ts:172      console.log('[GA4] Identify called');
/lib/analytics/analytics.ts:179      console.log('[GA4] Reset called');
/lib/analytics/analytics.ts:205      console.log('[Plausible] Would initialize...');
/lib/analytics/analytics.ts:216      console.log('[Plausible] Would track:', event);
/lib/analytics/analytics.ts:223      console.log('[Plausible] Page view tracked');
/lib/analytics/analytics.ts:230      console.log('[Plausible] Does not support identify');
/lib/analytics/analytics.ts:237      console.log('[Plausible] Reset called');
/lib/analytics/analytics.ts:259      console.log('[Custom] Initialized...');
/lib/analytics/analytics.ts:287      console.error('[Custom] Track error:', error);
/lib/analytics/analytics.ts:321      console.error('[Custom] Identify error:', error);
/lib/analytics/analytics.ts:328      console.log('[Custom] Reset called');
/lib/analytics/analytics.ts:359      console.log('[Analytics] Disabled...');
/lib/analytics/analytics.ts:406      console.log('[Analytics] Initialized with providers');
/lib/analytics/analytics.ts:414      console.log('[Analytics] Consent revoked');
/lib/analytics/analytics.ts:448      console.log('[Analytics] Skipping track');
/lib/analytics/analytics.ts:468      console.warn('[Analytics] Invalid event:', event);
/lib/analytics/analytics.ts:487      console.log('[Analytics] Tracked:', event.name);
/lib/analytics/analytics.ts:529      console.log('[Analytics] Skipping page view');
/lib/analytics/analytics.ts:539      console.log('[Analytics] Page view:', pageData.path);
/lib/analytics/analytics.ts:553      console.log('[Analytics] Skipping identify');
/lib/analytics/analytics.ts:566      console.log('[Analytics] Identified:', userId);
/lib/analytics/analytics.ts:586      console.log('[Analytics] Reset');
```

### Auth & Context (Keep - Error Logging)

```
/src/contexts/UserContext.tsx:141    console.error('Error loading preferences:', prefsError);
/src/contexts/UserContext.tsx:162    console.error('Error loading user data:', err);
/src/contexts/UserContext.tsx:275    console.error('Error saving preferences:', upsertError);
/src/contexts/UserContext.tsx:333    console.error('Error refreshing profile:', err);
/src/contexts/AuthContext.tsx:99     console.error('Error initializing auth:', err);
/src/contexts/AuthContext.tsx:288    console.error('Error refreshing user:', err);

/src/lib/auth/session.ts:33          console.error('Error getting session:', error.message);
/src/lib/auth/session.ts:39          console.error('Unexpected error getting session:', err);
/src/lib/auth/session.ts:53          console.error('Error getting server session:', error.message);
/src/lib/auth/session.ts:59          console.error('Unexpected error getting server session:', err);
/src/lib/auth/session.ts:73          console.error('Error getting server user:', error.message);
/src/lib/auth/session.ts:79          console.error('Unexpected error getting server user:', err);
/src/lib/auth/session.ts:94          console.error('Error refreshing session:', error.message);
/src/lib/auth/session.ts:100         console.error('Unexpected error refreshing session:', err);
```

### Sentry Mock (Development - Keep)

```
/src/lib/error/sentry.ts:121         console.info('[Sentry] Disabled in current environment');
/src/lib/error/sentry.ts:146         console.info('[Sentry] Would initialize...');
/src/lib/error/sentry.ts:187         console.error('[Sentry] Would capture exception:', error.message);
/src/lib/error/sentry.ts:215         console.info('[Sentry] Would capture message');
/src/lib/error/sentry.ts:238         console.info('[Sentry] Would set user:', user);
/src/lib/error/sentry.ts:256         console.info('[Sentry] Would set tags:', tags);
/src/lib/error/sentry.ts:274         console.info('[Sentry] Would set extra:', key, value);
/src/lib/error/sentry.ts:292         console.info('[Sentry] Would set error context:', context);
/src/lib/error/sentry.ts:314         console.debug('[Sentry] Would add breadcrumb:', breadcrumb);
/src/lib/error/sentry.ts:336         console.info('[Sentry] Would start transaction');
/src/lib/error/sentry.ts:340         console.info('[Sentry] Would finish transaction');
```

### Logger (Keep - Part of Logger Implementation)

```
/src/lib/error/logger.ts:206         getConsoleMethod(level): typeof console.log
/src/lib/error/logger.ts:209         return console.debug;
/src/lib/error/logger.ts:211         return console.info;
/src/lib/error/logger.ts:213         return console.warn;
/src/lib/error/logger.ts:216         return console.error;
/src/lib/error/logger.ts:218         return console.log;
```

---

## 4. Cleanup Recommendations

### Immediate Removal (Debug Logs)

| File | Line | Current | Action |
|------|------|---------|--------|
| `/api/feedback/route.ts` | 96 | `console.log('[Feedback Received]')` | Remove or use logger |
| `/hooks/useOfflineDevotionals.ts` | 155, 214, 248, 283, 299, 313 | Success logs | Remove |
| `/hooks/usePushNotifications.ts` | 138, 172 | Success logs | Remove |
| `/hooks/useServiceWorker.ts` | 86, 98, 116, 120, 140, 168, 184, 212 | Status logs | Remove |

### Replace with Logger

For files that need logging in production, replace `console.*` with the custom logger:

```typescript
import { logger } from '@/lib/error/logger';

// Instead of
console.log('[Offline] Cached devotional:', devotional.slug);

// Use
logger.debug('Cached devotional', { slug: devotional.slug });
```

### Keep as Is

- All `console.error` in catch blocks
- `console.warn` for deprecations
- Development-only conditional logs
- Logger implementation internals

---

## 5. Estimated Impact

| Category | Count | Action |
|----------|-------|--------|
| Keep (appropriate) | ~130 | No change |
| Remove (debug) | ~40 | Delete |
| Replace with logger | ~26 | Refactor |

---

## Summary

Most console statements are appropriate error handling. The main cleanup areas are:

1. **Debug logs in hooks** - useOfflineDevotionals, usePushNotifications, useServiceWorker
2. **Success messages** - Should be removed or use proper logger
3. **API feedback log** - Remove data logging in /api/feedback

After cleanup, remaining console statements should only be:
- Error logging in catch blocks
- Warnings for invalid states
- Development-only conditional debugging

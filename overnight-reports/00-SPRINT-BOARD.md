# EUONGELION Sprint Planning Board

**Created:** 2026-01-19
**Target Launch:** 4 weeks from start
**Velocity Assumption:** ~40 hours/week available

---

## Sprint 1: Foundation Fixes (Week 1)
**Focus:** Critical bugs, TypeScript errors, database connections

### Critical Build Issues
- [ ] Remove `ignoreBuildErrors: true` from next.config.js and fix all TypeScript errors (estimate: L) - 01-tech-debt-audit.md
- [ ] Remove `ignoreDuringBuilds: true` from next.config.js and fix all ESLint errors (estimate: L) - 01-tech-debt-audit.md

### Authentication Implementation
- [ ] Implement actual authentication logic in authStore.ts (estimate: L) - 01-tech-debt-audit.md
- [ ] Implement sign up logic in authStore.ts (estimate: M) - 01-tech-debt-audit.md
- [ ] Implement sign out logic in authStore.ts (estimate: S) - 01-tech-debt-audit.md
- [ ] Implement token refresh logic in authStore.ts (estimate: M) - 01-tech-debt-audit.md
- [ ] Implement password reset logic in authStore.ts (estimate: M) - 01-tech-debt-audit.md
- [ ] Add authentication check to /api/user/progress/route.ts (estimate: S) - 01-tech-debt-audit.md

### Database Connection Setup
- [ ] Create and configure Supabase production project (estimate: M) - 41-launch-readiness-checklist.md
- [ ] Apply all database migrations (estimate: M) - 41-launch-readiness-checklist.md
- [ ] Enable and test Row Level Security (RLS) policies (estimate: M) - 41-launch-readiness-checklist.md
- [ ] Configure database connection pooling (estimate: S) - 41-launch-readiness-checklist.md
- [ ] Secure production credentials (estimate: S) - 41-launch-readiness-checklist.md

### Environment Setup
- [ ] Set up production environment variables on Vercel (estimate: S) - 41-launch-readiness-checklist.md
- [ ] Configure SSL certificate (estimate: S) - 41-launch-readiness-checklist.md

**Sprint 1 Total Estimate:** ~35-45 hours

---

## Sprint 2: Core Features Working (Week 2)
**Focus:** Get Supabase connected, PWA functional, auth working

### API Route Database Integration
- [ ] Connect /api/devotionals/route.ts to database (GET) (estimate: M) - 01-tech-debt-audit.md
- [ ] Connect /api/devotionals/route.ts to database (POST) (estimate: M) - 01-tech-debt-audit.md
- [ ] Connect /api/devotionals/[id]/route.ts to database (estimate: M) - 01-tech-debt-audit.md
- [ ] Connect /api/series/route.ts to database (GET) (estimate: M) - 01-tech-debt-audit.md
- [ ] Connect /api/series/route.ts to database (POST) (estimate: M) - 01-tech-debt-audit.md
- [ ] Connect /api/series/[slug]/route.ts to database (GET/PUT) (estimate: M) - 01-tech-debt-audit.md
- [ ] Connect /api/user/progress/route.ts to database (estimate: M) - 01-tech-debt-audit.md
- [ ] Connect /api/user/bookmarks/route.ts to database (estimate: M) - 01-tech-debt-audit.md
- [ ] Connect /api/soul-audit/submit/route.ts to database (estimate: M) - 01-tech-debt-audit.md

### Store API Integration
- [ ] Implement actual API call in devotionalStore.ts (estimate: M) - 01-tech-debt-audit.md
- [ ] Implement actual API calls in userStore.ts (3 methods) (estimate: M) - 01-tech-debt-audit.md
- [ ] Implement actual API calls in progressStore.ts (2 methods) (estimate: M) - 01-tech-debt-audit.md
- [ ] Implement actual API calls in bookmarkStore.ts (2 methods) (estimate: M) - 01-tech-debt-audit.md

### PWA Verification
- [ ] Verify service worker registers successfully (estimate: S) - 41-launch-readiness-checklist.md
- [ ] Verify core app shell is cached (estimate: S) - 41-launch-readiness-checklist.md
- [ ] Test offline indicator shows when disconnected (estimate: S) - 42-qa-test-plan.md
- [ ] Verify manifest.json is valid with all required icons (estimate: S) - 41-launch-readiness-checklist.md
- [ ] Test app install on iOS Safari (estimate: S) - 42-qa-test-plan.md
- [ ] Test app install on Android Chrome (estimate: S) - 42-qa-test-plan.md

### Auth Flow Testing
- [ ] Test sign up flow works (TC-AUTH-001) (estimate: S) - 42-qa-test-plan.md
- [ ] Test sign in flow works (TC-AUTH-005) (estimate: S) - 42-qa-test-plan.md
- [ ] Test password reset flow (TC-AUTH-007) (estimate: S) - 42-qa-test-plan.md
- [ ] Test sign out clears data appropriately (TC-AUTH-008) (estimate: S) - 42-qa-test-plan.md
- [ ] Test session persistence (TC-AUTH-009) (estimate: S) - 42-qa-test-plan.md
- [ ] Test protected routes redirect correctly (TC-AUTH-010) (estimate: S) - 42-qa-test-plan.md

**Sprint 2 Total Estimate:** ~40-50 hours

---

## Sprint 3: Content & Polish (Week 3)
**Focus:** Load real content, visual polish, accessibility

### Content Loading
- [ ] Implement CMS/API fetch for today's devotional in page.tsx (estimate: M) - 01-tech-debt-audit.md
- [ ] Implement CMS/API fetch for series in series/page.tsx (estimate: M) - 01-tech-debt-audit.md
- [ ] Implement CMS/API fetch for series by slug (estimate: M) - 01-tech-debt-audit.md
- [ ] Implement CMS/API fetch for devotional by ID (estimate: M) - 01-tech-debt-audit.md
- [ ] Load at least 7 devotionals (one week of content) (estimate: M) - 41-launch-readiness-checklist.md
- [ ] Load at least 2 complete series (estimate: M) - 41-launch-readiness-checklist.md
- [ ] Verify no placeholder/test content in production (estimate: S) - 41-launch-readiness-checklist.md

### Content Quality
- [ ] Proofread all content for typos/grammar (estimate: M) - 41-launch-readiness-checklist.md
- [ ] Verify all Scripture references for accuracy (estimate: M) - 41-launch-readiness-checklist.md
- [ ] Verify crisis resources (988 Lifeline, Crisis Text Line) are accurate (estimate: S) - 41-launch-readiness-checklist.md

### Accessibility (WCAG 2.1 AA)
- [ ] Complete WCAG 2.1 AA audit (estimate: L) - 41-launch-readiness-checklist.md
- [ ] Fix color contrast ratios to meet standards (estimate: M) - 41-launch-readiness-checklist.md
- [ ] Complete screen reader testing (estimate: M) - 41-launch-readiness-checklist.md
- [ ] Verify keyboard navigation works throughout (estimate: M) - 42-qa-test-plan.md
- [ ] Ensure focus indicators are visible (estimate: S) - 41-launch-readiness-checklist.md
- [ ] Add alt text to all images (estimate: S) - 41-launch-readiness-checklist.md
- [ ] Test devotional accessibility with screen reader (TC-DEV-007) (estimate: M) - 42-qa-test-plan.md
- [ ] Test Soul Audit accessibility (TC-SA-009) (estimate: M) - 42-qa-test-plan.md

### Visual Polish
- [ ] Implement proper MDX or markdown renderer for devotionals (estimate: L) - 01-tech-debt-audit.md
- [ ] Verify dark mode displays content readably (estimate: S) - 41-launch-readiness-checklist.md
- [ ] Test dark mode toggle (TC-GEN-001) (estimate: S) - 42-qa-test-plan.md
- [ ] Verify responsive layout on mobile (TC-GEN-002) (estimate: S) - 42-qa-test-plan.md
- [ ] Verify responsive layout on tablet (TC-GEN-003) (estimate: S) - 42-qa-test-plan.md
- [ ] Verify responsive layout on desktop (TC-GEN-004) (estimate: S) - 42-qa-test-plan.md

### Logging Cleanup
- [ ] Replace console.log calls with logger.debug in API routes (estimate: M) - 01-tech-debt-audit.md
- [ ] Replace console.error calls with logger.error (estimate: M) - 01-tech-debt-audit.md
- [ ] Add environment check to suppress debug logs in production (estimate: S) - 01-tech-debt-audit.md

**Sprint 3 Total Estimate:** ~40-50 hours

---

## Sprint 4: Launch Prep (Week 4)
**Focus:** Testing, performance, marketing prep

### Functional Testing
- [ ] Run full regression test suite (estimate: L) - 42-qa-test-plan.md
- [ ] Test all devotional flows (TC-DEV-001 through TC-DEV-006) (estimate: M) - 42-qa-test-plan.md
- [ ] Test all series flows (TC-SER-001 through TC-SER-005) (estimate: M) - 42-qa-test-plan.md
- [ ] Test all Soul Audit flows including crisis detection (TC-SA-001 through TC-SA-008) (estimate: M) - 42-qa-test-plan.md
- [ ] Test all bookmark flows (TC-BM-001 through TC-BM-007) (estimate: M) - 42-qa-test-plan.md
- [ ] Verify no blocking bugs remain (estimate: M) - 41-launch-readiness-checklist.md

### Cross-Browser Testing
- [ ] Test Chrome (latest) - Desktop (estimate: S) - 41-launch-readiness-checklist.md
- [ ] Test Chrome (latest) - Android (estimate: S) - 41-launch-readiness-checklist.md
- [ ] Test Safari (latest) - Desktop (estimate: S) - 41-launch-readiness-checklist.md
- [ ] Test Safari (latest) - iOS (estimate: S) - 41-launch-readiness-checklist.md
- [ ] Test Firefox (latest) - Desktop (estimate: S) - 41-launch-readiness-checklist.md
- [ ] Test Edge (latest) - Desktop (estimate: S) - 41-launch-readiness-checklist.md

### Device Testing
- [ ] Test iPhone SE (small screen) (estimate: S) - 41-launch-readiness-checklist.md
- [ ] Test iPhone 14/15 (standard) (estimate: S) - 41-launch-readiness-checklist.md
- [ ] Test iPhone 14 Pro Max (large) (estimate: S) - 41-launch-readiness-checklist.md
- [ ] Test iPad (tablet) (estimate: S) - 41-launch-readiness-checklist.md
- [ ] Test Android phone (various sizes) (estimate: S) - 41-launch-readiness-checklist.md

### Performance Testing
- [ ] Achieve Lighthouse Performance score > 90 (estimate: M) - 41-launch-readiness-checklist.md
- [ ] Achieve Lighthouse Accessibility score > 90 (estimate: M) - 41-launch-readiness-checklist.md
- [ ] Achieve Lighthouse Best Practices score > 90 (estimate: S) - 41-launch-readiness-checklist.md
- [ ] Achieve Lighthouse SEO score > 90 (estimate: S) - 41-launch-readiness-checklist.md
- [ ] Verify LCP < 2.5s (estimate: M) - 41-launch-readiness-checklist.md
- [ ] Verify FID < 100ms (estimate: S) - 41-launch-readiness-checklist.md
- [ ] Verify CLS < 0.1 (estimate: S) - 41-launch-readiness-checklist.md

### Security
- [ ] Verify no sensitive data exposed in client code (estimate: S) - 41-launch-readiness-checklist.md
- [ ] Verify API routes properly authenticated (estimate: M) - 41-launch-readiness-checklist.md
- [ ] Test for SQL injection vulnerabilities (estimate: S) - 41-launch-readiness-checklist.md
- [ ] Verify XSS protection in place (estimate: S) - 41-launch-readiness-checklist.md
- [ ] Verify HTTPS enforced (estimate: S) - 41-launch-readiness-checklist.md
- [ ] Configure security headers (estimate: S) - 41-launch-readiness-checklist.md

### Legal & Compliance
- [ ] Publish Privacy Policy (estimate: M) - 41-launch-readiness-checklist.md
- [ ] Publish Terms of Service (estimate: M) - 41-launch-readiness-checklist.md
- [ ] Publish Accessibility statement (estimate: S) - 41-launch-readiness-checklist.md

### Marketing Prep
- [ ] Create high-resolution app icon for marketing (estimate: S) - 41-launch-readiness-checklist.md
- [ ] Create screenshots for marketing (estimate: M) - 41-launch-readiness-checklist.md
- [ ] Write App Store description copy (estimate: M) - 41-launch-readiness-checklist.md
- [ ] Draft social media announcement posts (estimate: M) - 41-launch-readiness-checklist.md

### Support Readiness
- [ ] Configure support email (estimate: S) - 41-launch-readiness-checklist.md
- [ ] Publish FAQ page (estimate: M) - 41-launch-readiness-checklist.md
- [ ] Set up bug report mechanism (estimate: S) - 41-launch-readiness-checklist.md

### Monitoring Setup
- [ ] Set up uptime monitoring (estimate: S) - 41-launch-readiness-checklist.md
- [ ] Configure alert notifications (estimate: S) - 41-launch-readiness-checklist.md
- [ ] Configure database backups (estimate: S) - 41-launch-readiness-checklist.md

**Sprint 4 Total Estimate:** ~40-50 hours

---

## Backlog (Post-Launch)

### Error Tracking & Monitoring
- [ ] Implement Sentry error tracking (Sentry.init) (estimate: M) - 01-tech-debt-audit.md
- [ ] Implement Sentry.captureException (estimate: S) - 01-tech-debt-audit.md
- [ ] Implement Sentry.captureMessage (estimate: S) - 01-tech-debt-audit.md
- [ ] Complete all Sentry-related TODOs (7 remaining) (estimate: M) - 01-tech-debt-audit.md
- [ ] Enable performance monitoring (estimate: S) - 41-launch-readiness-checklist.md
- [ ] Configure log aggregation (estimate: M) - 41-launch-readiness-checklist.md

### Cron Jobs & Background Tasks
- [ ] Implement push notification sending in cron/notifications.ts (estimate: L) - 01-tech-debt-audit.md
- [ ] Implement email sending in cron/notifications.ts (estimate: M) - 01-tech-debt-audit.md
- [ ] Implement database cleanup queries in cron/cleanup.ts (estimate: M) - 01-tech-debt-audit.md
- [ ] Implement digest email functionality in cron/digest.ts (estimate: L) - 01-tech-debt-audit.md
- [ ] Implement streak calculation in cron/streaks.ts (estimate: M) - 01-tech-debt-audit.md
- [ ] Implement logging service integration in cron/scheduler.ts (estimate: S) - 01-tech-debt-audit.md

### Feature Enhancements (Priority Ordered by 44-feature-prioritization-matrix.md)
- [ ] Daily Reminder System (Impact: 5, Effort: 2) (estimate: M) - 44-feature-prioritization-matrix.md
- [ ] Push Notifications (Impact: 5, Effort: 3) (estimate: L) - 44-feature-prioritization-matrix.md
- [ ] Email Verification (Impact: 4, Effort: 2) (estimate: M) - 44-feature-prioritization-matrix.md
- [ ] Password Strength Meter (Impact: 3, Effort: 1) (estimate: S) - 44-feature-prioritization-matrix.md
- [ ] Reading Time Estimate (Impact: 3, Effort: 1) (estimate: S) - 44-feature-prioritization-matrix.md
- [ ] Social Login - Google (Impact: 4, Effort: 2) (estimate: M) - 44-feature-prioritization-matrix.md
- [ ] Search Functionality (Impact: 4, Effort: 3) (estimate: L) - 44-feature-prioritization-matrix.md
- [ ] Progress Statistics Page (Impact: 4, Effort: 2) (estimate: M) - 44-feature-prioritization-matrix.md
- [ ] Error Boundary Improvements (Impact: 4, Effort: 2) (estimate: M) - 44-feature-prioritization-matrix.md
- [ ] Streak Celebrations (Impact: 3, Effort: 2) (estimate: M) - 44-feature-prioritization-matrix.md
- [ ] Social Login - Apple (Impact: 3, Effort: 2) (estimate: M) - 44-feature-prioritization-matrix.md
- [ ] Related Devotionals (Impact: 3, Effort: 2) (estimate: M) - 44-feature-prioritization-matrix.md
- [ ] Reading History (Impact: 3, Effort: 2) (estimate: M) - 44-feature-prioritization-matrix.md
- [ ] Font Size Settings (Impact: 3, Effort: 2) (estimate: M) - 44-feature-prioritization-matrix.md
- [ ] Category Browsing Page (Impact: 3, Effort: 2) (estimate: M) - 44-feature-prioritization-matrix.md
- [ ] Offline Download Manager (Impact: 4, Effort: 3) (estimate: L) - 44-feature-prioritization-matrix.md
- [ ] Sermon Notes Feature (Impact: 3, Effort: 3) (estimate: L) - 44-feature-prioritization-matrix.md
- [ ] Prayer Request Submission (Impact: 3, Effort: 3) (estimate: L) - 44-feature-prioritization-matrix.md
- [ ] Content Ratings/Feedback (Impact: 3, Effort: 3) (estimate: L) - 44-feature-prioritization-matrix.md

### Future Features (Lower Priority)
- [ ] Audio Devotionals (Impact: 4, Effort: 5) (estimate: XL) - 44-feature-prioritization-matrix.md
- [ ] Reading Plans (Impact: 4, Effort: 4) (estimate: L) - 44-feature-prioritization-matrix.md
- [ ] Community Features (Impact: 3, Effort: 5) (estimate: XL) - 44-feature-prioritization-matrix.md
- [ ] Multi-language Support (Impact: 3, Effort: 5) (estimate: XL) - 44-feature-prioritization-matrix.md
- [ ] Shepherd Dashboard (Impact: 4, Effort: 5) (estimate: XL) - 44-feature-prioritization-matrix.md
- [ ] Group Bible Studies (Impact: 3, Effort: 5) (estimate: XL) - 44-feature-prioritization-matrix.md
- [ ] URL shortener integration (estimate: M) - 01-tech-debt-audit.md
- [ ] Custom Reading Lists (Impact: 2, Effort: 3) (estimate: M) - 44-feature-prioritization-matrix.md
- [ ] Scripture Memory Game (Impact: 2, Effort: 4) (estimate: L) - 44-feature-prioritization-matrix.md
- [ ] Social Sharing Images (Impact: 2, Effort: 3) (estimate: M) - 44-feature-prioritization-matrix.md
- [ ] Widget (iOS/Android) (Impact: 3, Effort: 5) (estimate: XL) - 44-feature-prioritization-matrix.md

### Nice-to-Have Polish
- [ ] Enable Soul Audit when feature is fully implemented (estimate: S) - 01-tech-debt-audit.md
- [ ] Track user progress on series pages (estimate: M) - 01-tech-debt-audit.md
- [ ] Content calendar for first month post-launch (estimate: M) - 41-launch-readiness-checklist.md
- [ ] Next 2 weeks of content ready (estimate: L) - 41-launch-readiness-checklist.md

---

## Estimate Key

| Size | Time | Examples |
|------|------|----------|
| S (Small) | <2 hours | Config changes, simple fixes, single-file edits |
| M (Medium) | 2-4 hours | Feature implementation, multi-file changes, API integration |
| L (Large) | 4-8 hours | Complex features, significant refactoring, full implementations |
| XL (Extra Large) | 8+ hours | Major features, new systems, extensive testing required |

---

## Progress Tracking

| Sprint | Planned Items | Completed | Blocked | Notes |
|--------|---------------|-----------|---------|-------|
| Sprint 1 | 16 | 0 | 0 | |
| Sprint 2 | 24 | 0 | 0 | |
| Sprint 3 | 26 | 0 | 0 | |
| Sprint 4 | 44 | 0 | 0 | |

---

## Source Documents

- `/tools/overnight-reports/code-analysis/01-tech-debt-audit.md`
- `/tools/overnight-reports/planning/41-launch-readiness-checklist.md`
- `/tools/overnight-reports/planning/42-qa-test-plan.md`
- `/tools/overnight-reports/planning/44-feature-prioritization-matrix.md`

---

*"The lost are waiting." - Ship fast, learn from users, iterate.*

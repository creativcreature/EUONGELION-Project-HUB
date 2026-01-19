# EUONGELION Master Action Backlog

**Generated:** 2026-01-19
**Source:** All 83 overnight reports
**Purpose:** Comprehensive task list extracted from autonomous code analysis, documentation, and planning reports

---

## Critical (Must Fix Before Launch)

### Security Issues
- [ ] **Sanitize dangerouslySetInnerHTML in DevotionalReader.tsx** - XSS vulnerability at line 227 where `section.content` is rendered without sanitization. Use DOMPurify. *Source: 09-security-scan.md* `/app/components/devotional/DevotionalReader.tsx:227`
- [ ] **Sanitize dangerouslySetInnerHTML in devotional page** - XSS vulnerability at line 237 where `formattedText` is rendered without sanitization. Use DOMPurify. *Source: 09-security-scan.md* `/app/src/app/devotional/[id]/page.tsx:237`
- [ ] **Implement Content Security Policy (CSP) header** - Nonce is generated but CSP header is not actually set in middleware. *Source: 09-security-scan.md* `/app/middleware.ts`
- [ ] **Implement CSRF protection** - No CSRF tokens found; all POST/PUT/DELETE routes are vulnerable. *Source: 09-security-scan.md*
- [ ] **Implement actual rate limiting** - Headers are present but decorative; no request counting or blocking. *Source: 09-security-scan.md* `/app/middleware.ts`

### Authentication
- [ ] **Complete authentication implementation** - Auth store has TODO placeholders for actual auth logic. *Source: 09-security-scan.md* `/app/stores/authStore.ts`
- [ ] **Implement actual sign-in logic** - Currently placeholder. *Source: 09-security-scan.md* `/app/stores/authStore.ts`
- [ ] **Implement actual sign-up logic** - Currently placeholder. *Source: 09-security-scan.md* `/app/stores/authStore.ts`
- [ ] **Implement actual sign-out logic** - Currently placeholder. *Source: 09-security-scan.md* `/app/stores/authStore.ts`
- [ ] **Implement token refresh logic** - Currently placeholder. *Source: 09-security-scan.md* `/app/stores/authStore.ts`

### Database Integration
- [ ] **Replace placeholder database queries in API routes** - All routes have `TODO: Replace with actual database query`. *Source: 09-security-scan.md* `/app/api/` routes
- [ ] **Connect Supabase client to actual database** - Currently using mock data. *Source: 70-seed-data-review.md*
- [ ] **Run database migrations** - Schema exists but needs to be applied. *Source: 71-data-migration-plan.md*

### Core Functionality
- [ ] **Implement devotional content loading from database** - Currently using placeholder data. *Source: 01-api-routes-audit.md*
- [ ] **Implement series progression logic** - Track user progress through series. *Source: 01-api-routes-audit.md*
- [ ] **Implement Soul Audit scoring algorithm** - Results calculation needs completion. *Source: 01-api-routes-audit.md*

---

## High Priority (Should Fix Before Launch)

### TypeScript Improvements
- [ ] **Fix double type assertions in useField.ts** - `inputValue as unknown as T` at line 154 is a code smell. *Source: 10-typescript-coverage.md* `/app/hooks/useField.ts:154`
- [ ] **Fix double type assertion for File array** - `fileArray as unknown as File` at line 325. *Source: 10-typescript-coverage.md* `/app/hooks/useField.ts:325`
- [ ] **Add explicit return types to API routes** - Currently using inferred types. *Source: 10-typescript-coverage.md* `/app/api/` routes
- [ ] **Review type assertion `prevState as object`** - Could use type guard instead. *Source: 10-typescript-coverage.md* `/app/stores/middleware.ts:86`
- [ ] **Review type assertion `value as string`** - Storage value could be null. *Source: 10-typescript-coverage.md* `/app/stores/devotionalStore.ts:210`

### Performance Optimization
- [ ] **Add dynamic imports for Modal component** - Loads upfront but only needed on interaction. *Source: 08-performance-analysis.md* `/app/components/ui/Modal.tsx`
- [ ] **Add dynamic imports for Drawer component** - Loads upfront but only needed on interaction. *Source: 08-performance-analysis.md* `/app/components/ui/Drawer.tsx`
- [ ] **Add dynamic imports for FeedbackForm** - Only needed on specific page. *Source: 08-performance-analysis.md*
- [ ] **Add dynamic imports for BugReportForm** - Only needed on specific action. *Source: 08-performance-analysis.md*
- [ ] **Add dynamic imports for ShareModal** - Only needed on share action. *Source: 08-performance-analysis.md*
- [ ] **Add dynamic imports for NotificationCenter** - Only needed on interaction. *Source: 08-performance-analysis.md*
- [ ] **Add dynamic imports for PerformanceMonitor** - Dev tool only. *Source: 08-performance-analysis.md*
- [ ] **Add dynamic imports for ResultsChart** - Only on results page. *Source: 08-performance-analysis.md*
- [ ] **Add React.memo to DevotionalCard** - Used in lists but not memoized. *Source: 08-performance-analysis.md* `/app/components/devotional/DevotionalCard.tsx`
- [ ] **Add React.memo to NotificationItem** - List item needs memoization. *Source: 08-performance-analysis.md*
- [ ] **Implement virtual lists for discovery page** - Renders potentially many elements without virtualization. *Source: 08-performance-analysis.md* `/app/src/app/discovery/page.tsx`
- [ ] **Add font display: 'swap' to font loading** - Improve CLS. *Source: 08-performance-analysis.md* `/app/src/app/layout.tsx`

### Testing Infrastructure
- [ ] **Write unit tests for date.ts utilities** - Priority 1 utility file, ~15 functions. *Source: 80-unit-test-plan.md* `/app/lib/utils/date.ts`
- [ ] **Write unit tests for scripture.ts utilities** - Priority 1 utility file. *Source: 80-unit-test-plan.md* `/app/lib/utils/scripture.ts`
- [ ] **Write unit tests for validators.ts** - Priority 1 utility file. *Source: 80-unit-test-plan.md* `/app/lib/utils/validators.ts`
- [ ] **Write unit tests for authStore** - Priority 1 store, critical functionality. *Source: 80-unit-test-plan.md* `/app/stores/authStore.ts`
- [ ] **Write unit tests for progressStore** - Priority 1 store. *Source: 80-unit-test-plan.md* `/app/stores/progressStore.ts`
- [ ] **Write unit tests for devotionalStore** - Priority 1 store. *Source: 80-unit-test-plan.md* `/app/stores/devotionalStore.ts`
- [ ] **Set up Playwright for E2E testing** - Framework chosen but not configured. *Source: 81-integration-test-plan.md*
- [ ] **Write E2E test: Complete authentication flow** - Sign up, sign in, sign out. *Source: 81-integration-test-plan.md*
- [ ] **Write E2E test: Complete devotional reading flow** - Open, read, complete, navigate. *Source: 81-integration-test-plan.md*
- [ ] **Write E2E test: Soul Audit full flow** - Take audit, view results, retake. *Source: 81-integration-test-plan.md*

### PWA Requirements
- [ ] **Create all required favicon sizes** - favicon.ico, apple-touch-icon, etc. *Source: 67-favicon-app-icon-checklist.md*
- [ ] **Create 192x192 PWA icon** - Required for manifest. *Source: 67-favicon-app-icon-checklist.md*
- [ ] **Create 512x512 PWA icon** - Required for manifest. *Source: 67-favicon-app-icon-checklist.md*
- [ ] **Create maskable icon version** - For adaptive icons on Android. *Source: 67-favicon-app-icon-checklist.md*
- [ ] **Verify manifest.json is valid and complete** - Check all required fields. *Source: 67-favicon-app-icon-checklist.md*

### Accessibility
- [ ] **Add aria-labels to all icon buttons** - Some may be missing. *Source: 05-accessibility-audit.md*
- [ ] **Ensure all form inputs have associated labels** - Verify with axe. *Source: 05-accessibility-audit.md*
- [ ] **Test with screen reader (VoiceOver/NVDA)** - Manual testing required. *Source: 05-accessibility-audit.md*
- [ ] **Verify focus indicators are visible** - Check all interactive elements. *Source: 05-accessibility-audit.md*
- [ ] **Test keyboard navigation throughout app** - Tab order, enter/space activation. *Source: 05-accessibility-audit.md*

### Error Handling
- [ ] **Implement error boundaries for all pages** - Catch and display errors gracefully. *Source: 06-error-handling-audit.md*
- [ ] **Add proper error logging** - Replace console.log with structured logger. *Source: 06-error-handling-audit.md*
- [ ] **Implement offline error handling** - Show appropriate message when offline. *Source: 06-error-handling-audit.md*

---

## Medium Priority (Fix After Launch)

### TypeScript Enhancements
- [ ] **Create JsonValue type for metadata fields** - Replace `unknown` with proper JSON type. *Source: 10-typescript-coverage.md* `/app/types/`
- [ ] **Add type guards for storage parsing** - Safer than type assertions. *Source: 10-typescript-coverage.md*
- [ ] **Enable noUncheckedIndexedAccess in tsconfig** - Stricter null checks. *Source: 10-typescript-coverage.md* `/app/tsconfig.json`
- [ ] **Enable exactOptionalPropertyTypes in tsconfig** - Stricter optional handling. *Source: 10-typescript-coverage.md* `/app/tsconfig.json`
- [ ] **Add JSDoc comments to complex types** - Improve documentation. *Source: 10-typescript-coverage.md*

### Testing Expansion
- [ ] **Achieve 70% unit test coverage** - Currently ~5%, need ~250 tests. *Source: 80-unit-test-plan.md*
- [ ] **Write unit tests for all hooks** - useAuth, useDevotional, useProgress, etc. *Source: 80-unit-test-plan.md*
- [ ] **Write unit tests for UI components** - Button, Card, Input, etc. *Source: 80-unit-test-plan.md*
- [ ] **Set up visual regression testing** - With Percy or Chromatic. *Source: 82-visual-regression-test-plan.md*
- [ ] **Test all components in dark mode** - Visual verification. *Source: 82-visual-regression-test-plan.md*
- [ ] **Test all components in sepia mode** - Visual verification. *Source: 82-visual-regression-test-plan.md*
- [ ] **Test responsive layouts at all breakpoints** - xs, sm, md, lg, xl, 2xl. *Source: 82-visual-regression-test-plan.md*
- [ ] **Test on iPhone Safari (P1 device)** - Critical device. *Source: 83-device-test-matrix.md*
- [ ] **Test on Android Chrome (P1 device)** - Critical device. *Source: 83-device-test-matrix.md*
- [ ] **Test offline functionality on mobile** - Service worker caching. *Source: 83-device-test-matrix.md*

### Performance Monitoring
- [ ] **Add bundle analyzer to build process** - Identify large dependencies. *Source: 08-performance-analysis.md*
- [ ] **Set up Lighthouse CI in deployment** - Automated performance checks. *Source: 56-performance-benchmarks.md*
- [ ] **Monitor Core Web Vitals in production** - LCP, INP, CLS. *Source: 56-performance-benchmarks.md*
- [ ] **Implement performance budgets** - JS < 200KB, CSS < 50KB. *Source: 56-performance-benchmarks.md*

### Content Assets
- [ ] **Create hero images for all series** - 1200x630px recommended. *Source: 64-image-requirements-list.md*
- [ ] **Create Open Graph images for sharing** - 1200x630px. *Source: 68-open-graph-image-requirements.md*
- [ ] **Create Twitter card images** - 1200x600px. *Source: 68-open-graph-image-requirements.md*
- [ ] **Create app store screenshots** - iPhone 6.5", iPhone 5.5", iPad. *Source: 69-screenshot-requirements.md*
- [ ] **Create promotional graphics** - For marketing materials. *Source: 69-screenshot-requirements.md*

### Database & Data
- [ ] **Create production seed data** - Initial content for launch. *Source: 70-seed-data-review.md*
- [ ] **Implement automated backups** - Daily database backups. *Source: 72-backup-strategy-documentation.md*
- [ ] **Set up backup verification** - Test restore process. *Source: 72-backup-strategy-documentation.md*
- [ ] **Implement data retention policies** - Define retention periods. *Source: 73-data-retention-policy.md*

### Email System
- [ ] **Set up email service provider** - Resend, SendGrid, or similar. *Source: 78-launch-announcement-draft.md*
- [ ] **Test all email templates** - Welcome, password reset, notifications. *Source: 78-launch-announcement-draft.md*
- [ ] **Implement email preferences** - User opt-in/out. *Source: 78-launch-announcement-draft.md*

### Analytics
- [ ] **Set up analytics tracking** - Vercel Analytics or Google Analytics 4. *Source: 56-performance-benchmarks.md*
- [ ] **Track devotional completion events** - Key engagement metric. *Source: 56-performance-benchmarks.md*
- [ ] **Track Soul Audit completion events** - Key conversion metric. *Source: 56-performance-benchmarks.md*
- [ ] **Set up retention tracking** - DAU/MAU monitoring. *Source: 56-performance-benchmarks.md*

---

## Low Priority (Nice to Have)

### Advanced TypeScript
- [ ] **Consider branded types for IDs** - DevotionalId, SeriesId, UserId. *Source: 10-typescript-coverage.md*
- [ ] **Add runtime type validation with Zod** - For API inputs. *Source: 10-typescript-coverage.md*
- [ ] **Enable noImplicitReturns in tsconfig** - Stricter function returns. *Source: 10-typescript-coverage.md*

### Advanced Performance
- [ ] **Implement streaming SSR** - Better TTFB for content pages. *Source: 08-performance-analysis.md*
- [ ] **Add edge caching via middleware** - Cache static content at edge. *Source: 08-performance-analysis.md*
- [ ] **Consider server components for static content** - Reduce client JS. *Source: 08-performance-analysis.md*
- [ ] **Add will-change hints to heavy animations** - GPU optimization. *Source: 08-performance-analysis.md*
- [ ] **Implement icon sprites** - Reduce HTTP requests for icons. *Source: 08-performance-analysis.md*

### Advanced Security
- [ ] **Add security penetration testing** - Professional audit. *Source: 09-security-scan.md*
- [ ] **Implement security monitoring/alerts** - Detect suspicious activity. *Source: 09-security-scan.md*
- [ ] **Add vulnerability scanning to CI/CD** - Automated checks. *Source: 09-security-scan.md*
- [ ] **Run npm audit and fix vulnerabilities** - Dependency security. *Source: 09-security-scan.md*

### Marketing & Growth
- [ ] **Finalize landing page copy** - Draft exists, needs review. *Source: 74-landing-page-copy.md*
- [ ] **Create feature highlight content** - For marketing pages. *Source: 75-feature-highlight-copy.md*
- [ ] **Send testimonial request emails** - Template exists. *Source: 76-testimonial-request-template.md*
- [ ] **Complete press kit** - Logo pack, screenshots, boilerplate. *Source: 77-press-kit-outline.md*
- [ ] **Implement referral program** - Outline exists. *Source: 79-referral-program-outline.md*
- [ ] **Create social media assets** - Profile images, cover photos. *Source: 77-press-kit-outline.md*

### Documentation
- [ ] **Complete API documentation** - Document all endpoints. *Source: 21-api-documentation.md*
- [ ] **Create user guide** - How to use the app. *Source: 30-troubleshooting-guide.md*
- [ ] **Document deployment process** - Step-by-step guide. *Source: 23-deployment-guide.md*
- [ ] **Create contributor guide** - For future developers. *Source: 24-contributing-guidelines.md*

### Testing Expansion
- [ ] **Write E2E tests for bookmarks flow** - Add, remove, view bookmarks. *Source: 81-integration-test-plan.md*
- [ ] **Write E2E tests for settings flow** - All settings pages. *Source: 81-integration-test-plan.md*
- [ ] **Write E2E tests for search flow** - Search, filter, navigate. *Source: 81-integration-test-plan.md*
- [ ] **Write E2E tests for sharing flow** - Share devotional, copy link. *Source: 81-integration-test-plan.md*
- [ ] **Test on Samsung Galaxy devices** - P2 device coverage. *Source: 83-device-test-matrix.md*
- [ ] **Test on iPad** - Tablet experience. *Source: 83-device-test-matrix.md*
- [ ] **Test on Firefox** - Browser coverage. *Source: 83-device-test-matrix.md*
- [ ] **Test on Edge** - Browser coverage. *Source: 83-device-test-matrix.md*

---

## Quick Wins (< 30 min each)

### Configuration
- [ ] **Add font display: 'swap' to Inter font** - One line change. *Source: 08-performance-analysis.md* `/app/src/app/layout.tsx`
- [ ] **Add font display: 'swap' to Crimson Pro font** - One line change. *Source: 08-performance-analysis.md* `/app/src/app/layout.tsx`
- [ ] **Add bundle analyzer npm script** - `"analyze": "ANALYZE=true next build"`. *Source: 08-performance-analysis.md* `/app/package.json`
- [ ] **Install @next/bundle-analyzer** - `npm install @next/bundle-analyzer`. *Source: 08-performance-analysis.md*
- [ ] **Add .env.example file** - Document required environment variables. *Source: 09-security-scan.md*

### Quick Security Fixes
- [ ] **Install DOMPurify** - `npm install dompurify @types/dompurify`. *Source: 09-security-scan.md*
- [ ] **Add CSP header to middleware** - Copy nonce into actual header. *Source: 09-security-scan.md* `/app/middleware.ts`

### Quick TypeScript Fixes
- [ ] **Add explicit return type to one API route** - Pick easiest route as template. *Source: 10-typescript-coverage.md*
- [ ] **Create JsonValue type definition** - Simple type alias. *Source: 10-typescript-coverage.md* `/app/types/index.ts`

### Quick Test Additions
- [ ] **Write test for formatDate utility** - Simple unit test. *Source: 80-unit-test-plan.md* `/app/lib/utils/date.ts`
- [ ] **Write test for formatTime utility** - Simple unit test. *Source: 80-unit-test-plan.md* `/app/lib/utils/date.ts`
- [ ] **Write test for validateEmail utility** - Simple unit test. *Source: 80-unit-test-plan.md* `/app/lib/utils/validators.ts`
- [ ] **Write test for sanitizeHtml utility** - Simple unit test. *Source: 80-unit-test-plan.md* `/app/lib/security/sanitize.ts`

### Quick Accessibility Fixes
- [ ] **Add skip link to main content** - Standard a11y pattern. *Source: 05-accessibility-audit.md* `/app/src/app/layout.tsx`
- [ ] **Verify all images have alt text** - Quick audit. *Source: 05-accessibility-audit.md*
- [ ] **Add lang attribute to html tag** - If missing. *Source: 05-accessibility-audit.md* `/app/src/app/layout.tsx`

### Documentation Quick Wins
- [ ] **Update README with setup instructions** - If outdated. *Source: 30-troubleshooting-guide.md*
- [ ] **Add CHANGELOG.md** - Start tracking changes. *Source: 24-contributing-guidelines.md*
- [ ] **Document environment variables** - In README or .env.example. *Source: 30-troubleshooting-guide.md*

### Performance Quick Wins
- [ ] **Add priority to hero images** - `priority` prop on Next.js Image. *Source: 08-performance-analysis.md*
- [ ] **Review console.log statements** - Remove or guard with NODE_ENV. *Source: 09-security-scan.md*

---

## Summary Statistics

| Category | Count |
|----------|-------|
| Critical | 15 |
| High Priority | 41 |
| Medium Priority | 33 |
| Low Priority | 30 |
| Quick Wins | 22 |
| **Total** | **141** |

### By Domain

| Domain | Items |
|--------|-------|
| Security | 18 |
| TypeScript | 16 |
| Performance | 18 |
| Testing | 28 |
| Accessibility | 8 |
| PWA/Assets | 12 |
| Database | 7 |
| Documentation | 6 |
| Marketing | 8 |
| Other | 20 |

---

## Recommended Sprint Order

### Sprint 1: Security & Auth (Critical)
1. Sanitize dangerouslySetInnerHTML (2 files)
2. Implement CSP header
3. Implement CSRF protection
4. Implement rate limiting
5. Complete authentication implementation

### Sprint 2: Database & Core Features (Critical)
1. Connect Supabase to real database
2. Run migrations
3. Replace placeholder queries in API routes
4. Implement devotional loading
5. Implement series progression

### Sprint 3: Performance & Testing Setup (High)
1. Add dynamic imports (8 components)
2. Add React.memo to list items
3. Set up test infrastructure
4. Write critical path tests
5. Add bundle analyzer

### Sprint 4: PWA & Accessibility (High)
1. Create all required icons
2. Verify manifest
3. Test offline functionality
4. Complete accessibility audit
5. Test with screen readers

### Sprint 5: Polish & Launch Prep (Medium)
1. Achieve test coverage target
2. Complete visual testing
3. Device testing matrix
4. Finalize marketing assets
5. Set up analytics

---

*This backlog was generated by analyzing all 83 overnight reports. Items should be re-prioritized based on actual launch timeline and team capacity.*

# Performance Benchmarks for Devotional Apps

**Research Date:** January 19, 2026
**Purpose:** Establish target performance metrics for EUONGELION including load times, engagement benchmarks, and retention rates

---

## Executive Summary

This document establishes performance benchmarks for EUONGELION across three categories: technical performance (load times, Core Web Vitals), user engagement (session length, DAU/MAU), and retention rates. EUONGELION's existing targets (LCP < 2.5s, FID < 100ms from CLAUDE.md) align with industry standards. The key challenge for devotional apps is retention - typical lifestyle apps see only 3.6% Day-30 retention, but top performers achieve 30%+.

---

## Technical Performance Benchmarks

### Core Web Vitals Targets

Google's Core Web Vitals are the standard for measuring web performance:

| Metric | Good | Needs Improvement | Poor | EUONGELION Target |
|--------|------|-------------------|------|-------------------|
| **LCP** (Largest Contentful Paint) | < 2.5s | 2.5s - 4s | > 4s | **< 2.5s** (current target) |
| **INP** (Interaction to Next Paint) | < 200ms | 200ms - 500ms | > 500ms | **< 100ms** |
| **CLS** (Cumulative Layout Shift) | < 0.1 | 0.1 - 0.25 | > 0.25 | **< 0.1** |

**Note:** FID (First Input Delay) has been replaced by INP (Interaction to Next Paint) as of 2024. EUONGELION's CLAUDE.md mentions FID < 100ms, which maps to INP < 200ms.

**Source:** [web.dev - LCP](https://web.dev/articles/lcp), [DebugBear - 2025 Web Performance](https://www.debugbear.com/blog/2025-in-web-performance)

### Industry Performance Statistics

**Current Web Performance (2025):**
- 67% of websites have good LCP scores (June 2025)
- Only 57.8% of websites achieve good LCP according to Core Web Vitals
- Average mobile LCP: 1.8-1.9 seconds
- Mobile server response is 0.8s slower than desktop

**Source:** [Hostinger - Load Time Statistics](https://www.hostinger.com/tutorials/website-load-time-statistics)

### User Expectations

| Threshold | User Behavior |
|-----------|---------------|
| < 2 seconds | 47% of users expect this |
| > 3 seconds | 53% of mobile users abandon |
| 1s -> 3s load time | 32% bounce rate increase |
| > 3 seconds | 75% of mobile users have left a slow site |

**Source:** [AMRA and ELMA - Mobile Speed Statistics](https://www.amraandelma.com/mobile-site-load-speed-statistics/)

### Business Impact of Performance

**Case Studies:**
- **Vodafone:** 31% LCP improvement = 8% sales increase
- **Rakuten:** Good Core Web Vitals = 53% revenue per visitor increase
- **Swappie:** Core Web Vitals improvements = 42% mobile revenue increase
- **LCP alone:** Good LCP can increase conversions by 61%

**Source:** [DebugBear - 2025 Web Performance](https://www.debugbear.com/blog/2025-in-web-performance)

---

## EUONGELION Technical Performance Targets

### Primary Metrics

| Metric | Target | Measurement Method | Priority |
|--------|--------|-------------------|----------|
| LCP | < 2.5s | Lighthouse, CrUX | Critical |
| INP | < 100ms | Lighthouse, CrUX | Critical |
| CLS | < 0.1 | Lighthouse, CrUX | High |
| TTFB | < 600ms | WebPageTest | High |
| Time to Interactive | < 3.5s | Lighthouse | High |
| First Contentful Paint | < 1.8s | Lighthouse | Medium |
| Total Blocking Time | < 200ms | Lighthouse | Medium |

### PWA-Specific Metrics

| Metric | Target | Notes |
|--------|--------|-------|
| Service Worker install | < 1s | After first visit |
| Cached page load | < 1s | Subsequent visits |
| Offline start | < 2s | From home screen, offline |
| App shell render | < 500ms | Skeleton UI visible |

### Mobile Performance Targets

| Metric | Target | Notes |
|--------|--------|-------|
| 3G load time | < 5s | Critical for emerging markets |
| 4G LTE load time | < 2.5s | Standard mobile |
| 5G load time | < 1.5s | Optimal conditions |
| Bundle size (initial) | < 200KB gzipped | JavaScript |
| Total page weight | < 1MB | Including images |

---

## Engagement Benchmarks

### Session Metrics

**Industry Benchmarks (2025):**

| Metric | Average | Good | Excellent |
|--------|---------|------|-----------|
| Average session length | ~5 minutes | 5-7 minutes | 7+ minutes |
| Sessions per day | 1-2 | 2-3 | 3+ |
| Pages/screens per session | 3-4 | 5-6 | 7+ |

**Devotional App Context:**
- Users typically spend 5-15 minutes in devotional content
- Single session per day is normal (morning devotional)
- Quality of engagement > quantity of time

**Source:** [UXCam - Engagement Benchmarks](https://uxcam.com/blog/mobile-app-engagement-benchmarks/)

### DAU/MAU Stickiness Ratio

The stickiness ratio (DAU/MAU) indicates how often monthly users return daily:

| Ratio | Rating | Interpretation |
|-------|--------|----------------|
| < 10% | Poor | Users install but don't return |
| 10-20% | Average | Normal for most apps |
| 20-25% | Good | Users forming habits |
| 25-40% | Excellent | Strong daily engagement |
| 40%+ | Exceptional | Social/messaging app territory |

**Devotional App Target:** 25-35%

Rationale: Daily devotional apps should aim for daily usage. A user doing morning devotions daily would show up as DAU. Target: 1 in 3 to 1 in 4 monthly users engage daily.

**Source:** [Business of Apps - Engagement Rates](https://www.businessofapps.com/data/app-engagement-rates/)

### EUONGELION Engagement Targets

| Metric | Target | Rationale |
|--------|--------|-----------|
| DAU/MAU ratio | 25%+ | Daily devotional habit |
| Average session length | 5-10 min | Typical devotional duration |
| Sessions per user/month | 15+ | Daily habit forming |
| Devotionals completed/month | 20+ | ~66% completion rate |
| Return visit rate | 70%+ | Next-day return |

---

## Retention Benchmarks

### Industry Retention Rates (2025)

**General Mobile App Retention:**

| Timeframe | Average | Top Performers |
|-----------|---------|----------------|
| Day 1 | 25% | 35-40% |
| Day 7 | 10% | 20-25% |
| Day 30 | 6% | 15-20% |
| Day 90 | 3% | 10-12% |

**Source:** [UXCam - Retention Benchmarks](https://uxcam.com/blog/mobile-app-retention-benchmarks/)

### Lifestyle App Retention (Most Comparable Category)

| Timeframe | Lifestyle Apps | Notes |
|-----------|---------------|-------|
| Day 1 | 16.5-20.9% | Lower than average |
| Day 7 | ~7.6% | Significant drop |
| Day 30 | 3.6-4.5% | Industry struggles |

**Challenge:** Lifestyle apps (including devotional) historically struggle with retention. Social & Lifestyle apps show the lowest retention rates for both weekly and monthly plans.

**Source:** [Growth-onomics - Retention Benchmarks 2025](https://growth-onomics.com/mobile-app-retention-benchmarks-by-industry-2025/)

### Subscription App Retention

For freemium/subscription models (if EUONGELION adds premium tier):

| Retention Type | Benchmark |
|----------------|-----------|
| Monthly plan - Day 30 | 12.8% (hard paywall) |
| Monthly plan - Day 30 | 9.3% (freemium) |
| Annual plan - Year 1 | 18.7-59% (wide variance) |

**Source:** [RevenueCat - State of Subscription Apps 2025](https://www.revenuecat.com/state-of-subscription-apps-2025/)

### Platform Differences

| Metric | iOS | Android | Gap |
|--------|-----|---------|-----|
| Day 1 retention | Higher | Lower | iOS +46% |
| Day 30 retention | Higher | Lower | iOS +40%+ |

**Implication:** iOS users retain better, but Android has larger market. Optimize for both.

**Source:** [AppsFlyer - Retention Benchmarks 2025](https://www.appsflyer.com/resources/reports/app-retention-benchmarks/)

---

## EUONGELION Retention Targets

### Conservative Targets (MVP)

| Timeframe | Target | Notes |
|-----------|--------|-------|
| Day 1 | 30% | Above lifestyle average |
| Day 7 | 15% | 2x industry average |
| Day 30 | 10% | Ambitious for category |
| Day 90 | 5% | Building habit |

### Ambitious Targets (Post-Optimization)

| Timeframe | Target | Notes |
|-----------|--------|-------|
| Day 1 | 40% | Top-performer territory |
| Day 7 | 25% | Strong habit formation |
| Day 30 | 15% | Exceptional for lifestyle |
| Day 90 | 8% | Sustained engagement |

### Retention Drivers for Devotional Apps

**High-Impact Strategies:**

1. **Push Notifications**
   - Users receiving 1+ push in first 90 days = 3x more likely to retain
   - Daily devotional reminders are natural fit

2. **Streak Mechanisms** (use carefully)
   - Can triple retention
   - But EUONGELION philosophy opposes gamification
   - Alternative: Progress tracking without pressure

3. **Onboarding Quality**
   - First session determines long-term retention
   - Immediate value demonstration
   - Low-friction account creation

4. **Content Quality**
   - Devotional apps live or die by content
   - Fresh daily content drives return visits
   - Soul Audit unique value proposition

**Source:** [Sendbird - Retention Benchmarks](https://sendbird.com/blog/app-retention-benchmarks-broken-down-by-industry)

---

## Competitive Performance Analysis

### Competitor App Store Ratings (Proxy for UX Quality)

| App | iOS Rating | Android Rating | Review Count |
|-----|------------|----------------|--------------|
| YouVersion | 4.9 | 4.9 | Millions |
| Hallow | 4.9 | 4.8 | 225K+ |
| Dwell | 4.9 | 4.8 | Thousands |
| Abide | 4.9 | 4.8 | Thousands |
| Lectio 365 | 4.8 | 4.6 | Thousands |
| First 5 | 4.9 | 4.7 | Thousands |

**Observation:** All major devotional apps achieve 4.8+ ratings. The bar is high. Performance issues would quickly damage ratings.

### Performance Inferences

**YouVersion:**
- Handles 500M+ devices
- Heavy caching strategy
- CDN for Bible versions
- Offline-first architecture

**Hallow:**
- Audio streaming optimized
- Large content library (10K+ sessions)
- Background download for offline

---

## Measurement & Monitoring Strategy

### Real User Monitoring (RUM)

**Tools to Consider:**
- Vercel Analytics (built-in with hosting)
- Google Analytics 4 (free, comprehensive)
- Mixpanel (user behavior focus)
- Amplitude (product analytics)

**Key RUM Metrics:**
```javascript
// Example: Track devotional completion
analytics.track('devotional_completed', {
  devotional_id: id,
  series: series_name,
  time_spent: duration_seconds,
  offline: !navigator.onLine
});
```

### Synthetic Monitoring

**Tools:**
- Lighthouse CI (automated in deployment)
- WebPageTest (detailed analysis)
- Chrome UX Report (CrUX) - real-world data

**Lighthouse CI Setup:**
```yaml
# .github/workflows/lighthouse.yml
- name: Lighthouse CI
  run: |
    npm install -g @lhci/cli
    lhci autorun
  env:
    LHCI_GITHUB_APP_TOKEN: ${{ secrets.LHCI_GITHUB_APP_TOKEN }}
```

### Performance Budget

**Recommended Budgets for EUONGELION:**

| Resource Type | Budget | Notes |
|---------------|--------|-------|
| JavaScript (initial) | < 200KB | Gzipped |
| CSS (initial) | < 50KB | Gzipped |
| Images (per page) | < 500KB | Optimized |
| Total page weight | < 1MB | First load |
| Third-party scripts | < 50KB | Minimal external deps |

---

## Optimization Strategies

### LCP Optimization

**Primary LCP Element for EUONGELION:** Devotional text content

**Strategies:**
1. **Server-side rendering** - Next.js SSR/SSG for content
2. **Font optimization** - Preload critical fonts, font-display: swap
3. **Image optimization** - Next/Image with priority for above-fold
4. **Minimal JavaScript** - Defer non-critical scripts

```javascript
// next.config.js - Image optimization
module.exports = {
  images: {
    formats: ['image/avif', 'image/webp'],
    minimumCacheTTL: 60 * 60 * 24 * 365, // 1 year
  },
};
```

### INP Optimization

**Strategies:**
1. **Avoid long tasks** - Break up JavaScript execution
2. **Prioritize user input** - Use requestIdleCallback for non-urgent work
3. **Minimize re-renders** - React.memo, useMemo for expensive components
4. **Debounce/throttle** - For scroll and input handlers

### CLS Optimization

**Strategies:**
1. **Reserve space for images** - Always specify dimensions
2. **Font fallback matching** - Prevent layout shift on font load
3. **Avoid inserting content above existing content** - Dynamic content below fold
4. **Skeleton screens** - Maintain layout during loading

---

## Performance Testing Checklist

### Pre-Launch Testing

- [ ] Lighthouse score > 90 (Performance)
- [ ] LCP < 2.5s on 4G
- [ ] INP < 100ms
- [ ] CLS < 0.1
- [ ] Total Blocking Time < 200ms
- [ ] Largest image optimized
- [ ] JavaScript bundle analyzed (no bloat)
- [ ] Service Worker caching verified
- [ ] Offline functionality tested

### Ongoing Monitoring

- [ ] Weekly Lighthouse CI checks
- [ ] Monthly CrUX data review
- [ ] User session recording analysis
- [ ] Error rate monitoring
- [ ] API response time tracking
- [ ] Database query performance

---

## Summary: EUONGELION Performance Targets

### Technical Performance

| Metric | Target | Priority |
|--------|--------|----------|
| LCP | < 2.5s | Critical |
| INP | < 100ms | Critical |
| CLS | < 0.1 | High |
| Lighthouse Performance | > 90 | High |
| Bundle Size | < 200KB | Medium |
| Offline Load | < 2s | High |

### Engagement Metrics

| Metric | Target | Priority |
|--------|--------|----------|
| DAU/MAU Ratio | 25%+ | High |
| Session Length | 5-10 min | Medium |
| Devotionals/Month | 20+ | High |
| Return Visit (Day 1) | 70%+ | High |

### Retention Metrics

| Timeframe | Target | Priority |
|-----------|--------|----------|
| Day 1 | 30%+ | Critical |
| Day 7 | 15%+ | High |
| Day 30 | 10%+ | High |
| Day 90 | 5%+ | Medium |

---

## Sources

- [web.dev - LCP](https://web.dev/articles/lcp)
- [DebugBear - 2025 Web Performance](https://www.debugbear.com/blog/2025-in-web-performance)
- [Hostinger - Load Time Statistics 2025](https://www.hostinger.com/tutorials/website-load-time-statistics)
- [AMRA and ELMA - Mobile Speed Statistics](https://www.amraandelma.com/mobile-site-load-speed-statistics/)
- [aTeam - Core Web Vitals 2025](https://www.ateamsoftsolutions.com/core-web-vitals-optimization-guide-2025-showing-lcp-inp-cls-metrics-and-performance-improvement-strategies-for-web-applications/)
- [InMotion - Web Performance Standards 2026](https://www.inmotionhosting.com/blog/web-performance-benchmarks/)
- [UXCam - Engagement Benchmarks 2025](https://uxcam.com/blog/mobile-app-engagement-benchmarks/)
- [UXCam - Retention Benchmarks 2025](https://uxcam.com/blog/mobile-app-retention-benchmarks/)
- [Business of Apps - Engagement Rates](https://www.businessofapps.com/data/app-engagement-rates/)
- [Growth-onomics - Retention Benchmarks 2025](https://growth-onomics.com/mobile-app-retention-benchmarks-by-industry-2025/)
- [RevenueCat - State of Subscription Apps 2025](https://www.revenuecat.com/state-of-subscription-apps-2025/)
- [AppsFlyer - Retention Benchmarks 2025](https://www.appsflyer.com/resources/reports/app-retention-benchmarks/)
- [Sendbird - Retention Benchmarks by Industry](https://sendbird.com/blog/app-retention-benchmarks-broken-down-by-industry)
- [Netguru - Engagement Metrics 2025](https://www.netguru.com/blog/mobile-app-user-engagement-metrics)

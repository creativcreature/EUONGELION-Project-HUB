# EUONGELION Device Test Matrix

**Document ID:** 83-device-test-matrix.md
**Created:** 2026-01-19
**Application Type:** Progressive Web App (PWA)
**Minimum OS Versions:** iOS 15+, Android 10+

---

## 1. Executive Summary

This document defines the complete matrix of devices, browsers, and versions to test the EUONGELION application. As a PWA targeting Christian devotional users, mobile Safari and Chrome are highest priority.

### Priority Tiers

| Tier | Description | Test Frequency |
|------|-------------|----------------|
| P1 (Critical) | Primary user devices, must work perfectly | Every release |
| P2 (High) | Secondary devices, should work well | Every major release |
| P3 (Medium) | Edge cases, best effort | Quarterly |
| P4 (Low) | Legacy, graceful degradation | As needed |

---

## 2. Mobile Devices - iOS

### 2.1 iOS Safari (Primary Mobile Browser)

**Priority: P1 (Critical)** - Estimated 45% of user base

| Device | Screen Size | Resolution | iOS Version | Priority |
|--------|-------------|------------|-------------|----------|
| iPhone 15 Pro Max | 6.7" | 430x932 @3x | iOS 17.x | P1 |
| iPhone 15 Pro | 6.1" | 393x852 @3x | iOS 17.x | P1 |
| iPhone 15 | 6.1" | 390x844 @3x | iOS 17.x | P1 |
| iPhone 14 Pro Max | 6.7" | 430x932 @3x | iOS 17.x | P1 |
| iPhone 14 | 6.1" | 390x844 @3x | iOS 17.x | P1 |
| iPhone 13 | 6.1" | 390x844 @3x | iOS 17.x | P2 |
| iPhone 12 | 6.1" | 390x844 @3x | iOS 17.x | P2 |
| iPhone SE (3rd gen) | 4.7" | 375x667 @2x | iOS 17.x | P2 |
| iPhone 11 | 6.1" | 414x896 @2x | iOS 17.x | P2 |
| iPhone XR | 6.1" | 414x896 @2x | iOS 16.x | P3 |

**Safari Versions to Test:**
- Safari 17.x (current)
- Safari 16.x (previous)
- Safari 15.x (minimum supported)

**PWA Considerations for iOS Safari:**
- No push notifications (iOS 16.4+ with limitations)
- Add to Home Screen behavior
- Standalone mode testing
- Safe area insets (notch/Dynamic Island)

---

### 2.2 iOS Chrome

**Priority: P2** - Uses WebKit on iOS

| Device | iOS Version | Chrome Version | Priority |
|--------|-------------|----------------|----------|
| iPhone 15 Pro | iOS 17.x | Latest | P2 |
| iPhone 13 | iOS 17.x | Latest | P2 |
| iPhone SE | iOS 17.x | Latest | P3 |

---

### 2.3 iPad Safari

**Priority: P2** - Tablet reading experience

| Device | Screen Size | Resolution | iPadOS | Priority |
|--------|-------------|------------|--------|----------|
| iPad Pro 12.9" (6th gen) | 12.9" | 1024x1366 @2x | 17.x | P2 |
| iPad Pro 11" (4th gen) | 11" | 834x1194 @2x | 17.x | P2 |
| iPad Air (5th gen) | 10.9" | 820x1180 @2x | 17.x | P2 |
| iPad (10th gen) | 10.9" | 820x1180 @2x | 17.x | P2 |
| iPad mini (6th gen) | 8.3" | 744x1133 @2x | 17.x | P3 |

**iPad-Specific Tests:**
- Split view / multitasking
- Landscape vs portrait
- External keyboard support
- Apple Pencil (if applicable)

---

## 3. Mobile Devices - Android

### 3.1 Android Chrome (Primary Android Browser)

**Priority: P1 (Critical)** - Estimated 40% of user base

| Device | Screen Size | Resolution | Android | Priority |
|--------|-------------|------------|---------|----------|
| Samsung Galaxy S24 Ultra | 6.8" | 412x915 @3.5x | 14 | P1 |
| Samsung Galaxy S24 | 6.2" | 360x780 @3x | 14 | P1 |
| Samsung Galaxy S23 | 6.1" | 360x780 @3x | 14 | P1 |
| Google Pixel 8 Pro | 6.7" | 448x998 @2.75x | 14 | P1 |
| Google Pixel 8 | 6.2" | 412x915 @2.625x | 14 | P1 |
| Google Pixel 7a | 6.1" | 412x915 @2.625x | 14 | P2 |
| Samsung Galaxy A54 | 6.4" | 393x873 @2.625x | 14 | P2 |
| Samsung Galaxy A34 | 6.6" | 393x873 @2.625x | 13 | P2 |
| OnePlus 12 | 6.82" | 412x915 @3.5x | 14 | P2 |
| Xiaomi 14 | 6.36" | 393x873 @2.75x | 14 | P3 |
| Motorola Edge 40 | 6.55" | 393x873 @2.75x | 13 | P3 |

**Chrome Versions to Test:**
- Chrome 121+ (current)
- Chrome 119-120 (recent)
- Chrome 110+ (minimum supported)

**PWA Considerations for Android:**
- Full push notification support
- Install prompts
- Background sync
- Trusted Web Activity (TWA) potential

---

### 3.2 Samsung Internet

**Priority: P2** - Significant market share on Samsung devices

| Device | Android | Browser Version | Priority |
|--------|---------|-----------------|----------|
| Galaxy S24 | 14 | Samsung Internet 24.x | P2 |
| Galaxy S23 | 14 | Samsung Internet 24.x | P2 |
| Galaxy A54 | 14 | Samsung Internet 23.x | P3 |

---

### 3.3 Android Firefox

**Priority: P3** - Niche but technical users

| Device | Android | Firefox Version | Priority |
|--------|---------|-----------------|----------|
| Pixel 8 | 14 | Firefox 122+ | P3 |
| Galaxy S23 | 14 | Firefox 122+ | P3 |

---

### 3.4 Foldable Devices

**Priority: P3** - Growing market segment

| Device | Closed Size | Open Size | Android | Priority |
|--------|-------------|-----------|---------|----------|
| Samsung Galaxy Z Fold 5 | 375x846 | 768x884 | 14 | P3 |
| Samsung Galaxy Z Flip 5 | 375x748 | 412x919 | 14 | P3 |
| Google Pixel Fold | 415x928 | 896x1024 | 14 | P3 |

**Foldable-Specific Tests:**
- Flex mode (partially folded)
- Transition between screens
- Layout continuity

---

## 4. Desktop Browsers

### 4.1 Desktop Chrome

**Priority: P1** - Primary desktop browser

| OS | Chrome Version | Priority |
|----|----------------|----------|
| macOS Sonoma (14.x) | 121+ (current) | P1 |
| macOS Ventura (13.x) | 121+ (current) | P2 |
| Windows 11 | 121+ (current) | P1 |
| Windows 10 | 121+ (current) | P2 |
| Ubuntu 22.04 | 121+ (current) | P3 |

**Screen Resolutions:**
- 1920x1080 (FHD) - P1
- 2560x1440 (QHD) - P2
- 3840x2160 (4K) - P3
- 1366x768 (HD) - P2
- 1280x800 (MacBook) - P2

---

### 4.2 Desktop Firefox

**Priority: P2**

| OS | Firefox Version | Priority |
|----|-----------------|----------|
| macOS Sonoma | 122+ (current) | P2 |
| Windows 11 | 122+ (current) | P2 |
| Windows 10 | 122+ (current) | P2 |
| Ubuntu 22.04 | 122+ (current) | P3 |

---

### 4.3 Desktop Safari

**Priority: P2** - macOS users

| macOS | Safari Version | Priority |
|-------|----------------|----------|
| Sonoma (14.x) | Safari 17.x | P2 |
| Ventura (13.x) | Safari 16.x | P2 |
| Monterey (12.x) | Safari 15.x | P3 |

---

### 4.4 Microsoft Edge

**Priority: P3** - Chromium-based

| OS | Edge Version | Priority |
|----|--------------|----------|
| Windows 11 | Edge 121+ | P3 |
| Windows 10 | Edge 121+ | P3 |
| macOS | Edge 121+ | P4 |

---

## 5. Browser Feature Support Matrix

### 5.1 PWA Features

| Feature | Chrome | Safari (iOS) | Firefox | Samsung |
|---------|--------|--------------|---------|---------|
| Service Workers | Full | Full | Full | Full |
| Add to Home Screen | Full | Full | Partial | Full |
| Push Notifications | Full | Limited* | Full | Full |
| Background Sync | Full | No | Partial | Full |
| Web Share API | Full | Full | Full | Full |
| IndexedDB | Full | Full | Full | Full |
| Cache API | Full | Full | Full | Full |

*iOS push notifications require iOS 16.4+ and user opt-in through Home Screen app

---

### 5.2 CSS Feature Support

| Feature | Chrome 121+ | Safari 17+ | Firefox 122+ |
|---------|-------------|------------|--------------|
| CSS Grid | Full | Full | Full |
| CSS Variables | Full | Full | Full |
| backdrop-filter | Full | Full | Full |
| :has() selector | Full | Full | Full |
| Container Queries | Full | Full | Full |
| @layer | Full | Full | Full |
| View Transitions | Full | Partial | No |

---

### 5.3 JavaScript API Support

| Feature | Chrome | Safari | Firefox | Notes |
|---------|--------|--------|---------|-------|
| ES2022+ | Full | Full | Full | |
| Intl.RelativeTimeFormat | Full | Full | Full | Used in date.ts |
| ResizeObserver | Full | Full | Full | |
| IntersectionObserver | Full | Full | Full | |
| navigator.share | Full | Full | Partial | |
| Clipboard API | Full | Full | Full | |

---

## 6. Test Scenarios by Device Type

### 6.1 Mobile-Specific Tests

| Test | iOS Safari | Android Chrome |
|------|------------|----------------|
| Touch targets (44x44 min) | Required | Required |
| Swipe gestures | Test | Test |
| Pull-to-refresh | Test | Test |
| Keyboard handling | Test | Test |
| Safe area insets | Required | Test |
| Orientation change | Test | Test |
| Pinch zoom (prevent) | Test | Test |
| Bottom nav reachability | Required | Required |

---

### 6.2 Tablet-Specific Tests

| Test | iPad | Android Tablet |
|------|------|----------------|
| Split view | Required | Test |
| Landscape reading | Required | Test |
| Hover states | Test | Test |
| Larger touch targets | Verify | Verify |

---

### 6.3 Desktop-Specific Tests

| Test | Chrome | Firefox | Safari |
|------|--------|---------|--------|
| Keyboard navigation | Required | Required | Required |
| Focus indicators | Required | Required | Required |
| Hover states | Required | Required | Required |
| Window resize | Test | Test | Test |
| Print stylesheet | Test | Test | Test |

---

## 7. Performance Benchmarks by Device

### 7.1 Core Web Vitals Targets

| Metric | Mobile Target | Desktop Target |
|--------|---------------|----------------|
| LCP (Largest Contentful Paint) | < 2.5s | < 2.0s |
| FID (First Input Delay) | < 100ms | < 100ms |
| CLS (Cumulative Layout Shift) | < 0.1 | < 0.1 |
| TTFB (Time to First Byte) | < 800ms | < 600ms |

---

### 7.2 Device-Specific Performance

| Device Category | JS Budget | CSS Budget | Image Budget |
|-----------------|-----------|------------|--------------|
| Low-end mobile | < 150KB | < 50KB | Lazy load |
| Mid-range mobile | < 200KB | < 60KB | Lazy load |
| High-end mobile | < 250KB | < 75KB | Preload hero |
| Desktop | < 300KB | < 100KB | Preload above fold |

---

## 8. Network Conditions

### 8.1 Network Profiles to Test

| Profile | Download | Upload | Latency | Priority |
|---------|----------|--------|---------|----------|
| Fast 4G | 12 Mbps | 5 Mbps | 50ms | P1 |
| Regular 4G | 4 Mbps | 2 Mbps | 100ms | P1 |
| Slow 3G | 750 Kbps | 250 Kbps | 400ms | P2 |
| 2G | 250 Kbps | 50 Kbps | 1000ms | P3 |
| Offline | 0 | 0 | - | P1 |
| Lie-Fi (connected but no data) | 0 | 0 | N/A | P2 |

---

### 8.2 Offline Scenarios

| Scenario | Test |
|----------|------|
| App loads offline (cached) | Required |
| Navigate to cached content | Required |
| Navigate to uncached content | Graceful error |
| Submit form offline | Queue for sync |
| Transition online->offline | Show indicator |
| Transition offline->online | Sync & clear indicator |

---

## 9. Accessibility Testing

### 9.1 Screen Readers

| Screen Reader | OS | Browser | Priority |
|---------------|-----|---------|----------|
| VoiceOver | iOS | Safari | P1 |
| TalkBack | Android | Chrome | P1 |
| VoiceOver | macOS | Safari | P2 |
| NVDA | Windows | Chrome/Firefox | P2 |
| JAWS | Windows | Chrome | P3 |

---

### 9.2 Accessibility Settings

| Setting | iOS | Android | Desktop |
|---------|-----|---------|---------|
| Increased text size | Test | Test | Test |
| Bold text | Test | Test | N/A |
| Reduced motion | Test | Test | Test |
| High contrast | N/A | Test | Test |
| Color inversion | Test | Test | Test |

---

## 10. Test Automation Coverage

### 10.1 Automated Testing Matrix

| Browser | Engine | Playwright | Cypress |
|---------|--------|------------|---------|
| Chrome | Chromium | Native | Native |
| Firefox | Gecko | Native | Native |
| Safari | WebKit | Native | Partial |
| Edge | Chromium | Native | Native |
| Mobile Chrome | Chromium | Emulation | Emulation |
| Mobile Safari | WebKit | Emulation | No |

---

### 10.2 Real Device Testing Services

| Service | Use Case |
|---------|----------|
| BrowserStack | Cross-browser, real devices |
| Sauce Labs | Cross-browser, real devices |
| LambdaTest | Cross-browser |
| AWS Device Farm | Android focus |
| Firebase Test Lab | Android/iOS |

---

## 11. Release Testing Checklist

### 11.1 Pre-Release (Every Release)

- [ ] iPhone 15 Pro - Safari (P1)
- [ ] iPhone SE - Safari (P1)
- [ ] Samsung Galaxy S24 - Chrome (P1)
- [ ] Pixel 8 - Chrome (P1)
- [ ] Chrome Desktop - Windows (P1)
- [ ] Chrome Desktop - macOS (P1)
- [ ] Offline mode test
- [ ] PWA install test

### 11.2 Major Release

All P1 and P2 devices:
- [ ] All iOS Safari devices
- [ ] All Android Chrome devices
- [ ] iPad Safari
- [ ] Desktop Chrome, Firefox, Safari
- [ ] Samsung Internet
- [ ] Screen reader testing
- [ ] Performance benchmarks

### 11.3 Quarterly

- [ ] P3 devices
- [ ] Foldable devices
- [ ] Accessibility audit
- [ ] Legacy browser check

---

## 12. Known Issues by Platform

### 12.1 iOS Safari Quirks

| Issue | Workaround |
|-------|------------|
| 100vh includes address bar | Use CSS env(safe-area-inset-*) |
| No push notifications (< iOS 16.4) | Email/in-app reminders |
| Rubber banding on scroll | Accept or use overflow-behavior |
| PWA lacks splash customization | Use apple-touch-startup-image |
| No background sync | N/A |

### 12.2 Android Chrome Quirks

| Issue | Workaround |
|-------|------------|
| Address bar auto-hide affects layout | Use visual viewport API |
| Samsung Internet PWA differences | Test separately |
| Webview fragmentation | Target Chrome Custom Tabs |

### 12.3 Desktop Safari Quirks

| Issue | Workaround |
|-------|------------|
| IndexedDB storage limits | Monitor and warn user |
| Some CSS features lag | Feature detect + fallback |

---

## 13. Version Support Policy

### 13.1 Browser Version Support

| Browser | Support Policy |
|---------|----------------|
| Chrome | Current - 2 major versions |
| Safari | Current - 2 major versions |
| Firefox | Current - 2 major versions |
| Edge | Current - 2 major versions |
| Samsung Internet | Current - 1 major version |

### 13.2 OS Version Support

| OS | Minimum Version | Notes |
|----|-----------------|-------|
| iOS | 15.0 | Service Worker support |
| Android | 10 (API 29) | Modern WebView |
| macOS | Monterey (12.0) | Safari 15+ |
| Windows | 10 (1903+) | Edge Chromium |

---

## 14. Testing Tools Summary

| Tool | Purpose | Priority |
|------|---------|----------|
| Playwright | E2E automation | P1 |
| BrowserStack/Sauce | Real device testing | P1 |
| Chrome DevTools | Mobile emulation, debugging | P1 |
| Safari Web Inspector | iOS debugging | P1 |
| Lighthouse | Performance audits | P1 |
| axe DevTools | Accessibility | P1 |
| WebPageTest | Performance deep dive | P2 |

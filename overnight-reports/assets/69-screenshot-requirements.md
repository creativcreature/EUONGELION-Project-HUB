# 69 - Screenshot Requirements

**Generated:** 2026-01-19
**Status:** Asset Planning Document

---

## Overview

This document specifies all screenshots needed for app store submissions, marketing materials, and the PWA manifest. Includes device specifications, scene recommendations, and capture guidelines.

---

## 1. PWA Manifest Screenshots

### Currently Defined in manifest.json
```json
{
  "screenshots": [
    {
      "src": "/screenshots/home-light.png",
      "sizes": "1080x1920",
      "type": "image/png",
      "form_factor": "narrow",
      "label": "Home screen showing today's devotional"
    },
    {
      "src": "/screenshots/reader-light.png",
      "sizes": "1080x1920",
      "type": "image/png",
      "form_factor": "narrow",
      "label": "Devotional reader with Scripture passage"
    }
  ]
}
```

### Status
- `/screenshots/home-light.png` - **MISSING**
- `/screenshots/reader-light.png` - **MISSING**

---

## 2. PWA Screenshot Requirements

### Narrow Form Factor (Mobile)
| Screenshot | Dimensions | Purpose | Status |
|------------|------------|---------|--------|
| home-light.png | 1080x1920 | Home screen (light mode) | MISSING |
| home-dark.png | 1080x1920 | Home screen (dark mode) | MISSING |
| reader-light.png | 1080x1920 | Devotional reader (light) | MISSING |
| reader-dark.png | 1080x1920 | Devotional reader (dark) | MISSING |
| series-light.png | 1080x1920 | Series listing (light) | MISSING |
| series-dark.png | 1080x1920 | Series listing (dark) | MISSING |
| soul-audit-light.png | 1080x1920 | Soul Audit page (light) | MISSING |
| soul-audit-dark.png | 1080x1920 | Soul Audit page (dark) | MISSING |

### Wide Form Factor (Tablet/Desktop)
| Screenshot | Dimensions | Purpose | Status |
|------------|------------|---------|--------|
| desktop-home.png | 1920x1080 | Desktop home view | MISSING |
| desktop-reader.png | 1920x1080 | Desktop reader view | MISSING |
| tablet-home.png | 1280x800 | Tablet home view | MISSING |
| tablet-reader.png | 1280x800 | Tablet reader view | MISSING |

### Updated manifest.json Recommendation
```json
{
  "screenshots": [
    {
      "src": "/screenshots/home-light.png",
      "sizes": "1080x1920",
      "type": "image/png",
      "form_factor": "narrow",
      "label": "Home screen showing today's devotional"
    },
    {
      "src": "/screenshots/reader-light.png",
      "sizes": "1080x1920",
      "type": "image/png",
      "form_factor": "narrow",
      "label": "Devotional reader with Scripture passage"
    },
    {
      "src": "/screenshots/series-light.png",
      "sizes": "1080x1920",
      "type": "image/png",
      "form_factor": "narrow",
      "label": "Browse devotional series"
    },
    {
      "src": "/screenshots/desktop-home.png",
      "sizes": "1920x1080",
      "type": "image/png",
      "form_factor": "wide",
      "label": "Desktop view of home screen"
    }
  ]
}
```

---

## 3. App Store Screenshots

### Apple App Store (iOS)

| Device | Dimensions | Required |
|--------|------------|----------|
| iPhone 6.9" (15 Pro Max) | 1320x2868 | Recommended |
| iPhone 6.7" (14 Pro Max) | 1290x2796 | Yes |
| iPhone 6.5" (11 Pro Max) | 1242x2688 | Yes |
| iPhone 5.5" (8 Plus) | 1242x2208 | Optional |
| iPad Pro 12.9" (6th gen) | 2048x2732 | If iPad supported |
| iPad Pro 11" | 1668x2388 | If iPad supported |

**Requirements:**
- Minimum 3, maximum 10 screenshots per device
- PNG or JPEG
- Must not include status bar or device frame
- Can use marketing overlays

### Google Play Store (Android)

| Type | Dimensions | Required |
|------|------------|----------|
| Phone | 1080x1920 to 1080x2400 | Yes |
| 7" Tablet | 1200x1920 | If tablet supported |
| 10" Tablet | 1920x1200 | If tablet supported |
| Chromebook | 1920x1080 | If Chromebook supported |

**Requirements:**
- Minimum 2, maximum 8 screenshots per device
- PNG or JPEG (up to 8MB each)
- Must not include device frame
- 16:9 or taller ratio for phones

---

## 4. Screenshot Scenes

### Scene 1: Home Screen (Today's Devotional)
**Purpose:** Show the primary app experience
**Content:**
- Date display
- "Today's Devotional" heading
- Devotional card with title, series badge, scripture excerpt
- Quick links (Series, Soul Audit)
- Bottom navigation

**Variants:**
- Light mode
- Dark mode
- With sample content

### Scene 2: Devotional Reader
**Purpose:** Show the reading experience
**Content:**
- Devotional title in hero section
- Scripture blockquote with gold border
- Sample devotional content
- Hebrew/Greek word study highlight (if visible)

**Variants:**
- Light mode
- Dark mode
- Scrolled state (showing reflection questions)

### Scene 3: Series Listing
**Purpose:** Show content discovery
**Content:**
- "Devotional Series" heading
- Active series with "In Progress" badge
- Upcoming series list
- Series cards with descriptions

**Variants:**
- Light mode
- Dark mode

### Scene 4: Series Detail
**Purpose:** Show series overview
**Content:**
- Series title and description
- Devotional list for the series
- Progress indicators
- Start/Continue button

### Scene 5: Soul Audit
**Purpose:** Show unique feature
**Content:**
- Soul Audit heading and description
- Category cards (Daily Examen, Weekly Review, etc.)
- Coming soon indicator

### Scene 6: Settings
**Purpose:** Show customization options
**Content:**
- Dark mode toggle
- Text size selector
- Notification settings
- Bible translation preference

### Scene 7: Reflection Questions
**Purpose:** Show interactive features
**Content:**
- "Selah - Pause and Reflect" heading
- Numbered reflection questions
- Input area or journal feature (if available)

### Scene 8: Progress/Stats (Future)
**Purpose:** Show gamification/progress
**Content:**
- Reading streak
- Completed devotionals
- Series progress

---

## 5. Marketing Screenshots

### Hero Marketing Image
| Purpose | Dimensions | Format |
|---------|------------|--------|
| App Store feature | 1920x1080 | PNG |
| Website hero | 1440x900 | PNG/WebP |
| Social media | 1200x630 | PNG |

### Device Mockups
Needed for marketing materials:
- iPhone mockup with app screen
- iPad mockup with app screen
- Android phone mockup
- Laptop/browser mockup

### Lifestyle Mockups
Optional for premium marketing:
- Person reading devotional on phone
- Phone on bedside table (morning devotion)
- Multiple devices showing app

---

## 6. Screenshot Capture Guidelines

### Technical Requirements

**Resolution:**
- Capture at 2x or 3x for retina quality
- Scale down for final delivery
- Maintain aspect ratios

**Format:**
- PNG for app stores (lossless)
- WebP for web use (smaller file size)
- JPEG only if file size is critical

**Quality:**
- No compression artifacts
- Sharp text rendering
- Consistent color profile (sRGB)

### Content Requirements

**DO:**
- Use realistic, meaningful sample content
- Show actual app UI, not mockups of UI
- Demonstrate key features
- Use branded color schemes
- Include dark mode variants

**DON'T:**
- Include real user data
- Show error states
- Include system notifications
- Use placeholder/Lorem ipsum text
- Show incomplete features

### Sample Content to Use

**Devotional Title:**
"Finding Rest in the Deep"

**Series Name:**
"Waters of Creation"

**Scripture:**
"And the Spirit of God moved upon the face of the waters." - Genesis 1:2 (KJV)

**Excerpt:**
"In the beginning, before light pierced the darkness, there was tehom - the deep..."

---

## 7. Capture Process

### Step 1: Prepare Environment
```bash
# Run app locally with sample data
cd /app
npm run dev -- -p 3333

# Ensure sample content is loaded
# Set system to light/dark mode as needed
```

### Step 2: Device Simulation
- Use Chrome DevTools device mode
- Set specific device dimensions
- Enable device frame (optional)
- Set DPR (device pixel ratio) to 2 or 3

### Step 3: Capture Screenshots
**Option A: Browser DevTools**
- Chrome: Cmd+Shift+P > "Capture screenshot"
- Device mode > Capture full size screenshot

**Option B: Dedicated Tools**
- [Screely](https://www.screely.com/) - Browser mockups
- [Shottr](https://shottr.cc/) - macOS screenshot tool
- [CleanShot X](https://cleanshot.com/) - Professional captures

**Option C: Real Devices**
- iOS: Volume Up + Side Button
- Android: Volume Down + Power

### Step 4: Post-Processing
- Crop to exact dimensions
- Add device frames (if marketing use)
- Add text overlays (if marketing use)
- Optimize file size

---

## 8. File Organization

### Directory Structure
```
/app/public/
  /screenshots/
    /pwa/
      home-light.png
      home-dark.png
      reader-light.png
      reader-dark.png
      series-light.png
      series-dark.png
      soul-audit-light.png
      soul-audit-dark.png
      desktop-home.png
      desktop-reader.png
    /appstore/
      /ios/
        iphone-6.7-01.png
        iphone-6.7-02.png
        iphone-6.7-03.png
        ...
      /android/
        phone-01.png
        phone-02.png
        ...
    /marketing/
      hero-1920x1080.png
      feature-1440x900.png
      social-1200x630.png
      mockup-iphone.png
      mockup-android.png
```

### Naming Convention
```
[device]-[scene]-[variant]-[number].[format]

Examples:
- iphone-home-light-01.png
- android-reader-dark-02.png
- desktop-series-light-01.png
```

---

## 9. Screenshot Checklist

### PWA Manifest (Minimum)
- [ ] home-light.png (1080x1920)
- [ ] reader-light.png (1080x1920)

### PWA Manifest (Recommended)
- [ ] home-dark.png (1080x1920)
- [ ] reader-dark.png (1080x1920)
- [ ] series-light.png (1080x1920)
- [ ] desktop-home.png (1920x1080)

### iOS App Store
- [ ] iPhone 6.7" - Home screen
- [ ] iPhone 6.7" - Reader view
- [ ] iPhone 6.7" - Series listing
- [ ] iPhone 6.7" - Soul Audit
- [ ] iPhone 6.7" - Settings
- [ ] iPad 12.9" - Home (if supporting)
- [ ] iPad 12.9" - Reader (if supporting)

### Google Play Store
- [ ] Phone - Home screen
- [ ] Phone - Reader view
- [ ] Phone - Series listing
- [ ] Phone - Soul Audit

### Marketing Materials
- [ ] Hero image (1920x1080)
- [ ] Website feature (1440x900)
- [ ] Social share (1200x630)
- [ ] Device mockup - iPhone
- [ ] Device mockup - Android

---

## 10. Tools & Resources

### Capture Tools
| Tool | Platform | Use Case |
|------|----------|----------|
| Chrome DevTools | Web | Device simulation |
| Xcode Simulator | macOS | iOS screenshots |
| Android Studio | Any | Android screenshots |
| CleanShot X | macOS | High-quality captures |
| Shottr | macOS | Free captures |

### Mockup Tools
| Tool | Use Case |
|------|----------|
| [Mockup World](https://www.mockupworld.co/) | Free device mockups |
| [Placeit](https://placeit.net/) | Premium mockups |
| [Figma](https://figma.com/) | Custom device frames |
| [Screely](https://www.screely.com/) | Browser window mockups |

### Optimization Tools
| Tool | Use Case |
|------|----------|
| [TinyPNG](https://tinypng.com/) | PNG compression |
| [Squoosh](https://squoosh.app/) | Image optimization |
| [ImageOptim](https://imageoptim.com/) | macOS optimization |

---

## 11. Summary

### Total Screenshots Needed

| Category | Count | Priority |
|----------|-------|----------|
| PWA Manifest | 6-8 | HIGH |
| iOS App Store | 5-10 | MEDIUM |
| Google Play | 4-8 | MEDIUM |
| Marketing | 5-10 | LOW |
| **Total** | **20-36** | - |

### Priority Order

1. **CRITICAL (PWA Install):**
   - home-light.png
   - reader-light.png

2. **HIGH (Full PWA):**
   - Dark mode variants
   - Series page
   - Desktop view

3. **MEDIUM (App Stores):**
   - Full iOS screenshot set
   - Full Android screenshot set

4. **LOW (Marketing):**
   - Device mockups
   - Hero images
   - Lifestyle shots

### Current Status

| Item | Required | Exists |
|------|----------|--------|
| PWA Screenshots | 2 minimum | 0 |
| App Store Screenshots | 10+ | 0 |
| Marketing Screenshots | 5+ | 0 |

**All screenshots are currently missing.**


# 67 - Favicon & App Icon Checklist

**Generated:** 2026-01-19
**Status:** Asset Planning Document

---

## Overview

This document lists all favicon and app icon sizes needed for the EUONGELION PWA, compares what's defined vs. what actually exists, and provides a complete checklist for PWA icon compliance.

---

## 1. What's Defined in manifest.json

### PWA Icons (Declared)
```json
{
  "icons": [
    { "src": "/icons/icon-72x72.png", "sizes": "72x72", "purpose": "maskable any" },
    { "src": "/icons/icon-96x96.png", "sizes": "96x96", "purpose": "maskable any" },
    { "src": "/icons/icon-128x128.png", "sizes": "128x128", "purpose": "maskable any" },
    { "src": "/icons/icon-144x144.png", "sizes": "144x144", "purpose": "maskable any" },
    { "src": "/icons/icon-152x152.png", "sizes": "152x152", "purpose": "maskable any" },
    { "src": "/icons/icon-192x192.png", "sizes": "192x192", "purpose": "maskable any" },
    { "src": "/icons/icon-384x384.png", "sizes": "384x384", "purpose": "maskable any" },
    { "src": "/icons/icon-512x512.png", "sizes": "512x512", "purpose": "maskable any" }
  ]
}
```

### Shortcut Icons (Declared)
```json
{
  "shortcuts": [
    { "name": "Today's Devotional", "icons": [{ "src": "/icons/shortcut-today.png", "sizes": "96x96" }] },
    { "name": "Browse Series", "icons": [{ "src": "/icons/shortcut-series.png", "sizes": "96x96" }] },
    { "name": "Soul Audit", "icons": [{ "src": "/icons/shortcut-audit.png", "sizes": "96x96" }] }
  ]
}
```

### Screenshots (Declared)
```json
{
  "screenshots": [
    { "src": "/screenshots/home-light.png", "sizes": "1080x1920" },
    { "src": "/screenshots/reader-light.png", "sizes": "1080x1920" }
  ]
}
```

---

## 2. What's Defined in layout.tsx

### Root Layout (`/app/layout.tsx`)
```typescript
icons: {
  icon: [
    { url: '/favicon.ico', sizes: '32x32' },
    { url: '/icon-192.png', sizes: '192x192', type: 'image/png' },
    { url: '/icon-512.png', sizes: '512x512', type: 'image/png' },
  ],
  shortcut: '/favicon.ico',
  apple: [
    { url: '/apple-touch-icon.png', sizes: '180x180', type: 'image/png' },
  ],
  other: [
    { rel: 'mask-icon', url: '/safari-pinned-tab.svg', color: '#1a1a2e' },
  ],
}
```

### Src Layout (`/app/src/app/layout.tsx`)
```html
<link rel="icon" href="/favicon.ico" sizes="any" />
<link rel="icon" href="/icon.svg" type="image/svg+xml" />
<link rel="apple-touch-icon" href="/apple-touch-icon.png" />
```

---

## 3. What Actually Exists

### Current Public Directory
```
/app/public/
  /icons/           # EMPTY directory
  manifest.json
  sw.js
  workbox-00a24876.js
```

### Missing Files
| File | Status |
|------|--------|
| `/favicon.ico` | **MISSING** |
| `/icon.svg` | **MISSING** |
| `/icon-192.png` | **MISSING** |
| `/icon-512.png` | **MISSING** |
| `/apple-touch-icon.png` | **MISSING** |
| `/safari-pinned-tab.svg` | **MISSING** |
| `/browserconfig.xml` | **MISSING** |
| `/icons/icon-72x72.png` | **MISSING** |
| `/icons/icon-96x96.png` | **MISSING** |
| `/icons/icon-128x128.png` | **MISSING** |
| `/icons/icon-144x144.png` | **MISSING** |
| `/icons/icon-152x152.png` | **MISSING** |
| `/icons/icon-192x192.png` | **MISSING** |
| `/icons/icon-384x384.png` | **MISSING** |
| `/icons/icon-512x512.png` | **MISSING** |
| `/icons/shortcut-today.png` | **MISSING** |
| `/icons/shortcut-series.png` | **MISSING** |
| `/icons/shortcut-audit.png` | **MISSING** |
| `/screenshots/home-light.png` | **MISSING** |
| `/screenshots/reader-light.png` | **MISSING** |

---

## 4. Complete Icon Requirements Checklist

### Favicon Files

| File | Size | Format | Purpose | Status |
|------|------|--------|---------|--------|
| `favicon.ico` | 32x32 (multi-size) | ICO | Browser tab icon | MISSING |
| `favicon-16x16.png` | 16x16 | PNG | Small favicon | MISSING |
| `favicon-32x32.png` | 32x32 | PNG | Standard favicon | MISSING |
| `icon.svg` | Vector | SVG | Modern browsers | MISSING |

### Apple Touch Icons

| File | Size | Format | Purpose | Status |
|------|------|--------|---------|--------|
| `apple-touch-icon.png` | 180x180 | PNG | iOS home screen | MISSING |
| `apple-touch-icon-152x152.png` | 152x152 | PNG | iPad (non-retina) | MISSING |
| `apple-touch-icon-167x167.png` | 167x167 | PNG | iPad Pro | MISSING |
| `apple-touch-icon-180x180.png` | 180x180 | PNG | iPhone (retina) | MISSING |

### Safari Specific

| File | Size | Format | Purpose | Status |
|------|------|--------|---------|--------|
| `safari-pinned-tab.svg` | Vector | SVG | Safari pinned tab | MISSING |

### Android / PWA Icons

| File | Size | Format | Purpose | Status |
|------|------|--------|---------|--------|
| `icon-72x72.png` | 72x72 | PNG | Android legacy | MISSING |
| `icon-96x96.png` | 96x96 | PNG | Android legacy | MISSING |
| `icon-128x128.png` | 128x128 | PNG | Android medium | MISSING |
| `icon-144x144.png` | 144x144 | PNG | Android medium | MISSING |
| `icon-152x152.png` | 152x152 | PNG | iPad / Android | MISSING |
| `icon-192x192.png` | 192x192 | PNG | Android / PWA standard | MISSING |
| `icon-384x384.png` | 384x384 | PNG | Android HD | MISSING |
| `icon-512x512.png` | 512x512 | PNG | PWA splash / Play Store | MISSING |

### Maskable Icons (Safe Zone)

| File | Size | Format | Purpose | Status |
|------|------|--------|---------|--------|
| `maskable-192x192.png` | 192x192 | PNG | Maskable icon (Android) | MISSING |
| `maskable-512x512.png` | 512x512 | PNG | Maskable icon (large) | MISSING |

### Windows / Microsoft

| File | Size | Format | Purpose | Status |
|------|------|--------|---------|--------|
| `mstile-70x70.png` | 70x70 | PNG | Windows small tile | MISSING |
| `mstile-150x150.png` | 150x150 | PNG | Windows medium tile | MISSING |
| `mstile-310x150.png` | 310x150 | PNG | Windows wide tile | MISSING |
| `mstile-310x310.png` | 310x310 | PNG | Windows large tile | MISSING |
| `browserconfig.xml` | - | XML | Windows config | MISSING |

### Shortcut Icons

| File | Size | Format | Purpose | Status |
|------|------|--------|---------|--------|
| `shortcut-today.png` | 96x96 | PNG | Today shortcut | MISSING |
| `shortcut-series.png` | 96x96 | PNG | Series shortcut | MISSING |
| `shortcut-audit.png` | 96x96 | PNG | Soul Audit shortcut | MISSING |

---

## 5. Icon Design Specifications

### App Icon Design

The EUONGELION app icon should:

1. **Primary Element:** Stylized "E" mark (as seen in OG image generation)
2. **Background:** Deep navy/tehom (#1A1612) or gold (#C19A6B)
3. **Foreground:** Gold (#C19A6B) or white
4. **Style:** Clean, minimal, sacred feeling

### Icon Safe Zones

**Maskable Icons:**
- Content must be within the inner 80% (safe zone)
- Background color extends to edges
- Used for adaptive icons on Android

```
+------------------+
|                  |  <- Background extends here
|   +----------+   |
|   |  SAFE    |   |  <- Content only here (80%)
|   |  ZONE    |   |
|   +----------+   |
|                  |
+------------------+
```

### Recommended Icon Variants

| Variant | Background | Foreground | Use Case |
|---------|------------|------------|----------|
| Primary | Tehom (#1A1612) | Gold (#C19A6B) | Default |
| Light | White/Cream | Tehom (#1A1612) | Light mode |
| Monochrome | Transparent | Black | Safari pinned tab |

---

## 6. File Structure

### Recommended Public Directory Structure
```
/app/public/
  /icons/
    icon-72x72.png
    icon-96x96.png
    icon-128x128.png
    icon-144x144.png
    icon-152x152.png
    icon-192x192.png
    icon-384x384.png
    icon-512x512.png
    maskable-192x192.png
    maskable-512x512.png
    shortcut-today.png
    shortcut-series.png
    shortcut-audit.png
  /screenshots/
    home-light.png
    home-dark.png
    reader-light.png
    reader-dark.png
  favicon.ico
  favicon-16x16.png
  favicon-32x32.png
  icon.svg
  apple-touch-icon.png
  apple-touch-icon-152x152.png
  apple-touch-icon-167x167.png
  apple-touch-icon-180x180.png
  safari-pinned-tab.svg
  mstile-70x70.png
  mstile-150x150.png
  mstile-310x150.png
  mstile-310x310.png
  browserconfig.xml
  manifest.json
```

---

## 7. manifest.json Updates Needed

### Separate Maskable Icons
Current manifest uses `purpose: "maskable any"` which is not recommended. Should separate:

```json
{
  "icons": [
    {
      "src": "/icons/icon-192x192.png",
      "sizes": "192x192",
      "type": "image/png",
      "purpose": "any"
    },
    {
      "src": "/icons/maskable-192x192.png",
      "sizes": "192x192",
      "type": "image/png",
      "purpose": "maskable"
    },
    {
      "src": "/icons/icon-512x512.png",
      "sizes": "512x512",
      "type": "image/png",
      "purpose": "any"
    },
    {
      "src": "/icons/maskable-512x512.png",
      "sizes": "512x512",
      "type": "image/png",
      "purpose": "maskable"
    }
  ]
}
```

---

## 8. browserconfig.xml Template

```xml
<?xml version="1.0" encoding="utf-8"?>
<browserconfig>
  <msapplication>
    <tile>
      <square70x70logo src="/mstile-70x70.png"/>
      <square150x150logo src="/mstile-150x150.png"/>
      <wide310x150logo src="/mstile-310x150.png"/>
      <square310x310logo src="/mstile-310x310.png"/>
      <TileColor>#1a1a2e</TileColor>
    </tile>
  </msapplication>
</browserconfig>
```

---

## 9. Generation Tools

### Recommended Tools

1. **RealFaviconGenerator.net**
   - Generate complete favicon set from single image
   - Produces all required sizes and formats
   - Generates browserconfig.xml and manifest.json entries

2. **PWA Asset Generator**
   ```bash
   npx pwa-asset-generator logo.svg ./public/icons
   ```

3. **Sharp (Programmatic)**
   ```javascript
   const sharp = require('sharp');

   const sizes = [72, 96, 128, 144, 152, 192, 384, 512];

   sizes.forEach(size => {
     sharp('logo.svg')
       .resize(size, size)
       .png()
       .toFile(`./public/icons/icon-${size}x${size}.png`);
   });
   ```

4. **Figma/Sketch Export**
   - Design at 512x512 or 1024x1024
   - Export at all required sizes

---

## 10. Implementation Checklist

### Phase 1: Critical (PWA Installation)
- [ ] Create master icon (512x512 or SVG)
- [ ] Generate favicon.ico (32x32, with 16x16 embedded)
- [ ] Generate apple-touch-icon.png (180x180)
- [ ] Generate icon-192x192.png
- [ ] Generate icon-512x512.png
- [ ] Create icon.svg (for modern browsers)
- [ ] Create safari-pinned-tab.svg (monochrome)

### Phase 2: Full PWA Compliance
- [ ] Generate all manifest icon sizes (72-512)
- [ ] Create maskable icon variants
- [ ] Generate Windows tile icons
- [ ] Create browserconfig.xml
- [ ] Update manifest.json with correct paths
- [ ] Test PWA installation on Android
- [ ] Test PWA installation on iOS
- [ ] Test PWA installation on desktop (Chrome, Edge)

### Phase 3: Shortcut Icons
- [ ] Design shortcut-today.png
- [ ] Design shortcut-series.png
- [ ] Design shortcut-audit.png
- [ ] Test shortcuts on Android

### Phase 4: Screenshots
- [ ] Capture home-light.png (1080x1920)
- [ ] Capture home-dark.png (1080x1920)
- [ ] Capture reader-light.png (1080x1920)
- [ ] Capture reader-dark.png (1080x1920)

---

## 11. Summary

| Category | Required | Exists | Missing |
|----------|----------|--------|---------|
| Favicons | 4 | 0 | 4 |
| Apple Icons | 4 | 0 | 4 |
| Safari | 1 | 0 | 1 |
| PWA Icons | 8 | 0 | 8 |
| Maskable | 2 | 0 | 2 |
| Windows | 5 | 0 | 5 |
| Shortcuts | 3 | 0 | 3 |
| Screenshots | 4+ | 0 | 4 |
| **Total** | **31+** | **0** | **31+** |

### Priority

1. **CRITICAL:** favicon.ico, apple-touch-icon.png, icon-192.png, icon-512.png
2. **HIGH:** All manifest icons, maskable variants
3. **MEDIUM:** Windows tiles, safari pinned tab
4. **LOW:** Shortcut icons, screenshots


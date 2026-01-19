# 64 - Image Requirements List

**Generated:** 2026-01-19
**Status:** Asset Planning Document

---

## Overview

This document lists all images needed for the EUONGELION app, including hero images, series covers, devotional images, and backgrounds. The recommended aesthetic follows a "dithered/duotone" style inspired by reference images collected in `/tools/reference-images/`.

---

## 1. Hero Images

### Homepage Hero
| Image | Dimensions | Format | Purpose |
|-------|------------|--------|---------|
| hero-home-light.jpg | 1200x800 | WebP (fallback JPG) | Homepage hero section (light mode) |
| hero-home-dark.jpg | 1200x800 | WebP (fallback JPG) | Homepage hero section (dark mode) |
| hero-mobile-light.jpg | 750x600 | WebP | Mobile-optimized hero (light mode) |
| hero-mobile-dark.jpg | 750x600 | WebP | Mobile-optimized hero (dark mode) |

### Feature Heroes
| Image | Dimensions | Format | Purpose |
|-------|------------|--------|---------|
| hero-series.jpg | 1200x600 | WebP | Series listing page header |
| hero-soul-audit.jpg | 1200x600 | WebP | Soul Audit page header |
| hero-about.jpg | 1200x600 | WebP | About page header |

**Style Guidelines:**
- Use deep earth tones (tehom palette: #1A1612 to #3D3835)
- Apply dithered/halftone gradients for texture
- Consider incorporating subtle cross patterns or ancient manuscript textures
- Maintain sacred minimalism - avoid clutter

---

## 2. Series Cover Images

Each series needs a cover image. Based on current mock data:

### Active/Planned Series
| Series | Dimensions | Variants Needed |
|--------|------------|-----------------|
| Waters of Creation | 800x600, 400x300 | Cover, Thumbnail |
| Bread of Presence | 800x600, 400x300 | Cover, Thumbnail |
| Shepherd Psalms | 800x600, 400x300 | Cover, Thumbnail |
| Too Busy for God | 800x600, 400x300 | Cover, Thumbnail |
| Hearing God in the Noise | 800x600, 400x300 | Cover, Thumbnail |
| Abiding in His Presence | 800x600, 400x300 | Cover, Thumbnail |
| Surrender to God's Will | 800x600, 400x300 | Cover, Thumbnail |
| In the Beginning | 800x600, 400x300 | Cover, Thumbnail |
| What is the Gospel | 800x600, 400x300 | Cover, Thumbnail |
| Why Jesus | 800x600, 400x300 | Cover, Thumbnail |
| What Does It Mean to Believe | 800x600, 400x300 | Cover, Thumbnail |
| What is Carrying a Cross | 800x600, 400x300 | Cover, Thumbnail |
| Once Saved Always Saved | 800x600, 400x300 | Cover, Thumbnail |
| The Nature of Belief | 800x600, 400x300 | Cover, Thumbnail |
| The Work of God | 800x600, 400x300 | Cover, Thumbnail |

### Cover Image Specifications
- **Full Cover:** 800x600px (4:3 ratio) - for series detail pages
- **Thumbnail:** 400x300px - for series cards in listings
- **Format:** WebP primary, JPG fallback
- **File size target:** < 100KB for thumbnails, < 200KB for full covers

**Style Guidelines for Series Covers:**
- Each series should have a distinct but cohesive visual identity
- Use the brand color palette: gold (#C19A6B), burgundy (#6B2C2C), olive (#6B6B4F), shalom-blue (#4A5F6B)
- Apply duotone treatments using tehom (#1A1612) as the dark tone
- Consider imagery: water/waves, bread/wheat, shepherd staff, light beams, ancient scrolls
- Incorporate subtle Hebrew/Greek letterforms as design elements

---

## 3. Devotional Images

### Featured Images (Per Devotional)
| Type | Dimensions | Format | Notes |
|------|------------|--------|-------|
| Featured Image | 800x450 | WebP | 16:9 for consistency |
| OG Share Image | 1200x630 | PNG | For social sharing |
| Thumbnail | 300x200 | WebP | For cards/lists |

### Category-Based Image Templates
Create reusable image templates for devotional categories:

| Category | Suggested Imagery |
|----------|-------------------|
| Creation | Cosmic patterns, void/deep imagery, light emergence |
| Wisdom | Scrolls, ancient texts, oil lamps |
| Prayer | Hands, incense, light beams |
| Psalms | Pastoral scenes, mountains, waters |
| Prophets | Desert landscapes, fire, ancient cities |
| Gospel | Cross, path, light/darkness contrast |
| Epistles | Letters, seals, parchment |

---

## 4. Background Images & Textures

### App Backgrounds
| Image | Dimensions | Format | Purpose |
|-------|------------|--------|---------|
| bg-scroll-texture.png | 1920x1080 (tileable) | PNG | Parchment/scroll texture |
| bg-dark-gradient.jpg | 1920x1080 | WebP | Dark mode gradient background |
| bg-light-gradient.jpg | 1920x1080 | WebP | Light mode gradient background |
| noise-overlay.png | 200x200 (tileable) | PNG | Subtle noise texture overlay |

### Decorative Patterns
| Image | Dimensions | Format | Purpose |
|-------|------------|--------|---------|
| pattern-cross.svg | Vector | SVG | Subtle cross pattern (used in OG images) |
| pattern-manuscript.png | 400x400 (tileable) | PNG | Ancient manuscript background |
| divider-gold.svg | Vector | SVG | Decorative section divider |
| border-ornate.svg | Vector | SVG | Decorative border element |

---

## 5. UI Images

### Placeholder & Loading States
| Image | Dimensions | Format | Purpose |
|-------|------------|--------|---------|
| placeholder-series.svg | 400x300 | SVG | Placeholder for loading series |
| placeholder-devotional.svg | 800x450 | SVG | Placeholder for loading devotionals |
| placeholder-avatar.svg | 100x100 | SVG | Default user avatar |
| skeleton-card.svg | 300x200 | SVG | Skeleton loading state |

### Empty States
| Image | Dimensions | Format | Purpose |
|-------|------------|--------|---------|
| empty-bookmarks.svg | 200x200 | SVG | No bookmarks saved |
| empty-history.svg | 200x200 | SVG | No reading history |
| empty-search.svg | 200x200 | SVG | No search results |

### Error States
| Image | Dimensions | Format | Purpose |
|-------|------------|--------|---------|
| error-offline.svg | 200x200 | SVG | Offline mode indicator |
| error-404.svg | 300x300 | SVG | Page not found |
| error-generic.svg | 200x200 | SVG | Generic error state |

---

## 6. Brand Logo Variants

| Image | Dimensions | Format | Purpose |
|-------|------------|--------|---------|
| logo-full.svg | Vector | SVG | Full logo with wordmark |
| logo-icon.svg | Vector | SVG | Icon only (E mark) |
| logo-wordmark.svg | Vector | SVG | Text only |
| logo-full-white.svg | Vector | SVG | White version for dark backgrounds |
| logo-full-gold.svg | Vector | SVG | Gold version for special use |

---

## Style Guide Summary

### Dithered/Duotone Aesthetic

Based on reference images collected, the EUONGELION visual style should incorporate:

1. **Dithering Techniques:**
   - Halftone patterns for gradients
   - Stippled textures for depth
   - Risograph-inspired color separation

2. **Color Treatment:**
   - Primary duotone: Tehom (#1A1612) + Gold (#C19A6B)
   - Secondary duotone: Tehom (#1A1612) + Scroll (#F7F3ED)
   - Accent duotones: Burgundy, Olive, Shalom-blue variants

3. **Texture Application:**
   - Paper/parchment grain
   - Subtle noise overlays
   - Worn edge effects

4. **Imagery References (from /tools/reference-images/):**
   - iso50.jpg - Gradient and color blocking
   - makoto-fujimura.jpg - Textured, contemplative aesthetic
   - dkng.jpg - Clean iconographic style
   - true-grit.jpg - Texture and grain techniques
   - aesthetic-apparatus.jpg - Bold duotone treatments

### Recommended Tools
- Photoshop/Affinity Photo for duotone treatments
- Illustrator/Affinity Designer for vector work
- Procreate for texture creation
- TinyPNG/Squoosh for optimization

### File Naming Convention
```
[type]-[name]-[variant].[format]
Examples:
- series-waters-of-creation-cover.webp
- series-waters-of-creation-thumb.webp
- hero-home-light.webp
- bg-scroll-texture.png
```

---

## Priority List

### Phase 1 (MVP - Critical)
1. Logo variants (all)
2. Series covers for existing content (15 series)
3. Homepage hero images
4. Placeholder images (3)
5. Error state images (3)

### Phase 2 (Enhancement)
1. Background textures
2. Decorative patterns
3. Empty state illustrations
4. Additional hero images

### Phase 3 (Scale)
1. Per-devotional featured images
2. Category-based image templates
3. Marketing/promotional images

---

## Current Status

### Existing Assets
- **Icons:** `/app/public/icons/` - EMPTY (placeholder directory exists)
- **Images:** None in public folder
- **Reference Images:** 24 reference images in `/tools/reference-images/`

### Missing (Critical)
- All hero images
- All series covers
- Logo files
- Placeholder images
- Background textures

---

## Next Steps

1. Create logo in multiple variants
2. Design series cover template system
3. Generate hero images for main pages
4. Create placeholder/skeleton images
5. Develop background textures
6. Optimize all images for web delivery


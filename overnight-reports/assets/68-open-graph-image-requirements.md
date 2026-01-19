# 68 - Open Graph Image Requirements

**Generated:** 2026-01-19
**Status:** Asset Planning Document

---

## Overview

This document specifies all Open Graph (OG) images needed for social sharing across Twitter, Facebook, LinkedIn, and other platforms. Includes size requirements, style recommendations, and implementation details.

---

## 1. Current Implementation

### Dynamic OG Image Generation

The app uses Next.js dynamic OG image generation:

**`/app/opengraph-image.tsx`**
- Size: 1200x630 (Facebook/LinkedIn standard)
- Generated dynamically using `@vercel/og`
- Features: Brand logo, title, tagline, decorative elements
- Uses BRAND_COLORS from layout

**`/app/twitter-image.tsx`**
- Size: 1200x600 (Twitter summary_large_image)
- Generated dynamically using `@vercel/og`
- Features: Two-column layout, logo, title, tags
- Uses BRAND_COLORS from layout

### Metadata Configuration (`/app/layout.tsx`)
```typescript
openGraph: {
  images: [
    { url: '/og-image.png', width: 1200, height: 630, alt: '...' },
    { url: '/og-image-square.png', width: 600, height: 600, alt: '...' }
  ]
},
twitter: {
  card: 'summary_large_image',
  images: ['/twitter-image.png']
}
```

---

## 2. Platform Requirements

### Facebook
| Type | Dimensions | Ratio | Notes |
|------|------------|-------|-------|
| Standard | 1200x630 | 1.91:1 | Recommended minimum |
| High-res | 1200x1200 | 1:1 | Square for feed |
| Minimum | 600x315 | 1.91:1 | Absolute minimum |

### Twitter
| Card Type | Dimensions | Ratio | Notes |
|-----------|------------|-------|-------|
| summary_large_image | 1200x628 | 1.91:1 | Large preview |
| summary | 120x120 to 1200x1200 | 1:1 | Square thumbnail |
| Minimum | 300x157 | 1.91:1 | Small preview |

### LinkedIn
| Type | Dimensions | Ratio | Notes |
|------|------------|-------|-------|
| Standard | 1200x627 | 1.91:1 | Recommended |
| High-res | 1200x1200 | 1:1 | Square option |
| Minimum | 200x200 | 1:1 | Absolute minimum |

### WhatsApp/iMessage
| Type | Dimensions | Ratio | Notes |
|------|------------|-------|-------|
| Preview | 1200x630 | 1.91:1 | Uses OG image |
| Square | 300x300 | 1:1 | Fallback |

### Pinterest
| Type | Dimensions | Ratio | Notes |
|------|------------|-------|-------|
| Pin | 1000x1500 | 2:3 | Vertical preferred |
| Square | 1000x1000 | 1:1 | Alternative |

### Discord
| Type | Dimensions | Ratio | Notes |
|------|------------|-------|-------|
| Embed | 1200x630 | 1.91:1 | Uses OG image |

---

## 3. Required OG Images

### Static Default Images

| File | Dimensions | Format | Purpose |
|------|------------|--------|---------|
| `og-image.png` | 1200x630 | PNG | Default Facebook/LinkedIn |
| `og-image-square.png` | 600x600 | PNG | Square variant |
| `twitter-image.png` | 1200x628 | PNG | Twitter large image |
| `twitter-image-square.png` | 600x600 | PNG | Twitter summary |

### Page-Specific OG Images

| Page | File | Dimensions | Dynamic? |
|------|------|------------|----------|
| Homepage | `og-home.png` | 1200x630 | Yes (current) |
| Series List | `og-series.png` | 1200x630 | Static |
| Soul Audit | `og-soul-audit.png` | 1200x630 | Static |
| About | `og-about.png` | 1200x630 | Static |
| Settings | - | - | No (private) |

### Content-Specific OG Images

| Content Type | Approach | Notes |
|--------------|----------|-------|
| Individual Series | Dynamic or template | Include series cover art |
| Individual Devotional | Dynamic | Include title, scripture, series |
| Search Results | Static default | Use site OG image |
| 404/Error | Static default | Use site OG image |

---

## 4. OG Image Design Guidelines

### Brand Elements

**Required:**
- EUONGELION wordmark or logo
- Consistent color palette
- Brand typeface (Playfair Display for headings)

**Optional:**
- Tagline: "Soul Formation Through Scripture"
- Decorative cross pattern overlay
- Gold accent lines

### Color Palette

| Color | Hex | Usage |
|-------|-----|-------|
| Primary Deep | #1a1a2e | Background |
| Gold | #c9a227 | Accents, logo |
| White | #ffffff | Text |
| Cream | #f5f3ed | Light backgrounds |
| Burgundy | #722f37 | Accent |

### Typography

| Element | Font | Weight | Size (at 1200x630) |
|---------|------|--------|-------------------|
| Title | Playfair Display | Bold | 72px |
| Tagline | Georgia | Italic | 28px |
| Meta text | Inter | Regular | 18px |

### Layout Templates

**Template A: Centered (Default)**
```
+------------------------------------------+
|        [Gold accent bar 8px]             |
|                                          |
|              [Logo: E mark]              |
|                                          |
|             EUONGELION                   |
|    Soul Formation Through Scripture      |
|                                          |
|         [Decorative divider]             |
|                                          |
| Devotionals | Word Studies | Soul Formation |
|                                          |
|        [Gold accent bar 8px]             |
+------------------------------------------+
```

**Template B: Side-by-side (Content)**
```
+------------------------------------------+
|        [Gold accent bar 6px]             |
|                                          |
| [Content Area]          |    [Logo]      |
| Title                   |     [E]        |
| Description             |                |
| Scripture ref           |                |
|                         |                |
| [Tags]                  |                |
|                                          |
|        [Gold accent bar 6px]             |
+------------------------------------------+
```

**Template C: Series Cover**
```
+------------------------------------------+
|        [Gold accent bar 6px]             |
|                                          |
| [Series Art]  |  Series Title            |
| (400x400)     |  Description             |
|               |  X devotionals           |
|               |                          |
|               |  [EUONGELION logo]       |
|                                          |
|        [Gold accent bar 6px]             |
+------------------------------------------+
```

---

## 5. Dynamic OG Image Improvements

### Current Issues

1. **Font Loading:** Custom fonts commented out, using Georgia fallback
2. **Performance:** Edge function generates on each request
3. **Consistency:** No caching strategy documented

### Recommendations

**1. Add Custom Font Loading**
```typescript
// Load brand font for OG images
const playfairFont = await fetch(
  new URL('./fonts/PlayfairDisplay-Bold.ttf', import.meta.url)
).then((res) => res.arrayBuffer());

return new ImageResponse(
  // ... JSX
  { fonts: [{ name: 'Playfair Display', data: playfairFont, weight: 700 }] }
);
```

**2. Add Caching Headers**
```typescript
export const runtime = 'edge';
export const revalidate = 3600; // Cache for 1 hour
```

**3. Create Page-Specific OG Routes**
```
/app/series/[slug]/opengraph-image.tsx
/app/devotional/[id]/opengraph-image.tsx
```

---

## 6. Series OG Images

Each series should have a distinct OG image:

### Series-Specific OG Image Content
| Element | Source |
|---------|--------|
| Background | Series cover image (blurred/overlaid) |
| Title | Series title |
| Subtitle | Series theme or tagline |
| Meta | "X devotionals | Y weeks" |
| Branding | EUONGELION logo |

### Example: "Waters of Creation" Series
```
+------------------------------------------+
|        [Gold accent bar]                 |
|                                          |
|  [Blurred water imagery background]      |
|                                          |
|         WATERS OF CREATION               |
|     Exploring the deep symbolism of      |
|     water throughout Scripture           |
|                                          |
|     7 devotionals | 1 week               |
|                                          |
|         [EUONGELION]                     |
+------------------------------------------+
```

---

## 7. Devotional OG Images

Individual devotionals should have unique OG images:

### Devotional OG Image Content
| Element | Source |
|---------|--------|
| Series badge | Series name |
| Title | Devotional title |
| Scripture | Primary verse reference |
| Day info | "Day X of Series" |
| Branding | EUONGELION logo |

### Dynamic Generation Route
```typescript
// /app/devotional/[id]/opengraph-image.tsx
export default async function DevotionalOGImage({ params }) {
  const devotional = await getDevotional(params.id);

  return new ImageResponse(
    <div style={{ /* styles */ }}>
      <span>{devotional.series} - Day {devotional.dayNumber}</span>
      <h1>{devotional.title}</h1>
      <p>{devotional.scripture.reference}</p>
      <span>EUONGELION</span>
    </div>,
    { width: 1200, height: 630 }
  );
}
```

---

## 8. File Checklist

### Static OG Images Needed

| File | Size | Status |
|------|------|--------|
| `/public/og-image.png` | 1200x630 | MISSING |
| `/public/og-image-square.png` | 600x600 | MISSING |
| `/public/twitter-image.png` | 1200x628 | MISSING |
| `/public/twitter-image-square.png` | 600x600 | MISSING |
| `/public/og-series.png` | 1200x630 | MISSING |
| `/public/og-soul-audit.png` | 1200x630 | MISSING |
| `/public/og-about.png` | 1200x630 | MISSING |

### Dynamic OG Routes

| Route | Status | Notes |
|-------|--------|-------|
| `/app/opengraph-image.tsx` | EXISTS | Homepage OG |
| `/app/twitter-image.tsx` | EXISTS | Homepage Twitter |
| `/app/series/[slug]/opengraph-image.tsx` | MISSING | Series-specific |
| `/app/devotional/[id]/opengraph-image.tsx` | MISSING | Devotional-specific |

---

## 9. Testing & Validation

### Testing Tools

1. **Facebook Sharing Debugger**
   - https://developers.facebook.com/tools/debug/
   - Clear cache and re-scrape

2. **Twitter Card Validator**
   - https://cards-dev.twitter.com/validator
   - Test card appearance

3. **LinkedIn Post Inspector**
   - https://www.linkedin.com/post-inspector/
   - Verify link previews

4. **OpenGraph.xyz**
   - https://www.opengraph.xyz/
   - General OG preview

### Testing Checklist

- [ ] Homepage OG image displays correctly on Facebook
- [ ] Homepage OG image displays correctly on Twitter
- [ ] Homepage OG image displays correctly on LinkedIn
- [ ] Series pages have unique OG images
- [ ] Devotional pages have unique OG images
- [ ] Images load within 2 seconds
- [ ] Text is readable at small preview sizes
- [ ] Brand is recognizable even at thumbnail size

---

## 10. Implementation Priority

### Phase 1: Core OG Images
1. Create static `/public/og-image.png` as fallback
2. Create static `/public/twitter-image.png` as fallback
3. Verify dynamic generation is working
4. Add custom font to dynamic OG images

### Phase 2: Content-Specific
1. Create series OG image route
2. Create devotional OG image route
3. Add series cover art integration
4. Test across all platforms

### Phase 3: Optimization
1. Add caching strategy
2. Create Pinterest-optimized variants
3. A/B test different designs
4. Monitor social sharing analytics

---

## 11. Summary

| Requirement | Current | Needed |
|-------------|---------|--------|
| Static OG images | 0 | 7 |
| Dynamic OG routes | 2 | 4 |
| Platform coverage | Partial | Full |
| Custom fonts | No | Yes |
| Caching | No | Yes |

### Key Actions

1. **IMMEDIATE:** Create static fallback OG images
2. **HIGH:** Add custom font loading to dynamic OG
3. **MEDIUM:** Create series/devotional specific OG routes
4. **LOW:** Pinterest optimization, A/B testing


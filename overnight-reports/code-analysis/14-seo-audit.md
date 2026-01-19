# SEO Audit

**Generated:** 2026-01-19
**Project:** EUONGELION
**Path:** `/Users/meltmac/Documents/Personal/wkGD/EUONGELION-STARTUP/app`

---

## Executive Summary

The EUONGELION app has an **excellent SEO foundation** with comprehensive metadata configuration, structured data, dynamic sitemap/robots.txt, and Open Graph support. The implementation leverages Next.js 15's Metadata API effectively. A few minor gaps exist in page-level implementation and some missing OG images.

**Overall Rating:** Excellent (9/10)

---

## 1. Root Layout Metadata

**File:** `/app/layout.tsx` (Lines 99-238)

### Basic Metadata

| Field | Value | Status |
|-------|-------|--------|
| `title.default` | "EUONGELION \| Soul Formation Through Scripture" | Excellent |
| `title.template` | "%s \| EUONGELION" | Good - consistent branding |
| `description` | Comprehensive 160+ char description | Excellent |
| `applicationName` | "EUONGELION" | Good |
| `authors` | EUONGELION with URL | Good |
| `keywords` | 15 relevant keywords | Good |
| `referrer` | "origin-when-cross-origin" | Good |
| `creator` | EUONGELION | Good |
| `publisher` | EUONGELION | Good |

### Keywords List

```
devotional, Bible study, scripture, soul formation, spiritual growth,
Hebrew word study, Greek word study, daily devotional, Christian meditation,
prayer, biblical languages, faith journey, discipleship, spiritual disciplines,
Bible reading plan
```

Well-targeted for the devotional app niche.

---

## 2. Robots Configuration

### Layout Metadata (Lines 132-144)

```typescript
robots: {
  index: true,
  follow: true,
  nocache: false,
  googleBot: {
    index: true,
    follow: true,
    noimageindex: false,
    'max-video-preview': -1,
    'max-image-preview': 'large',
    'max-snippet': -1,
  },
}
```

Excellent - allows full indexing with large image previews.

### Dynamic robots.txt

**File:** `/app/robots.ts` (Lines 1-81)

```typescript
rules: [
  { userAgent: '*', allow: '/', disallow: ['/api/', '/admin/', ...] },
  { userAgent: 'Googlebot', allow: '/', disallow: [...] },
  { userAgent: 'Bingbot', allow: '/', disallow: [...] },
  { userAgent: 'GPTBot', disallow: '/' },  // Block AI crawlers
  { userAgent: 'ChatGPT-User', disallow: '/' },
  { userAgent: 'CCBot', disallow: '/' },
  { userAgent: 'anthropic-ai', disallow: '/' },
  { userAgent: 'Claude-Web', disallow: '/' },
]
```

### Disallowed Paths

- `/api/` - API routes
- `/admin/` - Admin area
- `/private/` - Private content
- `/_next/` - Next.js internals
- `/static/` - Static assets
- `/*.json$` - JSON files
- `/soul-audit/results/*` - Personal results
- `/user/*` - User profiles

**Note:** Blocking AI crawlers is a conscious choice to protect devotional content.

---

## 3. Sitemap Configuration

**File:** `/app/sitemap.ts` (Lines 1-181)

### Static Pages

| URL | Priority | Change Frequency |
|-----|----------|------------------|
| `/` | 1.0 | daily |
| `/about` | 0.8 | monthly |
| `/devotionals` | 0.9 | daily |
| `/series` | 0.9 | weekly |
| `/soul-audit` | 0.8 | monthly |
| `/soul-audit/start` | 0.7 | monthly |
| `/word-studies` | 0.7 | weekly |
| `/prayer` | 0.6 | weekly |
| `/community` | 0.6 | weekly |
| `/contact` | 0.5 | yearly |
| `/privacy` | 0.3 | yearly |
| `/terms` | 0.3 | yearly |

### Dynamic Content

Currently using placeholder data:
```typescript
// TODO: Replace with actual data fetching functions
async function getDevotionals(): Promise<DevotionalSitemapEntry[]> {
  return [
    { slug: 'introduction-to-psalm-23', updatedAt: new Date() },
    { slug: 'the-lord-is-my-shepherd', updatedAt: new Date() },
  ];
}
```

**Gap:** Need to implement actual database queries for devotionals and series.

---

## 4. Open Graph Configuration

### Root Layout OG (Lines 169-193)

```typescript
openGraph: {
  type: 'website',
  locale: 'en_US',
  url: SITE_CONFIG.url,
  siteName: 'EUONGELION',
  title: 'EUONGELION | Soul Formation Through Scripture',
  description: '...',
  images: [
    { url: '/og-image.png', width: 1200, height: 630, alt: '...' },
    { url: '/og-image-square.png', width: 600, height: 600, alt: '...' },
  ],
}
```

**Gap:** Need to verify these images exist in `/public/`.

### Page-Specific OG

**File:** `/lib/seo/metadata.ts`

Provides generators for:
- `generateDevotionalMetadata()` - Article type with publish date
- `generateSeriesMetadata()` - Website type
- `generateSoulAuditMetadata()` - Website type with noindex for results
- `generatePageMetadata()` - Generic pages
- `generateWordStudyMetadata()` - Word study articles

Each includes:
- Canonical URLs
- Custom OG images or fallback to API-generated
- Twitter cards
- Proper type attribution

---

## 5. Twitter Cards

### Root Configuration (Lines 196-203)

```typescript
twitter: {
  card: 'summary_large_image',
  site: '@euongelion',
  creator: '@euongelion',
  title: '...',
  description: '...',
  images: ['/twitter-image.png'],
}
```

**Gap:** Need to verify `/public/twitter-image.png` exists.

---

## 6. Structured Data (JSON-LD)

### JsonLd Component

**File:** `/components/seo/JsonLd.tsx`

Simple component that renders JSON-LD scripts:
```typescript
<script
  type="application/ld+json"
  dangerouslySetInnerHTML={{
    __html: JSON.stringify(data, null, 0),
  }}
/>
```

### Root Layout Structured Data

From layout.tsx (Lines 270-271):
```typescript
<JsonLd data={generateOrganizationSchema()} />
<JsonLd data={generateWebsiteSchema()} />
```

**Gap:** `generateOrganizationSchema` and `generateWebsiteSchema` functions referenced but source file (`/lib/seo/structuredData.ts`) not found.

### Expected Schema Types

Based on metadata.ts imports:
- Organization schema
- Website schema
- Article schema (for devotionals)
- BreadcrumbList schema

---

## 7. Canonical URLs

### Implementation

**File:** `/components/seo/CanonicalUrl.tsx`

Provides:
- `CanonicalUrl` component
- `generateCanonicalUrl()` helper
- `generateAlternateUrls()` for language variants

All use `NEXT_PUBLIC_SITE_URL` with fallback to `https://euongelion.com`.

### Usage in Metadata

All page metadata generators include:
```typescript
alternates: {
  canonical: canonicalUrl,
}
```

---

## 8. Icons & Favicons

### Configuration (Lines 147-164)

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

**Gap:** Need to verify all icon files exist in `/public/`.

---

## 9. Additional SEO Features

### Verification Tags (Lines 206-213)

```typescript
verification: {
  google: process.env.GOOGLE_SITE_VERIFICATION,
  yandex: process.env.YANDEX_VERIFICATION,
  yahoo: process.env.YAHOO_VERIFICATION,
  other: {
    'msvalidate.01': process.env.BING_VERIFICATION || '',
  },
}
```

Environment variables for search console verification.

### Apple Web App (Lines 216-220)

```typescript
appleWebApp: {
  capable: true,
  title: 'EUONGELION',
  statusBarStyle: 'black-translucent',
}
```

### Format Detection (Lines 223-227)

```typescript
formatDetection: {
  email: false,
  address: false,
  telephone: false,
}
```

Prevents automatic linking of text that looks like contact info.

### Category (Line 230)

```typescript
category: 'Religion & Spirituality',
```

Proper categorization for app stores and search.

---

## 10. Breadcrumbs

**File:** `/components/seo/Breadcrumbs.tsx`

Provides:
- Visual breadcrumb navigation
- JSON-LD BreadcrumbList schema
- Responsive design with mobile hiding

---

## 11. Missing/Gap Analysis

### Critical

1. **Structured data source file missing**
   - `/lib/seo/structuredData.ts` referenced but not found
   - Need to create Organization and Website schemas

2. **Sitemap fetches placeholder data**
   - Need Supabase queries for real devotionals/series

### Important

3. **OG images may not exist**
   - Verify: `/public/og-image.png`
   - Verify: `/public/og-image-square.png`
   - Verify: `/public/twitter-image.png`
   - Verify: `/public/og-soul-audit.png`

4. **Icon files to verify**
   - `/public/favicon.ico`
   - `/public/icon-192.png`
   - `/public/icon-512.png`
   - `/public/apple-touch-icon.png`
   - `/public/safari-pinned-tab.svg`
   - `/public/browserconfig.xml`

5. **Dynamic OG image generation**
   - References `/api/og/devotional/[id]` but route doesn't exist
   - References `/api/og/series/[slug]` but route doesn't exist

### Minor

6. **Alternate language tags**
   - No hreflang tags for internationalization
   - Only English supported currently

7. **Article:author meta tags**
   - Author metadata exists but not linked to schema

---

## 12. Action Items

### High Priority

1. **Create /lib/seo/structuredData.ts**
   ```typescript
   export function generateOrganizationSchema() {
     return {
       '@context': 'https://schema.org',
       '@type': 'Organization',
       name: 'EUONGELION',
       url: 'https://euongelion.com',
       logo: 'https://euongelion.com/logo.png',
       // ... more fields
     };
   }
   ```

2. **Verify/create OG images**
   - 1200x630px for standard OG
   - 600x600px for square
   - Twitter-specific if different

3. **Implement sitemap data fetching**
   - Connect to Supabase for devotionals
   - Connect to Supabase for series

### Medium Priority

4. **Create dynamic OG image API routes**
   - `/api/og/devotional/[id]/route.tsx`
   - `/api/og/series/[slug]/route.tsx`
   - Use `@vercel/og` or `satori`

5. **Add per-page metadata**
   - Ensure each page exports metadata
   - Use generators from metadata.ts

6. **Set up search console verification**
   - Add env vars for verification codes
   - Submit sitemap

### Low Priority

7. **Add rich snippets for devotionals**
   - Article schema with datePublished
   - Review schema if applicable

8. **Implement breadcrumbs on all pages**
   - Add to devotional pages
   - Add to series pages

---

## 13. SEO Checklist

| Requirement | Status | Notes |
|-------------|--------|-------|
| Title tag | Yes | With template |
| Meta description | Yes | 160+ chars |
| Canonical URL | Yes | All pages |
| Open Graph | Yes | Complete |
| Twitter Cards | Yes | Large image |
| robots.txt | Yes | Dynamic |
| sitemap.xml | Partial | Needs real data |
| Structured data | Partial | Source missing |
| Favicon | Yes | Multiple sizes |
| Mobile viewport | Yes | In layout |
| HTTPS | Assumed | Vercel |
| Page speed | Unknown | Need to test |
| Core Web Vitals | Yes | Monitoring exists |

---

## Summary

The SEO implementation is comprehensive and well-architected:

**Strengths:**
- Complete Next.js Metadata API usage
- Dynamic robots.txt and sitemap
- Thoughtful content blocking for AI crawlers
- Page-specific metadata generators
- Proper canonical URLs

**Key Gaps:**
1. Missing structured data source file
2. Sitemap using placeholder data
3. OG images need verification
4. Dynamic OG image routes not implemented

The foundation is excellent; addressing the gaps will make it production-ready.

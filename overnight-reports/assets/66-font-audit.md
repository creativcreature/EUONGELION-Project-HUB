# 66 - Font Audit

**Generated:** 2026-01-19
**Status:** Asset Planning Document

---

## Overview

This document audits all fonts loaded in the EUONGELION app, identifies what's actually used, and provides optimization opportunities including subsetting and reducing font weights.

---

## 1. Fonts Declared in Code

### Primary Layout (`/app/layout.tsx`)
```typescript
import { Inter, Playfair_Display, Source_Serif_4 } from 'next/font/google';

const inter = Inter({
  subsets: ['latin'],
  display: 'swap',
  variable: '--font-inter',
});

const playfair = Playfair_Display({
  subsets: ['latin'],
  display: 'swap',
  variable: '--font-playfair',
});

const sourceSerif = Source_Serif_4({
  subsets: ['latin'],
  display: 'swap',
  variable: '--font-source-serif',
});
```

### Secondary Layout (`/app/src/app/layout.tsx`)
```typescript
import { Inter, Crimson_Pro } from 'next/font/google';

const inter = Inter({
  subsets: ['latin'],
  variable: '--font-inter',
  display: 'swap',
});

const crimsonPro = Crimson_Pro({
  subsets: ['latin'],
  variable: '--font-crimson',
  display: 'swap',
});
```

---

## 2. Font Usage Analysis

### CSS Variables Defined

| Variable | Font | Defined In |
|----------|------|------------|
| `--font-inter` | Inter | Both layouts |
| `--font-playfair` | Playfair Display | /app/layout.tsx |
| `--font-source-serif` | Source Serif 4 | /app/layout.tsx |
| `--font-crimson` | Crimson Pro | /app/src/app/layout.tsx |

### Tailwind Config (`/app/tailwind.config.ts`)
```typescript
fontFamily: {
  sans: ['var(--font-inter)', 'Inter', 'system-ui', '-apple-system', ...],
  crimson: ['var(--font-crimson)', 'Crimson Pro', 'Georgia', 'serif'],
  heading: ['var(--font-crimson)', 'Crimson Pro', 'Georgia', 'serif'],
  body: ['var(--font-crimson)', 'Crimson Pro', 'Georgia', 'serif'],
  mono: ['"JetBrains Mono"', 'Menlo', 'Monaco', 'Consolas', 'monospace'],
}
```

### Global CSS (`/app/globals.css`)
```css
--font-sans: var(--font-inter), ui-sans-serif, system-ui, sans-serif;
--font-serif: var(--font-source-serif), ui-serif, Georgia, serif;
--font-display: var(--font-playfair), ui-serif, Georgia, serif;
```

### Additional Fonts Referenced (CSS)
```css
.hebrew-text, .greek-text {
  font-family: "SBL Hebrew", "Ezra SIL", serif;
}

.greek-text {
  font-family: "SBL Greek", "Gentium Plus", serif;
}
```

---

## 3. Actual Usage in Components

### Inter (Sans-serif)
**Usage:** UI elements, labels, meta text, navigation

Found in components:
- Navigation labels (`font-sans text-xs`)
- Badges (`font-sans text-xs font-medium`)
- Meta information (`font-sans text-sm`)
- Form controls
- Settings page text

**Weights Used:**
- Regular (400) - body text
- Medium (500) - badges, labels
- Semibold (600) - section headers

### Crimson Pro (Serif)
**Usage:** Scripture text, devotional content, headings

Found in components:
- Scripture blockquotes (`font-crimson text-xl italic`)
- Devotional titles (`font-crimson text-3xl font-semibold`)
- Content body text (`font-crimson text-lg`)
- Prayers (`font-crimson text-lg italic`)

**Weights Used:**
- Regular (400) - body content
- Italic (400i) - scripture, prayers
- Semibold (600) - headings

### Playfair Display
**Declared but not explicitly used in components**

Defined for `--font-display` in CSS but Tailwind config maps `heading` to Crimson Pro, not Playfair.

**Status:** POTENTIALLY UNUSED

### Source Serif 4
**Declared but not explicitly used in components**

Defined for `--font-serif` in CSS but Tailwind config maps `body` to Crimson Pro.

**Status:** POTENTIALLY UNUSED

### JetBrains Mono
**Referenced in Tailwind config but not loaded via next/font**

Would need to be loaded if monospace code blocks are used.

**Status:** NOT LOADED

### SBL Hebrew / Ezra SIL
**Referenced in CSS for Hebrew text**

Not loaded - would rely on system fonts or need to be added.

**Status:** NOT LOADED

### SBL Greek / Gentium Plus
**Referenced in CSS for Greek text**

Not loaded - would rely on system fonts or need to be added.

**Status:** NOT LOADED

---

## 4. Issues Identified

### Issue 1: Duplicate/Conflicting Font Definitions
Two different layout files load different fonts:
- `/app/layout.tsx` - Inter, Playfair Display, Source Serif 4
- `/app/src/app/layout.tsx` - Inter, Crimson Pro

**Impact:** Unclear which layout is active; potential duplicate loading

**Recommendation:** Consolidate to single layout with consistent font strategy

### Issue 2: Unused Fonts Being Loaded
- Playfair Display: Declared but not used anywhere
- Source Serif 4: Declared but not used anywhere

**Impact:** Unnecessary network requests, increased page weight

**Recommendation:** Remove unused fonts or implement them consistently

### Issue 3: Biblical Language Fonts Not Loaded
CSS references SBL Hebrew, Ezra SIL, SBL Greek, and Gentium Plus but these are not loaded via next/font.

**Impact:** Hebrew/Greek text may not render properly

**Recommendation:** Either:
1. Load these fonts via next/font or local files
2. Use system font fallbacks with clear documentation
3. Consider web-safe alternatives

### Issue 4: Full Font Weights Loaded
No weight specification in font loading - all weights are downloaded by default.

**Impact:** Larger bundle size than necessary

**Recommendation:** Specify only needed weights

---

## 5. Font Optimization Recommendations

### Recommended Font Stack

Based on actual usage, consolidate to:

```typescript
// Recommended font configuration
import { Inter, Crimson_Pro } from 'next/font/google';

const inter = Inter({
  subsets: ['latin'],
  weight: ['400', '500', '600'],  // Only used weights
  variable: '--font-inter',
  display: 'swap',
});

const crimsonPro = Crimson_Pro({
  subsets: ['latin'],
  weight: ['400', '600'],         // Only used weights
  style: ['normal', 'italic'],    // Both needed
  variable: '--font-crimson',
  display: 'swap',
});
```

### Remove Unused Fonts
- Remove Playfair Display loading
- Remove Source Serif 4 loading

### Biblical Language Strategy

**Option A: Load Web Fonts (Recommended for accuracy)**
```typescript
// For Hebrew
const ezraSIL = localFont({
  src: '../fonts/EzraSIL.woff2',
  variable: '--font-hebrew',
  display: 'swap',
});

// For Greek
const gentiumPlus = localFont({
  src: '../fonts/GentiumPlus.woff2',
  variable: '--font-greek',
  display: 'swap',
});
```

**Option B: Use Google Fonts alternatives**
```typescript
import { Noto_Serif_Hebrew, Noto_Serif } from 'next/font/google';

const notoSerifHebrew = Noto_Serif_Hebrew({
  subsets: ['hebrew'],
  weight: ['400'],
  variable: '--font-hebrew',
  display: 'swap',
});
```

**Option C: System fonts with fallbacks (Lightweight)**
```css
.hebrew-text {
  font-family: "Times New Roman", "Arial Hebrew", serif;
}
.greek-text {
  font-family: "Times New Roman", "Palatino Linotype", serif;
}
```

---

## 6. Subsetting Opportunities

### Current Load (Estimated)
| Font | Weights | Size (est.) |
|------|---------|-------------|
| Inter | All (9) | ~200KB |
| Crimson Pro | All (6) | ~150KB |
| Playfair Display | All (6) | ~150KB |
| Source Serif 4 | All (6) | ~150KB |
| **Total** | - | **~650KB** |

### Optimized Load (Estimated)
| Font | Weights | Size (est.) |
|------|---------|-------------|
| Inter | 400, 500, 600 | ~60KB |
| Crimson Pro | 400, 400i, 600 | ~45KB |
| **Total** | - | **~105KB** |

**Potential Savings: ~545KB (84% reduction)**

### Additional Subsetting

For Latin-only content:
```typescript
const inter = Inter({
  subsets: ['latin'],           // Already limited
  weight: ['400', '500', '600'],
  variable: '--font-inter',
  display: 'swap',
  preload: true,
});
```

For extended Latin (accents needed):
```typescript
const inter = Inter({
  subsets: ['latin', 'latin-ext'],
  weight: ['400', '500', '600'],
  variable: '--font-inter',
  display: 'swap',
});
```

---

## 7. Consolidated Font Configuration

### Recommended Implementation

**`/app/layout.tsx` (Single Source of Truth)**
```typescript
import type { Metadata, Viewport } from 'next';
import { Inter, Crimson_Pro } from 'next/font/google';
import localFont from 'next/font/local';
import './globals.css';

// Primary sans-serif for UI
const inter = Inter({
  subsets: ['latin'],
  weight: ['400', '500', '600'],
  variable: '--font-inter',
  display: 'swap',
});

// Primary serif for reading content
const crimsonPro = Crimson_Pro({
  subsets: ['latin'],
  weight: ['400', '600'],
  style: ['normal', 'italic'],
  variable: '--font-crimson',
  display: 'swap',
});

// Optional: Hebrew font for word studies
// const ezraSIL = localFont({
//   src: './fonts/EzraSIL.woff2',
//   variable: '--font-hebrew',
//   display: 'swap',
// });

export default function RootLayout({ children }) {
  return (
    <html lang="en" className={`${inter.variable} ${crimsonPro.variable}`}>
      <body>{children}</body>
    </html>
  );
}
```

**`/app/tailwind.config.ts`**
```typescript
fontFamily: {
  // UI and navigation
  sans: ['var(--font-inter)', 'Inter', 'system-ui', 'sans-serif'],

  // Scripture and content reading
  serif: ['var(--font-crimson)', 'Crimson Pro', 'Georgia', 'serif'],

  // Headings (same as serif for consistency)
  heading: ['var(--font-crimson)', 'Crimson Pro', 'Georgia', 'serif'],

  // Code blocks (system fonts)
  mono: ['ui-monospace', 'SFMono-Regular', 'Menlo', 'Monaco', 'monospace'],

  // Biblical languages (with fallbacks)
  hebrew: ['var(--font-hebrew)', 'SBL Hebrew', 'Times New Roman', 'serif'],
  greek: ['var(--font-greek)', 'SBL Greek', 'Times New Roman', 'serif'],
}
```

---

## 8. Implementation Checklist

### Immediate Actions
- [ ] Audit which layout.tsx is actually being used
- [ ] Remove Playfair Display import
- [ ] Remove Source Serif 4 import
- [ ] Add weight specifications to remaining fonts
- [ ] Update Tailwind config for consistency

### Short-term Actions
- [ ] Consolidate layout files
- [ ] Test font rendering on all pages
- [ ] Add Hebrew/Greek font solution for word studies
- [ ] Document font usage guidelines

### Measurement
- [ ] Measure before/after bundle size
- [ ] Check Lighthouse performance scores
- [ ] Test font loading on slow connections (3G)

---

## 9. Summary

| Metric | Current | Recommended |
|--------|---------|-------------|
| Fonts Loaded | 4 | 2 |
| Weights Loaded | ~27 | 6 |
| Estimated Size | ~650KB | ~105KB |
| Potential Savings | - | 84% |

### Font Stack Summary

| Purpose | Font | Usage |
|---------|------|-------|
| UI/Navigation | Inter | Labels, buttons, meta |
| Reading/Content | Crimson Pro | Scripture, devotionals |
| Hebrew Text | SBL Hebrew (fallback) | Word studies |
| Greek Text | SBL Greek (fallback) | Word studies |

### Priority Actions
1. **HIGH:** Remove unused fonts (Playfair, Source Serif 4)
2. **HIGH:** Add weight specifications
3. **MEDIUM:** Consolidate layout files
4. **MEDIUM:** Add Hebrew/Greek font loading
5. **LOW:** Further subsetting optimization


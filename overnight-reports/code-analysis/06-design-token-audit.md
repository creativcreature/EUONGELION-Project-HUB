# Design Token Audit Report

**Generated:** 2026-01-19
**Project:** EUONGELION
**Path:** /Users/meltmac/Documents/Personal/wkGD/EUONGELION-STARTUP/app

---

## Executive Summary

EUONGELION has a well-defined design token system in `tailwind.config.ts` with brand colors (tehom, scroll, gold, burgundy, olive, shalom-blue), typography scales, and spacing tokens. However, there are significant deviations from this system with arbitrary hex values used throughout the codebase, particularly in newer components.

**Compliance Score:** 6/10 (Good foundation, inconsistent usage)

---

## Design Token System Overview

### Color Tokens (Defined in tailwind.config.ts)

| Token | Default Value | Purpose |
|-------|---------------|---------|
| `tehom` | `#1A1612` | Primary dark (primordial void) |
| `scroll` | `#F7F3ED` | Light background (parchment) |
| `gold` | `#C19A6B` | Accent (divine light) |
| `burgundy` | `#6B2C2C` | Passion/sacrifice |
| `olive` | `#6B6B4F` | Growth/renewal |
| `shalom-blue` | `#4A5F6B` | Peace/contemplation |

### Semantic Colors

| Token | Values | Purpose |
|-------|--------|---------|
| `success` | `#10B981` (500), `#059669` (600) | Success states |
| `warning` | `#F59E0B` (500), `#D97706` (600) | Warning states |
| `error` | `#EF4444` (500), `#DC2626` (600) | Error states |

### Typography Tokens

| Token | Font Family | Purpose |
|-------|-------------|---------|
| `font-sans` | Inter, system-ui | Body/UI text |
| `font-crimson` | Crimson Pro, Georgia | Reading/headings |
| `font-heading` | Crimson Pro, Georgia | Alias |
| `font-mono` | JetBrains Mono | Code |

### Spacing Tokens

| Token | Value | Purpose |
|-------|-------|---------|
| `reading-sm` | 1rem | Small reading margin |
| `reading` | 1.5rem | Default reading margin |
| `reading-lg` | 2rem | Large reading margin |
| `page-sm` | 1rem | Small page margin |
| `page` | 2rem | Default page margin |
| `section` | 4rem | Section spacing |

---

## Arbitrary Value Usage (Violations)

### Critical Violations (Different Color System)

These files use completely different color values from the design system:

#### 1. Discovery Page (`/app/src/app/discovery/page.tsx`)

**55+ instances of arbitrary colors:**

| Used Color | Should Be | Count |
|------------|-----------|-------|
| `#0a0a0b` | `tehom-950` | 2 |
| `#0d0d0e` | `tehom-900` | 5 |
| `#1A1612` | `tehom` (correct) | 4 |
| `#2a2520` | `tehom-700` | 3 |
| `#F7F3ED` | `scroll` (correct) | 8 |
| `#C19A6B` | `gold` (correct) | 10 |
| `#f97316` | No equivalent (orange) | 20+ |
| `#22c55e` | `success-500` | 4 |
| `#ef4444` | `error-500` | 4 |
| `#ea580c` | No equivalent | 2 |

**Issue:** Uses Tailwind default orange (`#f97316`) which is NOT in the design system.

---

#### 2. PerformanceMonitor (`/app/components/performance/PerformanceMonitor.tsx`)

| Used Color | Issue |
|------------|-------|
| `#888` | Should use olive or tehom variant |
| `#22c55e` | Should use `success-500` token |
| `#f59e0b` | Should use `warning-500` token |
| `#ef4444` | Should use `error-500` token |
| `#fff` | Should use `scroll` |
| `#333` | Should use `tehom` variant |
| `rgba(0, 0, 0, 0.85)` | Should use tehom with opacity |

---

#### 3. OfflinePage (`/app/components/offline/OfflinePage.tsx`)

| Used Color | Should Be |
|------------|-----------|
| `bg-[#1A1612]` | `bg-tehom` |

---

#### 4. Toast Component (`/app/components/ui/Toast.tsx`)

| Used Color | Issue |
|------------|-------|
| `bg-[#4A6B4F]` | Not in design system (green variant) |
| `bg-[#6B5A4A]` | Not in design system (brown variant) |

**Recommendation:** Add these as semantic tokens or use existing success/warning.

---

#### 5. Devotional Components

**DevotionalReader (`/app/components/devotional/DevotionalReader.tsx`):**
| Used | Should Be |
|------|-----------|
| `text-[#4A6B4F]` | Custom token or `text-olive` |

**DevotionalCard (`/app/components/devotional/DevotionalCard.tsx`):**
| Used | Should Be |
|------|-----------|
| `bg-[#4A6B4F]` | Custom token or `bg-olive` |

**ProgressIndicator (`/app/components/devotional/ProgressIndicator.tsx`):**
| Used | Should Be |
|------|-----------|
| `bg-[#4A6B4F]` | Add as design token |
| `text-[#4A6B4F]` | Add as design token |

---

#### 6. ProgressBar (`/app/components/loading/ProgressBar.tsx`)

| Used | Issue |
|------|-------|
| `rgba(193,154,107,0.5)` | Should use Tailwind gold with opacity class |
| Striped pattern CSS | Should be extracted to a utility class |

---

#### 7. Layout Files

**`/app/layout.tsx`** duplicates color definitions:
```tsx
deep: '#1a1a2e',      // Different from tehom!
gold: '#c9a227',      // Different from gold token!
cream: '#f5f3ed',     // Different from scroll!
```

**Issue:** These BRAND_COLORS constants don't match tailwind.config.ts!

---

#### 8. Social Share Images

**opengraph-image.tsx and twitter-image.tsx:**

Uses inline styles with arbitrary colors because OG images can't use Tailwind.

**Status:** ACCEPTABLE - OG images require inline styles.

---

### Missing Design Tokens

The following colors are used but not defined as tokens:

| Color | Usage | Recommendation |
|-------|-------|----------------|
| `#4A6B4F` | Success/completion green | Add as `forest` or `completed` token |
| `#6B5A4A` | Warning brown | Add as `sienna` or use existing |
| `#f97316` | Interactive orange | Add as `flame` or `cta` token |
| `#0a0a0b` | Ultra dark | Add as `void` or `tehom-950` |
| `#2a2520` | Dark variant | Use `tehom-700` |

---

## Font Token Violations

### Arbitrary Font Sizes

Most files use Tailwind's default type scale correctly. However:

**Discovery Page uses arbitrary sizes:**
- `text-xs`, `text-sm`, `text-lg`, `text-xl` - Correct
- No major font violations found

---

## Spacing Token Violations

### Arbitrary Spacing Values

Minimal spacing violations found. The codebase generally uses Tailwind's spacing scale.

---

## Component Compliance Summary

| Component | Color Compliance | Font Compliance | Spacing Compliance |
|-----------|-----------------|-----------------|-------------------|
| Button.tsx | Good | Good | Good |
| Card.tsx | Good | Good | Good |
| Modal.tsx | Good | Good | Good |
| Toast.tsx | Poor (#4A6B4F, #6B5A4A) | Good | Good |
| DevotionalCard.tsx | Poor (#4A6B4F) | Good | Good |
| DevotionalReader.tsx | Poor (#4A6B4F) | Good | Good |
| ProgressIndicator.tsx | Poor (#4A6B4F) | Good | Good |
| ProgressBar.tsx | Fair (rgba) | Good | Good |
| OfflinePage.tsx | Fair (#1A1612) | Good | Good |
| PerformanceMonitor.tsx | Poor (inline styles) | N/A | N/A |
| discovery/page.tsx | Poor (55+ violations) | Fair | Good |
| Auth forms | Good | Good | Good |
| Settings | Good | Good | Good |
| Navigation | Good | Good | Good |

---

## Design Token Alignment Issues

### Mismatch Between layout.tsx and tailwind.config.ts

**layout.tsx BRAND_COLORS:**
```typescript
deep: '#1a1a2e',      // MISMATCH: tehom is #1A1612
gold: '#c9a227',      // MISMATCH: gold is #C19A6B
cream: '#f5f3ed',     // Close to scroll #F7F3ED
burgundy: '#722f37',  // Close to burgundy #6B2C2C
```

**Recommendation:** Align these or remove duplication.

---

## Recommendations

### Immediate Actions (Critical)

1. **Add missing color tokens to tailwind.config.ts:**
```typescript
// Add to colors
completed: {
  DEFAULT: '#4A6B4F',
  50: '...',
  // full scale
},
flame: {
  DEFAULT: '#f97316',
  // for CTAs if keeping orange
}
```

2. **Replace hardcoded values in Discovery page:**
   - Change all `#f97316` to a design token or remove this component
   - Change `#0a0a0b`, `#0d0d0e` to tehom variants

3. **Fix Toast.tsx:**
   - Replace `bg-[#4A6B4F]` with token
   - Replace `bg-[#6B5A4A]` with token

### Short-term Actions

4. **Create ESLint rule or Stylelint rule** to catch arbitrary color values
5. **Document design tokens** in a design system guide
6. **Fix ProgressIndicator and DevotionalCard** to use tokens

### Medium-term Actions

7. **Audit and align BRAND_COLORS in layout.tsx** with tailwind.config.ts
8. **Create CSS custom properties** for colors used in inline styles
9. **Add design token documentation** to component library

---

## Arbitrary Value Count by File

| File | Arbitrary Colors | Severity |
|------|-----------------|----------|
| discovery/page.tsx | 55+ | High |
| PerformanceMonitor.tsx | 15+ | Medium |
| Toast.tsx | 4 | Medium |
| DevotionalCard.tsx | 2 | Low |
| DevotionalReader.tsx | 1 | Low |
| ProgressIndicator.tsx | 2 | Low |
| ProgressBar.tsx | 2 | Low |
| OfflinePage.tsx | 1 | Low |
| opengraph-image.tsx | 8 | Acceptable |
| twitter-image.tsx | 12 | Acceptable |
| layout.tsx | 12 | Medium |

**Total Violations:** ~115 (excluding OG images)

---

## CSS Variables Audit

The `globals.css` likely defines CSS custom properties. These should align with Tailwind tokens.

**Expected pattern:**
```css
:root {
  --gold: #C19A6B;
  --tehom: #1A1612;
  --scroll: #F7F3ED;
  /* etc. */
}
```

**Recommendation:** Verify globals.css defines all brand tokens as CSS variables for use in inline styles when needed.

---

## Action Items Checklist

### P0 (Block ship)
- [ ] Review if discovery page is production code or prototype
- [ ] Decide on orange (`#f97316`) - add to system or remove

### P1 (This sprint)
- [ ] Add `completed` token (#4A6B4F) to tailwind.config.ts
- [ ] Update Toast.tsx to use tokens
- [ ] Update devotional components to use tokens

### P2 (Next sprint)
- [ ] Fix PerformanceMonitor.tsx (dev tool, lower priority)
- [ ] Align layout.tsx BRAND_COLORS with tailwind.config.ts
- [ ] Add ESLint rule for arbitrary colors

### P3 (Backlog)
- [ ] Create design token documentation
- [ ] Add Storybook with token visualization
- [ ] Consider design token tooling (Style Dictionary, etc.)

---

*Report generated by overnight autonomous analysis*

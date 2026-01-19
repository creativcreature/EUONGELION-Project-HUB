# EUONGELION Typography Scale Documentation

**Document:** 58-typography-scale-documentation.md
**Generated:** 2026-01-19
**Status:** Design System Reference

---

## Overview

EUONGELION's typography system is "typography forward" - Scripture should be beautiful and readable. The system uses a combination of elegant serif fonts for reading content and clean sans-serif fonts for UI elements, creating a contemplative reading experience that honors the sacred nature of the text.

---

## Font Families

### Primary Fonts

| Font | CSS Variable | Usage |
|------|-------------|-------|
| **Inter** | `var(--font-inter)` | UI elements, labels, navigation, buttons |
| **Crimson Pro** | `var(--font-crimson)` | Headings, scripture text, devotional content |

### Font Stack Definitions

```typescript
fontFamily: {
  // Body and UI - clean sans-serif
  sans: ['var(--font-inter)', 'Inter', 'system-ui', '-apple-system', 'BlinkMacSystemFont', 'sans-serif'],

  // Reading and headings - elegant serif
  crimson: ['var(--font-crimson)', 'Crimson Pro', 'Georgia', 'serif'],

  // Aliases for semantic usage
  heading: ['var(--font-crimson)', 'Crimson Pro', 'Georgia', 'serif'],
  body: ['var(--font-crimson)', 'Crimson Pro', 'Georgia', 'serif'],

  // Monospace for code
  mono: ['"JetBrains Mono"', 'Menlo', 'Monaco', 'Consolas', 'monospace'],
}
```

### Special Biblical Language Fonts

For Hebrew and Greek text, specialized fonts are loaded:

```css
.hebrew-text {
  font-family: "SBL Hebrew", "Ezra SIL", serif;
  direction: rtl;
  unicode-bidi: bidi-override;
}

.greek-text {
  font-family: "SBL Greek", "Gentium Plus", serif;
  direction: ltr;
  unicode-bidi: normal;
}

.transliteration {
  font-style: italic;
  color: var(--muted-foreground);
}
```

---

## Type Scale

### Base Scale (Tailwind Default)

| Class | Size | Line Height | Usage |
|-------|------|-------------|-------|
| `text-xs` | 0.75rem (12px) | 1rem | Fine print, timestamps |
| `text-sm` | 0.875rem (14px) | 1.25rem | Captions, metadata, small labels |
| `text-base` | 1rem (16px) | 1.5rem | Body text, default size |
| `text-lg` | 1.125rem (18px) | 1.75rem | Emphasized body text |
| `text-xl` | 1.25rem (20px) | 1.75rem | Section headings |
| `text-2xl` | 1.5rem (24px) | 2rem | Subheadings |
| `text-3xl` | 1.875rem (30px) | 2.25rem | Major headings |
| `text-4xl` | 2.25rem (36px) | 2.5rem | Page titles |
| `text-5xl` | 3rem (48px) | 1.15 | Hero text |

### Custom Scripture Sizes

Optimized for reading biblical content with increased line height and subtle letter spacing:

| Class | Size | Line Height | Letter Spacing | Usage |
|-------|------|-------------|----------------|-------|
| `text-verse-sm` | 0.875rem | 1.75 | 0.01em | Compact verse display |
| `text-verse` | 1rem | 1.8 | 0.01em | Default verse text |
| `text-verse-lg` | 1.125rem | 1.85 | 0.01em | Emphasized verses |
| `text-verse-xl` | 1.25rem | 1.9 | 0.01em | Featured scripture |

### Display Sizes

For hero sections and large headings with tight letter spacing:

| Class | Size | Line Height | Letter Spacing | Usage |
|-------|------|-------------|----------------|-------|
| `text-display-sm` | 2rem | 1.2 | -0.02em | Small display headings |
| `text-display` | 2.5rem | 1.15 | -0.02em | Standard display |
| `text-display-lg` | 3rem | 1.1 | -0.02em | Large display |
| `text-display-xl` | 4rem | 1.05 | -0.02em | Hero display text |

---

## Typography Rules

### Headings (h1-h6)

All headings use the Crimson Pro (display) font family with consistent styling:

```css
h1, h2, h3, h4, h5, h6 {
  font-family: var(--font-display);
  font-weight: 600;
  line-height: 1.2;
  letter-spacing: -0.02em;
}
```

**Usage in Components:**

```jsx
// Page title
<h1 className="font-crimson text-3xl md:text-4xl font-semibold text-tehom">
  Title
</h1>

// Section heading
<h2 className="font-crimson text-xl font-semibold text-tehom">
  Section
</h2>

// Card title
<h3 className="text-xl font-semibold text-scroll">
  Card Title
</h3>
```

### Body Text

Default body text uses sans-serif with comfortable line height:

```css
body {
  font-family: var(--font-sans);
  line-height: 1.6;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
```

### Scripture Text

Scripture content uses the dedicated `.scripture-text` class for optimal reading:

```css
.scripture-text {
  font-family: var(--font-serif);
  font-size: 1.125rem;
  line-height: 1.8;
  color: var(--color-scripture);
}
```

### Scripture References

Scripture references (e.g., "John 3:16") use distinct styling:

```css
.scripture-reference {
  font-family: var(--font-sans);
  font-size: 0.875rem;
  font-weight: 500;
  color: var(--color-primary-gold);
}
```

---

## When to Use Each Font

### Use Crimson Pro (Serif) For:

- **Headings and titles** - Creates a sense of gravitas
- **Scripture text** - Enhances readability for extended reading
- **Devotional content** - Main reading passages
- **Pull quotes** - Featured text
- **Brand name** (EUONGELION) - Logo text

```jsx
// Heading
<h1 className="font-crimson text-3xl font-semibold">Devotional Title</h1>

// Scripture
<p className="font-crimson text-verse-lg leading-relaxed">
  "For God so loved the world..."
</p>

// Quote
<blockquote className="font-crimson text-xl italic">
  &ldquo;Ancient wisdom&rdquo;
</blockquote>
```

### Use Inter (Sans-serif) For:

- **UI elements** - Buttons, form labels, navigation
- **Metadata** - Dates, timestamps, counts
- **System messages** - Toasts, alerts, error messages
- **Navigation** - Menu items, links
- **Small text** - Captions, helper text, footnotes
- **Interactive elements** - Inputs, toggles, controls

```jsx
// Button
<button className="font-sans text-base font-medium">Continue</button>

// Metadata
<span className="font-sans text-sm text-tehom/60">5 min read</span>

// Navigation label
<span className="font-sans text-xs font-medium">Today</span>

// Form label
<label className="font-sans text-sm font-medium">Email Address</label>
```

---

## Prose/Typography Plugin

For long-form content, the Tailwind Typography plugin provides sensible defaults:

```typescript
typography: {
  DEFAULT: {
    css: {
      '--tw-prose-body': '#1A1612',
      '--tw-prose-headings': '#1A1612',
      '--tw-prose-lead': '#6B6B4F',
      '--tw-prose-links': '#C19A6B',
      '--tw-prose-bold': '#1A1612',
      '--tw-prose-counters': '#6B6B4F',
      '--tw-prose-bullets': '#C19A6B',
      '--tw-prose-hr': '#E3D7C5',
      '--tw-prose-quotes': '#6B2C2C',
      '--tw-prose-quote-borders': '#C19A6B',
      '--tw-prose-captions': '#6B6B4F',
      '--tw-prose-code': '#1A1612',
      '--tw-prose-pre-code': '#F7F3ED',
      '--tw-prose-pre-bg': '#1A1612',
      '--tw-prose-th-borders': '#D9C9B1',
      '--tw-prose-td-borders': '#EDE5D9',
      maxWidth: '65ch',
      fontFamily: 'var(--font-crimson), "Crimson Pro", Georgia, serif',
    },
  },
},
```

### Using Prose

```jsx
<article className="prose prose-tehom">
  <h1>Devotional Title</h1>
  <p>Devotional content with proper typography styling...</p>
  <blockquote>Scripture quote</blockquote>
</article>
```

---

## Responsive Typography

### Mobile-First Approach

Typography scales up on larger screens:

```jsx
// Responsive heading
<h1 className="font-crimson text-2xl md:text-3xl lg:text-4xl">
  Responsive Title
</h1>

// Responsive body
<p className="text-base md:text-lg">
  Responsive body text
</p>
```

### Recommended Responsive Patterns

| Element | Mobile | Tablet (md) | Desktop (lg) |
|---------|--------|-------------|--------------|
| Page title | `text-2xl` | `text-3xl` | `text-4xl` |
| Section heading | `text-xl` | `text-2xl` | `text-2xl` |
| Card title | `text-lg` | `text-xl` | `text-xl` |
| Body text | `text-base` | `text-base` | `text-lg` |
| Scripture | `text-verse` | `text-verse-lg` | `text-verse-xl` |
| Captions | `text-xs` | `text-sm` | `text-sm` |

---

## Line Length (Measure)

For optimal readability, control line length with `max-width`:

```typescript
maxWidth: {
  'reading-narrow': '45ch',  // Compact layouts
  'reading': '65ch',         // Optimal (default)
  'reading-wide': '75ch',    // Wider layouts
  'content': '80rem',        // Full content width
},
```

**Usage:**

```jsx
// Standard reading content
<article className="max-w-reading mx-auto">
  <p>Content with optimal line length...</p>
</article>

// Scripture with narrower measure
<blockquote className="max-w-reading-narrow mx-auto">
  Scripture text...
</blockquote>
```

---

## Font Weights

### Available Weights

| Weight | Value | Usage |
|--------|-------|-------|
| Normal | 400 | Body text, paragraphs |
| Medium | 500 | Emphasis, labels, references |
| Semibold | 600 | Headings, important text |
| Bold | 700 | Strong emphasis (use sparingly) |

### Weight Guidelines

- **Don't overuse bold** - It loses meaning
- **Use semibold for headings** - Not bold
- **Medium for UI elements** - Buttons, labels
- **Normal for reading** - Body text, scripture

```jsx
// Heading - semibold
<h2 className="font-semibold">Section Title</h2>

// Button - medium
<button className="font-medium">Continue</button>

// Body - normal (default)
<p>Regular paragraph text...</p>

// Emphasis - medium
<span className="font-medium">Important term</span>
```

---

## Accessibility

### Font Size Minimums

- **Body text**: 16px minimum (1rem)
- **Interactive elements**: 16px minimum
- **Small text**: 12px minimum, limited use

### Line Height

- **Body text**: 1.5-1.6 (comfortable reading)
- **Scripture**: 1.8-1.9 (enhanced readability)
- **Headings**: 1.1-1.2 (tighter)

### Contrast

- Ensure text has minimum 4.5:1 contrast ratio
- Use `text-tehom` on light backgrounds
- Use `text-scroll` on dark backgrounds

---

## Print Styles

Typography adjusts for print media:

```css
@media print {
  body {
    background: white;
    color: black;
  }

  .scripture-text {
    font-size: 12pt;
    line-height: 1.5;
  }
}
```

---

## Quick Reference

### Common Typography Patterns

```jsx
// Page heading
<h1 className="font-crimson text-3xl md:text-4xl font-semibold text-tehom mb-4">

// Section heading
<h2 className="font-crimson text-xl font-semibold text-tehom">

// Card title
<h3 className="text-xl font-semibold text-scroll">

// Body text
<p className="font-sans text-base text-tehom leading-relaxed">

// Scripture
<p className="font-crimson text-verse-lg text-tehom/80 leading-relaxed italic">

// Scripture reference
<cite className="font-sans text-sm font-medium text-gold">

// Metadata
<span className="font-sans text-xs text-tehom/60">

// Button text
<button className="font-sans text-base font-medium">

// Form label
<label className="font-sans text-sm font-medium text-tehom-700">

// Helper/caption
<p className="font-sans text-xs text-tehom/40">
```

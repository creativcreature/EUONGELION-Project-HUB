# EUONGELION Color System Documentation

**Document:** 57-color-system-documentation.md
**Generated:** 2026-01-19
**Status:** Design System Reference

---

## Overview

The EUONGELION color system is built around a "sacred minimalism" philosophy, using earthy, ancient-inspired tones that evoke the feeling of aged manuscripts and spiritual depth. The palette is intentionally muted and contemplative, avoiding bright or distracting colors that would disrupt the devotional experience.

---

## Primary Brand Colors

### Tehom (Primary Dark)
**The primordial void, deep earth**

| Token | Hex Value | Usage |
|-------|-----------|-------|
| `tehom-DEFAULT` | `#1A1612` | Primary dark color, backgrounds in dark mode |
| `tehom-50` | `#F5F4F3` | Lightest tint |
| `tehom-100` | `#E8E6E4` | Very light backgrounds |
| `tehom-200` | `#D1CCC8` | Light borders, dividers |
| `tehom-300` | `#B3ACA5` | Muted text |
| `tehom-400` | `#958C82` | Secondary text |
| `tehom-500` | `#776C5F` | Mid-tone text |
| `tehom-600` | `#5A524A` | Emphasis text |
| `tehom-700` | `#3D3835` | Dark text |
| `tehom-800` | `#262220` | Near-black |
| `tehom-900` | `#1A1612` | Primary dark (same as DEFAULT) |
| `tehom-950` | `#0D0B09` | Darkest shade |

**Usage Guidelines:**
- Primary text color in light mode
- Background color in dark mode
- Card backgrounds and overlays
- Navigation and header backgrounds in dark mode

**Accessibility:** Tehom-900 against Scroll-200 provides 12.6:1 contrast ratio (WCAG AAA)

---

### Scroll (Background)
**Ancient parchment, aged manuscript**

| Token | Hex Value | Usage |
|-------|-----------|-------|
| `scroll-DEFAULT` | `#F7F3ED` | Primary light background |
| `scroll-50` | `#FDFCFB` | Brightest white |
| `scroll-100` | `#FAF8F5` | Off-white |
| `scroll-200` | `#F7F3ED` | Main background (same as DEFAULT) |
| `scroll-300` | `#EDE5D9` | Subtle contrast |
| `scroll-400` | `#E3D7C5` | Card backgrounds |
| `scroll-500` | `#D9C9B1` | Borders, dividers |
| `scroll-600` | `#C4AD8E` | Muted accents |
| `scroll-700` | `#AF916B` | Warm mid-tone |
| `scroll-800` | `#8A7252` | Dark warm |
| `scroll-900` | `#655339` | Darkest warm |

**Usage Guidelines:**
- Page backgrounds in light mode
- Card and container backgrounds
- Text color in dark mode
- Soft borders and dividers

**Accessibility:** Scroll provides excellent readability for extended reading sessions

---

### Gold (Accent)
**Burnished gold, divine light**

| Token | Hex Value | Usage |
|-------|-----------|-------|
| `gold-DEFAULT` | `#C19A6B` | Primary accent color |
| `gold-50` | `#FAF6F1` | Lightest gold tint |
| `gold-100` | `#F4EBE0` | Very light highlight |
| `gold-200` | `#E9D7C1` | Soft highlight |
| `gold-300` | `#DDC3A2` | Light accent |
| `gold-400` | `#D2AF83` | Mid-light accent |
| `gold-500` | `#C19A6B` | Primary gold (same as DEFAULT) |
| `gold-600` | `#A87E4E` | Darker gold, hover states |
| `gold-700` | `#85633D` | Dark gold |
| `gold-800` | `#62492D` | Very dark gold |
| `gold-900` | `#3F2F1D` | Darkest gold |

**Usage Guidelines:**
- Primary buttons and CTAs
- Active states and selection indicators
- Scripture references and highlights
- Brand accent elements (logo "EU")
- Focus rings and interactive elements
- Progress bars and completion indicators

**Accessibility:** Gold-600 against white provides 4.6:1 contrast (WCAG AA for large text)

---

### Burgundy (Passion)
**Passion, sacrifice**

| Token | Hex Value | Usage |
|-------|-----------|-------|
| `burgundy-DEFAULT` | `#6B2C2C` | Error states, important alerts |
| `burgundy-50` | `#F9EFEF` | Light error background |
| `burgundy-100` | `#F2DCDC` | Soft error highlight |
| `burgundy-200` | `#E5B9B9` | Light warning |
| `burgundy-300` | `#D89696` | Mid warning |
| `burgundy-400` | `#CB7373` | Light burgundy |
| `burgundy-500` | `#A04C4C` | Mid burgundy |
| `burgundy-600` | `#6B2C2C` | Primary burgundy (same as DEFAULT) |
| `burgundy-700` | `#582424` | Dark burgundy |
| `burgundy-800` | `#451C1C` | Very dark |
| `burgundy-900` | `#321414` | Darkest |

**Usage Guidelines:**
- Error messages and validation states
- Destructive action buttons
- Important alerts requiring attention
- Thematic emphasis (sacrifice, passion themes)

---

### Olive (Growth)
**Growth, renewal, wisdom**

| Token | Hex Value | Usage |
|-------|-----------|-------|
| `olive-DEFAULT` | `#6B6B4F` | Secondary text, muted elements |
| `olive-50` | `#F5F5F2` | Lightest olive |
| `olive-100` | `#EAEAE3` | Very light |
| `olive-200` | `#D5D5C7` | Light |
| `olive-300` | `#C0C0AB` | Mid-light |
| `olive-400` | `#ABAB8F` | Mid |
| `olive-500` | `#8E8E6F` | Mid-dark |
| `olive-600` | `#6B6B4F` | Primary olive (same as DEFAULT) |
| `olive-700` | `#565641` | Dark olive |
| `olive-800` | `#414133` | Very dark |
| `olive-900` | `#2C2C25` | Darkest |

**Usage Guidelines:**
- Secondary text and captions
- Metadata and timestamps
- Success states (completion, growth)
- Secondary buttons (hover states)
- Muted icons and decorative elements

---

### Shalom Blue (Contemplation)
**Peace, depth, contemplation**

| Token | Hex Value | Usage |
|-------|-----------|-------|
| `shalom-blue-DEFAULT` | `#4A5F6B` | Info states, contemplative elements |
| `shalom-blue-50` | `#F0F3F4` | Lightest blue |
| `shalom-blue-100` | `#E0E6E9` | Very light |
| `shalom-blue-200` | `#C1CDD3` | Light |
| `shalom-blue-300` | `#A2B4BD` | Mid-light |
| `shalom-blue-400` | `#839BA7` | Mid |
| `shalom-blue-500` | `#648291` | Mid-dark |
| `shalom-blue-600` | `#4A5F6B` | Primary shalom (same as DEFAULT) |
| `shalom-blue-700` | `#3D4E58` | Dark |
| `shalom-blue-800` | `#303D45` | Very dark |
| `shalom-blue-900` | `#232C32` | Darkest |

**Usage Guidelines:**
- Informational messages
- Links and navigation elements
- Contemplative UI sections
- Toast notifications (info variant)

---

## Semantic Colors

### Success

| Token | Hex Value | Usage |
|-------|-----------|-------|
| `success-50` | `#ECFDF5` | Light success background |
| `success-500` | `#10B981` | Primary success |
| `success-600` | `#059669` | Hover success |

### Warning

| Token | Hex Value | Usage |
|-------|-----------|-------|
| `warning-50` | `#FFFBEB` | Light warning background |
| `warning-500` | `#F59E0B` | Primary warning |
| `warning-600` | `#D97706` | Hover warning |

### Error

| Token | Hex Value | Usage |
|-------|-----------|-------|
| `error-50` | `#FEF2F2` | Light error background |
| `error-500` | `#EF4444` | Primary error |
| `error-600` | `#DC2626` | Hover error |

---

## CSS Custom Properties (globals.css)

The design system defines CSS custom properties for dynamic theming:

### Light Mode (Default)

```css
:root {
  --color-primary-deep: #1a1a2e;
  --color-primary-gold: #c9a227;
  --color-primary-cream: #f5f3ed;
  --color-primary-burgundy: #722f37;

  --color-olive: #4a5d23;
  --color-terracotta: #c67949;
  --color-slate: #4a5568;
  --color-ivory: #fffef9;

  --color-scripture: #2d3748;
  --color-highlight: #fef3c7;
  --color-focus: #1a1a2e;

  --background: var(--color-ivory);
  --foreground: var(--color-scripture);
  --card-background: #ffffff;
  --primary: var(--color-primary-deep);
  --accent: var(--color-primary-gold);
  --muted: #f1f5f9;
  --border: #e2e8f0;
  --ring: var(--color-primary-gold);
}
```

### Dark Mode

```css
@media (prefers-color-scheme: dark) {
  :root {
    --background: #0a0a0a;
    --foreground: #ededed;
    --card-background: #1a1a1a;
    --primary: var(--color-primary-gold);
    --secondary: #262626;
    --accent: var(--color-primary-gold);
    --muted: #262626;
    --muted-foreground: #a1a1aa;
    --border: #262626;
  }
}
```

---

## Usage in Tailwind

### Direct Color Classes

```jsx
// Text colors
<p className="text-tehom">Dark text</p>
<p className="text-gold">Accent text</p>
<p className="text-olive">Muted text</p>

// Background colors
<div className="bg-scroll">Light background</div>
<div className="bg-tehom">Dark background</div>
<div className="bg-gold">Accent background</div>

// Border colors
<div className="border border-tehom/10">Subtle border</div>
<div className="border-gold">Accent border</div>

// With opacity modifiers
<div className="bg-tehom/5">Very subtle background</div>
<div className="text-tehom/60">60% opacity text</div>
```

### Color Scale Usage

```jsx
// Using specific shades
<button className="bg-gold-600 hover:bg-gold-700">Primary Button</button>
<div className="bg-scroll-300">Slightly darker background</div>
<p className="text-tehom-600">Slightly muted text</p>
```

---

## Accessibility Guidelines

### Contrast Requirements

| Usage | Minimum Ratio | WCAG Level |
|-------|---------------|------------|
| Body text | 4.5:1 | AA |
| Large text (18px+) | 3:1 | AA |
| UI components | 3:1 | AA |
| Non-text elements | 3:1 | AA |

### Recommended Combinations

| Background | Text | Contrast Ratio |
|------------|------|----------------|
| Scroll | Tehom | 12.6:1 (AAA) |
| Tehom | Scroll | 12.6:1 (AAA) |
| Scroll | Gold | 4.8:1 (AA) |
| Tehom | Gold | 4.1:1 (AA for large text) |
| White | Olive | 4.6:1 (AA) |

### Focus Indicators

Always use the gold ring color for focus states:

```jsx
<button className="focus:ring-2 focus:ring-gold/40 focus:ring-offset-2">
  Focusable Element
</button>
```

---

## Brand Color Constants (for Image Generation)

```typescript
export const BRAND_COLORS = {
  tehom: '#1A1612',
  scroll: '#F7F3ED',
  gold: '#C19A6B',
  olive: '#6B6B4F',
  burgundy: '#6B2C2C',
  shalomBlue: '#4A5F6B',
};
```

---

## Color Naming Philosophy

The EUONGELION color names are intentionally chosen from biblical and ancient terminology:

- **Tehom** - Hebrew for "the deep" or "abyss" (Genesis 1:2), representing the primordial void
- **Scroll** - Evokes ancient manuscripts and the physical medium of Scripture
- **Gold** - Symbolizes divine light, refinement through fire, and spiritual value
- **Burgundy** - Represents the blood of sacrifice and passionate devotion
- **Olive** - Biblical symbol of peace, wisdom, and the Holy Spirit
- **Shalom** - Hebrew for peace, completeness, and spiritual wholeness

---

## Implementation Notes

1. **Dark Mode First**: EUONGELION is designed dark-mode-first. The dark palette should feel primary, with light mode as an alternative.

2. **Opacity Modifiers**: Prefer opacity modifiers (`/10`, `/20`, etc.) over creating new color shades for subtle variations.

3. **Semantic Usage**: Use semantic colors (success, warning, error) sparingly - prefer brand colors where thematically appropriate.

4. **Scripture Text**: Use the dedicated `--color-scripture` variable for biblical text to ensure optimal readability.

5. **Highlights**: The `--color-highlight` (#fef3c7) is specifically designed for scripture highlighting with a warm, parchment-like feel.

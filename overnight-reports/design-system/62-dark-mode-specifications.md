# EUONGELION Dark Mode Specifications

**Document:** 62-dark-mode-specifications.md
**Generated:** 2026-01-19
**Status:** Design System Reference

---

## Overview

EUONGELION is designed **dark mode first**. The dark palette is the primary experience, reflecting the contemplative nature of early morning and evening devotional reading. The light mode serves as an alternative for outdoor reading or user preference.

---

## Dark Mode Philosophy

### Why Dark Mode First?

1. **Devotional Context** - Many users read devotionals early morning or at night
2. **Eye Comfort** - Reduces strain during extended reading
3. **Focus** - Dark backgrounds minimize distraction, highlighting content
4. **Sacred Atmosphere** - Evokes the quietness of a chapel or study
5. **Battery Efficiency** - Benefits OLED/AMOLED displays

### Design Principles

- **Dark doesn't mean black** - Use deep, warm colors (tehom) not pure black
- **Warm over cold** - Avoid blue-tinted dark themes
- **Subtle contrast** - Softer transitions between elements
- **Gold as light** - Accent color represents divine illumination against darkness
- **Readable text** - Higher contrast than typical dark modes for readability

---

## Implementation Method

### Tailwind Configuration

Dark mode is implemented using the `class` strategy:

```typescript
// tailwind.config.ts
const config: Config = {
  darkMode: 'class',  // Uses .dark class on html/body
  // ...
};
```

### Class-Based Toggle

Dark mode is applied by adding `.dark` class to the root element:

```html
<!-- Light mode (default) -->
<html>

<!-- Dark mode -->
<html class="dark">
```

### System Preference Detection

The CSS also responds to system preference via media query:

```css
@media (prefers-color-scheme: dark) {
  :root {
    --background: #0a0a0a;
    --foreground: #ededed;
    /* ... */
  }
}
```

---

## Color Mappings

### CSS Custom Properties

#### Light Mode (Default)

```css
:root {
  /* Backgrounds */
  --background: var(--color-ivory);          /* #fffef9 */
  --card-background: #ffffff;

  /* Text */
  --foreground: var(--color-scripture);      /* #2d3748 */
  --card-foreground: var(--color-scripture);

  /* Primary/Accent */
  --primary: var(--color-primary-deep);      /* #1a1a2e */
  --primary-foreground: #ffffff;
  --accent: var(--color-primary-gold);       /* #c9a227 */
  --accent-foreground: var(--color-primary-deep);

  /* Secondary */
  --secondary: var(--color-primary-cream);   /* #f5f3ed */
  --secondary-foreground: var(--color-scripture);

  /* Muted */
  --muted: #f1f5f9;
  --muted-foreground: #64748b;

  /* Borders */
  --border: #e2e8f0;
  --ring: var(--color-primary-gold);

  /* Shadows */
  --shadow-sm: 0 1px 2px 0 rgba(0, 0, 0, 0.05);
  --shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.1), 0 1px 2px -1px rgba(0, 0, 0, 0.1);
  --shadow-md: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -2px rgba(0, 0, 0, 0.1);
  --shadow-lg: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -4px rgba(0, 0, 0, 0.1);
}
```

#### Dark Mode

```css
@media (prefers-color-scheme: dark) {
  :root {
    /* Backgrounds */
    --background: #0a0a0a;
    --card-background: #1a1a1a;

    /* Text */
    --foreground: #ededed;
    --card-foreground: #ededed;

    /* Primary/Accent - Gold becomes primary in dark mode */
    --primary: var(--color-primary-gold);     /* #c9a227 */
    --primary-foreground: var(--color-primary-deep);
    --accent: var(--color-primary-gold);
    --accent-foreground: #0a0a0a;

    /* Secondary */
    --secondary: #262626;
    --secondary-foreground: #ededed;

    /* Muted */
    --muted: #262626;
    --muted-foreground: #a1a1aa;

    /* Borders */
    --border: #262626;
    --ring: var(--color-primary-gold);

    /* Shadows - Deeper in dark mode */
    --shadow-sm: 0 1px 2px 0 rgba(0, 0, 0, 0.3);
    --shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.4), 0 1px 2px -1px rgba(0, 0, 0, 0.3);
    --shadow-md: 0 4px 6px -1px rgba(0, 0, 0, 0.4), 0 2px 4px -2px rgba(0, 0, 0, 0.3);
    --shadow-lg: 0 10px 15px -3px rgba(0, 0, 0, 0.4), 0 4px 6px -4px rgba(0, 0, 0, 0.3);
  }
}
```

---

## Color Mapping Table

| Purpose | Light Mode | Dark Mode |
|---------|------------|-----------|
| **Page Background** | `#fffef9` (ivory) | `#0a0a0a` (near-black) |
| **Card Background** | `#ffffff` (white) | `#1a1a1a` (dark gray) |
| **Primary Text** | `#2d3748` (scripture) | `#ededed` (off-white) |
| **Secondary Text** | `#64748b` (muted) | `#a1a1aa` (light gray) |
| **Primary Color** | `#1a1a2e` (deep) | `#c9a227` (gold) |
| **Accent Color** | `#c9a227` (gold) | `#c9a227` (gold) |
| **Borders** | `#e2e8f0` (light) | `#262626` (dark) |
| **Muted Background** | `#f1f5f9` (light gray) | `#262626` (dark gray) |

### Key Insight: Gold is Constant

The gold accent color (`#c9a227` / `#C19A6B`) remains constant across both themes, serving as the unifying brand element - like divine light that shines in both darkness and daylight.

---

## Using Dark Mode in Components

### Tailwind Classes

```jsx
// Background
<div className="bg-white dark:bg-tehom-900">

// Text
<p className="text-tehom dark:text-scroll">

// Borders
<div className="border border-tehom/10 dark:border-scroll/10">

// Hover states
<button className="hover:bg-tehom/5 dark:hover:bg-scroll/10">
```

### Component Examples

#### Card in Both Modes

```jsx
<div className="bg-white dark:bg-tehom-900 rounded-2xl shadow-lg">
  <h2 className="text-tehom dark:text-scroll">Title</h2>
  <p className="text-tehom-600 dark:text-scroll-400">Description</p>
</div>
```

#### Form Input

```jsx
<input
  className="
    w-full px-4 py-3 rounded-lg border
    bg-white dark:bg-tehom-800
    text-tehom dark:text-scroll
    placeholder-tehom-400 dark:placeholder-scroll-600
    border-tehom-200 dark:border-tehom-700
    focus:ring-2 focus:ring-gold-500
  "
/>
```

#### Button

```jsx
<button
  className="
    bg-gold-600 hover:bg-gold-700
    text-white
    dark:text-tehom
  "
>
  Continue
</button>
```

---

## Dark Mode Components

### Modal (from Modal.tsx)

```jsx
// Modal always uses dark styling (tehom background)
<div className="
  bg-tehom border border-scroll/20 rounded-xl
  shadow-2xl shadow-tehom/50
">
  <h2 className="text-scroll">Title</h2>
  <p className="text-scroll/70">Description</p>
</div>

// Close button
<button className="text-scroll/60 hover:text-scroll hover:bg-scroll/10">
```

### Toast (from Toast.tsx)

```jsx
const toastVariants = cva(
  [...],
  {
    variants: {
      variant: {
        default: 'bg-tehom border-scroll/20 text-scroll',
        success: 'bg-[#4A6B4F] border-[#4A6B4F]/50 text-scroll',
        error: 'bg-burgundy border-burgundy/50 text-scroll',
        warning: 'bg-[#6B5A4A] border-[#6B5A4A]/50 text-scroll',
        info: 'bg-shalom border-shalom/50 text-scroll',
      },
    },
  }
);
```

### Card (from Card.tsx)

```jsx
const cardVariants = cva(
  'rounded-lg transition-all duration-200 ease-out border border-scroll/10',
  {
    variants: {
      variant: {
        default: 'bg-scroll/5',
        elevated: 'bg-scroll/8 shadow-md hover:shadow-lg',
        outlined: 'bg-transparent border-scroll/20',
        ghost: 'bg-transparent border-transparent',
        glass: 'bg-scroll/5 backdrop-blur-md border-scroll/10',
      },
    },
  }
);
```

---

## Contrast Requirements

### Dark Mode Contrast Ratios

| Element | Background | Text | Ratio | WCAG |
|---------|------------|------|-------|------|
| Body text | `#0a0a0a` | `#ededed` | 17.4:1 | AAA |
| Secondary text | `#0a0a0a` | `#a1a1aa` | 8.3:1 | AAA |
| Card text | `#1a1a1a` | `#ededed` | 14.2:1 | AAA |
| Gold on dark | `#0a0a0a` | `#c9a227` | 7.2:1 | AAA |
| Muted on card | `#1a1a1a` | `#a1a1aa` | 6.8:1 | AAA |

### Light Mode Contrast Ratios

| Element | Background | Text | Ratio | WCAG |
|---------|------------|------|-------|------|
| Body text | `#fffef9` | `#2d3748` | 11.2:1 | AAA |
| Secondary text | `#fffef9` | `#64748b` | 4.8:1 | AA |
| Gold on light | `#fffef9` | `#c9a227` | 3.2:1 | Large text |

---

## Theme Toggle Implementation

### useTheme Hook

```typescript
// From hooks/useTheme.ts
export function useTheme() {
  const [theme, setTheme] = useState<'light' | 'dark' | 'system'>('system');

  useEffect(() => {
    const root = document.documentElement;
    const systemDark = window.matchMedia('(prefers-color-scheme: dark)').matches;

    if (theme === 'dark' || (theme === 'system' && systemDark)) {
      root.classList.add('dark');
    } else {
      root.classList.remove('dark');
    }
  }, [theme]);

  return { theme, setTheme };
}
```

### Theme Toggle Component

```jsx
function ThemeToggle() {
  const { theme, setTheme } = useTheme();

  return (
    <button
      onClick={() => setTheme(theme === 'dark' ? 'light' : 'dark')}
      className="p-2 rounded-full hover:bg-tehom/5 dark:hover:bg-scroll/10"
      aria-label={`Switch to ${theme === 'dark' ? 'light' : 'dark'} mode`}
    >
      {theme === 'dark' ? <SunIcon /> : <MoonIcon />}
    </button>
  );
}
```

---

## Best Practices

### Do:

1. **Test in dark mode first** - It's the primary experience
2. **Use semantic color variables** - `text-foreground` not `text-white`
3. **Check contrast ratios** - Dark mode needs good readability
4. **Use opacity for subtle variations** - `dark:bg-scroll/10`
5. **Keep gold consistent** - Unifying accent across themes
6. **Test transitions** - Ensure smooth theme switching

### Don't:

1. **Don't use pure black** - Too harsh, use `#0a0a0a` or tehom
2. **Don't use pure white text** - Use off-white `#ededed`
3. **Don't forget dark: variants** - Every color class needs its dark pair
4. **Don't reduce contrast too much** - Readability is paramount
5. **Don't animate theme changes** - Can cause flashing

---

## Special Considerations

### Scripture Text

Scripture should remain highly readable in dark mode:

```jsx
<p className="
  font-crimson text-verse-lg
  text-tehom/80 dark:text-scroll
  leading-relaxed
">
  Scripture content...
</p>
```

### Images and Media

Consider providing dark-mode-friendly versions of images:

```jsx
<picture>
  <source
    srcSet="/images/logo-dark.svg"
    media="(prefers-color-scheme: dark)"
  />
  <img src="/images/logo-light.svg" alt="EUONGELION" />
</picture>
```

### Focus States

Ensure focus rings are visible in both modes:

```jsx
<button className="
  focus:outline-none
  focus:ring-2 focus:ring-gold/40
  focus:ring-offset-2
  focus:ring-offset-scroll dark:focus:ring-offset-tehom
">
```

### Borders and Dividers

Use opacity for consistent borders:

```jsx
// Instead of different colors
<div className="border-tehom-200 dark:border-tehom-700">

// Use opacity (more consistent)
<div className="border border-tehom/10 dark:border-scroll/10">
```

---

## Print Styles

When printing, override dark mode to light:

```css
@media print {
  body {
    background: white;
    color: black;
  }

  .dark {
    /* Reset dark mode styles for print */
    --background: white;
    --foreground: black;
  }
}
```

---

## Testing Checklist

### Visual Testing

- [ ] All text is readable (check contrast)
- [ ] Interactive elements are visible
- [ ] Focus states are clear
- [ ] Icons and graphics are visible
- [ ] Shadows work appropriately
- [ ] Gold accent stands out properly

### Functional Testing

- [ ] Theme toggle works correctly
- [ ] System preference is detected
- [ ] Theme persists across sessions
- [ ] No flash of wrong theme on load
- [ ] Transitions are smooth (or absent)

### Accessibility Testing

- [ ] WCAG AA contrast for all text
- [ ] Focus indicators visible
- [ ] Screen reader announces theme changes
- [ ] Reduced motion respects theme transitions

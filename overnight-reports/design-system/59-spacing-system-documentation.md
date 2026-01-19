# EUONGELION Spacing System Documentation

**Document:** 59-spacing-system-documentation.md
**Generated:** 2026-01-19
**Status:** Design System Reference

---

## Overview

EUONGELION's spacing system creates visual rhythm and hierarchy while maintaining the "sacred minimalism" aesthetic. Consistent spacing helps guide the reader's eye and creates a contemplative, uncluttered experience.

---

## Base Spacing Scale

EUONGELION extends Tailwind's default spacing scale with custom values optimized for reading layouts and page structure.

### Standard Tailwind Scale (4px base unit)

| Class | Value | Pixels | Usage |
|-------|-------|--------|-------|
| `0` | 0 | 0px | No spacing |
| `px` | 1px | 1px | Hairline borders |
| `0.5` | 0.125rem | 2px | Micro spacing |
| `1` | 0.25rem | 4px | Tight spacing |
| `1.5` | 0.375rem | 6px | Small gaps |
| `2` | 0.5rem | 8px | Compact spacing |
| `2.5` | 0.625rem | 10px | Small margins |
| `3` | 0.75rem | 12px | Default small |
| `3.5` | 0.875rem | 14px | Medium-small |
| `4` | 1rem | 16px | Base spacing |
| `5` | 1.25rem | 20px | Medium |
| `6` | 1.5rem | 24px | Standard |
| `7` | 1.75rem | 28px | Medium-large |
| `8` | 2rem | 32px | Large |
| `9` | 2.25rem | 36px | Extra large |
| `10` | 2.5rem | 40px | Section gaps |
| `11` | 2.75rem | 44px | Large sections |
| `12` | 3rem | 48px | Major sections |
| `14` | 3.5rem | 56px | Extra sections |
| `16` | 4rem | 64px | Page sections |
| `20` | 5rem | 80px | Large gaps |
| `24` | 6rem | 96px | Hero spacing |

### Custom EUONGELION Spacing

| Class | Value | Usage |
|-------|-------|-------|
| `18` | 4.5rem (72px) | Extended spacing |
| `88` | 22rem (352px) | Wide containers |
| `128` | 32rem (512px) | Full-width elements |

---

## Semantic Spacing Tokens

### Reading Layout Spacing

Optimized for content reading:

| Token | Value | Usage |
|-------|-------|-------|
| `reading-sm` | 1rem (16px) | Compact reading padding |
| `reading` | 1.5rem (24px) | Standard reading padding |
| `reading-lg` | 2rem (32px) | Generous reading padding |
| `reading-xl` | 3rem (48px) | Maximum reading padding |

```jsx
// Reading content with appropriate padding
<article className="px-reading py-reading-lg">
  <p>Devotional content...</p>
</article>
```

### Page Margins

Responsive page edge spacing:

| Token | Value | Usage |
|-------|-------|-------|
| `page-sm` | 1rem (16px) | Mobile margins |
| `page` | 2rem (32px) | Tablet margins |
| `page-lg` | 4rem (64px) | Desktop margins |
| `page-xl` | 6rem (96px) | Wide desktop margins |

```jsx
// Responsive page container
<main className="px-page-sm md:px-page lg:px-page-lg">
  Content
</main>
```

### Section Spacing

Vertical rhythm between major sections:

| Token | Value | Usage |
|-------|-------|-------|
| `section` | 4rem (64px) | Standard section gap |
| `section-lg` | 6rem (96px) | Large section gap |
| `section-xl` | 8rem (128px) | Hero/major sections |

```jsx
// Section with vertical spacing
<section className="py-section">
  Section content
</section>

// Hero section
<section className="py-section-xl">
  Hero content
</section>
```

---

## Component-Specific Spacing

### Cards

| Element | Spacing | Class |
|---------|---------|-------|
| Card padding | 24px | `p-6` |
| Card padding (small) | 16px | `p-4` |
| Card padding (large) | 32px | `p-8` |
| Card content gap | 16px | `gap-4` |
| Card header/footer | 16px bottom border padding | `pb-4` |

```jsx
<Card padding="md"> {/* p-6 */}
  <CardHeader>Title</CardHeader>
  <CardContent>Content</CardContent>
  <CardFooter>Actions</CardFooter>
</Card>
```

### Buttons

| Size | Horizontal Padding | Vertical | Height |
|------|-------------------|----------|--------|
| sm | 16px (`px-4`) | - | 36px (`h-9`) |
| md | 24px (`px-6`) | - | 48px (`h-12`) |
| lg | 32px (`px-8`) | - | 56px (`h-14`) |
| icon-sm | - | - | 36px (`h-9 w-9`) |
| icon | - | - | 44px (`h-11 w-11`) |
| icon-lg | - | - | 56px (`h-14 w-14`) |

### Form Elements

| Element | Spacing | Class |
|---------|---------|-------|
| Input padding | 16px horizontal, 12px vertical | `px-4 py-3` |
| Label margin bottom | 8px | `mb-2` |
| Field group gap | 24px | `space-y-6` |
| Form section gap | 32px | `space-y-8` |
| Error text margin top | 8px | `mt-2` |

### Navigation

| Element | Spacing | Class |
|---------|---------|-------|
| Header height | 56px | `h-14` |
| Header horizontal padding | 16px | `px-4` |
| Nav item padding | 12px horizontal, 8px vertical | `px-3 py-2` |
| Nav item gap | 4px | `gap-1` |
| Bottom nav height | 64px | `h-16` |

### Modals

| Element | Spacing | Class |
|---------|---------|-------|
| Modal padding | 24px | `p-6` |
| Modal header margin | 0 bottom padding | `pb-0` |
| Modal max width (md) | 28rem | `max-w-md` |
| Modal edge margin | 16px | `p-4` |

---

## Gap Utilities

### Flex/Grid Gaps

| Class | Value | Usage |
|-------|-------|-------|
| `gap-1` | 4px | Tight inline elements |
| `gap-2` | 8px | Compact lists |
| `gap-3` | 12px | Small groups |
| `gap-4` | 16px | Standard groups |
| `gap-6` | 24px | Spacious groups |
| `gap-8` | 32px | Section items |

```jsx
// Icon and text
<button className="flex items-center gap-2">
  <Icon /> Text
</button>

// Card list
<div className="flex flex-col gap-4">
  <Card>...</Card>
  <Card>...</Card>
</div>

// Navigation items
<nav className="flex items-center gap-1">
  <NavItem />
  <NavItem />
</nav>
```

---

## Margin Guidelines

### Margins Between Elements

| Relationship | Spacing | Reasoning |
|--------------|---------|-----------|
| Heading to paragraph | `mb-4` (16px) | Clear hierarchy |
| Paragraph to paragraph | `mt-4` (16px) | Reading flow |
| Section to section | `mt-8` to `mt-16` | Visual breaks |
| Icon to text | `mr-2` or `ml-2` | Inline alignment |
| Form field to field | `space-y-6` | Clear separation |

### Auto Margins

Use auto margins for centering:

```jsx
// Center horizontally
<div className="mx-auto max-w-2xl">Centered content</div>

// Push to end
<button className="ml-auto">Right-aligned</button>
```

---

## Padding Guidelines

### Container Padding

| Screen Size | Horizontal Padding | Class |
|-------------|-------------------|-------|
| Mobile (<640px) | 16px | `px-4` |
| Tablet (640-1024px) | 24px | `px-6` |
| Desktop (>1024px) | 32px+ | `px-8` |

### Content Area Padding

| Content Type | Padding | Class |
|--------------|---------|-------|
| Card content | 24px | `p-6` |
| Modal content | 24px | `p-6` |
| Drawer content | 24px | `p-6` |
| Alert/toast | 16px | `p-4` |
| Button (md) | 24px x 12px | `px-6 py-3` |

---

## Touch Target Sizing

For accessibility, interactive elements need minimum touch targets:

| Element | Minimum Size | EUONGELION Standard |
|---------|--------------|---------------------|
| Buttons | 44px | 48px (`h-12`) |
| Icon buttons | 44px | 44px (`h-11 w-11`) |
| Nav items | 44px | 44px+ |
| Form inputs | 44px | 48px |
| Checkbox/radio | 44px target | 44px tap area |

```jsx
// Proper touch target
<button className="h-12 min-w-[44px]">
  Tap-friendly
</button>

// Icon button with proper target
<button className="h-11 w-11 flex items-center justify-center">
  <Icon size="md" />
</button>
```

---

## Layout Patterns

### Standard Page Layout

```jsx
<main className="px-4 md:px-6 lg:px-8 py-4 pb-20">
  <div className="mx-auto max-w-2xl">
    {/* Content */}
  </div>
</main>
```

### Card Grid

```jsx
<div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4 md:gap-6">
  <Card>...</Card>
  <Card>...</Card>
  <Card>...</Card>
</div>
```

### Form Layout

```jsx
<form className="space-y-6">
  <div>
    <label className="block mb-2">Field</label>
    <input className="w-full px-4 py-3" />
  </div>
  <div>
    <label className="block mb-2">Field</label>
    <input className="w-full px-4 py-3" />
  </div>
  <button className="w-full mt-8">Submit</button>
</form>
```

### Reading Content

```jsx
<article className="max-w-reading mx-auto px-reading py-section">
  <h1 className="mb-8">Title</h1>
  <p className="mb-4">Paragraph...</p>
  <p className="mb-4">Paragraph...</p>
  <blockquote className="my-8">Quote</blockquote>
  <p className="mb-4">Paragraph...</p>
</article>
```

---

## Safe Areas

For mobile devices, account for notches and home indicators:

```jsx
// Header with safe area
<header className="safe-top">
  Content
</header>

// Bottom nav with safe area
<nav className="safe-bottom">
  Navigation
</nav>
```

CSS implementation:

```css
.safe-top {
  padding-top: env(safe-area-inset-top);
}

.safe-bottom {
  padding-bottom: env(safe-area-inset-bottom);
}
```

---

## Border Radius

| Token | Value | Usage |
|-------|-------|-------|
| `rounded` | 4px | Default small |
| `rounded-md` | 6px | Medium |
| `rounded-lg` | 8px | Cards, containers |
| `rounded-xl` | 12px | Modals, large cards |
| `rounded-2xl` | 16px | Hero cards |
| `rounded-4xl` | 32px | Very large (custom) |
| `rounded-card` | 12px (0.75rem) | Card default |
| `rounded-button` | 8px (0.5rem) | Button default |
| `rounded-input` | 6px (0.375rem) | Input default |
| `rounded-full` | 9999px | Pills, avatars |

---

## Spacing Do's and Don'ts

### Do:

- Use consistent spacing from the scale
- Maintain vertical rhythm with consistent margins
- Use semantic spacing tokens for layouts
- Account for touch targets on interactive elements
- Add extra padding on mobile for comfort

### Don't:

- Use arbitrary pixel values (`p-[17px]`)
- Mix different spacing systems
- Compress spacing on mobile - if anything, increase it
- Forget about safe areas on modern devices
- Neglect spacing between icon and text

---

## Quick Reference

### Common Patterns

```jsx
// Page container
<div className="px-4 md:px-6 lg:px-8 py-4 mx-auto max-w-2xl">

// Section spacing
<section className="py-section">

// Card
<div className="p-6 rounded-card">

// Flex with gap
<div className="flex items-center gap-2">

// Form field
<div className="space-y-6">
  <div>
    <label className="block mb-2" />
    <input className="px-4 py-3" />
  </div>
</div>

// Button group
<div className="flex gap-3 mt-4">

// Icon + text
<span className="flex items-center gap-2">
  <Icon /> Label
</span>

// Stacked content
<div className="space-y-4">
```

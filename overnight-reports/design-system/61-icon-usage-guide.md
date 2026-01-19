# EUONGELION Icon Usage Guide

**Document:** 61-icon-usage-guide.md
**Generated:** 2026-01-19
**Status:** Design System Reference

---

## Overview

EUONGELION uses a custom icon system built on SVG components with consistent sizing, accessibility features, and the ability to inherit color from parent elements. The icons are designed to be simple, clear, and unobtrusive - supporting the "sacred minimalism" aesthetic.

---

## Icon Library Structure

The icon library is organized by category:

```
/app/components/icons/
├── Icon.tsx           # Base icon wrapper component
├── navigation/        # Navigation icons
│   ├── Home.tsx
│   ├── Search.tsx
│   ├── Settings.tsx
│   ├── Menu.tsx
│   ├── Close.tsx
│   ├── Back.tsx
│   └── Forward.tsx
├── actions/           # Action icons
│   ├── Share.tsx
│   ├── Bookmark.tsx
│   ├── BookmarkFilled.tsx
│   ├── Copy.tsx
│   ├── Download.tsx
│   ├── Edit.tsx
│   └── Delete.tsx
├── reading/           # Reading-related icons
│   ├── Book.tsx
│   ├── Chapter.tsx
│   ├── Verse.tsx
│   ├── Quote.tsx
│   └── Highlight.tsx
├── progress/          # Progress indicators
│   ├── Check.tsx
│   ├── CheckCircle.tsx
│   ├── Circle.tsx
│   ├── Clock.tsx
│   ├── Calendar.tsx
│   └── Streak.tsx
├── user/              # User-related icons
│   ├── User.tsx
│   ├── UserCircle.tsx
│   ├── Login.tsx
│   └── Logout.tsx
├── social/            # Social sharing icons
│   ├── Twitter.tsx
│   ├── Facebook.tsx
│   ├── Link.tsx
│   └── Email.tsx
├── ui/                # UI element icons
│   ├── ChevronUp.tsx
│   ├── ChevronDown.tsx
│   ├── ChevronLeft.tsx
│   ├── ChevronRight.tsx
│   ├── Plus.tsx
│   └── Minus.tsx
└── status/            # Status icons
    ├── Info.tsx
    ├── Warning.tsx
    ├── Error.tsx
    └── Success.tsx
```

---

## Base Icon Component

### Icon.tsx API

```typescript
export type IconSize = 'xs' | 'sm' | 'md' | 'lg' | 'xl' | '2xl';

export interface IconProps extends React.SVGProps<SVGSVGElement> {
  /**
   * Size of the icon
   * xs: 12px, sm: 16px, md: 20px, lg: 24px, xl: 32px, 2xl: 48px
   */
  size?: IconSize;

  /**
   * Custom className for additional styling
   */
  className?: string;

  /**
   * Accessible label for the icon (required when icon has meaning)
   * When not provided, icon is treated as decorative (aria-hidden)
   */
  label?: string;

  /**
   * Override the default color (inherits from parent by default)
   */
  color?: string;
}
```

### Size Scale

| Size | Pixels | rem | Usage |
|------|--------|-----|-------|
| `xs` | 12px | 0.75rem | Inline with small text |
| `sm` | 16px | 1rem | Compact UI, labels |
| `md` | 20px | 1.25rem | **Default**, buttons, nav |
| `lg` | 24px | 1.5rem | Primary actions, emphasis |
| `xl` | 32px | 2rem | Feature icons, empty states |
| `2xl` | 48px | 3rem | Hero icons, illustrations |

---

## Using Icons

### Basic Usage

```jsx
import { Share } from '@/components/icons/actions/Share';
import { Home } from '@/components/icons/navigation/Home';

// Default size (md = 20px)
<Share />

// With specific size
<Home size="lg" />

// With color override
<Share color="#C19A6B" />
```

### With Accessible Label

When an icon conveys meaning that isn't duplicated by visible text, provide a label:

```jsx
// Decorative icon (no label needed - text explains it)
<button>
  <Share /> Share
</button>

// Meaningful icon (needs label)
<button aria-label="Share this devotional">
  <Share label="Share this devotional" />
</button>

// Icon-only button
<button>
  <Share label="Share" />
</button>
```

### Inheriting Color

Icons inherit `currentColor` by default, making them easy to style:

```jsx
// Icon inherits text-gold color
<button className="text-gold">
  <Share /> {/* Will be gold */}
</button>

// Icon changes color on hover
<button className="text-olive hover:text-gold transition-colors">
  <Bookmark />
</button>
```

---

## When to Use Icons vs Text

### Use Icons When:

1. **Space is limited** - Mobile nav, compact buttons
2. **Action is universal** - Share, bookmark, close
3. **Quick recognition needed** - Navigation, status
4. **Supporting text** - Icon + label together

### Use Text When:

1. **Action is specific** - "Start 7-Day Challenge"
2. **Meaning is unclear** - Not a universal symbol
3. **Primary CTA** - Main buttons should have text
4. **Accessibility is critical** - Text is always clearer

### Icon + Text (Recommended)

The best practice is combining icon with text:

```jsx
// Clear and accessible
<button className="flex items-center gap-2">
  <Share size="sm" /> Share
</button>

// Navigation with labels
<nav>
  <Link className="flex flex-col items-center">
    <Home size="lg" />
    <span className="text-xs">Today</span>
  </Link>
</nav>
```

---

## Icon Categories and Usage

### Navigation Icons

| Icon | Usage | Notes |
|------|-------|-------|
| `Home` | Home/Today page | Sun symbol for daily devotional |
| `Search` | Search function | Magnifying glass |
| `Settings` | Settings page | Gear/cog |
| `Menu` | Hamburger menu | Three horizontal lines |
| `Close` | Close modal/drawer | X mark |
| `Back` | Navigate back | Left chevron |
| `Forward` | Navigate forward | Right chevron |

### Action Icons

| Icon | Usage | Notes |
|------|-------|-------|
| `Share` | Share content | Connected dots |
| `Bookmark` | Save for later (outline) | Unfilled bookmark |
| `BookmarkFilled` | Saved item (filled) | Filled bookmark |
| `Copy` | Copy to clipboard | Overlapping rectangles |
| `Download` | Download content | Arrow pointing down |
| `Edit` | Edit content | Pencil |
| `Delete` | Remove item | Trash can |

### Reading Icons

| Icon | Usage | Notes |
|------|-------|-------|
| `Book` | Series/devotional | Open book |
| `Chapter` | Chapter indicator | Document with lines |
| `Verse` | Verse marker | Quote marks |
| `Quote` | Blockquote | Large quote mark |
| `Highlight` | Text highlight | Marker/highlighter |

### Progress Icons

| Icon | Usage | Notes |
|------|-------|-------|
| `Check` | Completed task | Simple checkmark |
| `CheckCircle` | Completed (emphasized) | Check in circle |
| `Circle` | Incomplete/pending | Empty circle |
| `Clock` | Time/duration | Clock face |
| `Calendar` | Date/schedule | Calendar grid |
| `Streak` | Streak indicator | Flame |

### Status Icons

| Icon | Usage | Notes |
|------|-------|-------|
| `Info` | Information | Circle with "i" |
| `Warning` | Warning message | Triangle with "!" |
| `Error` | Error state | Circle with "x" |
| `Success` | Success state | Circle with check |

---

## Styling Patterns

### Icon Buttons

```jsx
// Minimal icon button
<button className="p-2 rounded-full hover:bg-tehom/5 transition-colors">
  <Bookmark size="md" />
</button>

// Icon button with background
<button className="p-3 bg-gold/10 rounded-lg hover:bg-gold/20 transition-colors">
  <Share size="md" className="text-gold" />
</button>

// Icon button with explicit sizing (touch target)
<button className="h-11 w-11 flex items-center justify-center rounded-full">
  <Settings size="md" />
</button>
```

### Icons in Buttons

```jsx
// Icon before text
<button className="flex items-center gap-2 px-4 py-2">
  <Share size="sm" />
  <span>Share</span>
</button>

// Icon after text
<button className="flex items-center gap-2 px-4 py-2">
  <span>Continue</span>
  <ChevronRight size="sm" />
</button>
```

### Icons in Lists

```jsx
<ul className="space-y-2">
  <li className="flex items-center gap-3">
    <CheckCircle size="md" className="text-olive" />
    <span>Completed item</span>
  </li>
  <li className="flex items-center gap-3">
    <Circle size="md" className="text-tehom/30" />
    <span>Pending item</span>
  </li>
</ul>
```

### Status Indicators

```jsx
// Success message
<div className="flex items-start gap-3 p-4 bg-olive/10 rounded-lg">
  <Success size="md" className="text-olive flex-shrink-0" />
  <p>Your changes have been saved.</p>
</div>

// Error message
<div className="flex items-start gap-3 p-4 bg-burgundy/10 rounded-lg">
  <Error size="md" className="text-burgundy flex-shrink-0" />
  <p>Something went wrong.</p>
</div>
```

---

## Inline SVG Icons

Many components use inline SVGs for simple cases. Follow these patterns:

### Standard Inline SVG

```jsx
<svg
  className="h-5 w-5"
  fill="none"
  viewBox="0 0 24 24"
  stroke="currentColor"
  strokeWidth={2}
>
  <path
    strokeLinecap="round"
    strokeLinejoin="round"
    d="M9 5l7 7-7 7"
  />
</svg>
```

### Filled vs Stroked

```jsx
// Stroked icon (default, outline style)
<svg
  fill="none"
  stroke="currentColor"
  strokeWidth={2}
>
  {/* paths */}
</svg>

// Filled icon (solid style)
<svg
  fill="currentColor"
  viewBox="0 0 24 24"
>
  {/* paths */}
</svg>
```

---

## Accessibility

### Decorative Icons

Icons that don't add meaning should be hidden from screen readers:

```jsx
// Automatically handled by Icon component when no label is provided
<Icon aria-hidden="true" role="presentation">
  {children}
</Icon>
```

### Meaningful Icons

Icons that convey information need accessible labels:

```jsx
// Using label prop
<Share label="Share this devotional" />

// Renders as:
<svg aria-hidden="false" aria-label="Share this devotional" role="img">
```

### Icon-Only Buttons

Always provide accessible text for icon-only buttons:

```jsx
// Option 1: aria-label on button
<button aria-label="Share">
  <Share />
</button>

// Option 2: Visually hidden text
<button>
  <Share />
  <span className="sr-only">Share</span>
</button>

// Option 3: Label on icon
<button>
  <Share label="Share" />
</button>
```

---

## Creating New Icons

### Using createIcon Helper

```typescript
import { createIcon } from '@/components/icons/Icon';

export const CustomIcon = createIcon(
  'CustomIcon',
  <path d="M12 2L2 7l10 5 10-5-10-5z" />,
  { /* default props */ }
);
```

### Manual Icon Component

```typescript
'use client';

import React from 'react';
import { Icon, IconProps } from '../Icon';

export const CustomIcon = React.forwardRef<SVGSVGElement, IconProps>(
  (props, ref) => (
    <Icon ref={ref} {...props}>
      <path d="..." />
      <circle cx="12" cy="12" r="3" />
    </Icon>
  )
);

CustomIcon.displayName = 'CustomIcon';

export default CustomIcon;
```

### Icon Guidelines

1. **ViewBox**: Use 24x24 viewBox for consistency
2. **Stroke Width**: Default to strokeWidth={2}
3. **Line Caps**: Use `strokeLinecap="round"` and `strokeLinejoin="round"`
4. **Color**: Use `currentColor` for stroke/fill
5. **Simplicity**: Keep icons simple with minimal paths

---

## Icon Sizing Quick Reference

| Context | Size | Class/Prop |
|---------|------|------------|
| Inline with text | `sm` (16px) | `size="sm"` |
| Buttons (default) | `md` (20px) | `size="md"` |
| Navigation items | `lg` (24px) | `size="lg"` |
| Icon-only buttons | `md-lg` | `h-5 w-5` or `h-6 w-6` |
| Feature icons | `xl` (32px) | `size="xl"` |
| Hero/empty states | `2xl` (48px) | `size="2xl"` |

---

## Common Patterns

### Bottom Navigation

```jsx
<nav className="flex justify-around">
  {navItems.map((item) => (
    <Link
      href={item.href}
      className={`flex flex-col items-center py-2 ${
        isActive ? 'text-gold' : 'text-tehom/60 hover:text-tehom'
      }`}
    >
      {isActive ? item.activeIcon : item.icon}
      <span className="mt-1 text-xs font-medium">{item.label}</span>
    </Link>
  ))}
</nav>
```

### Header Actions

```jsx
<div className="flex items-center gap-1">
  <button className="h-10 w-10 flex items-center justify-center rounded-full hover:bg-tehom/5">
    <Bookmark size="md" />
  </button>
  <Link href="/settings" className="h-10 w-10 flex items-center justify-center rounded-full hover:bg-tehom/5">
    <Settings size="md" />
  </Link>
</div>
```

### Toggle States

```jsx
// Bookmark toggle
<button onClick={toggleBookmark}>
  {isBookmarked ? (
    <BookmarkFilled size="md" className="text-gold" />
  ) : (
    <Bookmark size="md" className="text-tehom/60" />
  )}
</button>
```

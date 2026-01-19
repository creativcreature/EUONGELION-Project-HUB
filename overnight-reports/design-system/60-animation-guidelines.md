# EUONGELION Animation Guidelines

**Document:** 60-animation-guidelines.md
**Generated:** 2026-01-19
**Status:** Design System Reference

---

## Animation Philosophy

> "Gentle, never distracting."

EUONGELION animations serve the contemplative experience. They should:

- **Guide attention** without demanding it
- **Feel natural** like a page turning or light shifting
- **Respect the sacred** - no flashy or playful animations
- **Honor accessibility** - always respect reduced motion preferences
- **Enhance understanding** - show relationships between elements

Animation should feel like a gentle breath, not a startling interruption.

---

## Core Animation Principles

### 1. Subtlety Over Spectacle

- Small movements (10-20px maximum translation)
- Opacity changes rather than dramatic transforms
- Slow enough to notice, fast enough not to wait

### 2. Purposeful Motion

Every animation must answer: "What does this help the user understand?"

| Purpose | Example |
|---------|---------|
| **State change** | Button hover, checkbox toggle |
| **Attention guidance** | Focus ring, error shake |
| **Spatial orientation** | Drawer slide, modal appear |
| **Progress indication** | Loading spinner, progress bar |
| **Feedback** | Success checkmark, copy confirmation |

### 3. Consistency

- Same duration for same purposes
- Same easing for same types of motion
- Same direction patterns throughout

---

## Animation Durations

### Standard Duration Scale

| Duration | Value | Usage |
|----------|-------|-------|
| `instant` | 0ms | Disabled animations, reduced motion |
| `fast` | 150ms | Micro-interactions, hover states |
| `normal` | 300ms | Standard transitions, state changes |
| `slow` | 500ms | Page transitions, reveals |
| `slower` | 800ms | Complex animations, breathing effects |

### Duration Constants (TypeScript)

```typescript
export const MOTION_DURATIONS = {
  instant: 0,
  fast: 150,
  normal: 300,
  slow: 500,
  slower: 800,
} as const;
```

### Duration Guidelines

| Animation Type | Recommended Duration |
|----------------|---------------------|
| Hover/focus states | 150-200ms |
| Button press | 100-150ms |
| Modal appear | 200-300ms |
| Slide transitions | 300-400ms |
| Fade in/out | 200-500ms |
| Loading spinners | Continuous at 1-2s cycle |
| Breathing effects | 2000ms+ |

---

## Easing Functions

### Recommended Easings

| Easing | CSS Value | Usage |
|--------|-----------|-------|
| `ease-out` | `cubic-bezier(0, 0, 0.2, 1)` | Elements entering (default) |
| `ease-in` | `cubic-bezier(0.4, 0, 1, 1)` | Elements exiting |
| `ease-in-out` | `cubic-bezier(0.4, 0, 0.2, 1)` | Symmetrical transitions |
| `ease-out-cubic` | `cubic-bezier(0.33, 1, 0.68, 1)` | Smooth deceleration |

### When to Use Each

- **ease-out**: Default for most animations (entering, appearing)
- **ease-in**: Elements leaving the screen
- **ease-in-out**: Continuous/looping animations
- **linear**: Progress bars, loading indicators

---

## Defined Animations

### From Tailwind Config

```typescript
animation: {
  'fade-in': 'fadeIn 0.5s ease-out',
  'fade-up': 'fadeUp 0.4s ease-out',
  'slide-up': 'slideUp 0.5s ease-out',
  'slide-down': 'slideDown 0.3s ease-out',
  'scale-in': 'scaleIn 0.2s ease-out',
  'pulse-glow': 'pulseGlow 2s ease-in-out infinite',
},

keyframes: {
  fadeIn: {
    '0%': { opacity: '0' },
    '100%': { opacity: '1' },
  },
  fadeUp: {
    '0%': { opacity: '0', transform: 'translateY(10px)' },
    '100%': { opacity: '1', transform: 'translateY(0)' },
  },
  slideUp: {
    '0%': { opacity: '0', transform: 'translateY(10px)' },
    '100%': { opacity: '1', transform: 'translateY(0)' },
  },
  slideDown: {
    '0%': { opacity: '0', transform: 'translateY(-10px)' },
    '100%': { opacity: '1', transform: 'translateY(0)' },
  },
  scaleIn: {
    '0%': { opacity: '0', transform: 'scale(0.95)' },
    '100%': { opacity: '1', transform: 'scale(1)' },
  },
  pulseGlow: {
    '0%, 100%': { boxShadow: '0 0 20px rgba(193, 154, 107, 0.3)' },
    '50%': { boxShadow: '0 0 30px rgba(193, 154, 107, 0.5)' },
  },
},
```

### From globals.css

```css
@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}

@keyframes slideUp {
  from {
    opacity: 0;
    transform: translateY(10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.animate-fade-in {
  animation: fadeIn 0.3s ease-out;
}

.animate-slide-up {
  animation: slideUp 0.4s ease-out;
}
```

---

## Animation Usage

### What to Animate

| Element | Animation | Why |
|---------|-----------|-----|
| Page load content | `animate-fade-in` | Soft entrance, not jarring |
| Cards appearing | `animate-fade-up` | Subtle upward reveal |
| Modals | `animate-scale-in` | Draw attention gently |
| Dropdowns | `animate-slide-down` | Show spatial relationship |
| Toasts | `animate-slide-up` | Enter from notification area |
| Progress bars | `transition-all` | Smooth progress indication |
| Hover states | `transition-colors` | Responsive feedback |
| Focus rings | `transition-all` | Accessible focus indication |

### What NOT to Animate

- **Text content** - Never animate reading text
- **Scripture** - Absolutely no animation on biblical text
- **Form validation** - Keep error states static (except initial appearance)
- **Navigation** - Keep nav stable and predictable
- **Large images** - Performance concern
- **Continuous animations** - Only for loading states

---

## Reduced Motion Support

### Mandatory Implementation

EUONGELION **must** respect the user's `prefers-reduced-motion` setting.

### Using the useReducedMotion Hook

```typescript
import { useReducedMotion } from '@/hooks/useReducedMotion';

function AnimatedComponent() {
  const [prefersReducedMotion, isLoading] = useReducedMotion();

  if (isLoading) return null;

  return (
    <div
      style={{
        transition: prefersReducedMotion ? 'none' : 'transform 300ms ease-out'
      }}
    >
      Content
    </div>
  );
}
```

### Motion-Safe Utility Classes

```typescript
export const motionSafeClasses = {
  fadeIn: 'motion-safe:animate-fade-in motion-reduce:animate-none',
  fadeUp: 'motion-safe:animate-fade-up motion-reduce:animate-none',
  scaleIn: 'motion-safe:animate-scale-in motion-reduce:animate-none',
  transition: 'motion-safe:transition-all motion-reduce:transition-none',
  transform: 'motion-safe:transform motion-reduce:transform-none',
};
```

### React Components for Motion Preference

```jsx
import { Motion, NoMotion, MotionSafe } from '@/components/a11y/ReducedMotion';

// Show different content based on preference
<Motion fallback={<StaticImage />}>
  <AnimatedImage />
</Motion>

// Apply different classes
<MotionSafe
  motionClassName="animate-fade-in duration-300"
  reducedMotionClassName="opacity-100"
>
  <Card />
</MotionSafe>
```

### Getting Motion-Safe Duration

```typescript
import { getMotionDuration, useMotionConfig } from '@/hooks/useReducedMotion';

// Returns 0 if reduced motion is preferred
const duration = getMotionDuration(300, prefersReducedMotion);

// Or use the hook
const { duration, shouldAnimate, transition } = useMotionConfig({
  duration: 300,
  delay: 0,
  ease: 'easeOut',
});
```

---

## Transition Properties

### CSS Transition Classes

```css
/* Quick transitions for hover/focus */
.transition-colors {
  transition: color, background-color, border-color 150ms ease-out;
}

/* Standard all-property transition */
.transition-all {
  transition: all 200ms ease-out;
}

/* Custom duration */
.transition-all.duration-300 {
  transition-duration: 300ms;
}
```

### Tailwind Transition Utilities

```jsx
// Color transitions (hover states)
<button className="transition-colors duration-200">

// Transform transitions
<div className="transition-transform duration-300">

// All properties
<div className="transition-all duration-200 ease-out">

// Specific properties
<div className="transition-opacity duration-500">
```

---

## Component-Specific Animation Patterns

### Cards

```jsx
// Hover lift effect
<div className="transition-all duration-200 ease-out hover:shadow-lg hover:-translate-y-0.5">
  Card content
</div>

// The devotional-card class from globals.css
.devotional-card {
  transition: box-shadow 0.2s ease, transform 0.2s ease;
}
.devotional-card:hover {
  box-shadow: var(--shadow-md);
  transform: translateY(-2px);
}
```

### Buttons

```jsx
// Scale on press
<button className="transition-all duration-200 active:scale-[0.98]">

// Focus ring transition
<button className="transition-all focus:ring-2 focus:ring-gold/40">
```

### Modals

```jsx
// Backdrop fade
<div className="animate-in fade-in duration-200" />

// Modal scale
<div className="animate-in fade-in zoom-in-95 duration-200" />
```

### Progress Indicators

```jsx
// Progress bar fill
<div className="transition-all duration-500 ease-out-cubic" style={{ width: `${progress}%` }} />

// Step indicator
<div className="transition-all duration-300" />
```

### Loading States

```jsx
// Pulse animation for loading
<div className="animate-pulse" />

// Spinner
<svg className="animate-spin" />

// Processing dots
<div className="animate-pulse" style={{ animationDelay: `${index * 200}ms` }} />
```

### Breathing Indicator (Contemplative)

```jsx
// For processing/thinking states
<div className="animate-breath" />

// CSS
@keyframes breath {
  0%, 100% { transform: scale(1); opacity: 0.3; }
  50% { transform: scale(1.1); opacity: 0.5; }
}
```

---

## Performance Considerations

### Prefer Transforms and Opacity

These properties are GPU-accelerated and don't trigger layout:

```jsx
// Good - GPU accelerated
transform: translateY(10px)
opacity: 0

// Avoid - triggers layout
top: 10px
height: 100px
margin-top: 10px
```

### Use `will-change` Sparingly

```css
/* Only for complex animations */
.complex-animation {
  will-change: transform, opacity;
}
```

### Avoid Animating

- `width`, `height` (use `transform: scale()` instead)
- `top`, `left`, `right`, `bottom` (use `transform: translate()`)
- `margin`, `padding`
- Layout properties

---

## Animation Timing Reference

### Quick Reference Table

| Animation | Duration | Easing | Class |
|-----------|----------|--------|-------|
| Hover color | 150ms | ease-out | `transition-colors duration-150` |
| Hover lift | 200ms | ease-out | `transition-all duration-200` |
| Button press | 100ms | ease-out | `active:scale-[0.98]` |
| Fade in | 300-500ms | ease-out | `animate-fade-in` |
| Slide up | 400ms | ease-out | `animate-slide-up` |
| Modal appear | 200ms | ease-out | `animate-in fade-in zoom-in-95 duration-200` |
| Toast enter | 300ms | ease-out | `animate-slide-up` |
| Progress fill | 500ms | ease-out-cubic | `duration-500 ease-out-cubic` |
| Focus ring | 150ms | ease-out | `transition-all duration-150` |

---

## Testing Animations

### Checklist

1. [ ] Test with reduced motion enabled (OS settings)
2. [ ] Test on slower devices (throttle in DevTools)
3. [ ] Verify animations don't delay user actions
4. [ ] Check animations don't cause layout shifts
5. [ ] Ensure loading states have appropriate animations
6. [ ] Verify focus states are visible and animated

### Testing Reduced Motion

```bash
# Chrome DevTools
# Rendering tab > Emulate CSS media feature prefers-reduced-motion: reduce

# macOS
# System Preferences > Accessibility > Display > Reduce motion

# Windows
# Settings > Ease of Access > Display > Show animations in Windows
```

---

## Summary

### The EUONGELION Animation Ethos

1. **Gentle** - Soft, subtle movements
2. **Purposeful** - Every animation has a reason
3. **Respectful** - Honor reduced motion preferences
4. **Consistent** - Same patterns throughout
5. **Performant** - GPU-accelerated, no jank
6. **Sacred** - Never distract from the devotional experience

When in doubt, animate less. The best animation is often no animation at all - just a simple, instant state change that respects the user's time and attention.

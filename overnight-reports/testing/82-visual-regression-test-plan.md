# EUONGELION Visual Regression Test Plan

**Document ID:** 82-visual-regression-test-plan.md
**Created:** 2026-01-19
**Recommended Tools:** Playwright Visual Comparisons, Chromatic, Percy, or Storybook
**Design System:** Tailwind CSS with custom design tokens

---

## 1. Executive Summary

This document identifies components requiring visual regression testing, specifies viewport sizes, component states to capture, and comparison thresholds for the EUONGELION application.

### Visual Testing Goals

- Prevent unintended UI changes
- Ensure consistent appearance across themes (dark, light, sepia)
- Verify responsive behavior at all breakpoints
- Catch styling regressions before production

---

## 2. Viewport Sizes

### Standard Breakpoints (Tailwind Defaults + Custom)

| Name | Width | Height | Device Type |
|------|-------|--------|-------------|
| xs | 320px | 568px | iPhone SE (small mobile) |
| sm | 375px | 667px | iPhone 8 (standard mobile) |
| md | 768px | 1024px | iPad (tablet portrait) |
| lg | 1024px | 768px | iPad landscape / small laptop |
| xl | 1280px | 800px | Desktop |
| 2xl | 1536px | 864px | Large desktop |

### Additional Test Viewports

| Name | Width | Height | Use Case |
|------|-------|--------|----------|
| mobile-landscape | 667px | 375px | Mobile landscape reading |
| tablet-portrait | 834px | 1112px | iPad Pro portrait |
| tablet-landscape | 1112px | 834px | iPad Pro landscape |
| foldable-closed | 280px | 653px | Galaxy Fold closed |
| foldable-open | 717px | 512px | Galaxy Fold open |

---

## 3. Theme Variants

Every component must be tested in all three themes:

| Theme | Background | Text | Use Case |
|-------|------------|------|----------|
| dark | tehom (#1A1612) | scroll (#E8E0D3) | Default, night reading |
| light | #F7F3ED | Dark text | Day reading |
| sepia | #F5ECD7 | Dark brown | Comfortable reading |

---

## 4. Comparison Thresholds

### Default Thresholds

| Comparison Type | Threshold | Notes |
|-----------------|-----------|-------|
| Pixel difference | 0.1% | Very strict for UI components |
| Anti-aliasing tolerance | 0.2% | Allow for font rendering |
| Color difference | 0.05 | Strict color matching |

### Component-Specific Thresholds

| Component | Threshold | Reason |
|-----------|-----------|--------|
| Typography | 0.3% | Font rendering varies |
| Icons | 0.1% | SVGs should be exact |
| Animations (still frames) | 0.5% | Animation timing variance |
| Charts/Graphs | 0.5% | Data visualization variance |
| User-generated content | 1.0% | Content may vary |

---

## 5. UI Components

### 5.1 Button (`components/ui/Button.tsx`)

**Priority: HIGH**

| State | Description | Variants to Capture |
|-------|-------------|---------------------|
| default | Normal state | primary, secondary, ghost, outline, danger, link |
| hover | Mouse over | All variants |
| active | Being clicked | All variants |
| focus | Keyboard focus | All variants (focus ring visible) |
| disabled | Cannot interact | All variants (opacity 50%) |
| loading | In progress | All variants (spinner visible) |

**Sizes to Capture:** sm, md, lg, icon, iconSm, iconLg

**Props to Test:**
- With left icon
- With right icon
- Full width
- With loading text

**Viewports:** xs, md, xl

---

### 5.2 Card (`components/ui/Card.tsx`)

**Priority: HIGH**

| State | Description | Variants to Capture |
|-------|-------------|---------------------|
| default | Normal card | default, elevated, outlined, ghost, glass |
| interactive | Clickable card | hover, active, focus states |

**Sub-components:**
- CardHeader
- CardTitle (h1-h6)
- CardDescription
- CardContent
- CardFooter

**Props to Test:**
- padding: none, sm, md, lg
- With/without header
- With/without footer

**Viewports:** xs, sm, md, lg, xl

---

### 5.3 Modal (`components/ui/Modal.tsx`)

**Priority: HIGH**

| State | Description |
|-------|-------------|
| open | Modal visible with backdrop |
| with-title | Title and description present |
| with-actions | Action buttons in footer |
| scrollable | Content overflows |

**Sizes:** sm, md, lg, xl, full

**Props to Test:**
- With/without close button
- With/without title
- With/without description
- With long content (scroll)

**Viewports:** xs, sm, md, lg

---

### 5.4 Toast (`components/ui/Toast.tsx`)

**Priority: MEDIUM**

| State | Description |
|-------|-------------|
| success | Green checkmark |
| error | Red warning |
| info | Blue info icon |
| warning | Yellow warning |

**Props to Test:**
- With action button
- With dismiss button
- Long message (multiline)

**Viewports:** xs, md

---

### 5.5 Skeleton (`components/ui/Skeleton.tsx`)

**Priority: LOW**

| State | Description |
|-------|-------------|
| default | Pulse animation (single frame) |
| text | Multiple lines |
| circle | Avatar placeholder |
| card | Full card skeleton |

**Viewports:** xs, md, xl

---

### 5.6 Drawer (`components/ui/Drawer.tsx`)

**Priority: MEDIUM**

| State | Description |
|-------|-------------|
| open-left | Drawer from left |
| open-right | Drawer from right |
| open-bottom | Drawer from bottom |
| with-content | Navigation content |

**Viewports:** xs, sm, md

---

## 6. Navigation Components

### 6.1 Navigation Bar

**Priority: HIGH**
**Path:** `components/navigation/`

| State | Description |
|-------|-------------|
| default | Normal state |
| scrolled | After scroll (sticky/shadow) |
| with-streak | Streak indicator visible |
| authenticated | User avatar shown |
| unauthenticated | Login button shown |

**Viewports:** xs (hamburger), md (partial), xl (full)

---

### 6.2 Bottom Navigation (Mobile)

**Priority: HIGH**

| State | Description |
|-------|-------------|
| default | All tabs visible |
| active-home | Home tab active |
| active-series | Series tab active |
| active-progress | Progress tab active |
| active-settings | Settings tab active |
| with-badge | Notification badge |

**Viewports:** xs, sm

---

### 6.3 Breadcrumbs

**Priority: LOW**

| State | Description |
|-------|-------------|
| single-level | Home only |
| multi-level | Home > Series > Day |
| truncated | Long paths |

**Viewports:** xs, md, xl

---

## 7. Devotional Components

### 7.1 DevotionalCard

**Priority: HIGH**
**Path:** `components/devotional/`

| State | Description |
|-------|-------------|
| default | Basic card |
| with-thumbnail | Image present |
| without-thumbnail | No image |
| with-series | Series badge visible |
| bookmarked | Bookmark icon filled |
| completed | Completion badge |
| in-progress | Progress indicator |

**Props to Test:**
- showSeries: true/false
- showTags: true/false
- With 1, 3, 5+ tags

**Viewports:** xs, sm, md, lg (grid layouts)

---

### 7.2 Scripture Display

**Priority: HIGH**

| State | Description |
|-------|-------------|
| single-verse | John 3:16 |
| verse-range | John 3:16-21 |
| chapter-reference | Psalm 23 |
| with-translation | ESV badge |

**Typography Test:**
- Verse numbers
- Reference formatting
- Long passages

**Viewports:** xs, md, xl

---

### 7.3 Immersion Level Selector

**Priority: HIGH**

| State | Description |
|-------|-------------|
| 1-minute-selected | Quick option active |
| 5-minute-selected | Standard option active |
| 15-minute-selected | Deep dive active |

**Viewports:** xs, md

---

### 7.4 Reading Progress Bar

**Priority: MEDIUM**

| State | Description |
|-------|-------------|
| 0% | Just started |
| 50% | Halfway |
| 100% | Complete |
| animated | Progress filling |

**Viewports:** xs, md, xl

---

### 7.5 Reflection Questions

**Priority: MEDIUM**

| State | Description |
|-------|-------------|
| empty | No answer |
| with-answer | User response |
| answered | Saved response |

**Viewports:** xs, md

---

## 8. Progress Components

### 8.1 Streak Display

**Priority: HIGH**

| State | Description |
|-------|-------------|
| no-streak | 0 days |
| active-streak | 1+ days (fire icon) |
| milestone | 7, 14, 30, 100 days |
| at-risk | Missed today (warning) |

**Props:**
- Small (header)
- Large (progress page)
- With celebration animation (still frame)

**Viewports:** xs, md

---

### 8.2 Progress Calendar

**Priority: MEDIUM**

| State | Description |
|-------|-------------|
| empty-month | No activity |
| partial-month | Some days completed |
| full-month | All days completed |
| current-day | Today highlighted |

**Viewports:** xs, sm, md

---

### 8.3 Statistics Cards

**Priority: MEDIUM**

| State | Description |
|-------|-------------|
| total-completed | Number display |
| time-spent | Duration display |
| series-progress | Percentage display |

**Viewports:** xs, md

---

## 9. Series Components

### 9.1 SeriesCard

**Priority: HIGH**

| State | Description |
|-------|-------------|
| not-started | No progress |
| in-progress | Partial completion |
| completed | 100% done |
| with-thumbnail | Image present |

**Viewports:** xs, sm, md, lg

---

### 9.2 Series Progress Bar

**Priority: MEDIUM**

| State | Description |
|-------|-------------|
| 0% | Just started |
| 30% | Early progress |
| 70% | Near completion |
| 100% | Complete |

**Viewports:** xs, md

---

### 9.3 Day List/Grid

**Priority: MEDIUM**

| State | Description |
|-------|-------------|
| list-view | Vertical list |
| grid-view | Grid layout |
| mixed-state | Some complete, some not |

**Viewports:** xs, md, lg

---

## 10. Notification Components

### 10.1 Toast Notifications

**Priority: MEDIUM**
**Path:** `components/notifications/`

| State | Description |
|-------|-------------|
| success | Green success toast |
| error | Red error toast |
| info | Blue info toast |
| warning | Yellow warning toast |
| with-action | Action button |

**Viewports:** xs, md

---

### 10.2 Notification Badge

**Priority: LOW**

| State | Description |
|-------|-------------|
| single-digit | 1-9 |
| double-digit | 10-99 |
| overflow | 99+ |
| dot-only | No number |

**Viewports:** xs

---

### 10.3 Notification Center

**Priority: LOW**

| State | Description |
|-------|-------------|
| empty | No notifications |
| with-items | Multiple notifications |
| unread | Unread indicator |

**Viewports:** xs, md

---

## 11. Loading Components

### 11.1 Skeleton Loaders

**Priority: MEDIUM**
**Path:** `components/loading/`

| State | Description |
|-------|-------------|
| card-skeleton | Card placeholder |
| list-skeleton | List placeholders |
| page-skeleton | Full page |
| text-skeleton | Paragraph lines |

**Viewports:** xs, md, xl

---

### 11.2 Spinner/Loading Indicator

**Priority: LOW**

| State | Description |
|-------|-------------|
| small | Button size |
| medium | Standard |
| large | Page loading |
| with-text | "Loading..." text |

**Viewports:** xs

---

## 12. Form Components

### 12.1 Input Fields

**Priority: HIGH**

| State | Description |
|-------|-------------|
| default | Empty input |
| focus | Focused state |
| filled | With value |
| error | Validation error |
| disabled | Cannot edit |
| with-icon | Left/right icon |

**Viewports:** xs, md

---

### 12.2 Textarea

**Priority: MEDIUM**

| State | Description |
|-------|-------------|
| default | Empty |
| filled | With content |
| error | Validation error |
| auto-grow | Expanding |

**Viewports:** xs, md

---

### 12.3 Checkbox/Toggle

**Priority: MEDIUM**

| State | Description |
|-------|-------------|
| unchecked | Off state |
| checked | On state |
| focus | Keyboard focus |
| disabled | Cannot interact |

**Viewports:** xs

---

### 12.4 Select/Dropdown

**Priority: MEDIUM**

| State | Description |
|-------|-------------|
| closed | Default state |
| open | Options visible |
| selected | Value chosen |
| error | Validation error |

**Viewports:** xs, md

---

## 13. Offline Components

### 13.1 Offline Indicator

**Priority: HIGH**
**Path:** `components/offline/`

| State | Description |
|-------|-------------|
| offline | No connection banner |
| reconnecting | Attempting to connect |
| syncing | Sync in progress |

**Viewports:** xs, md

---

### 13.2 Offline Page

**Priority: MEDIUM**

| State | Description |
|-------|-------------|
| default | Offline message |
| with-cached-content | "View cached" option |

**Viewports:** xs, md

---

## 14. Theme-Specific Tests

### 14.1 Theme Switcher

**Priority: MEDIUM**
**Path:** `components/theme/`

| State | Description |
|-------|-------------|
| dark-selected | Dark mode active |
| light-selected | Light mode active |
| sepia-selected | Sepia mode active |
| system-selected | System preference |

**Viewports:** xs, md

---

### 14.2 Full Page Theme Comparison

For each major page, capture in all three themes:

| Page | Priority |
|------|----------|
| Home | HIGH |
| Devotional Reading | HIGH |
| Series List | MEDIUM |
| Progress | MEDIUM |
| Settings | LOW |

---

## 15. Accessibility States

### 15.1 Focus Indicators

All interactive elements should show clear focus rings:

| Component | Focus Style |
|-----------|-------------|
| Buttons | Gold ring, offset |
| Links | Underline + color |
| Form inputs | Gold ring |
| Cards | Subtle border |

---

### 15.2 Reduced Motion

Capture components with `prefers-reduced-motion`:

| Component | With Motion | Reduced Motion |
|-----------|-------------|----------------|
| Page transitions | Fade/slide | Instant |
| Loading spinners | Spinning | Pulsing |
| Celebrations | Confetti | Static badge |

---

## 16. Test Implementation

### Recommended Tool Setup

**Option 1: Playwright Visual Comparisons**
```typescript
// Example test structure
test('Button primary variants', async ({ page }) => {
  await page.goto('/storybook-static/iframe.html?id=button--primary');
  await expect(page).toHaveScreenshot('button-primary.png');
});
```

**Option 2: Chromatic with Storybook**
- Build Storybook for all components
- Connect to Chromatic CI
- Automatic visual diffing on PRs

**Option 3: Percy**
- Integrate with existing Playwright tests
- Cloud-based comparison
- Cross-browser snapshots

---

## 17. Snapshot Organization

### Directory Structure
```
visual-tests/
  snapshots/
    components/
      button/
        button-primary-dark-xs.png
        button-primary-dark-md.png
        button-primary-light-xs.png
        ...
      card/
        card-default-dark-xs.png
        ...
    pages/
      home-dark-xs.png
      home-light-xs.png
      ...
  diff/
    (generated differences)
```

---

## 18. Execution Schedule

| Test Type | Frequency | Duration |
|-----------|-----------|----------|
| Component snapshots | Every PR | 5-10 min |
| Page snapshots | Daily/Nightly | 15 min |
| Full theme comparison | Weekly | 30 min |
| Cross-browser | Pre-release | 45 min |

---

## 19. Snapshot Update Process

1. Review failing tests in CI
2. If intentional change: run update command
3. Commit updated snapshots
4. PR review includes visual diff review
5. Approve visual changes explicitly

---

## 20. Success Metrics

- Zero unreviewed visual regressions in production
- < 5 minute average visual test execution
- All components covered in all themes
- All breakpoints have test coverage

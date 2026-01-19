# Accessibility Best Practices for Devotional/Reading Apps

**Research Date:** January 19, 2026
**Purpose:** Research accessibility standards specifically for EUONGELION devotional app, ensuring WCAG 2.1 AA compliance and inclusive design for all believers

---

## Executive Summary

Accessibility in devotional apps is both a technical requirement and a spiritual imperative - Scripture should be accessible to everyone. This document covers font sizing, dyslexia considerations, screen reader optimization, and audio alternatives. EUONGELION's existing commitment to WCAG 2.1 AA compliance (noted in CLAUDE.md) provides a strong foundation.

**Key Principle:** "The lost are waiting" includes those with disabilities. Every design decision should ask: "Can ALL believers access this?"

---

## WCAG 2.1 AA Requirements Overview

### Core Principles (POUR)
1. **Perceivable** - Information must be presentable in ways users can perceive
2. **Operable** - Interface components must be operable by all users
3. **Understandable** - Information and UI operation must be understandable
4. **Robust** - Content must be robust enough for diverse user agents/assistive tech

### Key Success Criteria for Reading Apps

| Criterion | Level | Requirement |
|-----------|-------|-------------|
| 1.4.3 Contrast | AA | 4.5:1 for normal text, 3:1 for large text |
| 1.4.4 Resize Text | AA | Text resizable to 200% without loss of function |
| 1.4.10 Reflow | AA | Content reflows without horizontal scrolling at 320px |
| 1.4.12 Text Spacing | AA | No loss of content when adjusting spacing |
| 2.4.7 Focus Visible | AA | Keyboard focus indicator visible |
| 3.1.1 Language of Page | A | Programmatically determined language |

**Source:** [Section508.gov - Fonts and Typography](https://www.section508.gov/develop/fonts-typography/)

---

## Typography & Font Best Practices

### Font Size Recommendations

| Context | Minimum Size | Recommended | Notes |
|---------|--------------|-------------|-------|
| Body text (mobile) | 16px | 18-20px | Prevents eye strain |
| Body text (desktop) | 14px | 16-18px | Standard reading |
| Scripture quotes | 18px | 20-24px | Elevated importance |
| Headings | 24px+ | Scale appropriately | Clear hierarchy |
| Captions/labels | 12px | 14px | Never smaller than 12px |

**Key Finding:** "A minimum of 16px helps ensure that text remains comfortable to read and reduces the effort required to identify letter shapes."

**Source:** [Accessibly - Best Fonts for Dyslexia](https://accessiblyapp.com/blog/best-fonts-for-dyslexia/)

### User-Controlled Font Sizing

**Implementation Requirements:**
1. Allow text resize to 200% without loss of content
2. Respect system font size preferences
3. Provide in-app font size controls (A-, A, A+)
4. Persist user font preferences

**Code Pattern (React/CSS):**
```css
/* Use rem units based on user's root font size */
html {
  font-size: 100%; /* Respects user's browser setting */
}

body {
  font-size: 1rem; /* 16px default */
}

.scripture-text {
  font-size: 1.25rem; /* 20px at default */
}

/* Support dynamic sizing */
.font-size-small { font-size: 0.875rem; }
.font-size-medium { font-size: 1rem; }
.font-size-large { font-size: 1.25rem; }
.font-size-xlarge { font-size: 1.5rem; }
```

### Font Family Recommendations

**Best Sans-Serif Options (General Accessibility):**
1. **Arial** - Universal availability, clean letterforms
2. **Verdana** - Designed for screen, wide letterforms
3. **Tahoma** - Clear distinction between similar letters
4. **Century Gothic** - Modern, readable
5. **Calibri** - Microsoft default, highly readable

**Avoid:**
- Decorative/script fonts for body text
- Fonts with similar-looking letters (I, l, 1 confusion)
- Ultra-thin weights
- ALL CAPS for extended text

**Source:** [Dyslexic.com - Making Content Accessible](https://www.dyslexic.com/quick-guide-making-content-accessible/)

---

## Dyslexia-Friendly Design

### Understanding Dyslexia
- Affects ~10% of the population
- Causes difficulty distinguishing letter shapes
- "Rivers" of white space in justified text are problematic
- Visual crowding increases reading difficulty

### Typography for Dyslexia

**Font Choices:**
1. **OpenDyslexic** - Weighted bottoms help anchor letters
2. **Lexie Readable** - Designed specifically for dyslexia
3. **Dyslexie Font** - Award-winning dyslexia typeface

**Recommendation:** Offer dyslexia-friendly fonts as an optional toggle rather than default, respecting user choice.

**Line Spacing:**
- Minimum 1.5 line height
- 1.75-2.0 for dense Scripture passages
- Prevents "rivers" and visual crowding

**Letter & Word Spacing:**
- Increase character spacing by 0.12x font size
- Word spacing at least 0.16x font size
- Avoid condensed fonts

**Source:** [accessiBe - Dyslexia-Friendly Fonts](https://accessibe.com/blog/knowledgebase/dyslexia-friendly-fonts)

### Layout Principles

**Text Alignment:**
- **Use:** Left-aligned text (ragged right)
- **Avoid:** Justified text (creates uneven spacing)
- **Avoid:** Centered text for long passages

**Line Length:**
- Optimal: 50-75 characters per line
- Maximum: 80 characters
- Too wide = eyes lose track; too narrow = choppy reading

**Paragraph Structure:**
- Maximum 3 sentences per paragraph
- Clear visual separation between paragraphs
- Use whitespace generously

**Background Colors:**
- Offer customizable background colors
- Popular dyslexia-friendly options:
  - Cream/off-white (#FDF5E6)
  - Light blue (#E6F3FF)
  - Light yellow (#FFFACD)
  - Soft green (#E8F5E9)

**Source:** [Forbrain - Best Fonts for Dyslexia](https://www.forbrain.com/dyslexia-children/reading-difficulties/best-fonts/)

---

## Screen Reader Optimization

### Mobile Screen Readers

**iOS - VoiceOver:**
- Built-in screen reader
- Gesture-based navigation
- Reads all accessible content aloud

**Android - TalkBack:**
- Google's built-in screen reader
- Spoken feedback
- Explore by touch

**Source:** [BrowserStack - Screen Reader Testing](https://www.browserstack.com/docs/app-accessibility/screen-reader-testing/talkback)

### Implementation Requirements

**Semantic HTML:**
```html
<!-- Good: Semantic structure -->
<article>
  <header>
    <h1>Today's Devotional</h1>
    <time datetime="2026-01-19">January 19, 2026</time>
  </header>
  <main>
    <blockquote cite="John 3:16">
      For God so loved the world...
    </blockquote>
    <p>Today's reflection...</p>
  </main>
</article>

<!-- Bad: Div soup -->
<div class="devotional">
  <div class="title">Today's Devotional</div>
  <div class="content">...</div>
</div>
```

**ARIA Labels:**
```jsx
// Good: Descriptive labels
<button aria-label="Bookmark this devotional">
  <HeartIcon />
</button>

// Good: Live regions for updates
<div aria-live="polite" aria-atomic="true">
  {readingProgress}% complete
</div>

// Good: Landmarks
<nav aria-label="Main navigation">...</nav>
<main aria-label="Devotional content">...</main>
```

**Focus Management:**
```jsx
// Ensure logical focus order
// Skip to main content link
<a href="#main-content" className="skip-link">
  Skip to devotional
</a>

// Visible focus indicators
button:focus {
  outline: 2px solid var(--color-primary);
  outline-offset: 2px;
}
```

### Content Accessibility

**Alt Text for Images:**
```jsx
// Devotional illustration
<img
  src="/images/mountain-sunrise.jpg"
  alt="Sun rising over mountain peaks, symbolizing new beginnings"
/>

// Decorative images
<img src="/decorative-divider.svg" alt="" role="presentation" />
```

**Scripture Reading Order:**
```jsx
// Ensure verse numbers don't interrupt reading
<span className="verse-number" aria-hidden="true">16</span>
<span>For God so loved the world...</span>

// Screen reader reads: "For God so loved the world..."
// Visual display shows: "16 For God so loved the world..."
```

### Testing with Screen Readers

**Manual Testing Checklist:**
- [ ] All content announced in logical order
- [ ] Interactive elements have clear labels
- [ ] Form inputs have associated labels
- [ ] Error messages announced to screen readers
- [ ] Modal dialogs trap focus appropriately
- [ ] Navigation is possible with keyboard only

**Source:** [Level Access - Screen Reader Accessibility](https://www.levelaccess.com/blog/screen-reader-accessibility/)

---

## Audio Alternatives

### Why Audio Matters for Devotional Apps

**User Needs:**
- Blind/visually impaired users
- Users with reading difficulties
- Commuters/multitaskers
- Aging users with declining vision
- Users with motor impairments affecting scrolling

### Audio Implementation Options

**1. Text-to-Speech (TTS)**
- Leverage system TTS (Web Speech API)
- Lower cost than recorded audio
- Instant availability for all content

```javascript
// Web Speech API example
const speakDevotional = (text) => {
  const utterance = new SpeechSynthesisUtterance(text);
  utterance.rate = 0.9; // Slightly slower for reflection
  utterance.pitch = 1;
  speechSynthesis.speak(utterance);
};
```

**2. Pre-Recorded Audio**
- Higher quality, more engaging
- Requires recording for each devotional
- Consider multiple voice options (like Dwell)

**3. Hybrid Approach**
- Pre-recorded for Scripture
- TTS for devotional commentary
- Background music option (like competitors)

### Audio Best Practices

**Player Controls:**
- Play/Pause clearly visible
- Progress indicator
- Speed control (0.75x, 1x, 1.25x, 1.5x)
- Skip forward/back (10-30 seconds)
- Volume control

**Accessibility of Audio Player:**
```jsx
<audio controls aria-label="Devotional audio">
  <source src="devotional.mp3" type="audio/mpeg" />
  <p>Your browser doesn't support audio.
     <a href="devotional.mp3">Download the audio</a>.</p>
</audio>
```

### Competitor Approaches

**Dwell App:**
- 20+ voice options
- Background music (Ambient, Piano, Hymns)
- Read Along synchronized text
- Committed to accessibility for visually impaired

**YouVersion:**
- Audio Bible in 420+ languages
- Partnership with Davar Audio Bibles

**Lectio 365:**
- All content available in audio format
- Can download a week in advance

**Source:** [Dwell Help - Accessibility](https://help.dwellapp.io/article/101-accessability-for-the-blind-and-visually-impared)

---

## Color & Contrast

### WCAG Contrast Requirements

| Text Type | Minimum Ratio | Example |
|-----------|---------------|---------|
| Normal text (< 18px) | 4.5:1 | #595959 on #FFFFFF |
| Large text (18px+ or 14px bold) | 3:1 | #767676 on #FFFFFF |
| UI components | 3:1 | Borders, icons, focus indicators |

### Dark Mode Considerations

EUONGELION is "Dark Mode First" - ensure accessibility in dark themes:

```css
/* Dark mode with good contrast */
:root {
  --bg-primary: #121212;
  --bg-secondary: #1E1E1E;
  --text-primary: #E0E0E0; /* 11.5:1 contrast */
  --text-secondary: #A0A0A0; /* 6.5:1 contrast */
  --accent: #BB86FC;
}
```

**Testing Tools:**
- WebAIM Contrast Checker
- Chrome DevTools Lighthouse
- Axe browser extension

### Color Blindness Considerations

- Don't rely on color alone to convey information
- Add icons, labels, or patterns to complement color
- Test with color blindness simulators

```jsx
// Good: Color + icon
<span className="reading-complete">
  <CheckIcon /> Completed
</span>

// Bad: Color alone
<span style={{ color: 'green' }}>Completed</span>
```

---

## Touch & Motor Accessibility

### Touch Target Sizes

EUONGELION's CLAUDE.md specifies: "Touch targets 44px minimum"

**WCAG 2.1 AA Requirement:** 44x44 CSS pixels minimum for touch targets

```css
.touch-target {
  min-width: 44px;
  min-height: 44px;
  padding: 12px; /* Increases hit area */
}

/* For text links in content */
.devotional-content a {
  padding: 8px 0;
  display: inline-block;
}
```

### Spacing Between Targets

- Minimum 8px between adjacent touch targets
- Prevents accidental taps
- Critical for users with motor impairments

### Gesture Alternatives

For any gesture-based interaction, provide button alternative:
- Swipe to bookmark -> Also offer bookmark button
- Pull to refresh -> Also offer refresh button
- Pinch to zoom -> Also offer zoom controls

---

## Cognitive Accessibility

### Reducing Cognitive Load

**Simple Navigation:**
- Consistent navigation placement
- Clear labels (not clever/ambiguous)
- Breadcrumbs for deep content

**Progressive Disclosure:**
- Don't overwhelm with options
- Show core content first
- "Read more" for extended content

**Reading Level:**
- Aim for 8th-grade reading level for UI text
- Scripture and devotional content at appropriate level
- Clear, simple instructions

### Error Prevention & Recovery

```jsx
// Good: Clear error with recovery
<div role="alert" aria-live="assertive">
  <p>Unable to load devotional. </p>
  <button onClick={retry}>Try again</button>
</div>

// Good: Confirmation for destructive actions
<Dialog>
  <p>Remove this bookmark? This can't be undone.</p>
  <button>Keep bookmark</button>
  <button>Remove</button>
</Dialog>
```

---

## Implementation Checklist for EUONGELION

### Typography
- [ ] Base font size 16px minimum
- [ ] User-adjustable font size (A-, A, A+)
- [ ] Line height 1.5 minimum
- [ ] Left-aligned text (no justify)
- [ ] Sans-serif font for UI
- [ ] Optional dyslexia-friendly font

### Visual
- [ ] 4.5:1 contrast for body text
- [ ] 3:1 contrast for large text/UI
- [ ] Dark mode tested for contrast
- [ ] Color not sole indicator
- [ ] Visible focus indicators
- [ ] Touch targets 44px minimum

### Screen Reader
- [ ] Semantic HTML structure
- [ ] ARIA labels on interactive elements
- [ ] Alt text for meaningful images
- [ ] Logical reading order
- [ ] Skip navigation link
- [ ] Live regions for dynamic content

### Motor/Touch
- [ ] Keyboard navigation complete
- [ ] No gesture-only interactions
- [ ] Adequate spacing between targets
- [ ] No time limits on interactions

### Audio
- [ ] TTS option for devotionals
- [ ] Accessible audio player controls
- [ ] Transcripts for any audio-only content

### Cognitive
- [ ] Simple, consistent navigation
- [ ] Clear error messages with recovery
- [ ] Confirmation for destructive actions
- [ ] Reading level appropriate for audience

---

## Testing Strategy

### Automated Testing
- **Lighthouse** - Built into Chrome DevTools
- **axe DevTools** - Browser extension
- **WAVE** - Web accessibility evaluation tool
- **jest-axe** - Automated testing in Jest

### Manual Testing
- Navigate entire app with keyboard only
- Test with VoiceOver (iOS) and TalkBack (Android)
- Test at 200% zoom
- Test with system font size increased
- Review with users who have disabilities

### User Testing
- Recruit users with visual impairments
- Test with users who use screen readers daily
- Include users with dyslexia in testing
- Gather feedback on pain points

---

## Resources for Ongoing Accessibility

### Design Resources
- [Inclusive Design Principles](https://inclusivedesignprinciples.org/)
- [A11y Style Guide](https://a11y-style-guide.com/style-guide/)
- [Material Design Accessibility](https://material.io/design/usability/accessibility.html)

### Testing Tools
- [WebAIM WAVE](https://wave.webaim.org/)
- [axe DevTools](https://www.deque.com/axe/)
- [Colour Contrast Analyser](https://www.tpgi.com/color-contrast-checker/)

### Screen Reader Resources
- [VoiceOver Getting Started](https://support.apple.com/guide/voiceover/welcome/mac)
- [TalkBack Documentation](https://support.google.com/accessibility/android/answer/6283677)

---

## Sources

- [Section508.gov - Fonts and Typography](https://www.section508.gov/develop/fonts-typography/)
- [Accessibly - Best Fonts for Dyslexia](https://accessiblyapp.com/blog/best-fonts-for-dyslexia/)
- [accessiBe - Dyslexia-Friendly Fonts](https://accessibe.com/blog/knowledgebase/dyslexia-friendly-fonts)
- [Dyslexic.com - Making Content Accessible](https://www.dyslexic.com/quick-guide-making-content-accessible/)
- [Forbrain - Best Fonts for Dyslexia](https://www.forbrain.com/dyslexia-children/reading-difficulties/best-fonts/)
- [Level Access - Screen Reader Accessibility](https://www.levelaccess.com/blog/screen-reader-accessibility/)
- [BrowserStack - Screen Reader Testing](https://www.browserstack.com/docs/app-accessibility/screen-reader-testing/talkback)
- [Dwell Help - Accessibility](https://help.dwellapp.io/article/101-accessability-for-the-blind-and-visually-impared)
- [Stanford UIT - Typography Accessibility](https://uit.stanford.edu/accessibility/concepts/typography)
- [Medium - Inclusive Typography](https://medium.com/@blessingokpala/inclusive-typography-fonts-that-support-dyslexia-low-vision-and-adhd-1f6bc13aff50)

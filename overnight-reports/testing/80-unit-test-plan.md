# EUONGELION Unit Test Plan

**Document ID:** 80-unit-test-plan.md
**Created:** 2026-01-19
**Test Framework:** Vitest
**Coverage Target:** 70% (configured in vitest.config.ts)

---

## 1. Executive Summary

This document identifies all utility functions, hooks, and helpers in the EUONGELION codebase that require unit testing. Each item includes what to test and edge cases to consider.

### Current Test Coverage Status

| Category | Files | Existing Tests | Coverage |
|----------|-------|----------------|----------|
| Components | 2 | Button.test.tsx, DevotionalCard.test.tsx | Partial |
| Hooks | 0 | None | 0% |
| Lib/Utilities | 0 | None | 0% |
| Stores | 0 | None | 0% |

---

## 2. Utility Functions (lib/)

### 2.1 Date Utilities (`lib/date.ts`)

**Priority: HIGH** - Core functionality for streak tracking and reading progress.

| Function | Description | What to Test | Edge Cases |
|----------|-------------|--------------|------------|
| `formatDate()` | Format date by style | All style options (short, medium, long, full); locale variations | Invalid dates, null input, string vs Date vs timestamp input |
| `formatRelativeDate()` | Relative time strings | Seconds, minutes, hours, days, weeks, months, years | Boundary times (59s vs 1min), future dates, timezone differences |
| `getDayOfYear()` | Day number 1-366 | January 1st = 1, December 31st varies | Leap years, February 29th, timezone boundaries |
| `isToday()` | Check if date is today | True for today, false otherwise | Midnight boundary, different timezones |
| `isSameDay()` | Compare two dates | Same day different times, different days | Null inputs, string inputs, midnight edge |
| `getReadingStreak()` | Calculate reading streak | Consecutive days, gaps, longest vs current | Empty array, single date, duplicate dates, out-of-order dates |
| `startOfDay()` | Get midnight of date | Returns 00:00:00.000 | Timezone handling |
| `endOfDay()` | Get end of date | Returns 23:59:59.999 | Timezone handling |
| `addDays()` | Add/subtract days | Positive and negative values | Month/year boundaries, DST transitions |
| `getDayDifference()` | Days between dates | Absolute difference | Same day = 0, order independence |
| `isLeapYear()` | Check leap year | 2024 (true), 2023 (false), 2000 (true), 1900 (false) | Century rules |
| `getDaysInYear()` | 365 or 366 | Leap vs non-leap years | Defaults to current year |
| `formatDuration()` | Minutes to string | Under 60min, over 60min, exact hours | 0 minutes, decimal minutes |

### 2.2 String Utilities (`lib/string.ts`)

**Priority: HIGH** - Used throughout UI for content processing.

| Function | Description | What to Test | Edge Cases |
|----------|-------------|--------------|------------|
| `slugify()` | URL-friendly slugs | Basic conversion, options (separator, lowercase, maxLength) | Unicode/diacritics, empty string, special characters only |
| `truncate()` | Truncate with ellipsis | Under limit (no change), over limit, word boundary | Zero/negative length, ellipsis longer than text |
| `stripHtml()` | Remove HTML tags | Tags, entities, scripts | Nested tags, malformed HTML, XSS attempts |
| `escapeHtml()` | Escape for HTML | All special characters (&, <, >, ", ', /) | Empty string, already escaped |
| `unescapeHtml()` | Reverse escape | All entities | Empty string, partial entities |
| `highlightSearchTerm()` | Wrap matches in tag | Single match, multiple matches, case insensitivity | No match, regex special chars in search, empty term |
| `highlightSearchTerms()` | Multiple terms | Array of terms | Empty array, overlapping terms |
| `capitalize()` | First letter uppercase | Normal string, already capitalized | Empty string, single char |
| `titleCase()` | Each word capitalized | Multiple words | Empty string, single word |
| `normalizeWhitespace()` | Clean up whitespace | Multiple spaces, newlines, tabs | Empty string, whitespace only |
| `wordCount()` | Count words | Multiple words | Empty string, extra whitespace |
| `isBlank()` | Check if empty/whitespace | Empty, whitespace, null, undefined | Non-string inputs |
| `excerpt()` | Generate excerpt | Combines stripHtml + truncate | HTML content, short content |
| `generateId()` | Random alphanumeric | Default length, custom length | Zero length, very long |
| `pluralize()` | Word pluralization | Count of 1, count > 1, custom plural | Count of 0, negative count |

### 2.3 Scripture Utilities (`lib/scripture.ts`)

**Priority: HIGH** - Core devotional functionality.

| Function | Description | What to Test | Edge Cases |
|----------|-------------|--------------|------------|
| `parseScriptureReference()` | Parse "John 3:16" format | Single verse, verse range, chapter only, numbered books | Invalid books, out-of-range chapters, malformed input |
| `formatScriptureReference()` | Format reference object | All options (abbreviated, separators) | Missing fields, partial objects |
| `validateScriptureRef()` | Validate reference string | Valid refs, invalid refs | Genesis 51 (only 50 chapters), empty string |
| `getBookName()` | Full name from abbrev/alias | All abbreviations and aliases | Invalid input, case sensitivity |
| `getChapter()` | Extract chapter number | Valid refs, chapter-only refs | Invalid refs |
| `getVerse()` | Extract verse(s) | Single verse, range | Chapter-only refs, invalid refs |
| `getBooks()` | List all books | No filter, OT filter, NT filter | |
| `getChapterCount()` | Chapters in book | Various books | Invalid book |
| `isOldTestament()` / `isNewTestament()` | Testament check | OT books, NT books | Invalid book |
| `parseMultipleReferences()` | Parse semicolon/comma separated | Multiple refs | Empty string, single ref, invalid refs mixed |
| `getScriptureUrl()` | Generate Bible URL | All providers (biblegateway, youversion, esv) | Special characters in reference |

### 2.4 Validation Utilities (`lib/validation/`)

**Priority: HIGH** - Form validation across the app.

#### validators.ts

| Function | Description | What to Test | Edge Cases |
|----------|-------------|--------------|------------|
| `required` | Non-empty check | String, null, undefined, array | Whitespace-only string, empty array |
| `minLength()` | Minimum string length | At/above/below minimum | Empty string |
| `maxLength()` | Maximum string length | At/above/below maximum | Empty string |
| `exactLength()` | Exact length match | Match, no match | Empty string |
| `pattern()` | Regex validation | Match, no match | Empty string, custom message |
| `email` | Email format | Valid formats, invalid formats | Missing @, multiple @, special chars |
| `password()` | Password strength | All options (uppercase, lowercase, number, special) | Minimum lengths, edge cases |
| `confirmPassword()` | Password match | Match, no match | Empty strings |
| `number` | Numeric check | Numbers, non-numbers | Empty string, "NaN", floats |
| `min()` / `max()` | Numeric range | At/above/below boundaries | Non-numeric input |
| `integer` | Integer check | Integers, floats | Negative, zero |
| `url` / `urlWithProtocol` | URL format | Valid URLs, invalid URLs | Missing protocol |
| `phone` | Phone format | Various valid formats | International formats |
| `date` / `futureDate` / `pastDate` | Date validation | Valid dates, invalid dates | String vs Date input |
| `selected` / `minSelections` / `maxSelections` | Selection validation | Single, multiple selections | Empty array |
| `maxFileSize()` / `fileType()` | File validation | Valid files, oversized, wrong type | Multiple files |
| `terms` / `consent` | Boolean validation | True, false | |
| `scriptureReference` | Scripture format | Valid refs, invalid refs | |
| `compose()` | Combine validators | Multiple validators, first failure | Empty validators |
| `withMessage()` | Custom error message | Override default message | |

#### schemas.ts

| Function | Description | What to Test | Edge Cases |
|----------|-------------|--------------|------------|
| `validateSchema()` | Validate object against schema | All fields valid, some invalid | Extra fields, missing fields |
| `isValid()` | Check errors object | Empty errors, has errors | |
| Pre-built schemas | Login, signup, profile, etc. | Full form validation | |

### 2.5 Theme Utilities (`lib/theme/utils.ts`)

**Priority: MEDIUM** - Theme management.

| Function | Description | What to Test | Edge Cases |
|----------|-------------|--------------|------------|
| `getSystemTheme()` | Detect OS preference | Dark preference, light preference | SSR (no window) |
| `resolveTheme()` | Handle 'system' theme | System -> resolved, direct themes | |
| `getStoredTheme()` / `setStoredTheme()` | localStorage | Read/write theme | localStorage disabled |
| `isValidTheme()` | Validate theme name | Valid names, invalid names | |
| `applyTheme()` | Apply to DOM | All themes, CSS variables | SSR (no document) |
| `getNextTheme()` | Theme cycling | Full cycle, from 'system' | |
| `toggleDarkLight()` | Dark/light toggle | Both directions | |
| `disableTransitions()` | Temporary disable | Returns cleanup function | SSR |

### 2.6 Content Utilities (`lib/content/`)

**Priority: MEDIUM** - Content loading and parsing.

| Function | Description | What to Test | Edge Cases |
|----------|-------------|--------------|------------|
| `loader.ts` functions | Load devotional content | Valid content, missing content | Network errors, malformed data |
| `parser.ts` functions | Parse markdown/content | Valid formats | Malformed content |
| `validator.ts` functions | Validate content structure | Valid structure, missing fields | |

### 2.7 Animation Utilities (`lib/animations/`)

**Priority: LOW** - Visual enhancements.

| Function | Description | What to Test | Edge Cases |
|----------|-------------|--------------|------------|
| `variants.ts` | Animation variants | Object structure | |
| `transitions.ts` | Transition configs | Object structure | |
| `gestures.ts` | Gesture configs | Object structure | |

---

## 3. React Hooks (hooks/)

### 3.1 useForm (`hooks/useForm.ts`)

**Priority: HIGH** - Form state management.

| Behavior | What to Test | Edge Cases |
|----------|--------------|------------|
| Initial values | State initialization | Empty object, nested objects |
| setValue/setValues | Value updates | Single field, multiple fields, nested |
| Validation | validateField, validateForm | Schema validation, custom validators |
| Touched/Dirty state | Track user interaction | Reset behavior |
| Submit handling | handleSubmit flow | Success, error, validation failure |
| Reset | Form reset | Partial reset, full reset |
| getFieldProps | Props generation | All prop attributes |
| register | Field registration with validators | Multiple validators |

### 3.2 useOnlineStatus (`hooks/useOnlineStatus.ts`)

**Priority: HIGH** - PWA functionality.

| Behavior | What to Test | Edge Cases |
|----------|--------------|------------|
| Initial state | Detect online/offline | SSR |
| Event handling | Online/offline events | Rapid toggling |
| Connection check | checkConnection() | Network errors, timeout |
| Connection info | Type, effective type | Browser without API support |
| Pending sync count | IndexedDB operations | DB not available |
| Slow connection detection | effectiveType checking | |

### 3.3 useTheme (`hooks/useTheme.ts`)

**Priority: MEDIUM** - Theme management.

| Behavior | What to Test | Edge Cases |
|----------|--------------|------------|
| Theme state | Current, resolved, system theme | |
| setTheme | Theme changes | Invalid theme |
| toggleTheme | Dark/light toggle | |
| cycleTheme | Full cycle | |
| isDark/isLight/isSepia | Boolean checks | |
| useThemeValue | Value by theme | |
| useDarkModeValue | Binary value | |

### 3.4 useNotifications (`hooks/useNotifications.ts`)

**Priority: MEDIUM** - In-app notifications.

| Behavior | What to Test | Edge Cases |
|----------|--------------|------------|
| Load from storage | Initial load | Corrupted data, empty storage |
| Save to storage | Persistence | Storage full |
| markAsRead | Single notification | Invalid ID |
| dismiss | Remove notification | Invalid ID |
| markAllRead | Batch operation | Empty list |
| clearAll | Clear all | |
| addNotification | Add new | Max limit reached |
| Polling | Fetch from API | Network errors |

### 3.5 useAnalytics (`hooks/useAnalytics.ts`)

**Priority: MEDIUM** - Event tracking.

| Behavior | What to Test | Edge Cases |
|----------|--------------|------------|
| track | Generic event tracking | Disabled analytics, no consent |
| trackDevotionalStart/Complete | Devotional events | |
| trackSeriesStart/Complete | Series events | |
| trackBookmark/Share | Engagement events | |
| trackSearch | Search events | Empty query |
| Consent checking | hasConsent, isEnabled | |

### 3.6 Other Hooks

| Hook | Priority | Key Tests |
|------|----------|-----------|
| useFeatureFlag | LOW | Flag lookup, default values |
| useFeatureFlags | LOW | Multiple flags |
| useField | MEDIUM | Field state management |
| useFormSubmit | MEDIUM | Submission handling |
| useOfflineDevotionals | HIGH | Offline storage, sync |
| useOnboarding | LOW | Onboarding state |
| useOnboardingStep | LOW | Step navigation |
| usePushNotifications | MEDIUM | Permission, subscription |
| usePushPermission | MEDIUM | Permission state |
| useServiceWorker | HIGH | Registration, updates |
| useSystemTheme | LOW | OS theme detection |
| useToast | MEDIUM | Toast management |
| useValidation | MEDIUM | Field validation |

---

## 4. Zustand Stores (stores/)

### 4.1 authStore (`stores/authStore.ts`)

**Priority: HIGH** - Authentication state.

| Behavior | What to Test | Edge Cases |
|----------|--------------|------------|
| initialize | Session check, refresh | Expired session, no session |
| signIn | All providers | Invalid credentials, network error |
| signUp | Registration flow | Duplicate email, weak password |
| signOut | Logout flow | Error during logout |
| refreshToken | Token refresh | No session, refresh failure |
| resetPassword | Password reset | Invalid email |
| Selectors | All selector functions | |

### 4.2 devotionalStore (`stores/devotionalStore.ts`)

**Priority: HIGH** - Devotional reading state.

| Behavior | What to Test | Edge Cases |
|----------|--------------|------------|
| loadDevotional | Fetch devotional | Not found, network error |
| startReading | Initialize reading state | |
| updateReadingProgress | Progress updates | |
| completeReading | Mark complete, add to history | |
| addToHistory | History management | Duplicate entries, max limit |
| Selectors | All selector functions | |

### 4.3 progressStore (`stores/progressStore.ts`)

**Priority: HIGH** - Reading progress and streaks.

| Behavior | What to Test | Edge Cases |
|----------|--------------|------------|
| updateStreak | Streak calculation | First activity, consecutive day, gap, grace period |
| recordProgress | Progress recording | Stats updates |
| updateSeriesProgress | Series tracking | New series, existing series |
| loadProgress / syncProgress | API operations | Network errors |
| calculateStats | Stats calculation | Empty data |
| Selectors | All selector functions | |

### 4.4 bookmarkStore (`stores/bookmarkStore.ts`)

**Priority: MEDIUM** - Bookmark management.

| Behavior | What to Test | Edge Cases |
|----------|--------------|------------|
| Add/remove bookmarks | CRUD operations | Duplicate bookmark |
| Bookmark state | isBookmarked check | |
| Persistence | localStorage | |

### 4.5 userStore (`stores/userStore.ts`)

**Priority: MEDIUM** - User preferences.

| Behavior | What to Test | Edge Cases |
|----------|--------------|------------|
| User settings | Read/write | |
| Preferences | Update preferences | |

---

## 5. Implementation Priority

### Phase 1: Critical Path (Week 1)
1. `lib/date.ts` - Core streak functionality
2. `lib/scripture.ts` - Core devotional functionality
3. `lib/validation/validators.ts` - Form validation
4. `stores/authStore.ts` - Authentication
5. `stores/progressStore.ts` - Progress tracking

### Phase 2: Core Features (Week 2)
1. `lib/string.ts` - Content processing
2. `hooks/useForm.ts` - Form management
3. `hooks/useOnlineStatus.ts` - PWA support
4. `stores/devotionalStore.ts` - Reading state
5. `lib/validation/schemas.ts` - Form schemas

### Phase 3: Supporting Features (Week 3)
1. `hooks/useTheme.ts` - Theme management
2. `hooks/useNotifications.ts` - Notifications
3. `hooks/useAnalytics.ts` - Analytics
4. `lib/theme/utils.ts` - Theme utilities
5. Remaining stores

### Phase 4: Nice-to-Have (Week 4)
1. Animation utilities
2. Content utilities
3. Remaining hooks

---

## 6. Test File Naming Convention

```
__tests__/
  components/
    Button.test.tsx
    DevotionalCard.test.tsx
  hooks/
    useForm.test.ts
    useOnlineStatus.test.ts
  lib/
    date.test.ts
    string.test.ts
    scripture.test.ts
    validation/
      validators.test.ts
      schemas.test.ts
  stores/
    authStore.test.ts
    progressStore.test.ts
```

---

## 7. Test Utilities Available

From `__tests__/utils/test-utils.tsx`:
- Custom `render` function with providers
- `user` object for userEvent interactions
- Mocks for Supabase and Next.js router

---

## 8. Estimated Coverage Goals

| Area | Current | Target | Tests Needed |
|------|---------|--------|--------------|
| lib/ | 0% | 80% | ~100 tests |
| hooks/ | 0% | 75% | ~50 tests |
| stores/ | 0% | 75% | ~40 tests |
| components/ | ~10% | 70% | ~60 tests |
| **Total** | **~5%** | **70%** | **~250 tests** |

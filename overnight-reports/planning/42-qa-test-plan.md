# EUONGELION QA Test Plan

**Purpose:** Manual test cases for every feature with steps and expected results
**Last Updated:** 2026-01-19
**Version:** 1.0

---

## Test Environment Requirements

- **Browsers:** Chrome (latest), Safari (latest), Firefox (latest)
- **Devices:** iPhone (iOS Safari), Android (Chrome), Desktop
- **Network:** Test on WiFi, 4G, and Offline modes
- **Accounts:** One new user account, one existing user account with data

---

## Test Case Format

```
Test ID: XX-YYY
Feature: [Feature Name]
Priority: Critical | High | Medium | Low
Preconditions: [Setup required]
Steps: [Numbered steps]
Expected Result: [What should happen]
Actual Result: [Fill in during testing]
Status: Pass | Fail | Blocked
Notes: [Any observations]
```

---

## 1. DAILY DEVOTIONALS

### TC-DEV-001: View Devotional Content
**Priority:** Critical
**Preconditions:** At least one devotional exists in the database

**Steps:**
1. Navigate to the home page
2. Click on a devotional card/link
3. Observe the devotional page

**Expected Result:**
- Page loads within 2 seconds
- Title displays prominently
- Scripture reference shows with correct formatting
- Scripture text is readable and properly styled
- Devotional body content displays
- Reflection prompts/questions appear
- Dark mode styling is correct (if enabled)

---

### TC-DEV-002: Read Devotional to Completion
**Priority:** Critical
**Preconditions:** User is logged in

**Steps:**
1. Navigate to an unread devotional
2. Scroll to the bottom of the devotional
3. Look for completion indicator or button
4. Mark devotional as complete (if manual action required)
5. Navigate away and return to the same devotional

**Expected Result:**
- Devotional shows as "read" or "completed"
- Progress is saved
- Returning to devotional shows completed state
- Progress count increases on series/home page

---

### TC-DEV-003: Navigate Between Devotionals in Series
**Priority:** High
**Preconditions:** Series has at least 3 devotionals

**Steps:**
1. Open a devotional that is part of a series (not first or last)
2. Click "Next" navigation
3. Verify next devotional loads
4. Click "Previous" navigation
5. Verify previous devotional loads

**Expected Result:**
- Navigation buttons are visible and clickable
- Correct devotional loads in each direction
- Progress state preserved during navigation
- URL updates to reflect current devotional

---

### TC-DEV-004: Share Devotional - Native Share
**Priority:** High
**Preconditions:** Device supports Web Share API (mobile)

**Steps:**
1. Open any devotional
2. Click the share button/icon
3. Select "Share" or native share option
4. Choose any app to share to
5. Verify shared content

**Expected Result:**
- Native share sheet opens
- Share includes devotional title
- Share includes devotional URL
- Share includes brief excerpt or description

---

### TC-DEV-005: Share Devotional - Copy Link
**Priority:** High
**Preconditions:** None

**Steps:**
1. Open any devotional
2. Click the share button/icon
3. Select "Copy Link" option
4. Paste the copied content somewhere

**Expected Result:**
- "Copied" confirmation appears
- Correct URL is in clipboard
- URL is shareable (works when pasted in browser)

---

### TC-DEV-006: Devotional Offline Access
**Priority:** High
**Preconditions:** User has viewed a devotional while online

**Steps:**
1. View a devotional while online
2. Turn off network connection (airplane mode)
3. Navigate to the same devotional
4. View the content

**Expected Result:**
- Devotional loads from cache
- All text content displays
- Offline indicator may show
- No error messages for cached content

---

### TC-DEV-007: Devotional Accessibility - Screen Reader
**Priority:** Medium
**Preconditions:** Screen reader enabled (VoiceOver/TalkBack)

**Steps:**
1. Navigate to devotional page with screen reader
2. Move through all content elements
3. Interact with buttons and links

**Expected Result:**
- All content is announced
- Headings are properly structured (H1, H2, etc.)
- Scripture is distinguishable from body text
- Buttons announce their purpose
- Focus order is logical

---

## 2. SERIES NAVIGATION

### TC-SER-001: View Series Listing
**Priority:** Critical
**Preconditions:** At least 2 series exist

**Steps:**
1. Navigate to Series page
2. Observe the series list

**Expected Result:**
- All series are displayed
- Each series shows title
- Each series shows description or excerpt
- Progress indicator visible (if user has progress)
- Series are in correct order

---

### TC-SER-002: View Series Detail
**Priority:** Critical
**Preconditions:** Series has multiple devotionals

**Steps:**
1. Navigate to Series page
2. Click on a series
3. View series detail page

**Expected Result:**
- Series title displays
- Series description displays
- All devotionals in series are listed
- Devotional order is correct
- Read/unread status shown per devotional
- Overall progress shown (e.g., "3 of 7 complete")

---

### TC-SER-003: Navigate from Series to Devotional
**Priority:** High
**Preconditions:** Series has devotionals

**Steps:**
1. Open a series detail page
2. Click on any devotional in the list
3. View the devotional

**Expected Result:**
- Correct devotional opens
- Back navigation returns to series
- Series context is maintained

---

### TC-SER-004: Series Progress Tracking
**Priority:** High
**Preconditions:** User is logged in, series has 5+ devotionals

**Steps:**
1. Note current progress on a series
2. Complete one unread devotional
3. Return to series page
4. Check progress indicator

**Expected Result:**
- Progress updates immediately or on refresh
- Count increases by 1
- Visual progress indicator updates
- Completed devotional shows as read

---

### TC-SER-005: Empty Series State
**Priority:** Medium
**Preconditions:** Create or find series with no devotionals

**Steps:**
1. Navigate to empty series (if exists)

**Expected Result:**
- Appropriate empty state message
- No errors or broken UI
- Clear indication that content is coming

---

## 3. SOUL AUDIT

### TC-SA-001: Start Soul Audit - First Time User
**Priority:** Critical
**Preconditions:** User has not completed Soul Audit

**Steps:**
1. Navigate to Soul Audit page
2. View the initial screen

**Expected Result:**
- Question displays: "What are you wrestling with?"
- Supporting copy is visible
- Text input area is present
- Placeholder text shows
- Submit/Continue button visible

---

### TC-SA-002: Submit Minimal Response
**Priority:** High
**Preconditions:** On Soul Audit input screen

**Steps:**
1. Type only "sad" (3 characters)
2. Click submit/continue

**Expected Result:**
- Nudge message appears: "Would you like to share a bit more?"
- Option to continue anyway is available
- User is not blocked

---

### TC-SA-003: Submit Empty Response
**Priority:** High
**Preconditions:** On Soul Audit input screen

**Steps:**
1. Leave text input empty
2. Click submit/continue

**Expected Result:**
- Validation message appears
- User cannot proceed
- Input is highlighted or indicated as required

---

### TC-SA-004: Submit Full Response - High Confidence Match
**Priority:** Critical
**Preconditions:** On Soul Audit input screen

**Steps:**
1. Type: "I've been feeling exhausted and overwhelmed with work. I don't have time to rest."
2. Submit response

**Expected Result:**
- Response is processed
- Results page shows category match (likely "Rest & Renewal")
- Recommended content/series displayed
- Categories listed match user's needs

---

### TC-SA-005: Submit Full Response - Low Confidence Match
**Priority:** High
**Preconditions:** On Soul Audit input screen

**Steps:**
1. Type: "things have been okay"
2. Submit response

**Expected Result:**
- Low confidence detected
- Clarifying options displayed
- User can select from options like "I need rest", "I need answers", etc.
- "Let me browse all options" is available

---

### TC-SA-006: Crisis Detection Trigger
**Priority:** Critical
**Preconditions:** On Soul Audit input screen

**Steps:**
1. Type: "I don't want to live anymore"
2. Submit response

**Expected Result:**
- Crisis response screen appears immediately
- Acknowledgment message: "We hear you"
- Crisis resources displayed prominently
- 988 Suicide Prevention Lifeline shown
- Crisis Text Line shown
- Resources are clickable/actionable
- Option to continue when ready

---

### TC-SA-007: Soul Audit Results - View Recommendations
**Priority:** High
**Preconditions:** User has completed Soul Audit

**Steps:**
1. Complete Soul Audit with clear category match
2. View results page

**Expected Result:**
- Matched category shown with name and description
- Relevant Scripture theme displayed
- Recommended series/devotionals listed
- Clear path to start reading

---

### TC-SA-008: Retake Soul Audit
**Priority:** Medium
**Preconditions:** User has completed Soul Audit previously

**Steps:**
1. Navigate to Soul Audit
2. Look for retake option
3. Start new audit

**Expected Result:**
- Option to retake is visible
- Previous results may be shown for reference
- New audit starts fresh
- New results replace or supplement old

---

### TC-SA-009: Soul Audit Accessibility
**Priority:** Medium
**Preconditions:** Screen reader or keyboard-only navigation

**Steps:**
1. Navigate Soul Audit with keyboard only
2. Complete text input
3. Submit using keyboard
4. Navigate results

**Expected Result:**
- All elements keyboard accessible
- Focus states visible
- Form is properly labeled
- Results are announced

---

## 4. BOOKMARKS

### TC-BM-001: Add Bookmark
**Priority:** Critical
**Preconditions:** User is logged in, viewing a devotional

**Steps:**
1. Open any devotional
2. Click bookmark icon/button
3. Observe icon state change

**Expected Result:**
- Bookmark icon changes to "bookmarked" state
- Confirmation may appear (toast/message)
- Devotional is saved to bookmarks list

---

### TC-BM-002: Remove Bookmark
**Priority:** Critical
**Preconditions:** User has at least one bookmark

**Steps:**
1. Open a bookmarked devotional
2. Click bookmark icon to remove
3. Observe icon state change

**Expected Result:**
- Icon returns to "not bookmarked" state
- Confirmation may appear
- Devotional removed from bookmarks list

---

### TC-BM-003: View Bookmarks List
**Priority:** Critical
**Preconditions:** User has 3+ bookmarks

**Steps:**
1. Navigate to bookmarks page/section
2. View list

**Expected Result:**
- All bookmarked devotionals appear
- Each item shows title
- Each item shows series name (if applicable)
- Items are clickable
- List is scrollable if needed

---

### TC-BM-004: Navigate from Bookmark to Devotional
**Priority:** High
**Preconditions:** User has bookmarks

**Steps:**
1. Go to bookmarks list
2. Click on a bookmarked devotional
3. View the devotional

**Expected Result:**
- Correct devotional opens
- Bookmark state shows as bookmarked
- Back navigation returns to bookmarks

---

### TC-BM-005: Bookmark Sync Across Devices
**Priority:** High
**Preconditions:** User logged into two devices

**Steps:**
1. On Device A: Bookmark a devotional
2. On Device B: Refresh/navigate to bookmarks
3. Verify bookmark appears

**Expected Result:**
- Bookmark syncs to second device
- May require refresh
- Same bookmark state on both devices

---

### TC-BM-006: Bookmark as Guest User
**Priority:** Medium
**Preconditions:** User is not logged in

**Steps:**
1. View a devotional as guest
2. Attempt to bookmark

**Expected Result:**
- Prompt to sign up/log in appears
- Clear message about why login is needed
- Easy path to authentication

---

### TC-BM-007: Empty Bookmarks State
**Priority:** Low
**Preconditions:** User has no bookmarks

**Steps:**
1. Navigate to bookmarks with no saved items

**Expected Result:**
- Empty state message displays
- Suggestion to bookmark devotionals
- No errors or broken UI

---

## 5. AUTHENTICATION

### TC-AUTH-001: Sign Up - New User
**Priority:** Critical
**Preconditions:** Valid email not already registered

**Steps:**
1. Navigate to sign up page
2. Enter valid email address
3. Enter valid password (meeting requirements)
4. Submit form

**Expected Result:**
- Account created successfully
- User is logged in
- Redirected to appropriate page (home or onboarding)
- Welcome message may appear

---

### TC-AUTH-002: Sign Up - Invalid Email
**Priority:** High
**Preconditions:** On sign up page

**Steps:**
1. Enter invalid email (e.g., "notanemail")
2. Enter valid password
3. Attempt to submit

**Expected Result:**
- Validation error appears
- Form does not submit
- Error message is clear

---

### TC-AUTH-003: Sign Up - Weak Password
**Priority:** High
**Preconditions:** On sign up page

**Steps:**
1. Enter valid email
2. Enter weak password (e.g., "123")
3. Attempt to submit

**Expected Result:**
- Password requirements shown
- Form does not submit
- Clear error message

---

### TC-AUTH-004: Sign Up - Duplicate Email
**Priority:** High
**Preconditions:** Email already registered

**Steps:**
1. Attempt to sign up with existing email
2. Enter valid password
3. Submit form

**Expected Result:**
- Error message about existing account
- Suggestion to sign in instead
- No account created

---

### TC-AUTH-005: Sign In - Valid Credentials
**Priority:** Critical
**Preconditions:** Account exists

**Steps:**
1. Navigate to sign in page
2. Enter correct email
3. Enter correct password
4. Submit form

**Expected Result:**
- User logged in successfully
- Redirected to home or previous page
- User data loads (bookmarks, progress)

---

### TC-AUTH-006: Sign In - Invalid Credentials
**Priority:** High
**Preconditions:** On sign in page

**Steps:**
1. Enter email
2. Enter incorrect password
3. Submit form

**Expected Result:**
- Error message appears
- Generic message (don't reveal if email exists)
- Suggest password reset

---

### TC-AUTH-007: Password Reset Flow
**Priority:** High
**Preconditions:** Account exists

**Steps:**
1. Click "Forgot Password" on sign in page
2. Enter registered email
3. Submit request
4. Check email for reset link
5. Click reset link
6. Enter new password
7. Submit

**Expected Result:**
- Reset email sent confirmation
- Email received within minutes
- Reset link works
- Password can be changed
- Can sign in with new password

---

### TC-AUTH-008: Sign Out
**Priority:** Critical
**Preconditions:** User is logged in

**Steps:**
1. Click sign out option (settings or menu)
2. Confirm sign out if prompted

**Expected Result:**
- User is logged out
- Session cleared
- Redirected to home or sign in
- Protected routes no longer accessible

---

### TC-AUTH-009: Session Persistence
**Priority:** High
**Preconditions:** User is logged in

**Steps:**
1. Log in to the app
2. Close the browser/app completely
3. Reopen and navigate to app
4. Check logged in state

**Expected Result:**
- User remains logged in
- No need to re-authenticate
- Session persists for appropriate duration

---

### TC-AUTH-010: Protected Route Access
**Priority:** High
**Preconditions:** User is NOT logged in

**Steps:**
1. As guest, try to access a protected route directly (e.g., /settings)
2. Observe behavior

**Expected Result:**
- Redirected to sign in page
- Return URL preserved
- After sign in, redirected to intended page

---

## 6. PWA INSTALLATION

### TC-PWA-001: Install Prompt - Android Chrome
**Priority:** High
**Preconditions:** Using Chrome on Android, app not installed

**Steps:**
1. Visit the site
2. Use the app for a few sessions
3. Watch for install prompt/banner

**Expected Result:**
- Install prompt appears (not on first visit)
- Prompt shows app name and icon
- "Install" button functional

---

### TC-PWA-002: Install - Android Chrome
**Priority:** Critical
**Preconditions:** Install prompt visible

**Steps:**
1. Click "Install" on prompt
2. Wait for installation
3. Check home screen

**Expected Result:**
- App icon appears on home screen
- Icon is correct
- App name displays correctly

---

### TC-PWA-003: Launch Installed App - Android
**Priority:** Critical
**Preconditions:** App installed on Android

**Steps:**
1. Tap app icon on home screen
2. Wait for app to launch

**Expected Result:**
- App opens in standalone mode (no browser UI)
- Splash screen may appear briefly
- Home page loads
- User state preserved (if was logged in)

---

### TC-PWA-004: Install - iOS Safari
**Priority:** Critical
**Preconditions:** Using Safari on iOS

**Steps:**
1. Visit the site in Safari
2. Tap share button
3. Tap "Add to Home Screen"
4. Confirm name and tap "Add"

**Expected Result:**
- App appears on home screen
- Icon is correct
- Name displays correctly (may be truncated)

---

### TC-PWA-005: Launch Installed App - iOS
**Priority:** Critical
**Preconditions:** App installed on iOS

**Steps:**
1. Tap app icon on home screen
2. Wait for app to launch

**Expected Result:**
- App opens (standalone-like experience)
- Splash screen appears
- Home page loads
- User state preserved

---

### TC-PWA-006: Offline Mode Indication
**Priority:** Medium
**Preconditions:** App installed, network available

**Steps:**
1. Open app while online
2. Turn on airplane mode
3. Continue using app
4. Attempt to load new content

**Expected Result:**
- Offline indicator appears
- Cached content still accessible
- New content requests show offline message
- No crashes or unhandled errors

---

### TC-PWA-007: Background Sync (if implemented)
**Priority:** Medium
**Preconditions:** App installed, user logged in

**Steps:**
1. Go offline
2. Mark a devotional as complete
3. Go back online
4. Check if action synced

**Expected Result:**
- Action queued while offline
- Syncs when connection restored
- No data lost

---

## 7. CROSS-CUTTING CONCERNS

### TC-GEN-001: Dark Mode Toggle
**Priority:** High
**Preconditions:** App supports dark mode

**Steps:**
1. Open settings
2. Toggle dark mode on
3. Navigate through app
4. Toggle dark mode off

**Expected Result:**
- Mode switches immediately
- All pages respect dark mode
- Text remains readable
- No color contrast issues
- Preference persists

---

### TC-GEN-002: Responsive Layout - Mobile
**Priority:** Critical
**Preconditions:** Mobile device or narrow viewport

**Steps:**
1. View all main pages on mobile
2. Check navigation, content, buttons

**Expected Result:**
- No horizontal scrolling
- Touch targets 44px minimum
- Text readable without zooming
- Navigation accessible
- No overlapping elements

---

### TC-GEN-003: Responsive Layout - Tablet
**Priority:** High
**Preconditions:** Tablet or medium viewport

**Steps:**
1. View all main pages on tablet
2. Check layout adaptations

**Expected Result:**
- Layout adapts appropriately
- Good use of available space
- Not just stretched mobile view

---

### TC-GEN-004: Responsive Layout - Desktop
**Priority:** High
**Preconditions:** Desktop or wide viewport

**Steps:**
1. View all main pages on desktop
2. Check content width and layout

**Expected Result:**
- Content doesn't stretch too wide
- Readable line lengths
- Navigation works with mouse
- Hover states present

---

### TC-GEN-005: Error Handling - Network Failure
**Priority:** High
**Preconditions:** App is online

**Steps:**
1. Start loading a page
2. Kill network mid-request
3. Observe error handling

**Expected Result:**
- User-friendly error message
- Retry option available
- No technical error details exposed
- App doesn't crash

---

### TC-GEN-006: Error Handling - Server Error
**Priority:** High
**Preconditions:** Ability to trigger server error

**Steps:**
1. Trigger a 500 error (if possible in test environment)
2. Observe app behavior

**Expected Result:**
- Friendly error message
- App remains usable
- Clear path to recovery
- Error logged for debugging

---

### TC-GEN-007: Page Load Performance
**Priority:** High
**Preconditions:** Lighthouse or DevTools available

**Steps:**
1. Run Lighthouse on home page
2. Run Lighthouse on devotional page
3. Check key metrics

**Expected Result:**
- LCP < 2.5s
- FID < 100ms
- CLS < 0.1
- Performance score > 90

---

### TC-GEN-008: Keyboard Navigation
**Priority:** Medium
**Preconditions:** Desktop with keyboard

**Steps:**
1. Navigate entire app using only Tab, Enter, Escape
2. Check all interactive elements

**Expected Result:**
- All buttons/links reachable
- Focus visible at all times
- Logical tab order
- Modals trap focus appropriately

---

## Test Execution Log

| Test ID | Date | Tester | Browser/Device | Status | Notes |
|---------|------|--------|----------------|--------|-------|
| TC-DEV-001 | | | | | |
| TC-DEV-002 | | | | | |
| ... | | | | | |

---

## Regression Test Suite

**Before each release, run these critical path tests:**

1. TC-DEV-001 - View Devotional
2. TC-DEV-002 - Complete Devotional
3. TC-SA-001 - Start Soul Audit
4. TC-SA-004 - Full Soul Audit Flow
5. TC-SA-006 - Crisis Detection
6. TC-BM-001 - Add Bookmark
7. TC-AUTH-005 - Sign In
8. TC-AUTH-008 - Sign Out
9. TC-PWA-005 - Launch Installed App

---

## Bug Reporting

When a test fails, create a bug report using the template in `45-bug-triage-template.md` with:

- Test case ID that failed
- Steps to reproduce
- Expected vs actual result
- Screenshots/recordings
- Device and browser details

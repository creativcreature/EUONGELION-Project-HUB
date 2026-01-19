# EUONGELION Integration Test Plan

**Document ID:** 81-integration-test-plan.md
**Created:** 2026-01-19
**Test Framework:** Playwright (recommended for e2e)
**Environment:** Next.js 15 App Router

---

## 1. Executive Summary

This document defines end-to-end integration tests for critical user flows in the EUONGELION application. Each flow includes the test scenario, detailed steps, and assertions to verify correct behavior.

### User Flow Categories

| Category | Flows | Priority |
|----------|-------|----------|
| Authentication | 5 | Critical |
| Devotional Reading | 6 | Critical |
| Series Navigation | 4 | High |
| Soul Audit | 3 | High |
| Progress & Streaks | 4 | High |
| Bookmarks | 3 | Medium |
| Settings | 4 | Medium |
| Offline/PWA | 4 | High |
| Search | 2 | Medium |
| Sharing | 2 | Low |

---

## 2. Authentication Flows

### 2.1 Email Sign Up

**Test ID:** AUTH-001
**Priority:** Critical
**Pre-conditions:** User not logged in

| Step | Action | Expected Result |
|------|--------|-----------------|
| 1 | Navigate to `/auth/signup` | Sign up form displayed |
| 2 | Enter name "Test User" | Name field populated |
| 3 | Enter email "test@example.com" | Email field populated |
| 4 | Enter password "TestPass123!" | Password field populated, strength indicator shows "Strong" |
| 5 | Enter confirm password "TestPass123!" | Passwords match indicator shown |
| 6 | Check "Accept Terms" checkbox | Checkbox checked |
| 7 | Click "Create Account" button | Loading state shown |
| 8 | Wait for completion | Redirected to `/onboarding` or home page |

**Assertions:**
- [ ] User session created in auth store
- [ ] Welcome notification appears
- [ ] User can access authenticated routes

**Edge Cases to Test:**
- Existing email address
- Weak password
- Password mismatch
- Invalid email format
- Network timeout

---

### 2.2 Email Sign In

**Test ID:** AUTH-002
**Priority:** Critical
**Pre-conditions:** Existing user account

| Step | Action | Expected Result |
|------|--------|-----------------|
| 1 | Navigate to `/auth/login` | Login form displayed |
| 2 | Enter email | Email field populated |
| 3 | Enter password | Password field masked |
| 4 | Click "Sign In" button | Loading state shown |
| 5 | Wait for completion | Redirected to home page |

**Assertions:**
- [ ] Session stored in auth store
- [ ] "Remember me" persists session (if checked)
- [ ] Previous reading state restored

**Edge Cases to Test:**
- Invalid credentials
- Account not found
- Account locked
- Rate limiting

---

### 2.3 OAuth Sign In (Google)

**Test ID:** AUTH-003
**Priority:** High
**Pre-conditions:** User not logged in

| Step | Action | Expected Result |
|------|--------|-----------------|
| 1 | Navigate to `/auth/login` | Login form with OAuth buttons displayed |
| 2 | Click "Continue with Google" | Google OAuth popup/redirect |
| 3 | Complete Google authentication | Return to app |
| 4 | Wait for completion | Redirected to home or onboarding |

**Assertions:**
- [ ] User profile populated from Google data
- [ ] Session created
- [ ] Email verified status correct

---

### 2.4 Sign Out

**Test ID:** AUTH-004
**Priority:** High
**Pre-conditions:** User logged in

| Step | Action | Expected Result |
|------|--------|-----------------|
| 1 | Navigate to settings | Settings page displayed |
| 2 | Click "Sign Out" button | Confirmation dialog (if implemented) |
| 3 | Confirm sign out | Loading state |
| 4 | Wait for completion | Redirected to home/login |

**Assertions:**
- [ ] Session cleared from auth store
- [ ] localStorage cleared appropriately
- [ ] Cannot access protected routes

---

### 2.5 Password Reset

**Test ID:** AUTH-005
**Priority:** Medium
**Pre-conditions:** Existing user account

| Step | Action | Expected Result |
|------|--------|-----------------|
| 1 | Navigate to `/auth/forgot-password` | Password reset form displayed |
| 2 | Enter email address | Email field populated |
| 3 | Click "Send Reset Link" | Loading state |
| 4 | Wait for completion | Success message displayed |

**Assertions:**
- [ ] Reset email sent (mock in tests)
- [ ] Clear instructions displayed
- [ ] Rate limiting prevents abuse

---

## 3. Devotional Reading Flows

### 3.1 Browse Daily Devotional

**Test ID:** DEV-001
**Priority:** Critical
**Pre-conditions:** App loaded

| Step | Action | Expected Result |
|------|--------|-----------------|
| 1 | Navigate to home page `/` | Today's devotional featured prominently |
| 2 | View devotional card | Title, scripture reference, excerpt visible |
| 3 | Check "Today" indicator | Current date/day indicator shown |

**Assertions:**
- [ ] Correct devotional for current day displayed
- [ ] Day of year calculation correct
- [ ] Thumbnail loads (if present)

---

### 3.2 Start Reading Devotional

**Test ID:** DEV-002
**Priority:** Critical
**Pre-conditions:** Devotional available

| Step | Action | Expected Result |
|------|--------|-----------------|
| 1 | Click on devotional card | Navigate to `/devotional/[id]` |
| 2 | View devotional page | Full content loaded |
| 3 | Select immersion level (5-minute) | Content displayed for selected level |
| 4 | Scroll through content | Scroll position tracked |
| 5 | View scripture passage | Scripture formatted correctly |

**Assertions:**
- [ ] Reading state initialized in devotionalStore
- [ ] Timer started tracking reading time
- [ ] Correct immersion level content shown

---

### 3.3 Complete Devotional Reading

**Test ID:** DEV-003
**Priority:** Critical
**Pre-conditions:** Reading in progress

| Step | Action | Expected Result |
|------|--------|-----------------|
| 1 | Scroll to bottom of content | Full content visible |
| 2 | Click "Mark as Complete" | Completion modal/confirmation |
| 3 | Confirm completion | Success feedback |
| 4 | View completion animation | Celebration animation plays |

**Assertions:**
- [ ] Reading added to history
- [ ] Progress recorded in progressStore
- [ ] Streak updated if applicable
- [ ] Daily progress updated

---

### 3.4 Change Immersion Level

**Test ID:** DEV-004
**Priority:** High
**Pre-conditions:** Reading devotional

| Step | Action | Expected Result |
|------|--------|-----------------|
| 1 | View current level (5-minute) | 5-minute content displayed |
| 2 | Click "1-minute" option | Content changes to shorter version |
| 3 | Click "15-minute" option | Content expands to full version |

**Assertions:**
- [ ] Content updates without page reload
- [ ] Scroll position preserved or reset appropriately
- [ ] Reading state updated with new level

---

### 3.5 Add Reflection/Notes

**Test ID:** DEV-005
**Priority:** Medium
**Pre-conditions:** Reading devotional

| Step | Action | Expected Result |
|------|--------|-----------------|
| 1 | Scroll to reflection questions | Questions displayed |
| 2 | Click on text area | Keyboard appears (mobile) |
| 3 | Type reflection response | Text captured |
| 4 | Save reflection | Saved confirmation |

**Assertions:**
- [ ] Reflection saved to user notes
- [ ] Autosave works (if implemented)
- [ ] Notes persisted across sessions

---

### 3.6 View Devotional History

**Test ID:** DEV-006
**Priority:** Medium
**Pre-conditions:** User has reading history

| Step | Action | Expected Result |
|------|--------|-----------------|
| 1 | Navigate to progress page | History section visible |
| 2 | View past readings | List of completed devotionals |
| 3 | Click on past devotional | Navigate to that devotional |

**Assertions:**
- [ ] History sorted by date (newest first)
- [ ] Completed indicator shown
- [ ] Time spent recorded

---

## 4. Series Navigation Flows

### 4.1 Browse Series List

**Test ID:** SER-001
**Priority:** High
**Pre-conditions:** Series available

| Step | Action | Expected Result |
|------|--------|-----------------|
| 1 | Navigate to `/series` | Series grid/list displayed |
| 2 | View series cards | Title, description, day count visible |
| 3 | Filter/sort series (if available) | Results update |

**Assertions:**
- [ ] All published series displayed
- [ ] Progress indicators show for started series
- [ ] Thumbnails load correctly

---

### 4.2 Start New Series

**Test ID:** SER-002
**Priority:** High
**Pre-conditions:** Not enrolled in series

| Step | Action | Expected Result |
|------|--------|-----------------|
| 1 | Click on series card | Navigate to `/series/[slug]` |
| 2 | View series detail page | Full description, outline visible |
| 3 | Click "Start Series" | Series enrollment modal |
| 4 | Confirm start | Redirected to Day 1 devotional |

**Assertions:**
- [ ] Series progress initialized
- [ ] First devotional loaded
- [ ] "In Progress" indicator shown

---

### 4.3 Continue Series

**Test ID:** SER-003
**Priority:** High
**Pre-conditions:** Series in progress

| Step | Action | Expected Result |
|------|--------|-----------------|
| 1 | Navigate to series page | Current progress shown |
| 2 | Click "Continue" | Next unread devotional loaded |
| 3 | View progress bar | Accurate percentage |

**Assertions:**
- [ ] Correct next day calculated
- [ ] Previous completions tracked
- [ ] Progress percentage accurate

---

### 4.4 Complete Series

**Test ID:** SER-004
**Priority:** Medium
**Pre-conditions:** All but last devotional complete

| Step | Action | Expected Result |
|------|--------|-----------------|
| 1 | Complete final devotional | Completion modal |
| 2 | View series completion celebration | Special animation/message |
| 3 | Return to series page | "Completed" badge shown |

**Assertions:**
- [ ] Series marked complete in progressStore
- [ ] Achievement notification (if implemented)
- [ ] Stats updated

---

## 5. Soul Audit Flows

### 5.1 Start Soul Audit

**Test ID:** SOUL-001
**Priority:** High
**Pre-conditions:** Soul Audit available

| Step | Action | Expected Result |
|------|--------|-----------------|
| 1 | Navigate to `/soul-audit` | Soul Audit intro page |
| 2 | Read instructions | Clear explanation displayed |
| 3 | Click "Begin Assessment" | First question displayed |

**Assertions:**
- [ ] Session ID generated
- [ ] Analytics event fired
- [ ] Progress starts at 0%

---

### 5.2 Complete Soul Audit

**Test ID:** SOUL-002
**Priority:** High
**Pre-conditions:** Soul Audit started

| Step | Action | Expected Result |
|------|--------|-----------------|
| 1 | Answer question 1 | Progress to next question |
| 2 | Continue through all questions | Progress bar updates |
| 3 | Submit final answer | Processing state |
| 4 | View results | Comprehensive results displayed |

**Assertions:**
- [ ] All categories scored
- [ ] Recommendations generated
- [ ] Results saved to user profile

---

### 5.3 Review Soul Audit Results

**Test ID:** SOUL-003
**Priority:** Medium
**Pre-conditions:** Completed Soul Audit

| Step | Action | Expected Result |
|------|--------|-----------------|
| 1 | Navigate to results | Previous results displayed |
| 2 | View category breakdown | Score per category |
| 3 | View recommended series | Personalized recommendations |

**Assertions:**
- [ ] Historical results accessible
- [ ] Comparison over time (if multiple)
- [ ] Recommendations link to series

---

## 6. Progress & Streak Flows

### 6.1 View Current Streak

**Test ID:** PROG-001
**Priority:** High
**Pre-conditions:** Active streak

| Step | Action | Expected Result |
|------|--------|-----------------|
| 1 | View home page header | Streak count displayed |
| 2 | Navigate to progress | Detailed streak info |

**Assertions:**
- [ ] Streak count accurate
- [ ] Streak dates recorded
- [ ] Fire emoji or visual indicator

---

### 6.2 Maintain Streak (Complete Daily)

**Test ID:** PROG-002
**Priority:** High
**Pre-conditions:** Streak in progress

| Step | Action | Expected Result |
|------|--------|-----------------|
| 1 | Complete daily devotional | Streak maintained message |
| 2 | View updated streak | Count incremented |

**Assertions:**
- [ ] Streak continues
- [ ] Last activity date updated
- [ ] Calendar view updated (if present)

---

### 6.3 Streak Milestone Achievement

**Test ID:** PROG-003
**Priority:** Medium
**Pre-conditions:** Near milestone (7, 14, 30, etc.)

| Step | Action | Expected Result |
|------|--------|-----------------|
| 1 | Complete reading at milestone | Special celebration |
| 2 | View milestone notification | Achievement unlocked |

**Assertions:**
- [ ] Milestone notification shown
- [ ] Analytics event tracked
- [ ] Badge/achievement recorded

---

### 6.4 Streak Recovery (Grace Period)

**Test ID:** PROG-004
**Priority:** Medium
**Pre-conditions:** Missed one day

| Step | Action | Expected Result |
|------|--------|-----------------|
| 1 | Return within 48 hours | Streak intact warning |
| 2 | Complete reading | Streak continues |

**Assertions:**
- [ ] Grace period working (48 hours)
- [ ] Warning message displayed
- [ ] Streak preserved

---

## 7. Bookmark Flows

### 7.1 Bookmark Devotional

**Test ID:** BOOK-001
**Priority:** Medium
**Pre-conditions:** Viewing devotional

| Step | Action | Expected Result |
|------|--------|-----------------|
| 1 | Click bookmark icon | Icon fills/toggles |
| 2 | View confirmation | Toast/feedback shown |

**Assertions:**
- [ ] Bookmark saved to bookmarkStore
- [ ] Icon state updated
- [ ] Synced to server (if online)

---

### 7.2 View Bookmarks

**Test ID:** BOOK-002
**Priority:** Medium
**Pre-conditions:** Has bookmarks

| Step | Action | Expected Result |
|------|--------|-----------------|
| 1 | Navigate to bookmarks page | Bookmarked items listed |
| 2 | Click bookmarked item | Navigate to devotional |

**Assertions:**
- [ ] All bookmarks displayed
- [ ] Sorted by date bookmarked
- [ ] Can navigate to each

---

### 7.3 Remove Bookmark

**Test ID:** BOOK-003
**Priority:** Medium
**Pre-conditions:** Item bookmarked

| Step | Action | Expected Result |
|------|--------|-----------------|
| 1 | Click bookmark icon (filled) | Icon unfills |
| 2 | View bookmarks list | Item removed |

**Assertions:**
- [ ] Bookmark removed from store
- [ ] Immediate UI update
- [ ] Synced to server

---

## 8. Settings Flows

### 8.1 Change Theme

**Test ID:** SET-001
**Priority:** Medium
**Pre-conditions:** User logged in

| Step | Action | Expected Result |
|------|--------|-----------------|
| 1 | Navigate to settings | Theme options visible |
| 2 | Select "Light" theme | Theme changes immediately |
| 3 | Select "Sepia" theme | Theme changes to sepia |
| 4 | Select "System" | Matches OS preference |

**Assertions:**
- [ ] Theme persisted to localStorage
- [ ] CSS variables updated
- [ ] No flash on reload

---

### 8.2 Configure Notifications

**Test ID:** SET-002
**Priority:** Medium
**Pre-conditions:** User logged in

| Step | Action | Expected Result |
|------|--------|-----------------|
| 1 | Navigate to notification settings | Toggle options visible |
| 2 | Enable daily reminders | Permission request (if needed) |
| 3 | Set reminder time | Time picker works |

**Assertions:**
- [ ] Push permission requested
- [ ] Preferences saved
- [ ] Notification scheduled

---

### 8.3 Update Profile

**Test ID:** SET-003
**Priority:** Medium
**Pre-conditions:** User logged in

| Step | Action | Expected Result |
|------|--------|-----------------|
| 1 | Navigate to profile settings | Current info displayed |
| 2 | Update display name | Field editable |
| 3 | Save changes | Success feedback |

**Assertions:**
- [ ] Profile updated in database
- [ ] Display name reflects everywhere
- [ ] Validation enforced

---

### 8.4 Export Data

**Test ID:** SET-004
**Priority:** Low
**Pre-conditions:** User has data

| Step | Action | Expected Result |
|------|--------|-----------------|
| 1 | Navigate to data/privacy settings | Export option visible |
| 2 | Click "Export My Data" | Processing state |
| 3 | Download file | JSON/CSV downloaded |

**Assertions:**
- [ ] All user data included
- [ ] Format correct
- [ ] GDPR compliant

---

## 9. Offline/PWA Flows

### 9.1 Install PWA

**Test ID:** PWA-001
**Priority:** High
**Pre-conditions:** Browser supports PWA

| Step | Action | Expected Result |
|------|--------|-----------------|
| 1 | Visit app in supported browser | Install prompt appears |
| 2 | Click "Install" | App installs |
| 3 | Open installed app | App launches standalone |

**Assertions:**
- [ ] Service worker registered
- [ ] App manifest loaded
- [ ] Icon on home screen

---

### 9.2 Offline Reading

**Test ID:** PWA-002
**Priority:** High
**Pre-conditions:** Online, content cached

| Step | Action | Expected Result |
|------|--------|-----------------|
| 1 | Load devotional while online | Content cached |
| 2 | Go offline | Offline indicator appears |
| 3 | Navigate to cached devotional | Content displays |

**Assertions:**
- [ ] Offline indicator visible
- [ ] Cached content accessible
- [ ] Reading progress tracked locally

---

### 9.3 Sync When Online

**Test ID:** PWA-003
**Priority:** High
**Pre-conditions:** Offline changes made

| Step | Action | Expected Result |
|------|--------|-----------------|
| 1 | Complete devotional offline | Saved locally |
| 2 | Come back online | Sync begins |
| 3 | View sync status | "Synced" confirmation |

**Assertions:**
- [ ] Offline progress synced
- [ ] No data loss
- [ ] Server state updated

---

### 9.4 Download for Offline

**Test ID:** PWA-004
**Priority:** Medium
**Pre-conditions:** Online

| Step | Action | Expected Result |
|------|--------|-----------------|
| 1 | Navigate to series | Download option visible |
| 2 | Click "Download for Offline" | Download progress |
| 3 | Go offline and navigate | Series accessible |

**Assertions:**
- [ ] All series devotionals cached
- [ ] Images cached
- [ ] Storage quota respected

---

## 10. Search Flows

### 10.1 Search Devotionals

**Test ID:** SRCH-001
**Priority:** Medium
**Pre-conditions:** Search available

| Step | Action | Expected Result |
|------|--------|-----------------|
| 1 | Click search icon | Search modal/page opens |
| 2 | Type "love" | Results update as typing |
| 3 | Click result | Navigate to devotional |

**Assertions:**
- [ ] Results relevant to query
- [ ] Search highlights matches
- [ ] Recent searches saved

---

### 10.2 Search Scripture Reference

**Test ID:** SRCH-002
**Priority:** Medium
**Pre-conditions:** Search available

| Step | Action | Expected Result |
|------|--------|-----------------|
| 1 | Type "John 3:16" | Results with that scripture |
| 2 | View results | Scripture reference highlighted |

**Assertions:**
- [ ] Scripture parsing works
- [ ] Results include relevant devotionals
- [ ] Exact match prioritized

---

## 11. Sharing Flows

### 11.1 Share Devotional

**Test ID:** SHARE-001
**Priority:** Low
**Pre-conditions:** Viewing devotional

| Step | Action | Expected Result |
|------|--------|-----------------|
| 1 | Click share button | Share options displayed |
| 2 | Select share method | Native share dialog or copy link |

**Assertions:**
- [ ] Share link generated
- [ ] Link works for recipient
- [ ] Analytics tracked

---

### 11.2 Copy Scripture

**Test ID:** SHARE-002
**Priority:** Low
**Pre-conditions:** Viewing devotional

| Step | Action | Expected Result |
|------|--------|-----------------|
| 1 | Long press/right-click scripture | Copy option visible |
| 2 | Click "Copy" | Text copied to clipboard |

**Assertions:**
- [ ] Full verse text copied
- [ ] Reference included
- [ ] Toast confirmation

---

## 12. Test Data Requirements

### Required Test Fixtures

```
- Test user accounts (various states)
- Sample devotionals (various types)
- Sample series (7-day, 14-day, 30-day)
- Soul Audit questions and answers
- Pre-populated progress data
- Bookmarked items
```

### Environment Setup

```
- Clean database state before each test suite
- Seed data for specific scenarios
- Mock external services (email, push notifications)
- Network condition simulation (offline, slow)
```

---

## 13. Test Execution Schedule

| Phase | Flows | Duration | Frequency |
|-------|-------|----------|-----------|
| Smoke | AUTH-001, DEV-002, PWA-002 | 5 min | Every deploy |
| Critical Path | All AUTH, DEV | 15 min | Every PR |
| Full Regression | All flows | 45 min | Nightly |
| Manual Exploratory | Edge cases | 2 hrs | Weekly |

---

## 14. Success Criteria

- All Critical priority tests pass: 100%
- All High priority tests pass: 95%
- All Medium priority tests pass: 90%
- Total E2E test coverage: 80%
- Average test execution time: < 45 minutes

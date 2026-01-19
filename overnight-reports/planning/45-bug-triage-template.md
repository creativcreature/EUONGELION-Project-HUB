# EUONGELION Bug Triage Template

**Purpose:** Standardized template for categorizing, reporting, and tracking bugs
**Last Updated:** 2026-01-19
**Version:** 1.0

---

## Bug Report Template

Copy this template for each new bug:

```markdown
## Bug Report

### Bug ID: BUG-XXXX

**Reported By:** [Name/Email]
**Reported Date:** YYYY-MM-DD
**Status:** New | Triaged | In Progress | Fixed | Verified | Closed | Won't Fix

---

### Summary
[One sentence description of the bug]

---

### Severity
[ ] **Critical** - App unusable, data loss, security vulnerability
[ ] **High** - Major feature broken, no workaround
[ ] **Medium** - Feature impaired, workaround exists
[ ] **Low** - Minor issue, cosmetic, edge case

### Priority
[ ] **P1** - Fix immediately (within 24 hours)
[ ] **P2** - Fix this sprint
[ ] **P3** - Fix next sprint
[ ] **P4** - Fix when time permits
[ ] **P5** - Backlog / Nice to have

---

### Environment

**Device:** [iPhone 14, Samsung Galaxy S23, MacBook Pro, etc.]
**OS Version:** [iOS 17.2, Android 14, macOS 14.2, Windows 11, etc.]
**Browser:** [Safari 17, Chrome 120, Firefox 121, etc.]
**App Version:** [1.0.0, commit hash if known]
**Network:** [WiFi, 4G, Offline]
**User State:** [Logged in, Guest, New user]

---

### Steps to Reproduce

1. [First step]
2. [Second step]
3. [Third step]
4. [Continue as needed]

**Frequency:** [Always | Sometimes (X% of time) | Once]

---

### Expected Result
[What should happen]

---

### Actual Result
[What actually happens]

---

### Screenshots / Videos
[Attach or link to visual evidence]

---

### Logs / Error Messages
```
[Paste any console errors, network errors, or stack traces]
```

---

### Affected Users
[ ] All users
[ ] Logged-in users only
[ ] Guest users only
[ ] Specific device/browser
[ ] Specific user segment: [describe]

**Estimated Impact:** [Number or percentage of users affected]

---

### Workaround
[ ] None available
[ ] Workaround available:
    [Describe the workaround]

---

### Related Issues
- [Link to related bugs or features]

---

### Notes
[Any additional context, observations, or theories about the cause]
```

---

## Severity Definitions

### Critical (S1)
**Definition:** The application is completely unusable, data loss has occurred, or there is a security vulnerability.

**Examples:**
- App crashes on launch
- User data is deleted or corrupted
- Authentication bypass possible
- Payment processing broken
- Crisis resources (988 Lifeline) not displaying correctly
- User cannot sign in or sign up

**Response Time:** Immediate
**Resolution Target:** < 24 hours
**Escalation:** Alert entire team immediately

---

### High (S2)
**Definition:** A major feature is completely broken with no workaround available.

**Examples:**
- Devotionals won't load
- Soul Audit results not displaying
- Bookmarks not saving
- Reading progress not tracking
- PWA won't install
- Offline mode completely broken

**Response Time:** < 4 hours
**Resolution Target:** < 3 days
**Escalation:** Notify lead developer

---

### Medium (S3)
**Definition:** Feature is impaired but a workaround exists, or issue affects a subset of users.

**Examples:**
- Share to Twitter not working (copy link still works)
- Dark mode colors incorrect on some screens
- Slow performance on older devices
- Series progress shows wrong count
- Search results not quite accurate
- Minor layout issues on specific screen sizes

**Response Time:** < 24 hours
**Resolution Target:** Current or next sprint
**Escalation:** Standard process

---

### Low (S4)
**Definition:** Minor issues that don't significantly impact user experience.

**Examples:**
- Typo in UI text
- Minor animation glitch
- Icon slightly misaligned
- Hover state missing on desktop
- Console warnings (non-blocking)
- Edge case only reproducible under unusual conditions

**Response Time:** Next triage meeting
**Resolution Target:** When time permits
**Escalation:** None required

---

## Priority Definitions

### P1 - Emergency
- Drop everything and fix
- Affects all users or has security implications
- Typically Critical severity bugs
- Fixed and deployed within 24 hours

### P2 - Current Sprint
- Fix before sprint ends
- High severity bugs
- Significant user impact
- May delay other work

### P3 - Next Sprint
- Plan for upcoming sprint
- Medium severity bugs
- Can wait but shouldn't linger

### P4 - Backlog
- Add to backlog for future sprint
- Low severity or limited impact
- Fix when convenient

### P5 - Nice to Have
- May never fix
- Very edge case
- Minimal user impact
- Consider for future refactoring

---

## Triage Process

### Daily Triage (5 minutes)
1. Review new bug reports from past 24 hours
2. Assign initial severity
3. Escalate Critical/P1 bugs immediately
4. Add to triage queue for weekly meeting

### Weekly Triage Meeting (30 minutes)
1. Review all bugs in triage queue
2. Confirm severity assignments
3. Assign priority
4. Assign owner
5. Add to appropriate sprint/backlog
6. Review bug metrics

### Triage Checklist
- [ ] Bug is reproducible (or attempted reproduction)
- [ ] Severity assigned
- [ ] Priority assigned
- [ ] Owner assigned
- [ ] Added to sprint or backlog
- [ ] Reporter notified of status
- [ ] Related issues linked

---

## Bug Lifecycle

```
[New] -> [Triaged] -> [In Progress] -> [Fixed] -> [Verified] -> [Closed]
                |                          |
                +-- [Won't Fix] <----------+
                |
                +-- [Duplicate] (link to original)
```

### Status Definitions

| Status | Description |
|--------|-------------|
| New | Just reported, not yet reviewed |
| Triaged | Reviewed, severity/priority assigned |
| In Progress | Developer actively working on fix |
| Fixed | Code fix complete, awaiting deployment |
| Verified | Fix confirmed working in production |
| Closed | Issue fully resolved |
| Won't Fix | Decided not to fix (document reason) |
| Duplicate | Same as another bug (link to original) |

---

## Bug Categories

### Functional
- [ ] Authentication (login, signup, logout)
- [ ] Devotional Display
- [ ] Soul Audit
- [ ] Bookmarks
- [ ] Progress Tracking
- [ ] Series Navigation
- [ ] Search
- [ ] Share Functionality
- [ ] Settings

### Technical
- [ ] Performance
- [ ] PWA / Service Worker
- [ ] Offline Functionality
- [ ] API Errors
- [ ] Database Issues
- [ ] Caching
- [ ] State Management

### UI/UX
- [ ] Layout / Responsive
- [ ] Dark Mode
- [ ] Accessibility
- [ ] Animation
- [ ] Typography
- [ ] Color / Contrast
- [ ] Touch Targets

### Content
- [ ] Typo / Grammar
- [ ] Incorrect Scripture
- [ ] Missing Content
- [ ] Broken Links

### Platform-Specific
- [ ] iOS Safari
- [ ] Android Chrome
- [ ] Desktop Chrome
- [ ] Desktop Safari
- [ ] Desktop Firefox

---

## Bug Report Examples

### Example 1: Critical Bug

```markdown
## Bug Report

### Bug ID: BUG-0001

**Reported By:** jane@example.com
**Reported Date:** 2026-01-19
**Status:** New

---

### Summary
Crisis detection not showing 988 Lifeline resources

---

### Severity
[x] **Critical** - App unusable, data loss, security vulnerability

### Priority
[x] **P1** - Fix immediately (within 24 hours)

---

### Environment

**Device:** iPhone 14 Pro
**OS Version:** iOS 17.2
**Browser:** Safari 17
**App Version:** 1.0.0
**Network:** WiFi
**User State:** New user

---

### Steps to Reproduce

1. Navigate to Soul Audit
2. Enter text containing "I don't want to live anymore"
3. Submit the response
4. View results screen

**Frequency:** Always

---

### Expected Result
Crisis response screen should appear with 988 Lifeline, Crisis Text Line, and support resources prominently displayed.

---

### Actual Result
Regular results page appears without crisis resources. User in crisis does not see help information.

---

### Screenshots / Videos
[screenshot_crisis_bug.png]

---

### Affected Users
[x] All users

**Estimated Impact:** Any user in crisis - LIFE SAFETY ISSUE

---

### Workaround
[ ] None available

---

### Notes
This is a critical safety issue. The crisis detection keywords may not be matching correctly, or the conditional rendering is broken.
```

### Example 2: Medium Bug

```markdown
## Bug Report

### Bug ID: BUG-0015

**Reported By:** john@example.com
**Reported Date:** 2026-01-19
**Status:** Triaged

---

### Summary
Dark mode toggle doesn't persist after closing app

---

### Severity
[ ] Critical
[ ] High
[x] **Medium** - Feature impaired, workaround exists
[ ] Low

### Priority
[x] **P3** - Fix next sprint

---

### Environment

**Device:** Google Pixel 7
**OS Version:** Android 14
**Browser:** Chrome 120
**App Version:** 1.0.0
**Network:** WiFi
**User State:** Logged in

---

### Steps to Reproduce

1. Open app settings
2. Toggle dark mode ON
3. Close app completely (swipe away)
4. Reopen app
5. Observe theme setting

**Frequency:** Always

---

### Expected Result
Dark mode setting should persist, app should open in dark mode.

---

### Actual Result
App opens in light mode. User must toggle dark mode again each session.

---

### Affected Users
[ ] All users
[x] Logged-in users only

**Estimated Impact:** ~60% of users (those who prefer dark mode)

---

### Workaround
[x] Workaround available:
    User can toggle dark mode again each time they open the app.

---

### Notes
Likely issue with localStorage/preference not being read on app init, or preference not being saved correctly.
```

---

## Bug Metrics to Track

### Weekly Metrics
- Total open bugs by severity
- Bugs opened this week
- Bugs closed this week
- Average time to resolution by severity
- Bugs by category
- Bugs by platform

### Monthly Report Template

```markdown
## Bug Report - [Month Year]

### Summary
- Total bugs opened: XX
- Total bugs closed: XX
- Net change: +/- XX

### By Severity
| Severity | Opened | Closed | Open at End |
|----------|--------|--------|-------------|
| Critical | X | X | X |
| High | X | X | X |
| Medium | X | X | X |
| Low | X | X | X |

### Average Resolution Time
- Critical: X hours
- High: X days
- Medium: X days
- Low: X days

### Top Bug Categories
1. [Category] - XX bugs
2. [Category] - XX bugs
3. [Category] - XX bugs

### Notable Issues
- [BUG-XXXX] - [Brief description and impact]

### Recommendations
- [Areas needing attention]
```

---

## Integration with Tools

### GitHub Issues
When creating GitHub issues for bugs:
- Use label: `bug`
- Use label: `severity: critical|high|medium|low`
- Use label: `priority: p1|p2|p3|p4|p5`
- Include Bug ID in title: `[BUG-0001] Crisis resources not displaying`

### Sentry Integration
- Link Sentry issue IDs to bug reports
- Include stack traces from Sentry
- Tag bugs with Sentry event IDs for tracking

---

## Quick Reference Card

### When You Find a Bug
1. Check if already reported
2. Create bug report using template
3. Assign severity based on definitions
4. If Critical: Alert team immediately
5. Add screenshots/logs if possible

### Severity Quick Guide
| Severity | Ask Yourself |
|----------|--------------|
| Critical | Is the app unusable? Is data at risk? |
| High | Is a major feature broken with no workaround? |
| Medium | Can users work around it? |
| Low | Is it cosmetic or very edge case? |

### Priority Quick Guide
| Priority | When to Use |
|----------|-------------|
| P1 | Drop everything, fix now |
| P2 | Must fix this sprint |
| P3 | Plan for next sprint |
| P4 | Backlog, fix when able |
| P5 | May never fix |

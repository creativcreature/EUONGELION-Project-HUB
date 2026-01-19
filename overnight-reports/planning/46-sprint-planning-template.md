# EUONGELION Sprint Planning Template

**Purpose:** Reusable template for planning development sprints
**Last Updated:** 2026-01-19
**Version:** 1.0

---

## Sprint Template

Copy this template for each new sprint:

```markdown
# Sprint [NUMBER]: [THEME/NAME]

**Sprint Duration:** [Start Date] - [End Date]
**Sprint Goal:** [One sentence describing the main objective]

---

## Sprint Overview

### Theme
[Brief description of what this sprint focuses on]

### Success Criteria
At the end of this sprint, we will have:
- [ ] [Specific, measurable outcome 1]
- [ ] [Specific, measurable outcome 2]
- [ ] [Specific, measurable outcome 3]

### Key Metrics
- [ ] [Metric to track]
- [ ] [Metric to track]

---

## Sprint Backlog

### Features

| ID | Feature | Estimated Points | Owner | Status |
|----|---------|-----------------|-------|--------|
| F-XXX | [Feature name] | X | @name | Not Started |
| F-XXX | [Feature name] | X | @name | Not Started |

### Bug Fixes

| Bug ID | Description | Severity | Owner | Status |
|--------|-------------|----------|-------|--------|
| BUG-XXX | [Bug description] | High | @name | Not Started |
| BUG-XXX | [Bug description] | Medium | @name | Not Started |

### Technical Debt

| ID | Description | Impact | Owner | Status |
|----|-------------|--------|-------|--------|
| TD-XXX | [Description] | [Impact] | @name | Not Started |

### Content Tasks

| ID | Description | Owner | Status |
|----|-------------|-------|--------|
| C-XXX | [Content task] | @name | Not Started |

---

## Task Breakdown

### Feature: [F-XXX] [Feature Name]

**Acceptance Criteria:**
- [ ] [Criterion 1 - specific, testable]
- [ ] [Criterion 2]
- [ ] [Criterion 3]

**Tasks:**
- [ ] [Task 1] - X hours
- [ ] [Task 2] - X hours
- [ ] [Task 3] - X hours

**Dependencies:**
- [Any blockers or dependencies]

**Notes:**
- [Implementation notes, design decisions, etc.]

---

### Feature: [F-XXX] [Feature Name]

**Acceptance Criteria:**
- [ ] [Criterion 1]
- [ ] [Criterion 2]

**Tasks:**
- [ ] [Task 1] - X hours
- [ ] [Task 2] - X hours

---

## Capacity Planning

### Team Availability

| Team Member | Available Days | Notes |
|-------------|---------------|-------|
| @name | X days | [PTO, meetings, etc.] |
| @name | X days | |

### Total Capacity
- Available person-days: X
- Buffer (20%): X
- Net capacity: X days

### Point Allocation
- Features: X points
- Bugs: X points
- Tech Debt: X points
- **Total:** X points

---

## Risks & Mitigations

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| [Risk 1] | High/Med/Low | High/Med/Low | [How to mitigate] |
| [Risk 2] | | | |

---

## Dependencies

### External Dependencies
- [ ] [Dependency 1] - Owner: @name, Due: [Date]
- [ ] [Dependency 2]

### Internal Dependencies
- [ ] [Feature A must complete before Feature B]

---

## Definition of Done

For all items in this sprint:
- [ ] Code complete and tested
- [ ] Code reviewed and approved
- [ ] Unit tests passing
- [ ] Manual QA completed
- [ ] Documentation updated (if applicable)
- [ ] Deployed to staging
- [ ] Product owner approved
- [ ] Merged to main branch
- [ ] Deployed to production

---

## Sprint Events

### Planning
- **Date:** [Date]
- **Attendees:** [Names]
- **Duration:** 1-2 hours

### Daily Standups
- **Time:** [Time]
- **Format:** Async / Sync
- **Questions:**
  1. What did you complete?
  2. What are you working on?
  3. Any blockers?

### Mid-Sprint Check-in
- **Date:** [Mid-sprint date]
- **Focus:** Progress review, scope adjustment if needed

### Sprint Review
- **Date:** [End date]
- **Attendees:** [Names]
- **Agenda:**
  1. Demo completed work
  2. Review metrics
  3. Gather feedback

### Sprint Retrospective
- **Date:** [End date]
- **Format:** Start/Stop/Continue
- **Action Items:**
  - [ ] [Item from retro]

---

## Sprint Log

### [Date]
- [Notes, updates, decisions made]

### [Date]
- [Notes]

---

## Sprint Summary (Fill at end)

### Completed
- [x] [Item completed]
- [x] [Item completed]

### Not Completed (Carried Over)
- [ ] [Item] - Reason: [Why not completed]

### Metrics
- Features completed: X/X
- Bugs fixed: X/X
- Points completed: X/X
- Velocity: X points

### Lessons Learned
- [What went well]
- [What could improve]
- [Action items for next sprint]
```

---

## Sprint Cadence

### Recommended: 2-Week Sprints

```
Week 1:
  Mon: Sprint Planning (2 hrs)
  Tue-Thu: Development
  Fri: Mid-sprint check-in (30 min)

Week 2:
  Mon-Wed: Development
  Thu: Code freeze, final testing
  Fri: Sprint Review (1 hr) + Retrospective (30 min)
```

### Alternative: 1-Week Sprints (for early stage)

```
Mon: Planning (1 hr)
Tue-Thu: Development
Fri: Review + Retro (1 hr combined)
```

---

## Story Point Guide

### Fibonacci Scale (Recommended)

| Points | Description | Example |
|--------|-------------|---------|
| 1 | Trivial, < 2 hours | Fix typo, update copy |
| 2 | Simple, half day | Add loading state, minor styling |
| 3 | Moderate, 1 day | New component, simple feature |
| 5 | Medium, 2-3 days | Feature with API integration |
| 8 | Large, 3-5 days | Complex feature, multiple components |
| 13 | Very large, week+ | **Break this down** |

### Guidelines
- If estimate is 13+, break into smaller tasks
- Include testing time in estimates
- Account for code review time
- When uncertain, round up

---

## Acceptance Criteria Best Practices

### Format: Given/When/Then

```
Given [context/precondition]
When [action taken]
Then [expected result]
```

### Examples

**Feature: Bookmark a Devotional**
```
Given I am a logged-in user viewing a devotional
When I tap the bookmark icon
Then the icon should change to filled state
And the devotional should appear in my bookmarks list
And a success toast should appear briefly
```

**Feature: Dark Mode Toggle**
```
Given I am on the settings page
When I toggle the dark mode switch
Then the entire app should switch to dark theme immediately
And my preference should persist after closing the app
```

### Checklist for Good Acceptance Criteria
- [ ] Specific and measurable
- [ ] From user's perspective
- [ ] Testable
- [ ] Covers happy path
- [ ] Covers error cases
- [ ] Includes edge cases

---

## Sprint Ceremonies Details

### Sprint Planning

**Purpose:** Define sprint goal and select items for the sprint

**Inputs:**
- Prioritized backlog
- Team capacity
- Previous sprint velocity
- Technical dependencies

**Outputs:**
- Sprint goal
- Sprint backlog
- Task breakdown
- Commitments

**Agenda:**
1. Review product priorities (15 min)
2. Discuss top backlog items (30 min)
3. Estimate and select items (45 min)
4. Break down tasks (30 min)
5. Confirm commitments (15 min)

---

### Daily Standup

**Purpose:** Sync on progress and surface blockers

**Format Options:**

*Async (Slack/Discord):*
Post by 9 AM:
```
Yesterday: [What you completed]
Today: [What you're working on]
Blockers: [Any blockers or help needed]
```

*Sync (15 min max):*
- Each person answers three questions
- Park discussions for after standup
- Focus on blockers

---

### Sprint Review

**Purpose:** Demo work, gather feedback, celebrate wins

**Agenda:**
1. Sprint goal recap (5 min)
2. Demo completed features (20-30 min)
3. Review metrics (5 min)
4. Q&A and feedback (10 min)
5. Preview next sprint (5 min)

**Tips:**
- Demo in production if possible
- Show real user scenarios
- Celebrate the wins!

---

### Sprint Retrospective

**Purpose:** Continuous improvement

**Format Options:**

*Start/Stop/Continue:*
- Start: What should we start doing?
- Stop: What should we stop doing?
- Continue: What's working well?

*4 L's:*
- Liked: What did we like?
- Learned: What did we learn?
- Lacked: What were we missing?
- Longed for: What do we wish we had?

*Mad/Sad/Glad:*
- Mad: What frustrated us?
- Sad: What disappointed us?
- Glad: What made us happy?

**Output:** 1-3 actionable improvements for next sprint

---

## Velocity Tracking

### Sprint Velocity Log

| Sprint | Planned Points | Completed Points | Velocity |
|--------|---------------|-----------------|----------|
| 1 | 20 | 18 | 18 |
| 2 | 20 | 22 | 22 |
| 3 | 22 | 20 | 20 |
| **Avg** | | | **20** |

### Using Velocity
- Use 3-sprint rolling average for planning
- Don't inflate velocity artificially
- Velocity is for planning, not performance measurement
- Expect variation (+/- 20%)

---

## Example: Sprint 1 Post-Launch

```markdown
# Sprint 1: Quick Wins & Stability

**Sprint Duration:** 2026-02-01 - 2026-02-14
**Sprint Goal:** Deliver quick wins that improve daily engagement while fixing critical post-launch bugs

---

## Sprint Overview

### Theme
Address early user feedback, implement daily reminders, and stabilize the platform.

### Success Criteria
At the end of this sprint, we will have:
- [ ] Daily reminder system working for all users
- [ ] All critical bugs from launch week fixed
- [ ] Email verification flow complete
- [ ] Reading time estimates on all devotionals

### Key Metrics
- [ ] Daily active users stable or increasing
- [ ] Crash rate < 1%
- [ ] Customer support tickets decreasing

---

## Sprint Backlog

### Features

| ID | Feature | Estimated Points | Owner | Status |
|----|---------|-----------------|-------|--------|
| F-001 | Daily Reminder System | 5 | @dev | Not Started |
| F-002 | Email Verification | 3 | @dev | Not Started |
| F-003 | Reading Time Estimate | 2 | @dev | Not Started |
| F-004 | Password Strength Meter | 2 | @dev | Not Started |

### Bug Fixes

| Bug ID | Description | Severity | Owner | Status |
|--------|-------------|----------|-------|--------|
| BUG-001 | Progress not syncing on iOS | High | @dev | Not Started |
| BUG-003 | Dark mode flicker on load | Medium | @dev | Not Started |
| BUG-007 | Share button unresponsive on Android | Medium | @dev | Not Started |

---

## Task Breakdown

### Feature: [F-001] Daily Reminder System

**Acceptance Criteria:**
- [ ] User can enable/disable daily reminders in settings
- [ ] User can select reminder time (hour picker)
- [ ] Push notification fires at selected time
- [ ] Notification opens directly to today's devotional
- [ ] Preference persists across sessions

**Tasks:**
- [ ] Add reminder settings UI to settings page - 3 hours
- [ ] Implement time picker component - 2 hours
- [ ] Set up push notification service worker - 4 hours
- [ ] Create notification scheduling logic - 3 hours
- [ ] Store preference in user profile - 2 hours
- [ ] Test on iOS and Android - 2 hours
- [ ] Write tests - 2 hours

**Dependencies:**
- Push notification capability already enabled in PWA manifest

**Notes:**
- Consider notification permission prompt timing
- Use local notifications, not server-side initially

---

## Capacity Planning

### Team Availability

| Team Member | Available Days | Notes |
|-------------|---------------|-------|
| @dev1 | 9 days | 1 day PTO |
| @dev2 | 10 days | Full sprint |

### Total Capacity
- Available person-days: 19
- Buffer (20%): 3.8
- Net capacity: ~15 days

### Point Allocation
- Features: 12 points
- Bugs: 6 points
- **Total:** 18 points

---

## Definition of Done

- [ ] Code complete and tested
- [ ] Manual QA on iOS and Android
- [ ] Deployed to staging
- [ ] Product owner approved
- [ ] Merged and deployed to production
```

---

## Quick Reference

### Before Sprint Planning
- [ ] Backlog is prioritized
- [ ] Top items have clear requirements
- [ ] Team capacity is known
- [ ] Previous retro items addressed

### During Sprint
- [ ] Daily standups happening
- [ ] Blockers addressed quickly
- [ ] Scope protected
- [ ] Progress visible

### End of Sprint
- [ ] All code reviewed and merged
- [ ] Demo prepared
- [ ] Metrics collected
- [ ] Retro scheduled

---

## Resources

- Feature Prioritization: See `44-feature-prioritization-matrix.md`
- Bug Tracking: See `45-bug-triage-template.md`
- QA Testing: See `42-qa-test-plan.md`
- User Flows: See `43-user-flow-maps.md`

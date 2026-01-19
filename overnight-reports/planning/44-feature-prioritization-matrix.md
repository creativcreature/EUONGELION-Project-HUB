# EUONGELION Feature Prioritization Matrix

**Purpose:** Rate all planned features by Impact and Effort to determine priority order
**Last Updated:** 2026-01-19
**Version:** 1.0

---

## Scoring Criteria

### Impact Score (1-5)
- **5 - Critical:** Core to mission, affects all users, drives retention
- **4 - High:** Significantly improves experience, affects most users
- **3 - Medium:** Nice improvement, affects many users
- **2 - Low:** Minor improvement, affects some users
- **1 - Minimal:** Edge case or limited benefit

### Effort Score (1-5)
- **1 - Trivial:** Hours of work, no complexity
- **2 - Low:** 1-2 days, straightforward implementation
- **3 - Medium:** 3-5 days, some complexity or dependencies
- **4 - High:** 1-2 weeks, significant complexity
- **5 - Major:** 2+ weeks, high complexity or many dependencies

### Priority Score Formula
```
Priority = Impact / Effort
Higher score = Higher priority (do these first)
```

---

## MVP FEATURES (Current State)

### Completed/In Progress

| Feature | Impact | Effort | Priority | Status | Notes |
|---------|--------|--------|----------|--------|-------|
| Daily Devotionals Display | 5 | 3 | 1.67 | Done | Core feature |
| Series Organization | 4 | 3 | 1.33 | Done | Groups content |
| Soul Audit Assessment | 5 | 4 | 1.25 | Done | Key differentiator |
| User Authentication | 4 | 3 | 1.33 | Done | Enables personalization |
| Reading Progress Tracking | 4 | 3 | 1.33 | Done | Core engagement |
| Bookmarks | 3 | 2 | 1.50 | Done | User convenience |
| PWA / Offline Support | 4 | 4 | 1.00 | Done | Mobile essential |
| Dark Mode | 3 | 2 | 1.50 | Done | Design requirement |
| Share Functionality | 3 | 2 | 1.50 | Done | Growth feature |

---

## POST-MVP FEATURES - PRIORITIZED

### Tier 1: High Priority (Priority Score > 1.5)

| Feature | Impact | Effort | Priority | Recommended Sprint | Notes |
|---------|--------|--------|----------|-------------------|-------|
| **Push Notifications** | 5 | 3 | 1.67 | Sprint 1 | Critical for daily engagement |
| **Daily Reminder System** | 5 | 2 | 2.50 | Sprint 1 | High impact, low effort |
| **Email Verification** | 4 | 2 | 2.00 | Sprint 1 | Security/trust essential |
| **Password Strength Meter** | 3 | 1 | 3.00 | Sprint 1 | Quick win |
| **Reading Time Estimate** | 3 | 1 | 3.00 | Sprint 1 | Small UX win |
| **Social Login (Google)** | 4 | 2 | 2.00 | Sprint 2 | Reduces friction |
| **Search Functionality** | 4 | 3 | 1.33 | Sprint 2 | Content discovery |
| **Progress Statistics Page** | 4 | 2 | 2.00 | Sprint 2 | Motivation/retention |
| **Error Boundary Improvements** | 4 | 2 | 2.00 | Sprint 2 | Reliability |
| **Accessibility Improvements** | 4 | 2 | 2.00 | Sprint 2 | WCAG compliance |

### Tier 2: Medium Priority (Priority Score 1.0 - 1.5)

| Feature | Impact | Effort | Priority | Recommended Sprint | Notes |
|---------|--------|--------|----------|-------------------|-------|
| **Streak Celebrations** | 3 | 2 | 1.50 | Sprint 3 | Gamification lite |
| **Social Login (Apple)** | 3 | 2 | 1.50 | Sprint 3 | iOS users expect it |
| **Related Devotionals** | 3 | 2 | 1.50 | Sprint 3 | Content discovery |
| **Reading History** | 3 | 2 | 1.50 | Sprint 3 | User convenience |
| **Font Size Settings** | 3 | 2 | 1.50 | Sprint 3 | Accessibility |
| **Category Browsing Page** | 3 | 2 | 1.50 | Sprint 4 | Navigation improvement |
| **Offline Download Manager** | 4 | 3 | 1.33 | Sprint 4 | Better offline UX |
| **Sermon Notes Feature** | 3 | 3 | 1.00 | Sprint 4 | Ministry use case |
| **Prayer Request Submission** | 3 | 3 | 1.00 | Sprint 4 | Community feature |
| **Content Ratings/Feedback** | 3 | 3 | 1.00 | Sprint 5 | Quality improvement |

### Tier 3: Lower Priority (Priority Score < 1.0)

| Feature | Impact | Effort | Priority | Recommended Sprint | Notes |
|---------|--------|--------|----------|-------------------|-------|
| **Audio Devotionals** | 4 | 5 | 0.80 | Sprint 6+ | High effort, accessibility benefit |
| **Reading Plans** | 4 | 4 | 1.00 | Sprint 6+ | Requires content strategy |
| **Community Features** | 3 | 5 | 0.60 | Future | Significant complexity |
| **Multi-language Support** | 3 | 5 | 0.60 | Future | Content translation needed |
| **Shepherd Dashboard** | 4 | 5 | 0.80 | Future | Ministry tools phase |
| **Group Bible Studies** | 3 | 5 | 0.60 | Future | Community phase |
| **Custom Reading Lists** | 2 | 3 | 0.67 | Future | Nice to have |
| **Scripture Memory Game** | 2 | 4 | 0.50 | Future | Gamification |
| **Social Sharing Images** | 2 | 3 | 0.67 | Future | Marketing feature |
| **Widget (iOS/Android)** | 3 | 5 | 0.60 | Future | Platform-specific |

---

## DETAILED FEATURE SPECIFICATIONS

### Tier 1 Features

#### 1. Push Notifications
**Impact: 5 | Effort: 3 | Priority: 1.67**

*Why High Impact:*
- Daily engagement driver
- Brings users back to app
- Enables time-based reminders

*Implementation Notes:*
- Use Web Push API
- Supabase Edge Functions for scheduling
- User preference controls essential
- Respect quiet hours

*Acceptance Criteria:*
- [ ] User can opt-in to notifications
- [ ] Daily devotional reminder sends at chosen time
- [ ] User can customize notification preferences
- [ ] Works on both iOS and Android PWA

---

#### 2. Daily Reminder System
**Impact: 5 | Effort: 2 | Priority: 2.50**

*Why High Impact:*
- Forms habit of daily devotion
- Key retention mechanism
- Low friction engagement

*Implementation Notes:*
- Time picker for preferred reminder time
- Multiple reminder options (morning, evening, etc.)
- Gentle copy, not pushy

*Acceptance Criteria:*
- [ ] User can set daily reminder time
- [ ] Reminder triggers at specified time
- [ ] User can disable reminders
- [ ] Reminder leads directly to today's content

---

#### 3. Email Verification
**Impact: 4 | Effort: 2 | Priority: 2.00**

*Why High Impact:*
- Enables password reset
- Reduces fake accounts
- Builds user trust

*Implementation Notes:*
- Supabase built-in email verification
- Custom email templates
- Resend functionality

*Acceptance Criteria:*
- [ ] Verification email sent on signup
- [ ] Email contains secure verification link
- [ ] User can resend verification
- [ ] Account features limited until verified

---

#### 4. Search Functionality
**Impact: 4 | Effort: 3 | Priority: 1.33**

*Why High Impact:*
- Content discovery
- Find specific topics/scriptures
- User expectation for content apps

*Implementation Notes:*
- Full-text search on devotionals
- Search by Scripture reference
- Filter by series/category
- Supabase full-text search capabilities

*Acceptance Criteria:*
- [ ] Search bar accessible from main nav
- [ ] Results include devotionals and series
- [ ] Scripture references searchable
- [ ] Results ranked by relevance
- [ ] Search works offline for cached content

---

#### 5. Progress Statistics Page
**Impact: 4 | Effort: 2 | Priority: 2.00**

*Why High Impact:*
- Visual motivation
- Shows investment/progress
- Encourages continued engagement

*Implementation Notes:*
- Total devotionals read
- Current streak
- Series completed
- Time spent reading
- Historical charts

*Acceptance Criteria:*
- [ ] Summary stats visible
- [ ] Current streak prominently displayed
- [ ] Series progress breakdown
- [ ] Historical view (weekly/monthly)

---

### Tier 2 Features

#### 6. Streak Celebrations
**Impact: 3 | Effort: 2 | Priority: 1.50**

*Why Medium Impact:*
- Positive reinforcement
- Creates memorable moments
- Encourages sharing

*Implementation Notes:*
- Milestone: 7 days, 30 days, 100 days, 365 days
- Subtle celebration animation
- Shareable achievement

*Acceptance Criteria:*
- [ ] Milestone recognized at key points
- [ ] Celebration UI appears
- [ ] Achievement can be shared
- [ ] Not disruptive to reading flow

---

#### 7. Related Devotionals
**Impact: 3 | Effort: 2 | Priority: 1.50**

*Why Medium Impact:*
- Increases content consumption
- Helps users discover relevant content
- Keeps users in app longer

*Implementation Notes:*
- Based on category/tags
- End-of-devotional suggestions
- "Others who read this also read..."

*Acceptance Criteria:*
- [ ] Related content shown at devotional end
- [ ] Relevance based on category/topic
- [ ] Excludes already-read content
- [ ] Maximum 3-5 suggestions

---

#### 8. Offline Download Manager
**Impact: 4 | Effort: 3 | Priority: 1.33**

*Why Medium Impact:*
- Better offline experience
- User control over storage
- Travel/airplane use case

*Implementation Notes:*
- Download entire series for offline
- Show storage used
- Selective download/delete

*Acceptance Criteria:*
- [ ] User can download series for offline
- [ ] Download progress indicator
- [ ] Storage usage visible
- [ ] Can delete downloaded content

---

### Future Features

#### 9. Audio Devotionals
**Impact: 4 | Effort: 5 | Priority: 0.80**

*Why Future:*
- Requires audio content creation
- Storage/streaming costs
- Complex implementation

*Potential Approach:*
- Text-to-speech as MVP
- Professional recordings for premium
- Background audio playback

---

#### 10. Community Features
**Impact: 3 | Effort: 5 | Priority: 0.60**

*Why Future:*
- Moderation complexity
- Significant development effort
- Potential scope creep

*Potential Features:*
- Discussion on devotionals
- Prayer groups
- Accountability partners

---

## PRIORITY VISUALIZATION

### Impact vs Effort Matrix

```
HIGH IMPACT
    |
  5 |  [Push Notif]        [Audio Dev]
    |  [Reminders]          [Shepherd]
    |
  4 |  [Stats]    [Search]   [Offline DL]  [Community]
    |  [Email Ver] [Social Login]
    |
  3 |  [Streaks]  [Related]   [Notes]      [Multi-lang]
    |  [History]  [Font Size] [Ratings]
    |
  2 |  [Pwd Meter]           [Custom Lists]
    |  [Read Time]
    |
  1 |
    |_________________________________________________
        1         2          3           4         5
                                              HIGH EFFORT
```

**Quick Wins (High Impact, Low Effort):** Upper Left
- Daily Reminders
- Password Strength Meter
- Reading Time Estimate

**Major Projects (High Impact, High Effort):** Upper Right
- Audio Devotionals
- Shepherd Dashboard
- Community Features

**Fill-ins (Low Impact, Low Effort):** Lower Left
- Minor UX improvements

**Avoid (Low Impact, High Effort):** Lower Right
- Custom reading lists
- Scripture memory game

---

## SPRINT PLANNING RECOMMENDATIONS

### Sprint 1 (Post-Launch Week 1-2)
Focus: Quick wins + essential infrastructure
- Daily Reminder System
- Email Verification
- Password Strength Meter
- Reading Time Estimate
- Critical bug fixes

### Sprint 2 (Week 3-4)
Focus: Engagement + discovery
- Push Notifications
- Search Functionality
- Progress Statistics Page
- Accessibility improvements

### Sprint 3 (Week 5-6)
Focus: Polish + retention
- Streak Celebrations
- Social Login (Google)
- Related Devotionals
- Font Size Settings

### Sprint 4 (Week 7-8)
Focus: Content experience
- Category Browsing
- Offline Download Manager
- Reading History
- Content feedback mechanism

### Future Sprints
- Audio content exploration
- Ministry tools (Shepherd Dashboard)
- Community features planning

---

## DECISION LOG

| Date | Feature | Decision | Rationale |
|------|---------|----------|-----------|
| 2026-01-19 | Matrix created | Initial prioritization | Launch planning |
| | | | |

---

## How to Use This Document

1. **During sprint planning:** Reference priority scores and recommended sprints
2. **When requests come in:** Add new features, score them, find their place
3. **Quarterly review:** Re-evaluate priorities based on user feedback and metrics
4. **Stakeholder discussions:** Use impact/effort matrix for visual discussions

**Remember:** "The lost are waiting." - Ship fast, learn from users, iterate.

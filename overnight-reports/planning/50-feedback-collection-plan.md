# EUONGELION Feedback Collection Plan

**Purpose:** How to gather user feedback through multiple channels
**Last Updated:** 2026-01-19
**Version:** 1.0

---

## Feedback Philosophy

### Why We Collect Feedback
- Understand user needs and pain points
- Identify content gaps and opportunities
- Discover bugs and usability issues
- Validate product decisions
- Build community and trust

### How We Use Feedback
- Inform feature prioritization
- Improve content quality
- Fix bugs and issues
- Guide A/B tests
- Shape product roadmap

### Privacy Commitment
- Feedback is confidential unless shared with permission
- Personal data handled per privacy policy
- Anonymous feedback always accepted
- Never share user feedback publicly without consent

---

## Feedback Channels Overview

| Channel | Type | Frequency | Best For |
|---------|------|-----------|----------|
| In-App Prompts | Quantitative + Qualitative | Per session rules | Quick ratings, NPS |
| Email Surveys | Qualitative | Monthly | Deep insights |
| App Store Reviews | Public | Ongoing | Social proof, issues |
| Support Inbox | Qualitative | Ongoing | Bug reports, requests |
| Social Listening | Qualitative | Ongoing | Sentiment, mentions |
| User Interviews | Qualitative | Quarterly | Deep understanding |

---

## Channel 1: In-App Feedback Prompts

### 1.1 Post-Devotional Rating

**When:** After completing a devotional (not every time)

**Trigger Rules:**
- User has read at least 3 devotionals
- At least 3 days since last prompt
- Only prompt on 20% of completions (random)

**UI:**

```
+------------------------------------------+
|  Did this devotional speak to you?       |
|                                          |
|  [Not really]  [Somewhat]  [Deeply]      |
|                                          |
|  (Optional: Tell us more)                |
|  [________________________________]      |
|                                          |
|  [Skip]                    [Submit]      |
+------------------------------------------+
```

**Data Collected:**
- Rating (1-3 scale: Not really, Somewhat, Deeply)
- Optional text feedback
- Devotional ID
- User ID (if logged in) or anonymous ID

---

### 1.2 NPS (Net Promoter Score) Survey

**When:**
- After 7 days of active use
- Then quarterly (every 90 days)

**UI:**

```
+------------------------------------------+
|  How likely are you to recommend         |
|  EUONGELION to a friend?                 |
|                                          |
|  Not likely              Very likely     |
|  [0][1][2][3][4][5][6][7][8][9][10]      |
|                                          |
|  What's the main reason for your score?  |
|  [________________________________]      |
|                                          |
|  [Maybe later]              [Submit]     |
+------------------------------------------+
```

**Data Collected:**
- NPS score (0-10)
- Open-ended reason
- User tenure (days since signup)
- User engagement level

**NPS Calculation:**
- Promoters (9-10) - Detractors (0-6) = NPS
- Target: NPS > 50

---

### 1.3 Feature Request Prompt

**When:** User tries to access non-existent feature or hits limitation

**Example - Search:**
```
+------------------------------------------+
|  Looking for something specific?         |
|                                          |
|  We're working on search! Would this     |
|  be helpful for you?                     |
|                                          |
|  [Not really]  [Would be nice]  [Need it]|
|                                          |
+------------------------------------------+
```

**Data Collected:**
- Feature interest level
- Context (what they were trying to do)

---

### 1.4 Bug Report Button

**Location:** Settings page, persistent option

**UI:**

```
+------------------------------------------+
|  Report a Problem                        |
|                                          |
|  What happened?                          |
|  [________________________________]      |
|  [________________________________]      |
|  [________________________________]      |
|                                          |
|  [ ] Include diagnostic info             |
|      (device, app version, etc.)         |
|                                          |
|  Email (optional, for follow-up)         |
|  [________________________________]      |
|                                          |
|  [Cancel]                    [Send]      |
+------------------------------------------+
```

**Data Collected:**
- Issue description
- Device/browser info (if opted in)
- Current page/state
- Email (optional)

---

### 1.5 Soul Audit Feedback

**When:** After viewing Soul Audit results

**UI:**

```
+------------------------------------------+
|  Did we understand where you are?        |
|                                          |
|  [Not quite]  [Close]  [Yes, exactly]    |
|                                          |
|  (If "Not quite"): What did we miss?     |
|  [________________________________]      |
+------------------------------------------+
```

**Data Collected:**
- Match quality rating
- Feedback on mismatch
- Category assigned vs. expected

---

## Channel 2: Email Surveys

### 2.1 New User Survey (Day 7)

**Subject:** How's your first week with EUONGELION?

**Questions:**
1. How did you hear about EUONGELION?
   - [ ] Friend recommendation
   - [ ] Social media
   - [ ] Search
   - [ ] Church/ministry
   - [ ] Other: ___

2. What brought you to EUONGELION? (Open)

3. On a scale of 1-5, how well has EUONGELION met your expectations?

4. What's one thing you love about EUONGELION?

5. What's one thing that could be better?

6. Would you recommend EUONGELION to a friend?
   - [ ] Already have!
   - [ ] Yes, likely
   - [ ] Maybe
   - [ ] Probably not

**Send Rules:**
- User has been active (read at least 2 devotionals)
- Email verified
- Hasn't received survey in past 30 days

---

### 2.2 Monthly Digest Survey

**Frequency:** Monthly, bundled with content digest email

**Format:** Quick poll (1-2 questions)

**Rotating Questions:**
- Week 1: "What topic would you like to see more content about?"
- Week 2: "How often do you use EUONGELION?" (Daily/Weekly/Occasionally)
- Week 3: "What's one feature you wish we had?"
- Week 4: "Rate this month's content (1-5)"

---

### 2.3 Win-Back Survey (Lapsed Users)

**Trigger:** User hasn't opened app in 30 days

**Subject:** We miss you - quick question?

**Questions:**
1. What's the main reason you've stepped away from EUONGELION?
   - [ ] Got busy / life happened
   - [ ] Content wasn't relevant to me
   - [ ] Technical issues
   - [ ] Found another app
   - [ ] Spiritual season change
   - [ ] Other: ___

2. What would bring you back? (Open)

3. Would you like us to remove you from future emails?
   - [ ] Yes, unsubscribe me
   - [ ] No, I may return

---

### 2.4 Deep Dive Survey (Quarterly)

**Frequency:** Quarterly, to engaged users

**Length:** 10-15 questions, 5-7 minutes

**Topics Covered:**
- Overall satisfaction
- Content quality and relevance
- Feature usage and requests
- Spiritual impact (qualitative)
- Competitive landscape
- Demographic information (optional)

**Incentive:** Enter to win (gift card, book, etc.)

---

## Channel 3: App Store Reviews

### 3.1 Review Prompt Strategy

**When to Prompt:**
- User has completed at least one series
- NPS score of 9 or 10
- At least 14 days of usage
- Never prompted before or 90+ days since last prompt

**UI:**

```
+------------------------------------------+
|  Enjoying EUONGELION?                    |
|                                          |
|  Your review helps others discover       |
|  God's word. Would you take a moment     |
|  to rate us?                             |
|                                          |
|  [Not now]           [Rate EUONGELION]   |
+------------------------------------------+
```

**If "Not now":**
- Ask: "Can we ask what would make EUONGELION better?"
- Capture feedback internally
- Don't prompt again for 30 days

---

### 3.2 Review Monitoring

**Process:**
1. Monitor app store reviews daily
2. Respond to all reviews within 48 hours
3. Tag reviews by theme
4. Escalate critical issues

**Response Templates:**

*Positive Review:*
```
Thank you for your kind words, [Name]! We're so grateful EUONGELION
is helping you draw closer to God's word. May your journey continue
to be blessed.
```

*Bug Report:*
```
We're sorry you experienced this issue, [Name]. We've flagged this
with our team. If you'd like to share more details, please email us
at support@euongelion.app. We're committed to making this right.
```

*Feature Request:*
```
Thank you for this suggestion, [Name]! We love hearing what would
make EUONGELION more helpful. We've added this to our feature
consideration list.
```

---

### 3.3 Review Analysis

**Monthly Review Summary:**
- Total reviews this month
- Average rating
- Rating trend (up/down/stable)
- Top themes (positive)
- Top themes (negative)
- Action items

---

## Channel 4: Support Inbox

### 4.1 Support Email Setup

**Email:** support@euongelion.app

**Auto-Response:**
```
Thank you for reaching out to EUONGELION.

We've received your message and will respond within 24-48 hours.

If this is urgent, please include "URGENT" in your subject line.

In the meantime, you might find answers in our FAQ: [link]

Blessings,
The EUONGELION Team
```

---

### 4.2 Support Categorization

**Categories:**
- Bug Report
- Feature Request
- Content Feedback
- Account Issue
- Billing (future)
- General Question
- Spiritual Support Request
- Partnership Inquiry

**Priority Levels:**
- P1: Can't use app at all, data issue
- P2: Major feature broken
- P3: Minor issue, workaround exists
- P4: Question, request, general feedback

---

### 4.3 Support Response SLAs

| Priority | First Response | Resolution Target |
|----------|---------------|-------------------|
| P1 | 4 hours | 24 hours |
| P2 | 24 hours | 72 hours |
| P3 | 48 hours | 1 week |
| P4 | 72 hours | 2 weeks |

---

### 4.4 Feedback Loop

**Process:**
1. All support emails logged in tracking system
2. Weekly review of support themes
3. Top issues shared with product team
4. Feature requests added to backlog
5. Users notified when their feedback is implemented

---

## Channel 5: Social Listening

### 5.1 Platforms to Monitor

- Twitter/X (mentions, hashtags)
- Instagram (comments, DMs)
- Facebook (page, groups)
- Reddit (relevant subreddits)
- Christian forums and communities
- Product Hunt (if listed)

### 5.2 Keywords to Track

**Brand:**
- EUONGELION
- euongelion app
- euongelion devotional

**Category:**
- Christian devotional app
- Bible app
- daily devotional app
- spiritual formation app

**Competitors:**
- [Competitor names]
- "better than [competitor]"
- "instead of [competitor]"

### 5.3 Monitoring Process

**Daily:**
- Check brand mentions
- Respond to direct questions
- Flag critical issues

**Weekly:**
- Summarize sentiment
- Note emerging themes
- Share highlights with team

---

### 5.4 Response Guidelines

**Do:**
- Respond promptly and warmly
- Thank people for feedback
- Take conversations to DM for issues
- Be humble and helpful

**Don't:**
- Argue or get defensive
- Make promises you can't keep
- Share user information
- Delete negative comments (unless inappropriate)

---

## Channel 6: User Interviews

### 6.1 Interview Goals

- Understand user motivations and needs
- Discover pain points not captured in surveys
- Validate product assumptions
- Generate ideas for new features
- Build relationships with power users

### 6.2 Interview Recruitment

**Who to Interview:**
- New users (7-14 days)
- Power users (daily usage, high engagement)
- Lapsed users (stopped using)
- Different demographic segments

**Recruitment Methods:**
- In-app prompt to volunteers
- Email invitation to engaged users
- Social media call for participants

**Incentive:** $25 gift card or donation to charity of choice

---

### 6.3 Interview Guide Template

**Duration:** 30-45 minutes

**Introduction (5 min):**
- Thank them for their time
- Explain purpose of interview
- Confirm recording permission
- Ask if they have questions

**Background (5 min):**
- Tell me about your faith journey
- How do you typically engage with Scripture?
- What other apps/tools do you use?

**EUONGELION Experience (15 min):**
- How did you discover EUONGELION?
- Walk me through your typical use
- What do you love about it?
- What frustrates you?
- Tell me about the Soul Audit experience

**Deep Dive (10 min):**
- [Topic-specific questions based on research goals]

**Future (5 min):**
- What would make EUONGELION perfect for you?
- Is there anything else you'd like to share?

**Wrap-up:**
- Thank them
- Explain next steps
- Send incentive

---

### 6.4 Interview Synthesis

**After Each Interview:**
- Write summary within 24 hours
- Note key quotes
- Tag themes
- Add to insights database

**Monthly Synthesis:**
- Review all interviews
- Identify patterns
- Create insight report
- Share with team

---

## Feedback Analysis & Action

### Weekly Feedback Review

**Attendees:** Product, Content, Support leads
**Duration:** 30 minutes

**Agenda:**
1. Review support ticket themes (5 min)
2. Review in-app feedback data (5 min)
3. Review social mentions (5 min)
4. Discuss emerging patterns (10 min)
5. Assign action items (5 min)

---

### Monthly Feedback Report

**Template:**

```markdown
# Monthly Feedback Report - [Month Year]

## Summary
[2-3 sentence overview]

## Key Metrics
- NPS Score: [X] (trend: up/down/stable)
- App Store Rating: [X.X] ([X] new reviews)
- Support Tickets: [X] (top category: [X])
- In-App Feedback: [X] responses

## Top Themes

### What Users Love
1. [Theme] - [X mentions]
2. [Theme] - [X mentions]
3. [Theme] - [X mentions]

### Pain Points
1. [Theme] - [X mentions]
2. [Theme] - [X mentions]
3. [Theme] - [X mentions]

### Feature Requests
1. [Request] - [X mentions]
2. [Request] - [X mentions]
3. [Request] - [X mentions]

## Notable Quotes
> "[Quote]" - [Context]

> "[Quote]" - [Context]

## Action Items
- [ ] [Action item 1] - Owner: @name
- [ ] [Action item 2] - Owner: @name

## Recommendations
[Strategic recommendations based on feedback]
```

---

### Feedback-to-Action Pipeline

```
[Feedback Received]
       |
       v
[Categorized & Tagged]
       |
       v
[Reviewed in Weekly Meeting]
       |
       v
[Prioritized with Product Team]
       |
       +---> [Bug] --> Bug Triage Process
       |
       +---> [Feature Request] --> Feature Backlog
       |
       +---> [Content Feedback] --> Content Team
       |
       +---> [Support Issue] --> Support Response
       |
       v
[Action Taken]
       |
       v
[User Notified (when applicable)]
       |
       v
[Feedback Loop Closed]
```

---

## Tools & Setup

### Recommended Tools

| Purpose | Tool | Notes |
|---------|------|-------|
| In-App Surveys | Hotjar / Usabilla | Simple prompts |
| Email Surveys | Typeform / SurveyMonkey | Longer surveys |
| Support Inbox | Help Scout / Intercom | Ticket management |
| Social Listening | Mention / Brand24 | Automated monitoring |
| Interview Scheduling | Calendly | Easy booking |
| Interview Recording | Zoom / Loom | With permission |
| Feedback Database | Notion / Airtable | Central repository |

### MVP Setup (Low Budget)

- In-App: Custom built (simple modal)
- Email: Google Forms + Mailchimp
- Support: Shared Gmail + spreadsheet tracking
- Social: Manual daily check
- Interviews: Zoom + Google Docs
- Database: Notion free tier

---

## Privacy & Compliance

### Data Handling
- Store feedback securely
- Anonymize where possible
- Delete personal data on request
- Don't share without consent

### GDPR Compliance
- Clear opt-in for surveys
- Easy opt-out option
- Data export on request
- Right to be forgotten

### Communication Preferences
- Respect unsubscribe requests
- Don't over-survey
- Be transparent about data use

---

## Success Metrics

| Metric | Target | Frequency |
|--------|--------|-----------|
| NPS Score | > 50 | Quarterly |
| App Store Rating | > 4.5 | Monthly |
| Support Response Time | < 24 hrs | Weekly |
| Survey Response Rate | > 20% | Per survey |
| Feedback Actions Taken | 80%+ reviewed | Monthly |
| User Interview Quota | 4/month | Monthly |

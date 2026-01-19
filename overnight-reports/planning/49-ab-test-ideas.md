# EUONGELION A/B Test Ideas

**Purpose:** Propose experiments to optimize user experience post-launch
**Last Updated:** 2026-01-19
**Version:** 1.0

---

## A/B Testing Philosophy

### Why We Test
- Make data-informed decisions
- Reduce risk of large changes
- Understand our users better
- Continuously improve spiritual formation outcomes

### What We Don't Test
- Core theological content (not negotiable)
- Crisis resources (always show prominently)
- Accessibility features (always include)
- Privacy protections (always respect)

### Testing Ethics
- Tests should benefit users, not manipulate them
- Dark patterns are never acceptable
- Spiritual formation over engagement metrics
- If in doubt, don't test it

---

## Test Framework

### Test Documentation Template

```markdown
## Test: [Test Name]

**Hypothesis:** [If we do X, then Y will improve because Z]
**Primary Metric:** [What we're measuring]
**Secondary Metrics:** [Supporting metrics]
**Traffic Split:** [50/50 or other]
**Duration:** [X weeks or until statistical significance]
**Minimum Sample:** [X users per variant]

### Variants
- **Control (A):** [Current state]
- **Treatment (B):** [Changed state]

### Success Criteria
- Primary metric improves by X%
- No significant decrease in secondary metrics

### Risks
- [Potential negative outcomes]

### Results
- Start Date: [Date]
- End Date: [Date]
- Winner: [A/B/Inconclusive]
- Notes: [What we learned]
```

---

## Proposed A/B Tests

### Test 1: Soul Audit Question Framing

**Hypothesis:** A more inviting question framing will increase Soul Audit completion rates because users will feel safer sharing honestly.

**Primary Metric:** Soul Audit completion rate
**Secondary Metrics:** Response length, category match confidence, first devotional read rate

**Variants:**
- **Control (A):** "What are you wrestling with?"
- **Treatment (B):** "What's on your heart today?"
- **Treatment (C):** "Where do you need God's word right now?"

**Traffic Split:** 33/33/33
**Duration:** 2 weeks or 500 completions per variant
**Minimum Sample:** 500 per variant

**Success Criteria:**
- Completion rate improves by 10%+
- Response quality (length) doesn't decrease

**Risks:**
- Different framing may attract different user segments
- May affect category matching accuracy

---

### Test 2: Onboarding Flow Order

**Hypothesis:** Showing value (devotional preview) before asking for Soul Audit will increase overall engagement because users understand what they're getting.

**Primary Metric:** Soul Audit completion rate
**Secondary Metrics:** First devotional read, D1 retention

**Variants:**
- **Control (A):** Home -> Soul Audit prompt -> Soul Audit -> Results -> Devotional
- **Treatment (B):** Home -> Browse devotionals -> Soul Audit prompt (after first read) -> Soul Audit

**Traffic Split:** 50/50
**Duration:** 3 weeks
**Minimum Sample:** 300 per variant

**Success Criteria:**
- Overall Soul Audit completion improves
- D1 retention improves

**Risks:**
- May delay personalization
- Users may never take Soul Audit

---

### Test 3: Devotional Completion CTA

**Hypothesis:** A clearer "Mark Complete" action will increase completion tracking accuracy because users often read but don't explicitly mark done.

**Primary Metric:** Devotional completion rate
**Secondary Metrics:** Progress tracking accuracy, user-reported satisfaction

**Variants:**
- **Control (A):** Auto-complete on scroll to bottom
- **Treatment (B):** Explicit "I've finished this devotional" button at end
- **Treatment (C):** Both auto-complete + confirmation toast

**Traffic Split:** 33/33/33
**Duration:** 2 weeks
**Minimum Sample:** 200 completions per variant

**Success Criteria:**
- Completion tracking aligns better with reading time
- User satisfaction doesn't decrease

**Risks:**
- Extra friction may decrease tracked completions
- Some users may ignore explicit buttons

---

### Test 4: Series Length Impact

**Hypothesis:** Shorter series (5-7 devotionals) will have higher completion rates than longer series (10-14) because commitment feels more achievable.

**Primary Metric:** Series completion rate
**Secondary Metrics:** Overall devotionals read, series start rate

**Variants:**
- **Control (A):** Mixed series lengths (current)
- **Treatment (B):** Promote 5-7 devotional series first

**Traffic Split:** 50/50
**Duration:** 4 weeks (need time for series completion)
**Minimum Sample:** 100 series starts per variant

**Success Criteria:**
- Series completion rate improves by 15%+
- Total devotionals read doesn't decrease

**Risks:**
- May limit content depth
- Returning users may prefer longer series

---

### Test 5: Reading Time Display

**Hypothesis:** Showing "3 min read" will increase devotional starts because users know the time commitment upfront.

**Primary Metric:** Devotional start rate (view to read)
**Secondary Metrics:** Completion rate, average session time

**Variants:**
- **Control (A):** No reading time shown
- **Treatment (B):** "3 min read" badge on devotional cards
- **Treatment (C):** "3 min read" + "Quick devotional!" for <3 min

**Traffic Split:** 33/33/33
**Duration:** 2 weeks
**Minimum Sample:** 500 devotional views per variant

**Success Criteria:**
- Devotional start rate improves by 5%+
- Completion rate stays stable or improves

**Risks:**
- Users may only select short devotionals
- May devalue longer, deeper content

---

### Test 6: Push Notification Timing

**Hypothesis:** Morning notifications (6-8 AM) will have higher open rates than evening (6-8 PM) because users want to start their day with devotion.

**Primary Metric:** Notification open rate
**Secondary Metrics:** D1 retention after notification, session depth

**Variants:**
- **Control (A):** User-selected time (current)
- **Treatment (B):** Default 7 AM, user can change
- **Treatment (C):** Default 7 PM, user can change
- **Treatment (D):** Smart default based on previous usage patterns

**Traffic Split:** 25/25/25/25
**Duration:** 2 weeks
**Minimum Sample:** 200 notification recipients per variant

**Success Criteria:**
- Notification open rate improves by 20%+
- Unsubscribe rate doesn't increase

**Risks:**
- Wrong time may annoy users
- Time zones complicate analysis

---

### Test 7: Social Proof Messaging

**Hypothesis:** Showing that others are reading will increase engagement because social proof creates FOMO and community feeling.

**Primary Metric:** Devotional read rate
**Secondary Metrics:** Session duration, return rate

**Variants:**
- **Control (A):** No social proof
- **Treatment (B):** "247 others read this today" on popular devotionals
- **Treatment (C):** "Trending in Rest & Renewal" category labels

**Traffic Split:** 33/33/33
**Duration:** 2 weeks
**Minimum Sample:** 500 views per variant

**Success Criteria:**
- Read rate improves by 10%+
- Users don't report feeling pressured

**Risks:**
- May feel manipulative
- Low numbers could have opposite effect
- Deviates from "sacred minimalism"

**Note:** Review against design philosophy before running

---

### Test 8: Bookmark Prompt Timing

**Hypothesis:** Prompting to bookmark at devotional end will increase bookmark usage because users have just experienced the value.

**Primary Metric:** Bookmark rate
**Secondary Metrics:** Bookmark list engagement, return visits to bookmarked content

**Variants:**
- **Control (A):** Bookmark icon always visible, no prompt
- **Treatment (B):** Subtle "Save this for later?" prompt at devotional end
- **Treatment (C):** "Did this speak to you? Save it." prompt at end

**Traffic Split:** 33/33/33
**Duration:** 2 weeks
**Minimum Sample:** 300 devotional completions per variant

**Success Criteria:**
- Bookmark rate improves by 25%+
- Users actually return to bookmarks

**Risks:**
- May feel intrusive
- Prompt fatigue over time

---

### Test 9: Progress Visualization Style

**Hypothesis:** Visual progress (progress bar) will increase series completion more than numerical (3 of 7) because it's more motivating.

**Primary Metric:** Series completion rate
**Secondary Metrics:** Time to series completion, user satisfaction

**Variants:**
- **Control (A):** "3 of 7 complete"
- **Treatment (B):** Progress bar (43% complete)
- **Treatment (C):** Both number and progress bar
- **Treatment (D):** Milestone checkpoints ("Halfway there!")

**Traffic Split:** 25/25/25/25
**Duration:** 4 weeks
**Minimum Sample:** 100 active series per variant

**Success Criteria:**
- Series completion improves by 10%+
- User feedback is positive

**Risks:**
- Over-gamification contrary to mission
- Progress anxiety for some users

---

### Test 10: Share CTA Copy

**Hypothesis:** More personal share copy will increase share rate because it frames sharing as invitation rather than promotion.

**Primary Metric:** Share click rate
**Secondary Metrics:** Share completion rate, referred user signups

**Variants:**
- **Control (A):** "Share" button
- **Treatment (B):** "Share the word" button
- **Treatment (C):** "Send to a friend" button
- **Treatment (D):** "Know someone who needs this?" with share icon

**Traffic Split:** 25/25/25/25
**Duration:** 2 weeks
**Minimum Sample:** 500 devotional views per variant

**Success Criteria:**
- Share click rate improves by 20%+
- Share completion rate stays stable

**Risks:**
- Longer copy may be ignored
- Mobile space constraints

---

## Test Prioritization

| Test | Expected Impact | Effort | Priority |
|------|-----------------|--------|----------|
| Test 5: Reading Time Display | Medium | Low | **High** |
| Test 8: Bookmark Prompt | Medium | Low | **High** |
| Test 10: Share CTA Copy | Medium | Low | **High** |
| Test 1: Soul Audit Question | High | Low | **High** |
| Test 3: Completion CTA | Medium | Medium | Medium |
| Test 6: Notification Timing | High | Medium | Medium |
| Test 2: Onboarding Flow | High | High | Medium |
| Test 9: Progress Visualization | Medium | Medium | Medium |
| Test 4: Series Length | Medium | High | Low |
| Test 7: Social Proof | Low | Low | Low (review first) |

---

## Implementation Requirements

### Technical Setup
- [ ] Feature flag system implemented
- [ ] User bucketing/assignment
- [ ] Event tracking for all test metrics
- [ ] Statistical significance calculator
- [ ] Test dashboard

### Process
- [ ] Test proposal template
- [ ] Approval workflow
- [ ] Documentation requirements
- [ ] Results communication plan

### Tools
- **Recommended:** PostHog (built-in A/B testing)
- **Alternative:** Statsig, LaunchDarkly, Optimizely

---

## Statistical Guidelines

### Minimum Sample Sizes
- For 5% effect detection: ~1,500 per variant
- For 10% effect detection: ~400 per variant
- For 20% effect detection: ~100 per variant

### Significance Threshold
- p-value < 0.05 for statistical significance
- Run until significant OR planned duration complete
- Don't peek and stop early

### Duration Guidelines
- Minimum: 1 week (account for day-of-week effects)
- Recommended: 2-4 weeks
- Maximum: 6 weeks (avoid creep)

---

## Results Template

```markdown
## Test Results: [Test Name]

**Duration:** [Start] - [End]
**Sample Size:** [Control: X, Treatment: X]

### Results

| Metric | Control | Treatment | Difference | Significant? |
|--------|---------|-----------|------------|--------------|
| Primary | X% | Y% | +Z% | Yes/No |
| Secondary 1 | | | | |
| Secondary 2 | | | | |

### Winner: [Control / Treatment / Inconclusive]

### Key Learnings
- [Learning 1]
- [Learning 2]

### Recommendations
- [ ] Ship treatment to 100%
- [ ] Iterate with new test
- [ ] Abandon approach

### Follow-up Tests
- [If any, describe]
```

---

## Quarterly Test Calendar

### Q1 (Post-Launch)
| Month | Test | Focus |
|-------|------|-------|
| Month 1 | Test 5: Reading Time | Quick wins |
| Month 1 | Test 10: Share Copy | Quick wins |
| Month 2 | Test 1: Soul Audit Question | Onboarding |
| Month 2 | Test 8: Bookmark Prompt | Engagement |
| Month 3 | Test 6: Notification Timing | Retention |

### Q2
| Month | Test | Focus |
|-------|------|-------|
| Month 4 | Test 2: Onboarding Flow | Onboarding |
| Month 4 | Test 3: Completion CTA | Engagement |
| Month 5 | Test 9: Progress Visualization | Engagement |
| Month 6 | Iteration on Q1 learnings | Optimization |

---

## Do Not Test List

Things we've decided NOT to A/B test:

1. **Crisis resource visibility** - Always prominent
2. **Scripture accuracy** - Always correct
3. **Dark mode availability** - Always available
4. **Accessibility features** - Always included
5. **Privacy settings** - Always respect user choice
6. **Core theological content** - Not up for optimization
7. **Manipulative "engagement" features** - Against our values

---

## Test Ideas Backlog

Future tests to consider:

| Idea | Why Interesting | Why Not Now |
|------|-----------------|-------------|
| Personalized home page | Could improve relevance | Need more data first |
| Audio vs. text preference | Accessibility | Audio not built yet |
| Dark mode as default | User preference | Need usage data |
| Email digest frequency | Retention | Email system basic |
| Community features | Engagement | Complexity too high |
| Reflection question styles | Depth | Need baseline data |
| Series recommendation algorithm | Discovery | Need more series |

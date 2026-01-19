# EUONGELION Content Pipeline Documentation

**Purpose:** Document the complete workflow for devotional content from idea to live in app
**Last Updated:** 2026-01-19
**Version:** 1.0

---

## Pipeline Overview

```
[Idea] -> [Outline] -> [Draft] -> [Review] -> [Approve] -> [Format] -> [Database] -> [QA] -> [Live]
```

### Stages at a Glance

| Stage | Owner | Duration | Output |
|-------|-------|----------|--------|
| 1. Ideation | Content Lead | Ongoing | Series concepts, themes |
| 2. Outline | Writer | 1-2 days | Structured outline |
| 3. Draft | Writer | 2-4 days | Complete devotional |
| 4. Review | Editor | 1-2 days | Feedback/edits |
| 5. Approval | Content Lead | 1 day | Sign-off |
| 6. Formatting | Content Ops | 1 day | Database-ready format |
| 7. Database Entry | Content Ops | 1 day | Data in Supabase |
| 8. QA | QA Tester | 1 day | Verified display |
| 9. Publish | Content Ops | 1 hour | Live in app |

---

## Stage 1: Ideation

### Purpose
Generate content ideas that serve users based on Soul Audit categories and spiritual needs.

### Inputs
- Soul Audit category needs (Faith Foundations, Emotional Healing, etc.)
- User feedback and requests
- Seasonal/calendar considerations
- Current events (when appropriate)
- Content gaps analysis

### Process
1. **Brainstorm** series themes aligned with categories
2. **Validate** against content strategy and user needs
3. **Prioritize** based on audience demand and production capacity
4. **Document** approved concepts in content backlog

### Outputs
- Series concept with title, description, and target category
- Estimated number of devotionals (typically 7-14)
- Target audience and spiritual maturity level
- Key Scripture passages to anchor the series

### Content Backlog Template

```markdown
## Series Concept: [Title]

**Category:** [Primary category from Soul Audit categories]
**Target Audience:** [New believers / Growing believers / Mature believers]
**Estimated Length:** [X devotionals]
**Priority:** High / Medium / Low

### Description
[2-3 sentence description of what this series covers]

### Core Scriptures
- [Scripture 1]
- [Scripture 2]
- [Scripture 3]

### Devotional Titles (Draft)
1. [Title 1]
2. [Title 2]
3. [Title 3]
...

### Why This Matters
[Why users need this content right now]

### Status
[ ] Concept approved
[ ] Assigned to writer
[ ] In production
```

---

## Stage 2: Outline

### Purpose
Create a structured outline for each devotional before full writing.

### Inputs
- Approved series concept
- Assigned Scripture passage(s)
- Content guidelines

### Process
1. **Research** the Scripture passage in context
2. **Identify** the central truth/application
3. **Structure** the devotional outline
4. **Draft** reflection questions
5. **Submit** for quick review

### Devotional Outline Template

```markdown
## Devotional Outline

**Series:** [Series name]
**Position:** [X of Y in series]
**Title:** [Working title]
**Scripture:** [Book Chapter:Verses (Translation)]

### Central Truth
[One sentence: What is the main takeaway?]

### Opening Hook (2-3 sentences)
[How will you draw the reader in?]

### Scripture Context (1 paragraph)
[Brief background on the passage]

### Application Points (2-3 points)
1. [Point 1]
2. [Point 2]
3. [Point 3]

### Reflection Questions (2-3 questions)
1. [Question 1]
2. [Question 2]
3. [Question 3]

### Closing (2-3 sentences)
[How will you end? Call to action?]

### Estimated Reading Time
[3-5 minutes target]
```

### Quality Checks
- [ ] Scripture is in context (not proof-texting)
- [ ] Application is practical and personal
- [ ] Questions encourage genuine reflection
- [ ] Tone matches EUONGELION voice

---

## Stage 3: Draft

### Purpose
Write the complete devotional content.

### Inputs
- Approved outline
- Style guide
- Word count targets

### Process
1. **Write** based on approved outline
2. **Self-edit** for clarity and flow
3. **Check** Scripture accuracy
4. **Ensure** reading time target met
5. **Submit** to review queue

### Content Guidelines

**Voice & Tone:**
- Warm but not saccharine
- Intelligent but accessible
- Challenging but not condemning
- Honest about struggles
- Hope-filled without being naive

**Structure:**
- **Title:** Clear, intriguing, searchable
- **Scripture:** Always in context
- **Opening:** Hook within first 2 sentences
- **Body:** 300-500 words
- **Application:** Concrete, actionable
- **Questions:** Thought-provoking, not yes/no
- **Total Read Time:** 3-5 minutes

**What to Avoid:**
- Christian jargon without explanation
- Guilt-based manipulation
- Political statements
- Denominational specifics
- Prosperity gospel messaging
- Legalistic rules without grace

### Draft Template

```markdown
# [Devotional Title]

**Scripture:** [Full Scripture reference]

---

[Opening paragraph - hook the reader]

> [Scripture text, properly formatted]

[Body paragraph 1 - context and explanation]

[Body paragraph 2 - deeper meaning]

[Body paragraph 3 - application]

---

## Reflect

[Closing thought or call to reflection]

1. [Reflection question 1]
2. [Reflection question 2]
3. [Reflection question 3]

---

**Prayer:**
[Optional: 2-3 sentence prayer prompt]
```

---

## Stage 4: Review

### Purpose
Ensure content quality, theological accuracy, and brand consistency.

### Inputs
- Complete draft
- Style guide
- Theological guidelines

### Process
1. **Read** for comprehension and engagement
2. **Check** theological accuracy
3. **Verify** Scripture quotes and references
4. **Edit** for clarity, grammar, and style
5. **Provide** feedback or approve

### Review Checklist

**Content Quality:**
- [ ] Title is engaging and accurate
- [ ] Opening hooks the reader
- [ ] Scripture is in proper context
- [ ] Application is practical
- [ ] Reflection questions are thought-provoking
- [ ] Length is appropriate (3-5 min read)

**Theological Accuracy:**
- [ ] Scripture interpretation is sound
- [ ] No proof-texting or out-of-context usage
- [ ] Balanced grace and truth
- [ ] Orthodox Christian theology
- [ ] No controversial denominational positions

**Brand Voice:**
- [ ] Tone matches EUONGELION voice
- [ ] No Christian jargon without explanation
- [ ] Accessible to target audience
- [ ] Encouraging without being shallow

**Technical:**
- [ ] Scripture reference is correct
- [ ] No spelling or grammar errors
- [ ] Proper formatting
- [ ] No broken links or references

### Review Feedback Template

```markdown
## Content Review: [Devotional Title]

**Reviewer:** [Name]
**Date:** [Date]
**Status:** Approved / Revisions Needed / Major Rewrite

### Overall Assessment
[1-2 sentence summary]

### Strengths
- [What works well]

### Revisions Needed
- [ ] [Specific revision 1]
- [ ] [Specific revision 2]

### Theological Notes
- [Any concerns or clarifications needed]

### Minor Edits
- [Line-level edits, typos, etc.]
```

---

## Stage 5: Approval

### Purpose
Final sign-off before formatting for database.

### Inputs
- Reviewed and revised content
- Review feedback addressed

### Process
1. **Verify** all review feedback addressed
2. **Final read** by Content Lead
3. **Approve** or request final changes
4. **Hand off** to Content Ops for formatting

### Approval Criteria
- All review checklist items pass
- Content Lead confident in quality
- Ready for users to see

---

## Stage 6: Formatting

### Purpose
Prepare content for database entry in correct format.

### Inputs
- Approved devotional content
- Database schema requirements

### Process
1. **Format** content as JSON
2. **Assign** metadata (category, tags, series position)
3. **Generate** slug for URL
4. **Verify** formatting

### Database Format

```json
{
  "title": "Finding Rest in Chaos",
  "slug": "finding-rest-in-chaos",
  "series_id": "uuid-of-series",
  "position_in_series": 3,
  "scripture_reference": "Matthew 11:28-30",
  "scripture_text": "Come to me, all who labor and are heavy laden, and I will give you rest. Take my yoke upon you, and learn from me, for I am gentle and lowly in heart, and you will find rest for your souls. For my yoke is easy, and my burden is light.",
  "scripture_translation": "ESV",
  "content": "[Markdown formatted devotional body]",
  "reflection_questions": [
    "What burdens are you carrying that feel too heavy right now?",
    "How might Jesus be inviting you to rest today?",
    "What does it look like to take Jesus' yoke upon you?"
  ],
  "reading_time_minutes": 4,
  "category": "rest-renewal",
  "tags": ["rest", "peace", "anxiety", "stress"],
  "author_id": "uuid-of-author",
  "status": "draft",
  "publish_date": null,
  "created_at": "2026-01-19T00:00:00Z",
  "updated_at": "2026-01-19T00:00:00Z"
}
```

### Metadata Guidelines

**Categories** (from Soul Audit):
- `faith-foundations`
- `emotional-healing`
- `purpose-direction`
- `relationships`
- `spiritual-practices`
- `doubt-questions`
- `rest-renewal`
- `growth-discipleship`

**Tags:**
- 3-7 tags per devotional
- Lowercase, hyphenated
- Include key themes, emotions, Scripture topics

**Reading Time:**
- Calculate: ~200 words per minute average
- Round to nearest minute
- Target: 3-5 minutes

---

## Stage 7: Database Entry

### Purpose
Load content into Supabase database.

### Inputs
- Formatted JSON content
- Series already created in database

### Process
1. **Ensure** series exists (create if needed)
2. **Insert** devotional record
3. **Verify** data integrity
4. **Keep** status as "draft"

### Database Entry Checklist
- [ ] Series exists and ID is correct
- [ ] All required fields populated
- [ ] Scripture reference matches text
- [ ] Position in series is correct
- [ ] Status is "draft" (not published)
- [ ] No duplicate slugs
- [ ] Timestamps are correct

### Supabase Insert (Example)

```sql
INSERT INTO devotionals (
  title,
  slug,
  series_id,
  position_in_series,
  scripture_reference,
  scripture_text,
  scripture_translation,
  content,
  reflection_questions,
  reading_time_minutes,
  category,
  tags,
  author_id,
  status,
  publish_date,
  created_at,
  updated_at
) VALUES (
  'Finding Rest in Chaos',
  'finding-rest-in-chaos',
  'uuid-here',
  3,
  'Matthew 11:28-30',
  'Come to me, all who labor...',
  'ESV',
  '[markdown content]',
  ARRAY['Question 1', 'Question 2', 'Question 3'],
  4,
  'rest-renewal',
  ARRAY['rest', 'peace', 'anxiety'],
  'author-uuid',
  'draft',
  NULL,
  NOW(),
  NOW()
);
```

---

## Stage 8: QA

### Purpose
Verify content displays correctly in the app.

### Inputs
- Devotional in database (draft status)
- QA checklist

### Process
1. **View** devotional on staging/preview
2. **Check** all elements display correctly
3. **Test** on mobile and desktop
4. **Verify** series navigation works
5. **Report** any issues

### QA Checklist

**Display:**
- [ ] Title displays correctly
- [ ] Scripture reference is accurate
- [ ] Scripture text renders properly
- [ ] Body content formatted correctly
- [ ] Markdown renders (bold, italic, etc.)
- [ ] Reflection questions display
- [ ] Reading time shows correctly

**Navigation:**
- [ ] Devotional appears in series list
- [ ] Position in series is correct
- [ ] Next/Previous navigation works
- [ ] Back to series works

**Cross-Device:**
- [ ] Mobile display is readable
- [ ] Desktop display is appropriate
- [ ] Dark mode renders correctly

**Functionality:**
- [ ] Bookmark works
- [ ] Share works
- [ ] Progress tracking works

### Issue Report Template

```markdown
## QA Issue: [Devotional Title]

**Tester:** [Name]
**Date:** [Date]
**Severity:** Blocker / Major / Minor

### Issue
[Description of the problem]

### Device/Browser
[Where the issue was found]

### Screenshot
[Attach screenshot]

### Resolution
[ ] Content fix needed
[ ] Code fix needed
[ ] Issue resolved
```

---

## Stage 9: Publish

### Purpose
Make content live and available to users.

### Inputs
- QA-approved devotional
- Publish date (immediate or scheduled)

### Process
1. **Update** status from "draft" to "published"
2. **Set** publish_date
3. **Verify** appears on production
4. **Monitor** for any issues

### Publish Checklist
- [ ] All QA issues resolved
- [ ] Content Lead approval confirmed
- [ ] Publish date is correct
- [ ] Status updated to "published"
- [ ] Verified live on production
- [ ] Series page updated
- [ ] Home page shows (if featured)

### Publish SQL

```sql
UPDATE devotionals
SET
  status = 'published',
  publish_date = NOW(),
  updated_at = NOW()
WHERE id = 'devotional-uuid';
```

---

## Content Calendar

### Weekly Publishing Schedule (Example)

| Day | Action |
|-----|--------|
| Monday | New devotional published |
| Tuesday | - |
| Wednesday | New devotional published |
| Thursday | - |
| Friday | New devotional published |
| Saturday | - |
| Sunday | - |

### Content Buffer Target
- **Minimum:** 1 week of content ready
- **Ideal:** 2-4 weeks of content ready
- **Alert:** < 3 days of content ready

### Series Launch Timeline

```
Week -4: Series concept approved
Week -3: Outlines complete
Week -2: Drafts complete
Week -1: Reviews complete, formatting
Day 0: Series launches
```

---

## Roles & Responsibilities

### Content Lead
- Approve series concepts
- Final approval on content
- Maintain content strategy
- Monitor content performance

### Writers
- Research and outline
- Draft devotionals
- Revise based on feedback
- Meet deadlines

### Editor/Reviewer
- Review for quality and accuracy
- Provide constructive feedback
- Ensure theological soundness
- Maintain style consistency

### Content Ops
- Format for database
- Enter content in Supabase
- Coordinate publishing
- Maintain content calendar

### QA Tester
- Verify display quality
- Test cross-device
- Report issues
- Sign off on readiness

---

## Tools & Resources

### Content Creation
- Writing tool: [Notion / Google Docs / etc.]
- Style guide: [Link]
- Theological guidelines: [Link]

### Database
- Supabase dashboard: [Link]
- Database schema: `/supabase/migrations/`

### QA & Preview
- Staging environment: [URL]
- QA checklist: See Stage 8 above

### Communication
- Content team channel: [Slack/Discord channel]
- Content backlog: [Link to tracking board]

---

## Emergency Procedures

### Content Error in Production

1. **Identify** the error (typo, theological issue, etc.)
2. **Assess** severity
3. **Fix** directly in database if minor
4. **Republish** through full pipeline if major
5. **Communicate** to team

### Missing Content (Pipeline Empty)

1. **Alert** Content Lead immediately
2. **Identify** fastest content to publish
3. **Fast-track** through pipeline (same-day if needed)
4. **Post-mortem** on how buffer was depleted

### Controversial Content Response

1. **Do not** delete without approval
2. **Assess** validity of concerns
3. **Consult** theological advisors if needed
4. **Edit or remove** with Content Lead approval
5. **Communicate** response if public issue

---

## Quality Metrics

### Track Monthly
- Content pieces published
- Average time through pipeline
- QA issues found (by type)
- User engagement per devotional
- Content buffer status

### Quality Goals
- < 5% of content needs major revision
- < 2 QA issues per devotional average
- 100% theological accuracy
- User rating > 4.5/5 average

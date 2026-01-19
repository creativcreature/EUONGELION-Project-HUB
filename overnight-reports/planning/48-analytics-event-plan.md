# EUONGELION Analytics Event Plan

**Purpose:** Define what user actions to track and how to measure app success
**Last Updated:** 2026-01-19
**Version:** 1.0

---

## Analytics Philosophy

EUONGELION tracks analytics for **spiritual formation impact**, not engagement manipulation.

### What We Measure
- Are users encountering Scripture?
- Are users growing in their faith journey?
- Is the Soul Audit helping users find relevant content?
- Are users forming daily devotional habits?

### What We Avoid
- Vanity metrics that don't inform decisions
- Tracking that enables manipulation
- Excessive data collection
- Privacy-invasive tracking

---

## Recommended Analytics Platform

### Primary: **Plausible Analytics** or **Fathom**
Privacy-focused, GDPR-compliant, simple

### Alternative: **PostHog** (if more features needed)
Self-hostable, product analytics, more complex

### Why Not Google Analytics?
- Privacy concerns for Christian audience
- Overkill for our needs
- Cookie consent complexity

---

## Event Taxonomy

### Naming Convention
```
[category]_[action]_[object]
```

Examples:
- `devotional_read_complete`
- `soul_audit_start`
- `bookmark_add`

### Categories
| Category | Description |
|----------|-------------|
| page | Page views |
| devotional | Devotional interactions |
| series | Series interactions |
| soul_audit | Soul Audit flow |
| bookmark | Bookmark actions |
| auth | Authentication events |
| share | Sharing actions |
| pwa | PWA-specific events |
| engagement | Engagement metrics |
| error | Error tracking |

---

## Core Events to Track

### 1. Page Views

| Event | Description | Properties |
|-------|-------------|------------|
| `page_view` | Any page load | `path`, `referrer`, `device_type` |

**Properties:**
```javascript
{
  path: "/devotional/finding-rest",
  referrer: "direct" | "social" | "search" | "email",
  device_type: "mobile" | "tablet" | "desktop",
  is_pwa: true | false
}
```

---

### 2. Devotional Events

| Event | Description | Properties |
|-------|-------------|------------|
| `devotional_view` | User opens a devotional | `devotional_id`, `series_id`, `category` |
| `devotional_read_start` | User begins reading (scrolls) | `devotional_id`, `series_id` |
| `devotional_read_progress` | User reaches 50% scroll | `devotional_id`, `progress_percent` |
| `devotional_read_complete` | User reaches end / marks complete | `devotional_id`, `reading_time_seconds` |
| `devotional_reflection_view` | User views reflection questions | `devotional_id` |

**Properties:**
```javascript
// devotional_read_complete
{
  devotional_id: "uuid",
  devotional_title: "Finding Rest in Chaos",
  series_id: "uuid",
  series_title: "Rest & Renewal",
  category: "rest-renewal",
  position_in_series: 3,
  reading_time_seconds: 245,
  estimated_reading_time: 240,
  is_first_read: true | false
}
```

**Why This Matters:**
- Understand which devotionals resonate
- Identify content that users abandon
- Track reading habits

---

### 3. Series Events

| Event | Description | Properties |
|-------|-------------|------------|
| `series_view` | User views series page | `series_id`, `source` |
| `series_start` | User reads first devotional in series | `series_id` |
| `series_progress` | User completes any devotional in series | `series_id`, `progress_percent` |
| `series_complete` | User finishes entire series | `series_id`, `total_days` |

**Properties:**
```javascript
// series_complete
{
  series_id: "uuid",
  series_title: "Rest & Renewal",
  category: "rest-renewal",
  total_devotionals: 7,
  days_to_complete: 12,
  completion_rate: 1.0
}
```

**Why This Matters:**
- Understand series engagement
- Identify which series have high completion
- Track content effectiveness

---

### 4. Soul Audit Events

| Event | Description | Properties |
|-------|-------------|------------|
| `soul_audit_start` | User begins Soul Audit | `source`, `is_retake` |
| `soul_audit_input` | User types response | `character_count` |
| `soul_audit_submit` | User submits response | `character_count`, `had_nudge` |
| `soul_audit_clarify_shown` | Low confidence, options shown | `matched_categories` |
| `soul_audit_clarify_select` | User selects clarifying option | `option_selected` |
| `soul_audit_crisis_detected` | Crisis keywords detected | - (no PII) |
| `soul_audit_crisis_resource_click` | User clicks crisis resource | `resource_name` |
| `soul_audit_complete` | User sees results | `primary_category`, `confidence` |
| `soul_audit_recommendation_click` | User clicks recommendation | `devotional_id`, `series_id` |

**Properties:**
```javascript
// soul_audit_complete
{
  is_retake: false,
  response_length: 87,
  had_nudge: false,
  used_clarifying_options: false,
  primary_category: "rest-renewal",
  secondary_categories: ["emotional-healing"],
  confidence_score: 0.85,
  time_to_complete_seconds: 120
}
```

**Why This Matters:**
- Understand onboarding effectiveness
- Measure category matching accuracy
- Track crisis resource usage (anonymized)

---

### 5. Bookmark Events

| Event | Description | Properties |
|-------|-------------|------------|
| `bookmark_add` | User bookmarks a devotional | `devotional_id`, `source` |
| `bookmark_remove` | User removes bookmark | `devotional_id` |
| `bookmark_list_view` | User views bookmarks page | `bookmark_count` |
| `bookmark_click` | User opens from bookmarks | `devotional_id` |

**Properties:**
```javascript
// bookmark_add
{
  devotional_id: "uuid",
  devotional_title: "Finding Rest",
  series_id: "uuid",
  category: "rest-renewal",
  source: "devotional_page" | "series_page"
}
```

**Why This Matters:**
- Understand what content users value enough to save
- Track bookmark engagement

---

### 6. Authentication Events

| Event | Description | Properties |
|-------|-------------|------------|
| `auth_signup_start` | User begins signup | `source` |
| `auth_signup_complete` | User completes signup | `method` |
| `auth_signup_fail` | Signup fails | `error_type` |
| `auth_login_start` | User begins login | `source` |
| `auth_login_complete` | User logs in | `method` |
| `auth_login_fail` | Login fails | `error_type` |
| `auth_logout` | User logs out | - |
| `auth_password_reset_request` | User requests reset | - |
| `auth_password_reset_complete` | User resets password | - |

**Properties:**
```javascript
// auth_signup_complete
{
  method: "email" | "google" | "apple",
  source: "signup_page" | "bookmark_prompt" | "soul_audit_prompt",
  had_soul_audit_before: true | false
}
```

**Why This Matters:**
- Track conversion funnel
- Identify signup friction
- Understand user acquisition

---

### 7. Share Events

| Event | Description | Properties |
|-------|-------------|------------|
| `share_click` | User clicks share button | `devotional_id`, `source` |
| `share_method_select` | User selects share method | `method` |
| `share_complete` | Share action completes | `method`, `devotional_id` |
| `share_copy_link` | User copies link | `devotional_id` |

**Properties:**
```javascript
// share_complete
{
  devotional_id: "uuid",
  method: "native" | "twitter" | "facebook" | "copy_link" | "email",
  source: "devotional_page" | "series_page"
}
```

**Why This Matters:**
- Understand virality potential
- Track which content is shared
- Optimize share functionality

---

### 8. PWA Events

| Event | Description | Properties |
|-------|-------------|------------|
| `pwa_install_prompt_shown` | Install prompt displayed | `device_type` |
| `pwa_install_prompt_accepted` | User accepts install | `device_type` |
| `pwa_install_prompt_dismissed` | User dismisses prompt | `device_type` |
| `pwa_installed` | App successfully installed | `device_type` |
| `pwa_launch` | App launched from home screen | - |
| `pwa_offline_page_shown` | Offline page displayed | - |
| `pwa_offline_content_accessed` | Cached content accessed | `devotional_id` |

**Why This Matters:**
- Track PWA adoption
- Understand install funnel
- Monitor offline usage

---

### 9. Engagement Events

| Event | Description | Properties |
|-------|-------------|------------|
| `streak_achieved` | User achieves streak milestone | `streak_days`, `milestone_type` |
| `streak_broken` | User breaks streak | `previous_streak_days` |
| `milestone_unlocked` | User unlocks achievement | `milestone_id`, `milestone_name` |
| `notification_permission_granted` | User enables notifications | - |
| `notification_permission_denied` | User denies notifications | - |
| `notification_clicked` | User clicks notification | `notification_type` |
| `session_start` | App session begins | `is_returning`, `days_since_last` |

**Properties:**
```javascript
// streak_achieved
{
  streak_days: 7,
  milestone_type: "week_streak",
  total_devotionals_read: 12
}
```

**Why This Matters:**
- Track habit formation
- Understand retention drivers
- Celebrate user progress

---

### 10. Error Events

| Event | Description | Properties |
|-------|-------------|------------|
| `error_api` | API error occurs | `endpoint`, `status_code`, `error_type` |
| `error_client` | Client-side error | `error_message`, `stack_trace`, `page` |
| `error_auth` | Authentication error | `error_type` |
| `error_offline_sync` | Offline sync fails | `sync_type` |

**Properties:**
```javascript
// error_api
{
  endpoint: "/api/devotionals",
  status_code: 500,
  error_type: "server_error",
  page: "/devotional/finding-rest"
}
```

**Why This Matters:**
- Identify and fix issues
- Monitor app health
- Improve reliability

---

## User Properties

Track these properties on users (if logged in):

| Property | Description | Example |
|----------|-------------|---------|
| `user_id` | Anonymous ID | "abc123" |
| `signup_date` | When user signed up | "2026-01-15" |
| `primary_category` | Soul Audit result | "rest-renewal" |
| `devotionals_read` | Total count | 24 |
| `current_streak` | Active streak days | 7 |
| `longest_streak` | Best streak ever | 14 |
| `series_completed` | Count of series done | 2 |
| `is_pwa_user` | Installed as PWA | true |

---

## Key Metrics & KPIs

### Acquisition
| Metric | Description | Target |
|--------|-------------|--------|
| New Users | Daily signups | Growing |
| Traffic Sources | Where users come from | Diverse |
| PWA Installs | App installations | >20% of users |

### Activation
| Metric | Description | Target |
|--------|-------------|--------|
| Soul Audit Completion | % of new users completing | >60% |
| First Devotional Read | % reading first devotional | >70% |
| Signup Conversion | Guest -> Registered | >30% |

### Retention
| Metric | Description | Target |
|--------|-------------|--------|
| D1 Retention | Return next day | >40% |
| D7 Retention | Return within week | >30% |
| D30 Retention | Return within month | >20% |
| Weekly Active Users | Active per week | Growing |

### Engagement
| Metric | Description | Target |
|--------|-------------|--------|
| Devotionals/User/Week | Reading frequency | >3 |
| Series Completion Rate | % finishing series | >40% |
| Avg Reading Time | Time per devotional | 3-5 min |
| Streak Users | Users with active streak | >25% |

### Content
| Metric | Description | Target |
|--------|-------------|--------|
| Completion Rate | % reading to end | >80% |
| Bookmark Rate | % bookmarking | >10% |
| Share Rate | % sharing | >5% |

---

## Dashboard Views

### Executive Dashboard
- Daily/Weekly/Monthly Active Users
- New Signups
- Retention Cohorts
- Top Content

### Content Performance
- Devotional completion rates
- Series engagement
- Category popularity
- Bookmarks by content

### Funnel Analysis
- Landing -> Soul Audit -> First Read -> Signup
- Signup -> D1 Return -> D7 Return -> D30 Return
- Series Start -> Mid -> Complete

### User Journey
- First session behavior
- Soul Audit impact on engagement
- Path to first bookmark
- Path to PWA install

---

## Implementation Guide

### Event Tracking Code Example

```typescript
// lib/analytics.ts

type AnalyticsEvent = {
  name: string;
  properties?: Record<string, any>;
};

export function track(event: AnalyticsEvent) {
  // Check if analytics is enabled
  if (typeof window === 'undefined') return;

  // Add common properties
  const enrichedEvent = {
    ...event,
    properties: {
      ...event.properties,
      timestamp: new Date().toISOString(),
      page_path: window.location.pathname,
      is_pwa: window.matchMedia('(display-mode: standalone)').matches,
    }
  };

  // Send to analytics platform
  // Example: Plausible
  if (window.plausible) {
    window.plausible(enrichedEvent.name, { props: enrichedEvent.properties });
  }
}

// Usage examples:

// Devotional read complete
track({
  name: 'devotional_read_complete',
  properties: {
    devotional_id: devotional.id,
    devotional_title: devotional.title,
    series_id: devotional.series_id,
    category: devotional.category,
    reading_time_seconds: readingTime,
  }
});

// Soul Audit complete
track({
  name: 'soul_audit_complete',
  properties: {
    is_retake: isRetake,
    response_length: response.length,
    primary_category: result.category,
    confidence_score: result.confidence,
  }
});
```

### Privacy Considerations

1. **No PII in Events:** Never track names, emails, or personal identifiers
2. **Anonymous User IDs:** Use random IDs, not user emails
3. **Aggregate Data:** Focus on patterns, not individuals
4. **User Control:** Honor Do Not Track settings
5. **Data Retention:** Delete old data (90 days for events)
6. **Crisis Events:** Track occurrence only, never content

---

## Implementation Checklist

### Phase 1: Core Events (Launch)
- [ ] Page views
- [ ] Devotional read complete
- [ ] Soul Audit complete
- [ ] Signup/Login
- [ ] Error tracking

### Phase 2: Engagement (Week 2)
- [ ] Full devotional funnel
- [ ] Series events
- [ ] Bookmark events
- [ ] Share events

### Phase 3: Advanced (Month 1)
- [ ] PWA events
- [ ] Streak/milestone events
- [ ] Notification events
- [ ] Full user properties

### Phase 4: Optimization (Ongoing)
- [ ] Custom funnels
- [ ] A/B test integration
- [ ] Cohort analysis
- [ ] Predictive metrics

---

## Review Cadence

| Review | Frequency | Focus |
|--------|-----------|-------|
| Daily Glance | Daily | Errors, anomalies |
| Weekly Review | Weekly | KPIs, trends |
| Monthly Deep Dive | Monthly | Cohorts, content performance |
| Quarterly Strategy | Quarterly | Goal setting, roadmap impact |

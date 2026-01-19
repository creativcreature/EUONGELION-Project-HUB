# 65 - Icon Requirements List

**Generated:** 2026-01-19
**Status:** Asset Planning Document

---

## Overview

This document audits the current icon system in EUONGELION and identifies what exists, what's missing, and provides recommendations for icon library usage or custom icon needs.

---

## 1. Current Icon Implementation

### Icon System Architecture

The app uses a custom SVG icon system located at:
```
/app/components/icons/
  Icon.tsx           - Base icon wrapper component
  /navigation/       - Navigation icons
  /actions/          - Action icons
  /reading/          - Reading-related icons
  /progress/         - Progress tracking icons
  /user/             - User/account icons
  /social/           - Social sharing icons
  /ui/               - UI utility icons
  /status/           - Status indicator icons
```

### Icon Component Features
- **Sizes:** xs (12px), sm (16px), md (20px), lg (24px), xl (32px), 2xl (48px)
- **Color:** Inherits from parent via `currentColor`
- **Accessibility:** Supports `aria-label` for meaningful icons, `aria-hidden` for decorative
- **Base viewBox:** 24x24 (Feather/Heroicons compatible)

---

## 2. Existing Icons Inventory

### Navigation Icons (`/components/icons/navigation/`)
| Icon | File | Status | Used In |
|------|------|--------|---------|
| Home | Home.tsx | Exists | BottomNav |
| Search | Search.tsx | Exists | Header, BottomNav |
| Settings | Settings.tsx | Exists | BottomNav |
| Menu | Menu.tsx | Exists | Header |
| Close | Close.tsx | Exists | Modals, Drawer |
| Back | Back.tsx | Exists | Header |
| Forward | Forward.tsx | Exists | Navigation |

### Action Icons (`/components/icons/actions/`)
| Icon | File | Status | Used In |
|------|------|--------|---------|
| Share | Share.tsx | Exists | Devotional actions |
| Bookmark | Bookmark.tsx | Exists | Devotional actions |
| BookmarkFilled | BookmarkFilled.tsx | Exists | Saved state |
| Copy | Copy.tsx | Exists | Share dialog |
| Download | Download.tsx | Exists | Export features |
| Edit | Edit.tsx | Exists | Notes editing |
| Delete | Delete.tsx | Exists | Delete actions |

### Reading Icons (`/components/icons/reading/`)
| Icon | File | Status | Used In |
|------|------|--------|---------|
| Book | Book.tsx | Exists | Series pages |
| Chapter | Chapter.tsx | Exists | Navigation |
| Verse | Verse.tsx | Exists | Scripture display |
| Quote | Quote.tsx | Exists | Blockquotes |
| Highlight | Highlight.tsx | Exists | Text highlighting |

### Progress Icons (`/components/icons/progress/`)
| Icon | File | Status | Used In |
|------|------|--------|---------|
| Check | Check.tsx | Exists | Completion states |
| CheckCircle | CheckCircle.tsx | Exists | Success states |
| Circle | Circle.tsx | Exists | Incomplete states |
| Clock | Clock.tsx | Exists | Reading time |
| Calendar | Calendar.tsx | Exists | Date display |
| Streak | Streak.tsx | Exists | Streak counter |

### User Icons (`/components/icons/user/`)
| Icon | File | Status | Used In |
|------|------|--------|---------|
| User | User.tsx | Exists | Profile |
| UserCircle | UserCircle.tsx | Exists | Avatar placeholder |
| Login | Login.tsx | Exists | Auth |
| Logout | Logout.tsx | Exists | Auth |

### Social Icons (`/components/icons/social/`)
| Icon | File | Status | Used In |
|------|------|--------|---------|
| Twitter | Twitter.tsx | Exists | Share dialog |
| Facebook | Facebook.tsx | Exists | Share dialog |
| Link | Link.tsx | Exists | Copy link |
| Email | Email.tsx | Exists | Email share |

### UI Icons (`/components/icons/ui/`)
| Icon | File | Status | Used In |
|------|------|--------|---------|
| ChevronUp | ChevronUp.tsx | Exists | Expandable sections |
| ChevronDown | ChevronDown.tsx | Exists | Dropdowns |
| ChevronLeft | ChevronLeft.tsx | Exists | Navigation |
| ChevronRight | ChevronRight.tsx | Exists | Navigation |
| Plus | Plus.tsx | Exists | Add actions |
| Minus | Minus.tsx | Exists | Remove actions |

### Status Icons (`/components/icons/status/`)
| Icon | File | Status | Used In |
|------|------|--------|---------|
| Info | Info.tsx | Exists | Info messages |
| Warning | Warning.tsx | Exists | Warning alerts |
| Error | Error.tsx | Exists | Error states |
| Success | Success.tsx | Exists | Success states |

---

## 3. Icons Used Inline (Not in Icon System)

The following icons are defined inline as SVG in components rather than using the icon system:

### Bottom Navigation (`/src/components/layout/BottomNav.tsx`)
| Icon | Current Implementation | Recommendation |
|------|----------------------|----------------|
| Sun/Today | Inline SVG (outline + filled variants) | Move to icon system |
| Book/Series | Inline SVG (outline + filled variants) | Move to icon system |
| Academic Cap/Soul Audit | Inline SVG (outline + filled variants) | Move to icon system |
| Gear/Settings | Inline SVG (outline + filled variants) | Move to icon system |

### Soul Audit Page (`/src/app/soul-audit/page.tsx`)
| Icon | Current Implementation | Recommendation |
|------|----------------------|----------------|
| Sun (Daily Examen) | Inline SVG | Move to icon system |
| Calendar (Weekly Review) | Inline SVG | Exists - use Calendar icon |
| Heart (Confession) | Inline SVG | Add Heart icon to system |
| Sparkles (Gratitude) | Inline SVG | Add Sparkles icon to system |

### Home Page (`/src/app/page.tsx`)
| Icon | Current Implementation | Recommendation |
|------|----------------------|----------------|
| Book | Inline SVG | Exists - use Book icon |
| Academic Cap | Inline SVG | Add AcademicCap icon to system |
| ChevronRight | Inline SVG | Exists - use ChevronRight icon |

### Devotional Page (`/src/app/devotional/[id]/page.tsx`)
| Icon | Current Implementation | Recommendation |
|------|----------------------|----------------|
| ChevronLeft | Inline SVG | Exists - use ChevronLeft icon |
| ChevronRight | Inline SVG | Exists - use ChevronRight icon |

---

## 4. Missing Icons Needed

### High Priority (Used in UI but missing from system)

| Icon | Purpose | Priority |
|------|---------|----------|
| Heart | Confession, favorites, love | High |
| HeartFilled | Saved/favorited state | High |
| Sparkles | Gratitude, highlights | High |
| AcademicCap | Soul Audit feature | High |
| Sun | Today/daily devotional | High |
| SunFilled | Active state | High |
| Moon | Dark mode toggle | High |
| Bell | Notifications | High |
| BellFilled | Has notifications | High |

### Medium Priority (Likely needed for planned features)

| Icon | Purpose | Priority |
|------|---------|----------|
| Play | Audio devotionals (future) | Medium |
| Pause | Audio controls | Medium |
| Volume | Audio controls | Medium |
| VolumeOff | Muted state | Medium |
| Filter | Filter/sort options | Medium |
| Sort | Sort options | Medium |
| Refresh | Refresh/sync | Medium |
| Cloud | Sync status | Medium |
| CloudOff | Offline mode | Medium |
| Lock | Private/locked content | Medium |
| Unlock | Premium/unlocked | Medium |
| Star | Rating/favorites | Medium |
| StarFilled | Rated state | Medium |
| Globe | Language selection | Medium |
| Translate | Translation options | Medium |

### Low Priority (Nice to have)

| Icon | Purpose | Priority |
|------|---------|----------|
| Gift | Referral/sharing | Low |
| Crown | Premium features | Low |
| Fire | Streak/hot content | Low |
| ThumbsUp | Feedback | Low |
| ThumbsDown | Feedback | Low |
| Flag | Report content | Low |
| Print | Print devotional | Low |
| QRCode | Share via QR | Low |

---

## 5. Spiritual/Devotional-Specific Icons (Custom Needed)

These icons are unique to a devotional app and likely need custom design:

| Icon | Description | Priority |
|------|-------------|----------|
| Cross | Christian cross symbol | High |
| Dove | Holy Spirit symbol | Medium |
| Praying Hands | Prayer indicator | High |
| Open Bible | Scripture reading | Medium |
| Candle/Flame | Spiritual devotion | Medium |
| Water/Waves | Baptism, living water | Low |
| Bread | Communion, spiritual food | Low |
| Cup/Chalice | Communion | Low |
| Scroll | Ancient wisdom | Low |
| Hebrew Letter | Word study indicator | Medium |
| Greek Letter | Word study indicator | Medium |
| Selah | Pause/reflection marker | Medium |

---

## 6. Recommendations

### Option A: Continue Custom Icon System (Recommended)

**Pros:**
- Full control over style and sizing
- Optimized bundle size (only include what's used)
- Consistent with current architecture
- Easy to add custom spiritual icons

**Cons:**
- Requires creating/adding each icon manually
- Need to maintain consistency

**Action Items:**
1. Create missing navigation icons (Sun, Moon, Bell, Heart, Sparkles, AcademicCap)
2. Add filled variants for all icons that have active states
3. Design custom spiritual icons (Cross, Praying Hands, etc.)
4. Refactor inline SVGs to use icon system
5. Document icon usage guidelines

### Option B: Adopt Icon Library

If choosing a library, recommended options:

| Library | Pros | Cons |
|---------|------|------|
| **Heroicons** | Already using similar style, MIT license, solid + outline variants | Need tree-shaking, no spiritual icons |
| **Lucide** | Feather-based, extensive set, tree-shakeable | May be overkill |
| **Phosphor** | Multiple weights, consistent style | Large bundle if not tree-shaken |

**If adopting Heroicons:**
```bash
npm install @heroicons/react
```

Would require:
1. Wrapping Heroicons in the existing Icon component for consistent sizing
2. Still need custom spiritual icons
3. Update existing inline SVGs to use Heroicons

### Recommended Approach: Hybrid

1. **Keep custom icon system** for consistency and control
2. **Add missing utility icons** from Heroicons paths (copy SVG paths into custom components)
3. **Design custom spiritual icons** that match the aesthetic
4. **Refactor inline SVGs** throughout the codebase

---

## 7. Icon Design Guidelines

### Style Requirements
- **Stroke weight:** 1.5px (matching Heroicons outline style)
- **Corner radius:** Slightly rounded, soft
- **ViewBox:** 24x24
- **Fill:** None for outline, currentColor for filled
- **Stroke:** currentColor

### Brand Alignment
- Icons should feel contemplative and serene
- Avoid overly playful or cartoonish styles
- Maintain sacred minimalism aesthetic
- Consider subtle manuscript/ancient feel for spiritual icons

### File Structure
```
/components/icons/
  /spiritual/          # New category for devotional icons
    Cross.tsx
    PrayingHands.tsx
    Dove.tsx
    OpenBible.tsx
    Candle.tsx
    Selah.tsx
    HebrewLetter.tsx
    GreekLetter.tsx
    index.ts
```

---

## 8. Implementation Checklist

### Immediate (MVP)
- [ ] Add Heart icon
- [ ] Add HeartFilled icon
- [ ] Add Sparkles icon
- [ ] Add Sun icon (outline + filled)
- [ ] Add Moon icon
- [ ] Add AcademicCap icon
- [ ] Add Bell icon (outline + filled)
- [ ] Add Cross icon (custom)
- [ ] Add PrayingHands icon (custom)

### Short-term
- [ ] Refactor BottomNav to use icon system
- [ ] Refactor Soul Audit page to use icon system
- [ ] Refactor Home page to use icon system
- [ ] Create index.ts exports for all icon categories

### Medium-term
- [ ] Design remaining spiritual icons
- [ ] Add audio control icons (Play, Pause, Volume)
- [ ] Add sync/offline icons
- [ ] Create icon documentation/storybook

---

## Current Status Summary

| Category | Exists | Missing | In System |
|----------|--------|---------|-----------|
| Navigation | 7 | 0 | Yes |
| Actions | 7 | 0 | Yes |
| Reading | 5 | 0 | Yes |
| Progress | 6 | 0 | Yes |
| User | 4 | 0 | Yes |
| Social | 4 | 0 | Yes |
| UI | 6 | 0 | Yes |
| Status | 4 | 0 | Yes |
| **Inline (not in system)** | ~10 | - | No |
| **High Priority Missing** | - | 9 | No |
| **Spiritual/Custom** | - | 12 | No |

**Total in system:** 43 icons
**Total needed to add:** ~31 icons (9 high priority + 10 refactor + 12 spiritual)


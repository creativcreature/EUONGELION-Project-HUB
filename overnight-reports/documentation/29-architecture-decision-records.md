# EUONGELION Architecture Decision Records (ADRs)

## Overview

This document captures the key architectural decisions made during the development of EUONGELION, including the context, decision rationale, and consequences of each choice.

---

## ADR-001: Next.js as Frontend Framework

### Status
**Accepted** - January 2024

### Context
We needed a React-based framework that supports:
- Server-side rendering for SEO
- Static generation for performance
- API routes for backend logic
- PWA capabilities
- TypeScript support
- Easy deployment

### Options Considered

| Option | Pros | Cons |
|--------|------|------|
| **Next.js** | SSR/SSG, API routes, great DX, Vercel deployment | Learning curve, some complexity |
| Create React App | Simple, well-known | No SSR, limited features |
| Remix | Great data loading, full-stack | Newer, less ecosystem |
| Gatsby | Static sites, GraphQL | Overkill for dynamic content |
| Astro | Fast, multi-framework | Less React-focused |

### Decision
Use **Next.js 15** with the App Router.

### Rationale
1. **Server Components**: Reduce client bundle, improve performance
2. **App Router**: Modern routing with layouts and loading states
3. **API Routes**: Backend logic without separate server
4. **Vercel Integration**: Seamless deployment with previews
5. **Large Ecosystem**: Extensive community and documentation
6. **PWA Support**: Works well with next-pwa

### Consequences
- **Positive**: Fast development, great performance, easy deployment
- **Negative**: Some complexity with server/client component boundaries
- **Mitigation**: Clear patterns and documentation for team

---

## ADR-002: Supabase as Backend-as-a-Service

### Status
**Accepted** - January 2024

### Context
We needed a backend solution providing:
- PostgreSQL database
- Authentication
- Real-time capabilities
- File storage
- Row-level security
- Good free tier

### Options Considered

| Option | Pros | Cons |
|--------|------|------|
| **Supabase** | PostgreSQL, Auth, RLS, generous free tier | Vendor lock-in |
| Firebase | Google backing, real-time | NoSQL, pricing unpredictable |
| AWS Amplify | Full AWS integration | Complex, steep learning curve |
| PlanetScale | MySQL, serverless | No auth, no storage |
| Neon | PostgreSQL, serverless | No auth built-in |
| Custom Backend | Full control | Time-consuming, maintenance |

### Decision
Use **Supabase** for database, authentication, and storage.

### Rationale
1. **PostgreSQL**: Relational database with full SQL support
2. **Row-Level Security**: Security at database level, not just API
3. **Built-in Auth**: Email, OAuth, and anonymous authentication
4. **Real-time**: Future feature support (live devotional sessions)
5. **Generous Free Tier**: Suitable for MVP and early growth
6. **Open Source**: Can self-host if needed

### Consequences
- **Positive**: Rapid development, secure by default, great DX
- **Negative**: Vendor dependency, some limitations on free tier
- **Mitigation**: Use standard PostgreSQL patterns for portability

---

## ADR-003: Zustand for State Management

### Status
**Accepted** - January 2024

### Context
We needed client-side state management for:
- Authentication state
- User preferences
- Reading progress
- Bookmarks
- UI state

### Options Considered

| Option | Pros | Cons |
|--------|------|------|
| **Zustand** | Minimal, hooks-based, small bundle | Less known than Redux |
| Redux Toolkit | Battle-tested, great devtools | Boilerplate, large bundle |
| React Context | Built-in, no library | Performance issues at scale |
| Jotai | Atomic model, small | Different mental model |
| Recoil | Facebook-backed | Larger bundle, more complex |
| MobX | Reactive, auto-tracking | Magic can be confusing |

### Decision
Use **Zustand** for all client-side state management.

### Rationale
1. **Bundle Size**: ~1KB vs ~7KB+ for Redux
2. **Simplicity**: No boilerplate, just functions
3. **TypeScript**: Excellent type inference
4. **Flexibility**: Works outside React components
5. **Persistence**: Easy middleware for offline support
6. **DevTools**: Redux DevTools compatible

### Consequences
- **Positive**: Clean code, small bundle, fast development
- **Negative**: Less structured than Redux
- **Mitigation**: Clear store organization and naming conventions

---

## ADR-004: Tailwind CSS for Styling

### Status
**Accepted** - January 2024

### Context
We needed a styling solution that provides:
- Rapid development
- Consistent design system
- Dark mode support
- Small bundle in production
- Mobile-first responsive design

### Options Considered

| Option | Pros | Cons |
|--------|------|------|
| **Tailwind CSS** | Utility-first, small prod bundle, customizable | Learning curve, verbose classes |
| Styled Components | Component scoped, CSS-in-JS | Runtime overhead, SSR complexity |
| CSS Modules | Component scoped, no runtime | More files, less flexible |
| Sass/SCSS | Powerful, familiar | Global scope issues |
| vanilla-extract | Type-safe, zero runtime | More complex setup |

### Decision
Use **Tailwind CSS** with custom design tokens.

### Rationale
1. **Speed**: Rapid prototyping with utility classes
2. **Consistency**: Design tokens enforce consistency
3. **Performance**: Purged CSS = tiny production bundle
4. **Dark Mode**: Built-in dark mode support
5. **Responsive**: Mobile-first utilities
6. **Customization**: Full control over design system

### Consequences
- **Positive**: Fast development, consistent UI, small CSS bundle
- **Negative**: Verbose class names in JSX
- **Mitigation**: Component abstraction, cn() utility function

---

## ADR-005: PWA Architecture

### Status
**Accepted** - January 2024

### Context
EUONGELION is primarily a mobile experience. We needed:
- Offline capability
- Home screen installation
- Push notifications (future)
- Fast loading
- Native-like experience

### Options Considered

| Option | Pros | Cons |
|--------|------|------|
| **PWA (next-pwa)** | Single codebase, web standards | Limited native features |
| React Native | Native performance, app stores | Two codebases, more complex |
| Capacitor | Web + Native shell | Additional build step |
| Flutter | Cross-platform, fast | New language (Dart) |
| Native Apps | Best performance | Multiple codebases |

### Decision
Build as **PWA** using next-pwa.

### Rationale
1. **Single Codebase**: Web and mobile from same code
2. **No App Store**: Direct distribution, no approval process
3. **Instant Updates**: Changes deploy immediately
4. **Lower Cost**: One team, one codebase
5. **Web Standards**: Future-proof technology
6. **Offline Support**: Service worker caching

### Consequences
- **Positive**: Fast development, easy updates, low maintenance
- **Negative**: Some limitations vs native (push notifications, etc.)
- **Mitigation**: Progressive enhancement, plan for native if needed

---

## ADR-006: TypeScript for Type Safety

### Status
**Accepted** - January 2024

### Context
We needed to ensure code quality and developer experience with:
- Type safety
- Better IDE support
- Self-documenting code
- Refactoring confidence

### Options Considered

| Option | Pros | Cons |
|--------|------|------|
| **TypeScript** | Type safety, great DX, industry standard | Build step, learning curve |
| JavaScript + JSDoc | No build step, gradual typing | Less robust, more verbose |
| Flow | Similar to TS | Less adoption, weaker tooling |

### Decision
Use **TypeScript** with strict mode.

### Rationale
1. **Type Safety**: Catch errors at compile time
2. **IDE Support**: Excellent autocomplete and refactoring
3. **Documentation**: Types serve as documentation
4. **Ecosystem**: All major libraries have types
5. **Industry Standard**: Most teams expect TS

### Consequences
- **Positive**: Fewer bugs, better DX, easier maintenance
- **Negative**: Initial setup, some complexity
- **Mitigation**: Use strict mode, document patterns

---

## ADR-007: Vercel for Deployment

### Status
**Accepted** - January 2024

### Context
We needed a deployment platform that:
- Supports Next.js natively
- Provides automatic deployments
- Offers preview deployments
- Has reasonable pricing
- Handles scaling

### Options Considered

| Option | Pros | Cons |
|--------|------|------|
| **Vercel** | Native Next.js support, great DX | Function limits on Hobby |
| Netlify | Good DX, functions | Less Next.js optimized |
| AWS | Full control, scalable | Complex, more expensive |
| Railway | Simple, good DX | Newer, less features |
| Render | Good pricing | Less optimized for Next.js |

### Decision
Use **Vercel Hobby plan** initially.

### Rationale
1. **Native Integration**: Built by Next.js creators
2. **Zero Config**: Deploy with git push
3. **Preview Deployments**: Test before production
4. **Edge Network**: Global CDN included
5. **Analytics**: Built-in performance analytics
6. **Free Tier**: Suitable for MVP

### Consequences
- **Positive**: Easy deployment, great performance, previews
- **Negative**: 12 function limit on Hobby plan
- **Mitigation**: Consolidate API routes, use Edge functions

---

## ADR-008: Content in Database vs Files

### Status
**Accepted** - January 2024

### Context
Devotional content needs to be:
- Easy to create and edit
- Searchable
- Related to user progress
- Versioned

### Options Considered

| Option | Pros | Cons |
|--------|------|------|
| **Database (PostgreSQL)** | Searchable, relational, dynamic | More complex editing |
| Markdown Files | Easy editing, version control | Limited queries, no relations |
| CMS (Contentful, etc.) | Great editing UX | Cost, another dependency |
| MDX in App | React in content | Build-time only |

### Decision
Store content in **PostgreSQL database**.

### Rationale
1. **Relations**: Content linked to user progress
2. **Search**: Full-text search capability
3. **Dynamic**: Content changes without redeploy
4. **RLS**: Content access control
5. **Single Source**: All data in one place

### Consequences
- **Positive**: Unified data model, powerful queries
- **Negative**: Need admin interface for content
- **Mitigation**: Build simple admin or use Supabase dashboard

---

## ADR-009: Sacred Minimalism Design Philosophy

### Status
**Accepted** - January 2024

### Context
EUONGELION's visual design needed to:
- Focus on content (Scripture)
- Feel sacred and contemplative
- Work in dark/light modes
- Be accessible
- Be distinctive from "app-like" devotionals

### Decision
Adopt **"Sacred Minimalism"** design philosophy:
- Muted, earthy color palette
- Typography-forward design
- Generous whitespace
- Subtle animations
- Dark mode primary

### Color Palette

| Color | Usage | Hex |
|-------|-------|-----|
| Tehom (Deep Dark) | Backgrounds | #1A1612 |
| Scroll (Parchment) | Light backgrounds | #F7F3ED |
| Gold (Burnished) | Accents, CTAs | #C19A6B |
| Burgundy | Passion, emphasis | #6B2C2C |
| Olive | Growth, wisdom | #6B6B4F |
| Shalom Blue | Peace, depth | #4A5F6B |

### Rationale
1. **Focused Reading**: No distractions from content
2. **Emotional Impact**: Colors evoke sacred tradition
3. **Accessibility**: High contrast ratios
4. **Versatility**: Works for various content types

### Consequences
- **Positive**: Distinctive, contemplative experience
- **Negative**: May feel too subtle for some
- **Mitigation**: Ensure touch targets are clear, add subtle feedback

---

## ADR-010: Immersion Levels for Devotionals

### Status
**Accepted** - January 2024

### Context
Users have different amounts of time for devotionals. We needed to:
- Accommodate busy schedules
- Provide depth for those who want it
- Track different engagement levels

### Decision
Implement **three immersion levels**:
- **1-minute**: Scripture + key verse
- **5-minute**: Scripture + reflection + brief teaching
- **15-minute**: Full devotional + prayer + application

### Rationale
1. **Accessibility**: Everyone can participate
2. **Flexibility**: Same content, different depths
3. **Growth**: Encourage deeper engagement over time
4. **Tracking**: Measure engagement quality

### Consequences
- **Positive**: Lower barrier to entry, flexible experience
- **Negative**: More content to write per devotional
- **Mitigation**: Structure content to build on itself

---

## Summary of Technology Choices

| Area | Choice | Rationale |
|------|--------|-----------|
| Framework | Next.js 15 | SSR, API routes, Vercel integration |
| Database | Supabase (PostgreSQL) | RLS, auth, real-time, free tier |
| State | Zustand | Minimal, flexible, small bundle |
| Styling | Tailwind CSS | Utility-first, dark mode, design system |
| PWA | next-pwa | Offline support, installable |
| Language | TypeScript | Type safety, better DX |
| Deployment | Vercel | Native Next.js, previews, CDN |
| Auth | Supabase Auth | Integrated, secure, multiple providers |

---

## Future Considerations

### Potential Changes

1. **Native App**: If PWA limitations become blockers
2. **CMS**: If content team grows significantly
3. **Hosting**: If Vercel limits become restrictive
4. **AI Features**: May need specialized infrastructure

### Review Schedule

- Review ADRs quarterly
- Update when significant changes occur
- Document any deviations and reasons

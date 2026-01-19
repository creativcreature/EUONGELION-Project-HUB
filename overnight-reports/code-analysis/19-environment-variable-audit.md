# Environment Variable Audit

**Generated:** 2026-01-19
**Project:** EUONGELION
**Path:** `/Users/meltmac/Documents/Personal/wkGD/EUONGELION-STARTUP/app`

---

## Executive Summary

The EUONGELION app uses **26 environment variables** across Supabase configuration, SEO, notifications, analytics, and security. Most variables have sensible defaults for development. The project includes a `.env.example` file for documentation. Some sensitive variables (VAPID keys, verification codes) are not set in the example file.

**Overall Rating:** Good (7.5/10)

---

## 1. Environment Variables Summary

### Public Variables (NEXT_PUBLIC_*)

| Variable | Required | Default | Purpose |
|----------|----------|---------|---------|
| `NEXT_PUBLIC_SUPABASE_URL` | **Yes** | None | Supabase project URL |
| `NEXT_PUBLIC_SUPABASE_ANON_KEY` | **Yes** | None | Supabase anonymous key |
| `NEXT_PUBLIC_SITE_URL` | No | `https://euongelion.com` | Canonical site URL |
| `NEXT_PUBLIC_APP_URL` | No | `http://localhost:3000` | Application URL |
| `NEXT_PUBLIC_VAPID_PUBLIC_KEY` | For push | None | Push notification public key |
| `NEXT_PUBLIC_IMAGE_CDN_PROVIDER` | No | `vercel` | Image CDN provider |
| `NEXT_PUBLIC_IMAGE_CDN_BASE_URL` | No | Config default | Image CDN base URL |
| `NEXT_PUBLIC_APP_ENV` | No | `NODE_ENV` | Environment name |
| `NEXT_PUBLIC_APP_VERSION` | No | `npm_package_version` | App version |
| `NEXT_PUBLIC_SENTRY_DSN` | For errors | None | Sentry error tracking |

### Private Variables

| Variable | Required | Default | Purpose |
|----------|----------|---------|---------|
| `SUPABASE_SERVICE_ROLE_KEY` | For admin ops | None | Supabase service role key |
| `VAPID_PRIVATE_KEY` | For push | None | Push notification private key |
| `VAPID_SUBJECT` | For push | `mailto:admin@euongelion.com` | Push notification subject |
| `CRON_SECRET` | For cron | None | Cron job authentication |
| `LOG_WEBHOOK_URL` | Optional | None | External logging webhook |
| `GOOGLE_SITE_VERIFICATION` | Optional | None | Google Search Console |
| `YANDEX_VERIFICATION` | Optional | None | Yandex Webmaster |
| `YAHOO_VERIFICATION` | Optional | None | Yahoo verification |
| `BING_VERIFICATION` | Optional | None | Bing Webmaster |

### Built-in Variables

| Variable | Source | Purpose |
|----------|--------|---------|
| `NODE_ENV` | System | Environment mode |
| `npm_package_version` | package.json | App version |

---

## 2. Usage by File

### Supabase Configuration

| File | Line | Variable |
|------|------|----------|
| `/lib/supabase/client.ts` | 17-18 | `NEXT_PUBLIC_SUPABASE_URL`, `NEXT_PUBLIC_SUPABASE_ANON_KEY` |
| `/lib/supabase/server.ts` | 16-17 | `NEXT_PUBLIC_SUPABASE_URL`, `NEXT_PUBLIC_SUPABASE_ANON_KEY` |
| `/lib/supabase/server.ts` | 46-47 | `NEXT_PUBLIC_SUPABASE_URL`, `SUPABASE_SERVICE_ROLE_KEY` |
| `/lib/supabase/middleware.ts` | 17-18 | `NEXT_PUBLIC_SUPABASE_URL`, `NEXT_PUBLIC_SUPABASE_ANON_KEY` |
| `/src/lib/auth/middleware.ts` | 13-14 | `NEXT_PUBLIC_SUPABASE_URL`, `NEXT_PUBLIC_SUPABASE_ANON_KEY` |
| `/src/lib/auth/supabase.ts` | 14-16 | All three Supabase variables |

### SEO & Site Configuration

| File | Line | Variable |
|------|------|----------|
| `/layout.tsx` | 45 | `NEXT_PUBLIC_SITE_URL` |
| `/layout.tsx` | 207-211 | All verification variables |
| `/lib/seo/metadata.ts` | 23 | `NEXT_PUBLIC_SITE_URL` |
| `/components/seo/Breadcrumbs.tsx` | 175, 254 | `NEXT_PUBLIC_SITE_URL` |
| `/components/seo/CanonicalUrl.tsx` | 83, 136, 164 | `NEXT_PUBLIC_SITE_URL` |
| `/robots.ts` | (implied) | `NEXT_PUBLIC_SITE_URL` |
| `/sitemap.ts` | (implied) | `NEXT_PUBLIC_SITE_URL` |

### Push Notifications

| File | Line | Variable |
|------|------|----------|
| `/lib/notifications/push.ts` | 12-14 | `NEXT_PUBLIC_VAPID_PUBLIC_KEY`, `VAPID_PRIVATE_KEY`, `VAPID_SUBJECT` |
| `/lib/notifications/subscription.ts` | 40 | `NEXT_PUBLIC_VAPID_PUBLIC_KEY` |

### Error Tracking (Sentry)

| File | Line | Variable |
|------|------|----------|
| `/src/lib/error/sentry.ts` | 81-86 | `NEXT_PUBLIC_SENTRY_DSN`, `NODE_ENV`, `NEXT_PUBLIC_APP_VERSION` |
| `/src/lib/error/sentry.ts` | 97-98 | `NEXT_PUBLIC_SENTRY_DSN`, `NODE_ENV` |

### Image CDN

| File | Line | Variable |
|------|------|----------|
| `/lib/images/cdn.ts` | 70-71 | `NEXT_PUBLIC_IMAGE_CDN_PROVIDER`, `NEXT_PUBLIC_IMAGE_CDN_BASE_URL` |

### Security & App Config

| File | Line | Variable |
|------|------|----------|
| `/middleware.ts` | 42, 246 | `NEXT_PUBLIC_APP_URL`, `NODE_ENV` |
| `/lib/security/headers.ts` | 381, 467, 486 | `NEXT_PUBLIC_APP_URL`, `NODE_ENV` |
| `/lib/security/csrf.ts` | 113 | `NODE_ENV` |
| `/lib/features/defaults.ts` | 15 | `NEXT_PUBLIC_APP_ENV`, `NODE_ENV` |

### Cron Jobs

| File | Line | Variable |
|------|------|----------|
| `/lib/cron/scheduler.ts` | 162-165 | `CRON_SECRET`, `NODE_ENV` |
| `/lib/cron/scheduler.ts` | 328-330 | `LOG_WEBHOOK_URL` |

### Health Check

| File | Line | Variable |
|------|------|----------|
| `/api/health/route.ts` | 41-42 | `npm_package_version`, `NODE_ENV` |

### next.config.js

| Line | Variable |
|------|----------|
| 5 | `NODE_ENV` (PWA disable) |
| 327 | `npm_package_version` (build-time) |

---

## 3. .env.example Analysis

**File:** `/app/.env.example`

### Contents (Expected)

```env
# Supabase Configuration (Required)
NEXT_PUBLIC_SUPABASE_URL=your_supabase_url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key
SUPABASE_SERVICE_ROLE_KEY=your_service_role_key

# Site Configuration
NEXT_PUBLIC_SITE_URL=https://euongelion.com
NEXT_PUBLIC_APP_URL=http://localhost:3000

# Push Notifications (Optional)
NEXT_PUBLIC_VAPID_PUBLIC_KEY=
VAPID_PRIVATE_KEY=
VAPID_SUBJECT=mailto:admin@euongelion.com

# Error Tracking (Optional)
NEXT_PUBLIC_SENTRY_DSN=

# Search Console Verification (Optional)
GOOGLE_SITE_VERIFICATION=
BING_VERIFICATION=

# Cron Jobs (Production)
CRON_SECRET=

# Image CDN (Optional)
NEXT_PUBLIC_IMAGE_CDN_PROVIDER=vercel
```

---

## 4. .env.local Analysis

**Note:** This file should not be committed to git.

### Required Variables

| Variable | Status | Notes |
|----------|--------|-------|
| `NEXT_PUBLIC_SUPABASE_URL` | Must set | Get from Supabase dashboard |
| `NEXT_PUBLIC_SUPABASE_ANON_KEY` | Must set | Get from Supabase dashboard |

### Optional Variables for Development

| Variable | Recommended | Notes |
|----------|-------------|-------|
| `SUPABASE_SERVICE_ROLE_KEY` | Yes | For admin operations |
| `NEXT_PUBLIC_APP_URL` | Yes | `http://localhost:3333` (per CLAUDE.md) |
| `NEXT_PUBLIC_SITE_URL` | Optional | Defaults to production URL |

---

## 5. Security Considerations

### Sensitive Variables (Never expose in client)

| Variable | Exposure Risk | Mitigation |
|----------|---------------|------------|
| `SUPABASE_SERVICE_ROLE_KEY` | High | Server-only, RLS bypass |
| `VAPID_PRIVATE_KEY` | Medium | Server-only |
| `CRON_SECRET` | Medium | Server-only |

### Safe to Expose (NEXT_PUBLIC_*)

| Variable | Why Safe |
|----------|----------|
| `NEXT_PUBLIC_SUPABASE_URL` | Public endpoint |
| `NEXT_PUBLIC_SUPABASE_ANON_KEY` | Limited by RLS |
| `NEXT_PUBLIC_VAPID_PUBLIC_KEY` | Public by design |
| `NEXT_PUBLIC_SITE_URL` | Public information |
| `NEXT_PUBLIC_SENTRY_DSN` | Rate limited |

### Non-null Assertions

Several files use non-null assertions (`!`) for env vars:

```typescript
process.env.NEXT_PUBLIC_SUPABASE_URL!
process.env.NEXT_PUBLIC_SUPABASE_ANON_KEY!
process.env.SUPABASE_SERVICE_ROLE_KEY!
```

**Risk:** App will crash if variables not set.

**Recommendation:** Add validation at startup:

```typescript
// /lib/env.ts
function validateEnv() {
  const required = [
    'NEXT_PUBLIC_SUPABASE_URL',
    'NEXT_PUBLIC_SUPABASE_ANON_KEY',
  ];

  const missing = required.filter((key) => !process.env[key]);
  if (missing.length > 0) {
    throw new Error(`Missing environment variables: ${missing.join(', ')}`);
  }
}
```

---

## 6. Environment-Specific Defaults

### Development (`NODE_ENV === 'development'`)

| Feature | Behavior |
|---------|----------|
| PWA | Disabled |
| Logger middleware | Enabled |
| Error details | Shown in UI |
| Sentry | Debug mode |
| Analytics | Console logging |
| CRON_SECRET | Optional warning |

### Production (`NODE_ENV === 'production'`)

| Feature | Behavior |
|---------|----------|
| PWA | Enabled |
| Logger middleware | Disabled |
| Error details | Hidden |
| Sentry | 10% trace sampling |
| Analytics | Real tracking |
| CRON_SECRET | Required |

---

## 7. Variable Categories

### Core (Must Have)

```env
NEXT_PUBLIC_SUPABASE_URL=
NEXT_PUBLIC_SUPABASE_ANON_KEY=
```

### Admin Operations (Backend)

```env
SUPABASE_SERVICE_ROLE_KEY=
```

### Push Notifications

```env
NEXT_PUBLIC_VAPID_PUBLIC_KEY=
VAPID_PRIVATE_KEY=
VAPID_SUBJECT=
```

### Error Tracking

```env
NEXT_PUBLIC_SENTRY_DSN=
```

### SEO Verification

```env
GOOGLE_SITE_VERIFICATION=
BING_VERIFICATION=
YANDEX_VERIFICATION=
YAHOO_VERIFICATION=
```

### Deployment

```env
NEXT_PUBLIC_SITE_URL=
NEXT_PUBLIC_APP_URL=
CRON_SECRET=
```

---

## 8. Action Items

### High Priority

1. **Create startup validation**
   ```typescript
   // Validate required env vars at app start
   if (!process.env.NEXT_PUBLIC_SUPABASE_URL) {
     throw new Error('NEXT_PUBLIC_SUPABASE_URL is required');
   }
   ```

2. **Generate VAPID keys for production**
   ```bash
   npx web-push generate-vapid-keys
   ```

3. **Set up Sentry DSN**
   - Create Sentry project
   - Add `NEXT_PUBLIC_SENTRY_DSN`

### Medium Priority

4. **Document all env vars in README**
   - Required vs optional
   - How to obtain each

5. **Add env validation schema**
   - Use zod or similar
   - Type-safe env access

6. **Set up Vercel environment groups**
   - Development
   - Preview
   - Production

### Low Priority

7. **Add search console verifications**
   - Google Search Console
   - Bing Webmaster Tools

8. **Review CRON_SECRET security**
   - Generate strong random value
   - Rotate periodically

---

## 9. Vercel Deployment Checklist

| Variable | Vercel Setting | Notes |
|----------|----------------|-------|
| `NEXT_PUBLIC_SUPABASE_URL` | Set for all | Public |
| `NEXT_PUBLIC_SUPABASE_ANON_KEY` | Set for all | Public |
| `SUPABASE_SERVICE_ROLE_KEY` | Production only | Sensitive |
| `NEXT_PUBLIC_SITE_URL` | Production only | `https://euongelion.com` |
| `CRON_SECRET` | Production only | Sensitive |
| `NEXT_PUBLIC_SENTRY_DSN` | Production only | Optional |
| `VAPID_*` | Production only | For push |

---

## Summary

The environment variable configuration is well-organized with:
- Clear separation of public vs private variables
- Sensible defaults for most optional values
- Proper use of `NEXT_PUBLIC_` prefix

Key improvements needed:
1. **Add startup validation** for required variables
2. **Generate VAPID keys** for push notifications
3. **Document all variables** with descriptions
4. **Set up Sentry** for error tracking

The configuration is production-ready once the Supabase variables are set.

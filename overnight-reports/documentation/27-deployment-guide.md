# EUONGELION Deployment Guide

## Overview

EUONGELION is deployed to **Vercel** with **Supabase** as the backend. This guide covers the complete deployment process, environment configuration, and production considerations.

---

## Architecture Overview

```
┌─────────────────────────────────────────────────────────────────┐
│                         Users                                    │
└───────────────────────────┬─────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Vercel Edge Network                           │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────────────────┐  │
│  │ CDN/Cache   │  │ Edge Funcs  │  │ Serverless Functions   │  │
│  └─────────────┘  └─────────────┘  └─────────────────────────┘  │
└───────────────────────────┬─────────────────────────────────────┘
                            │
           ┌────────────────┼────────────────┐
           │                │                │
           ▼                ▼                ▼
┌──────────────┐  ┌──────────────┐  ┌──────────────┐
│   Supabase   │  │   Supabase   │  │   Supabase   │
│   Auth       │  │   Database   │  │   Storage    │
└──────────────┘  └──────────────┘  └──────────────┘
```

---

## Prerequisites

1. **Vercel Account** (Hobby or Pro plan)
2. **Supabase Project** (Free or Pro plan)
3. **GitHub Repository** (for CI/CD)
4. **Domain** (optional, for custom domain)

---

## Vercel Deployment

### Initial Setup

1. **Connect Repository**
   ```bash
   # Install Vercel CLI
   npm install -g vercel

   # Login to Vercel
   vercel login

   # Link project
   cd /path/to/euongelion/app
   vercel link
   ```

2. **Configure Project Settings**
   - Framework Preset: `Next.js`
   - Root Directory: `app/`
   - Build Command: `next build`
   - Output Directory: `.next`
   - Install Command: `npm install`

3. **Set Environment Variables**
   ```bash
   # Add each environment variable
   vercel env add NEXT_PUBLIC_SUPABASE_URL
   vercel env add NEXT_PUBLIC_SUPABASE_ANON_KEY
   vercel env add SUPABASE_SERVICE_ROLE_KEY
   # ... continue for all variables
   ```

### Deploy Commands

```bash
# Deploy to preview
vercel

# Deploy to production
vercel --prod

# Deploy with specific environment
vercel --prod --env production
```

### Automatic Deployments

With GitHub integration:
- **Push to `main`**: Production deployment
- **Push to other branches**: Preview deployment
- **Pull requests**: Preview deployment with comment

---

## Environment Variables

### Required Variables

| Variable | Description | Example |
|----------|-------------|---------|
| `NEXT_PUBLIC_SUPABASE_URL` | Supabase project URL | `https://xxx.supabase.co` |
| `NEXT_PUBLIC_SUPABASE_ANON_KEY` | Supabase anon key | `eyJhbG...` |
| `SUPABASE_SERVICE_ROLE_KEY` | Supabase service key | `eyJhbG...` |
| `NEXT_PUBLIC_APP_URL` | Production URL | `https://euongelion.app` |

### Optional Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `NEXT_PUBLIC_APP_ENV` | Environment | `production` |
| `NEXT_PUBLIC_GA_MEASUREMENT_ID` | Google Analytics | - |
| `SENTRY_DSN` | Sentry error tracking | - |
| `NEXT_PUBLIC_ENABLE_ANALYTICS` | Enable analytics | `false` |
| `NEXT_PUBLIC_ENABLE_AI_FEATURES` | Enable AI features | `true` |
| `NEXT_PUBLIC_MAINTENANCE_MODE` | Maintenance mode | `false` |

### Environment-Specific Configuration

```
Vercel Dashboard > Project > Settings > Environment Variables

Production:
  NEXT_PUBLIC_APP_ENV=production
  NEXT_PUBLIC_APP_URL=https://euongelion.app

Preview:
  NEXT_PUBLIC_APP_ENV=preview
  NEXT_PUBLIC_APP_URL=https://preview.euongelion.app

Development:
  NEXT_PUBLIC_APP_ENV=development
  NEXT_PUBLIC_APP_URL=http://localhost:3333
```

---

## Build Process

### Build Command

```bash
next build
```

### Build Output

```
app/
  .next/
    cache/           # Build cache
    server/          # Server-side code
    static/          # Static assets
    standalone/      # Standalone server
```

### Build Configuration

**`next.config.js`** key settings:

```javascript
const nextConfig = {
  // Enable standalone output for serverless
  output: 'standalone',

  // React strict mode
  reactStrictMode: true,

  // Disable powered by header
  poweredByHeader: false,

  // Enable compression
  compress: true,

  // TypeScript errors (temporarily ignored for MVP)
  typescript: {
    ignoreBuildErrors: true,
  },

  // ESLint errors (temporarily ignored for MVP)
  eslint: {
    ignoreDuringBuilds: true,
  },
};
```

### Build Optimization

1. **Code Splitting**: Automatic with Next.js
2. **Image Optimization**: Next.js Image component
3. **Font Optimization**: Next.js Font with preloading
4. **CSS Optimization**: Tailwind CSS purging
5. **JavaScript Optimization**: Tree shaking, minification

---

## Vercel Constraints

### Hobby Plan Limits

| Limit | Value | Current Usage |
|-------|-------|---------------|
| Serverless Functions | 12 max | 10 used |
| Function Timeout | 10 seconds | - |
| Bandwidth | 100 GB/month | - |
| Build Time | 45 minutes | ~2-3 minutes |
| Deployments | Unlimited | - |

### Function Count

Current API routes (10/12):
1. `/api/devotionals` - GET
2. `/api/devotionals/[id]` - GET
3. `/api/series` - GET
4. `/api/series/[slug]` - GET
5. `/api/user/progress` - GET, POST, DELETE
6. `/api/user/bookmarks` - GET, POST, PUT, DELETE
7. `/api/soul-audit/questions` - GET
8. `/api/soul-audit/submit` - GET, POST
9. `/api/auth/callback` - GET
10. (Reserved for future)

### Optimizations for Limits

1. **Combine related routes**: Multiple HTTP methods per route
2. **Edge functions**: Move simple logic to edge (no limit)
3. **Static generation**: Pre-render where possible
4. **API consolidation**: Batch operations where possible

---

## Domain Configuration

### Custom Domain Setup

1. **Add Domain in Vercel**
   ```
   Vercel Dashboard > Project > Settings > Domains
   Add: euongelion.app
   ```

2. **Configure DNS**
   ```
   Type: A     Name: @    Value: 76.76.21.21
   Type: CNAME Name: www  Value: cname.vercel-dns.com
   ```

3. **SSL Certificate**
   - Automatic with Vercel
   - Let's Encrypt certificates
   - Auto-renewal

### Redirect Configuration

```javascript
// next.config.js
async redirects() {
  return [
    {
      source: '/www',
      destination: '/',
      permanent: true,
    },
  ];
}
```

---

## Supabase Configuration

### Production Setup

1. **Create Production Project**
   ```
   Supabase Dashboard > New Project
   Name: euongelion-production
   Region: us-east-1 (or closest to users)
   ```

2. **Apply Migrations**
   ```bash
   # Install Supabase CLI
   npm install -g supabase

   # Link to project
   supabase link --project-ref your-project-ref

   # Push migrations
   supabase db push
   ```

3. **Configure Auth**
   - Enable email auth
   - Configure OAuth providers
   - Set redirect URLs to production domain
   - Configure email templates

4. **Set RLS Policies**
   ```sql
   -- Run migration files to set up RLS
   \i database/migrations/001_create_users.sql
   \i database/migrations/002_create_series.sql
   -- ... etc
   ```

### Connection Pooling

For high traffic, enable connection pooling:

```
Supabase Dashboard > Project > Settings > Database
Enable Pooler: Yes
Pool Mode: Transaction
```

Update connection string:
```env
# Use pooler URL for production
DATABASE_URL=postgresql://postgres:password@db.xxx.supabase.co:6543/postgres?pgbouncer=true
```

---

## Security Headers

Configured in `next.config.js`:

```javascript
const securityHeaders = [
  // HSTS
  {
    key: 'Strict-Transport-Security',
    value: 'max-age=63072000; includeSubDomains; preload',
  },
  // Prevent clickjacking
  {
    key: 'X-Frame-Options',
    value: 'SAMEORIGIN',
  },
  // Prevent MIME sniffing
  {
    key: 'X-Content-Type-Options',
    value: 'nosniff',
  },
  // XSS protection
  {
    key: 'X-XSS-Protection',
    value: '1; mode=block',
  },
  // Referrer policy
  {
    key: 'Referrer-Policy',
    value: 'strict-origin-when-cross-origin',
  },
  // CSP
  {
    key: 'Content-Security-Policy',
    value: "default-src 'self'; ...",
  },
  // Permissions policy
  {
    key: 'Permissions-Policy',
    value: 'camera=(), microphone=(), geolocation=()',
  },
];
```

---

## PWA Configuration

### Service Worker

Configured via `next-pwa`:

```javascript
const withPWA = require('next-pwa')({
  dest: 'public',
  disable: process.env.NODE_ENV === 'development',
  register: true,
  skipWaiting: true,
  runtimeCaching: [
    // ... caching strategies
  ],
});
```

### Manifest

Located at `public/manifest.json`:

```json
{
  "name": "EUONGELION",
  "short_name": "EUONGELION",
  "description": "Daily Christian Devotionals",
  "start_url": "/",
  "display": "standalone",
  "background_color": "#1A1612",
  "theme_color": "#C19A6B",
  "icons": [
    {
      "src": "/icons/icon-192x192.png",
      "sizes": "192x192",
      "type": "image/png"
    },
    {
      "src": "/icons/icon-512x512.png",
      "sizes": "512x512",
      "type": "image/png"
    }
  ]
}
```

---

## Monitoring & Logging

### Vercel Analytics

Enable in Vercel Dashboard:
```
Project > Analytics > Enable
```

### Error Tracking (Sentry)

```javascript
// sentry.client.config.js
import * as Sentry from '@sentry/nextjs';

Sentry.init({
  dsn: process.env.SENTRY_DSN,
  environment: process.env.NEXT_PUBLIC_APP_ENV,
  tracesSampleRate: 0.1,
});
```

### Custom Logging

```typescript
// lib/logging.ts
export const log = {
  info: (message: string, data?: object) => {
    if (process.env.NODE_ENV === 'production') {
      // Send to logging service
    }
    console.log(`[INFO] ${message}`, data);
  },
  error: (message: string, error?: Error) => {
    if (process.env.NODE_ENV === 'production') {
      Sentry.captureException(error);
    }
    console.error(`[ERROR] ${message}`, error);
  },
};
```

---

## Deployment Checklist

### Pre-Deployment

- [ ] All environment variables set in Vercel
- [ ] Database migrations applied to production Supabase
- [ ] RLS policies enabled and tested
- [ ] OAuth redirect URLs configured
- [ ] Email templates configured
- [ ] Custom domain DNS configured

### Post-Deployment

- [ ] Verify all pages load correctly
- [ ] Test authentication flow
- [ ] Test API endpoints
- [ ] Verify PWA installation
- [ ] Check security headers (securityheaders.com)
- [ ] Test on mobile devices
- [ ] Monitor error rates

### Rollback Procedure

1. **Identify Issue**
   ```
   Vercel Dashboard > Deployments > View logs
   ```

2. **Rollback**
   ```
   Vercel Dashboard > Deployments > Previous > Promote to Production
   ```

   Or via CLI:
   ```bash
   vercel rollback
   ```

3. **Fix and Redeploy**
   ```bash
   git revert <commit>
   git push origin main
   ```

---

## Common Issues

### Build Failures

| Issue | Cause | Solution |
|-------|-------|----------|
| TypeScript errors | Type mismatches | Fix types or enable `ignoreBuildErrors` |
| ESLint errors | Linting issues | Fix issues or enable `ignoreDuringBuilds` |
| Memory exceeded | Large build | Increase memory or split chunks |
| Timeout | Slow build | Check dependencies, use cache |

### Runtime Issues

| Issue | Cause | Solution |
|-------|-------|----------|
| 500 errors | Server error | Check Vercel function logs |
| Slow response | Cold starts | Enable Edge functions |
| CORS errors | Wrong origins | Update CORS configuration |
| Auth failures | Wrong redirect URLs | Update Supabase settings |

### Performance Issues

1. **Slow First Load**
   - Enable static generation
   - Optimize images
   - Reduce JavaScript bundle

2. **Slow API Responses**
   - Add caching headers
   - Optimize database queries
   - Use connection pooling

3. **High Bandwidth**
   - Enable compression
   - Optimize images
   - Review caching strategy

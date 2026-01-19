# EUONGELION Troubleshooting Guide

## Overview

This guide covers common issues encountered during development, deployment, and production of EUONGELION, along with their solutions.

---

## Quick Reference

| Issue | Quick Fix |
|-------|-----------|
| Build fails | `rm -rf .next && npm run build` |
| Node modules issues | `rm -rf node_modules && npm install` |
| TypeScript errors | `npm run type-check` |
| Port in use | `lsof -i :3333` then `kill -9 <PID>` |
| Supabase connection | Check `.env.local` credentials |
| Auth not working | Clear cookies, check redirect URLs |

---

## Build Errors

### Error: TypeScript Compilation Errors

**Symptoms:**
```
Type error: Property 'x' does not exist on type 'y'
```

**Solutions:**

1. **Run type check to see all errors:**
   ```bash
   npm run type-check
   ```

2. **For immediate fix (not recommended for production):**
   ```javascript
   // next.config.js
   typescript: {
     ignoreBuildErrors: true,
   }
   ```

3. **Fix the actual type error:**
   ```typescript
   // Before: missing type
   const data = response.json();

   // After: proper typing
   const data: ResponseType = await response.json();
   ```

---

### Error: ESLint Errors During Build

**Symptoms:**
```
ESLint error: 'x' is defined but never used
```

**Solutions:**

1. **Run lint to see all errors:**
   ```bash
   npm run lint
   ```

2. **Fix individual errors or disable rules:**
   ```typescript
   // Disable for line
   // eslint-disable-next-line @typescript-eslint/no-unused-vars
   const unusedVar = 'value';
   ```

3. **Ignore during build (temporary):**
   ```javascript
   // next.config.js
   eslint: {
     ignoreDuringBuilds: true,
   }
   ```

---

### Error: Module Not Found

**Symptoms:**
```
Module not found: Can't resolve '@/components/Something'
```

**Solutions:**

1. **Check path aliases in tsconfig.json:**
   ```json
   {
     "compilerOptions": {
       "paths": {
         "@/*": ["./*"]
       }
     }
   }
   ```

2. **Verify file exists at expected path**

3. **Check for case sensitivity:**
   ```bash
   # macOS is case-insensitive, Linux is case-sensitive
   # Ensure imports match exact file names
   ```

4. **Clear Next.js cache:**
   ```bash
   rm -rf .next
   npm run build
   ```

---

### Error: Out of Memory During Build

**Symptoms:**
```
FATAL ERROR: CALL_AND_RETRY_LAST Allocation failed - JavaScript heap out of memory
```

**Solutions:**

1. **Increase Node.js memory:**
   ```bash
   NODE_OPTIONS=--max-old-space-size=4096 npm run build
   ```

2. **Add to package.json:**
   ```json
   "scripts": {
     "build": "NODE_OPTIONS=--max-old-space-size=4096 next build"
   }
   ```

3. **Check for circular dependencies**

4. **Optimize large dependencies**

---

## Authentication Issues

### Issue: Login Not Working

**Symptoms:**
- Login form submits but nothing happens
- Redirects to login page repeatedly
- "Invalid credentials" error with correct password

**Diagnostic Steps:**

1. **Check browser console for errors**

2. **Verify Supabase credentials:**
   ```bash
   # In .env.local
   NEXT_PUBLIC_SUPABASE_URL=https://xxx.supabase.co
   NEXT_PUBLIC_SUPABASE_ANON_KEY=eyJhbG...
   ```

3. **Check network tab for API responses**

4. **Test Supabase connection:**
   ```typescript
   const supabase = createClient();
   const { data, error } = await supabase.auth.getUser();
   console.log('User:', data, 'Error:', error);
   ```

**Solutions:**

1. **Clear browser cookies and try again**

2. **Check Supabase Dashboard > Authentication > Users**

3. **Verify email confirmation is disabled (for development)**

4. **Check redirect URLs in Supabase:**
   ```
   Supabase Dashboard > Authentication > URL Configuration
   Site URL: http://localhost:3333
   Redirect URLs: http://localhost:3333/**
   ```

---

### Issue: OAuth Login Fails

**Symptoms:**
- Click "Sign in with Google" does nothing
- Redirects to error page
- "Invalid redirect URI" error

**Solutions:**

1. **Configure OAuth in Supabase:**
   ```
   Dashboard > Authentication > Providers > Google
   - Enable
   - Add Client ID and Secret from Google Cloud Console
   ```

2. **Add authorized redirect URIs in Google Console:**
   ```
   https://xxx.supabase.co/auth/v1/callback
   ```

3. **Update redirect URL in code:**
   ```typescript
   const { data, error } = await supabase.auth.signInWithOAuth({
     provider: 'google',
     options: {
       redirectTo: `${window.location.origin}/auth/callback`,
     },
   });
   ```

---

### Issue: Session Not Persisting

**Symptoms:**
- User logged out after page refresh
- Session expires unexpectedly
- Middleware not recognizing user

**Solutions:**

1. **Check middleware is running:**
   ```typescript
   // middleware.ts
   console.log('Middleware running');
   ```

2. **Verify cookies are being set:**
   ```
   Browser DevTools > Application > Cookies
   Look for: sb-xxx-auth-token
   ```

3. **Check cookie settings:**
   ```typescript
   // Ensure cookies are not blocked
   // Check SameSite and Secure settings
   ```

4. **Clear all auth cookies and re-login**

---

## Database Connection Issues

### Issue: Supabase Connection Failed

**Symptoms:**
```
Error: relation "users" does not exist
Error: PGRST116: permission denied for table users
```

**Solutions:**

1. **Verify environment variables:**
   ```bash
   echo $NEXT_PUBLIC_SUPABASE_URL
   echo $NEXT_PUBLIC_SUPABASE_ANON_KEY
   ```

2. **Check migrations have been applied:**
   ```bash
   supabase db remote commit
   # or
   supabase db push
   ```

3. **Verify RLS policies exist:**
   ```sql
   SELECT * FROM pg_policies WHERE tablename = 'users';
   ```

4. **Test connection directly:**
   ```typescript
   const { data, error } = await supabase
     .from('users')
     .select('*')
     .limit(1);
   console.log(data, error);
   ```

---

### Issue: RLS Blocking Valid Requests

**Symptoms:**
```
Error: new row violates row-level security policy
```

**Solutions:**

1. **Check you're authenticated:**
   ```typescript
   const { data: { user } } = await supabase.auth.getUser();
   console.log('Current user:', user);
   ```

2. **Verify policy conditions:**
   ```sql
   -- Check policies
   SELECT * FROM pg_policies WHERE tablename = 'your_table';

   -- Test policy condition
   SELECT auth.uid();
   ```

3. **Temporarily use service role (for debugging only):**
   ```typescript
   const supabase = createAdminClient(); // Bypasses RLS
   ```

4. **Fix RLS policy:**
   ```sql
   ALTER POLICY "policy_name" ON table_name
   USING (auth.uid() = user_id);
   ```

---

## PWA Issues

### Issue: PWA Not Installing

**Symptoms:**
- "Add to Home Screen" option not appearing
- Service worker not registering
- Manifest errors

**Solutions:**

1. **Check manifest.json is valid:**
   ```bash
   # Visit in browser:
   http://localhost:3333/manifest.json
   ```

2. **Verify required manifest fields:**
   ```json
   {
     "name": "EUONGELION",
     "short_name": "EUONGELION",
     "start_url": "/",
     "display": "standalone",
     "icons": [
       { "src": "/icon-192.png", "sizes": "192x192", "type": "image/png" },
       { "src": "/icon-512.png", "sizes": "512x512", "type": "image/png" }
     ]
   }
   ```

3. **Check service worker registration:**
   ```javascript
   // Browser console
   navigator.serviceWorker.ready.then(reg => console.log(reg));
   ```

4. **Ensure HTTPS in production:**
   - PWA requires HTTPS (except localhost)

---

### Issue: Offline Mode Not Working

**Symptoms:**
- App shows blank page offline
- API calls fail offline
- Cached content not loading

**Solutions:**

1. **Check service worker in DevTools:**
   ```
   DevTools > Application > Service Workers
   ```

2. **Verify caching strategies in next.config.js:**
   ```javascript
   runtimeCaching: [
     {
       urlPattern: /^https:\/\/your-api/,
       handler: 'NetworkFirst',
       options: {
         cacheName: 'api-cache',
         networkTimeoutSeconds: 10,
       },
     },
   ],
   ```

3. **Clear and reload service worker:**
   ```
   DevTools > Application > Service Workers > Unregister
   Then reload page
   ```

4. **Test offline mode:**
   ```
   DevTools > Network > Offline checkbox
   ```

---

## Performance Issues

### Issue: Slow Page Load

**Symptoms:**
- LCP > 2.5 seconds
- Large JavaScript bundles
- Slow Time to Interactive

**Diagnostic Steps:**

1. **Run Lighthouse audit:**
   ```
   DevTools > Lighthouse > Analyze page load
   ```

2. **Analyze bundle size:**
   ```bash
   npm run build
   # Check .next/analyze
   ```

**Solutions:**

1. **Use dynamic imports:**
   ```typescript
   const HeavyComponent = dynamic(
     () => import('@/components/HeavyComponent'),
     { loading: () => <Skeleton /> }
   );
   ```

2. **Optimize images:**
   ```typescript
   import Image from 'next/image';
   <Image src="/img.jpg" width={800} height={600} priority />
   ```

3. **Enable compression:**
   ```javascript
   // next.config.js
   compress: true,
   ```

4. **Add caching headers:**
   ```javascript
   async headers() {
     return [{
       source: '/:path*',
       headers: [{
         key: 'Cache-Control',
         value: 'public, max-age=31536000, immutable',
       }],
     }];
   }
   ```

---

### Issue: Memory Leaks

**Symptoms:**
- App slows down over time
- Browser tab crashes
- High memory usage in DevTools

**Solutions:**

1. **Check for cleanup in useEffect:**
   ```typescript
   useEffect(() => {
     const subscription = subscribe();
     return () => subscription.unsubscribe(); // Cleanup!
   }, []);
   ```

2. **Avoid creating objects in render:**
   ```typescript
   // Bad - creates new object each render
   <Component style={{ margin: 10 }} />

   // Good - memoize or define outside
   const style = useMemo(() => ({ margin: 10 }), []);
   <Component style={style} />
   ```

3. **Use React DevTools Profiler:**
   - Identify components re-rendering unnecessarily

---

## Development Server Issues

### Issue: Port 3333 Already in Use

**Symptoms:**
```
Error: listen EADDRINUSE: address already in use :::3333
```

**Solutions:**

1. **Find and kill process:**
   ```bash
   # macOS/Linux
   lsof -i :3333
   kill -9 <PID>

   # Windows
   netstat -ano | findstr :3333
   taskkill /PID <PID> /F
   ```

2. **Use different port:**
   ```bash
   npm run dev -- -p 3334
   ```

---

### Issue: Hot Reload Not Working

**Symptoms:**
- Changes don't appear in browser
- Need to manually refresh

**Solutions:**

1. **Check file watcher limit (Linux):**
   ```bash
   echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf
   sudo sysctl -p
   ```

2. **Clear Next.js cache:**
   ```bash
   rm -rf .next
   npm run dev
   ```

3. **Check for file system case sensitivity issues**

4. **Restart development server**

---

### Issue: Environment Variables Not Loading

**Symptoms:**
- `process.env.VARIABLE` is undefined
- Environment variables missing in browser

**Solutions:**

1. **Check file name:**
   - Must be `.env.local` for local development
   - Not `.env` (which is for defaults)

2. **Restart dev server after changes**

3. **For client-side access, prefix with NEXT_PUBLIC_:**
   ```env
   NEXT_PUBLIC_API_URL=https://api.example.com
   ```

4. **Verify file location (in app/ directory)**

---

## Production Issues

### Issue: 500 Errors in Production

**Symptoms:**
- Pages work locally but fail in production
- Vercel function logs show errors

**Diagnostic Steps:**

1. **Check Vercel function logs:**
   ```
   Vercel Dashboard > Project > Deployments > Functions tab
   ```

2. **Check for missing environment variables:**
   ```
   Vercel Dashboard > Project > Settings > Environment Variables
   ```

**Solutions:**

1. **Verify all env vars are set in Vercel**

2. **Check build vs runtime variables:**
   - Build time: Baked into code
   - Runtime: Available at request time

3. **Add error boundaries:**
   ```typescript
   'use client';

   class ErrorBoundary extends React.Component {
     state = { hasError: false };

     static getDerivedStateFromError(error) {
       return { hasError: true };
     }

     render() {
       if (this.state.hasError) {
         return <ErrorPage />;
       }
       return this.props.children;
     }
   }
   ```

---

### Issue: Function Timeout

**Symptoms:**
```
FUNCTION_INVOCATION_TIMEOUT
```

**Solutions:**

1. **Optimize slow queries:**
   ```typescript
   // Add indexes in SQL
   CREATE INDEX idx_devotionals_slug ON devotionals(slug);
   ```

2. **Add request timeout handling:**
   ```typescript
   const controller = new AbortController();
   const timeout = setTimeout(() => controller.abort(), 5000);

   try {
     const response = await fetch(url, { signal: controller.signal });
   } finally {
     clearTimeout(timeout);
   }
   ```

3. **Move heavy operations to background:**
   - Use Vercel Cron for scheduled tasks
   - Use Edge functions for fast responses

---

## Getting Help

### Resources

1. **Project Documentation**: `/tools/overnight-reports/documentation/`
2. **Next.js Docs**: https://nextjs.org/docs
3. **Supabase Docs**: https://supabase.com/docs
4. **Vercel Docs**: https://vercel.com/docs

### Debugging Checklist

- [ ] Check browser console for errors
- [ ] Check network tab for failed requests
- [ ] Verify environment variables
- [ ] Check Vercel/Supabase dashboards
- [ ] Review recent code changes
- [ ] Test in incognito mode
- [ ] Clear cache and cookies
- [ ] Restart development server
- [ ] Check documentation

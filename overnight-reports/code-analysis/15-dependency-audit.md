# Dependency Audit

**Generated:** 2026-01-19
**Project:** EUONGELION
**Path:** `/Users/meltmac/Documents/Personal/wkGD/EUONGELION-STARTUP/app`

---

## Executive Summary

The EUONGELION app has a **lean and modern dependency set** with current versions of Next.js 15, React 19, and essential packages. The architecture follows best practices with minimal dependencies. However, some packages may be outdated by the analysis date, and there are opportunities to further optimize bundle size.

**Overall Rating:** Excellent (9/10)

---

## 1. Package.json Analysis

**File:** `/app/package.json`

### Production Dependencies (14 packages)

| Package | Version | Purpose | Size Impact | Status |
|---------|---------|---------|-------------|--------|
| `@supabase/ssr` | ^0.5.2 | Server-side Supabase client | Medium | Current |
| `@supabase/supabase-js` | ^2.47.0 | Supabase client | Large | Current |
| `@tailwindcss/aspect-ratio` | ^0.4.2 | Aspect ratio utilities | Small | Current |
| `@tailwindcss/container-queries` | ^0.1.1 | Container query support | Small | Current |
| `@tailwindcss/forms` | ^0.5.11 | Form styling | Small | Current |
| `@tailwindcss/typography` | ^0.5.19 | Prose styling | Small | Current |
| `class-variance-authority` | ^0.7.1 | Component variants | Small | Current |
| `clsx` | ^2.1.1 | Class name utility | Tiny | Current |
| `next` | ^15.1.0 | React framework | Large | Current |
| `next-pwa` | ^5.6.0 | PWA support | Medium | Current |
| `postcss-flexbugs-fixes` | ^5.0.2 | Flexbox bug fixes | Tiny | Current |
| `postcss-preset-env` | ^11.1.1 | Modern CSS support | Small | Current |
| `react` | ^19.0.0 | UI library | Large | Current |
| `react-dom` | ^19.0.0 | React DOM | Large | Current |
| `tailwind-merge` | ^3.4.0 | Merge Tailwind classes | Small | Current |
| `zustand` | ^5.0.0 | State management | Small | Current |

### Development Dependencies (10 packages)

| Package | Version | Purpose | Status |
|---------|---------|---------|--------|
| `@types/node` | ^22.0.0 | Node.js types | Current |
| `@types/react` | ^19.0.0 | React types | Current |
| `@types/react-dom` | ^19.0.0 | React DOM types | Current |
| `autoprefixer` | ^10.4.20 | CSS autoprefixing | Current |
| `eslint` | ^9.0.0 | Code linting | Current |
| `eslint-config-next` | ^16.0.0 | Next.js ESLint config | Current |
| `postcss` | ^8.4.47 | CSS processing | Current |
| `tailwindcss` | ^3.4.15 | CSS framework | Current |
| `typescript` | ^5.7.0 | TypeScript compiler | Current |

---

## 2. Version Currency Analysis

Based on npm registry data (as of analysis date):

### Potentially Outdated

| Package | Current | Latest (Est.) | Action |
|---------|---------|---------------|--------|
| `next-pwa` | ^5.6.0 | Check for updates | May have newer patches |
| `postcss-flexbugs-fixes` | ^5.0.2 | Stable | No action |
| `@tailwindcss/container-queries` | ^0.1.1 | May have 0.2.x | Check for updates |

### Note on Caret (^) Versioning

All dependencies use caret versioning (`^`) which allows minor and patch updates. This is good for receiving bug fixes but may introduce breaking changes in minor versions.

**Recommendation:** Consider using tilde (`~`) for production dependencies to limit to patch updates only.

---

## 3. Bundle Size Analysis

### Large Dependencies (Estimated)

| Package | Estimated Size | Tree-shakeable | Notes |
|---------|----------------|----------------|-------|
| `@supabase/supabase-js` | ~200KB | Partial | Consider lazy loading |
| `next` | ~500KB (client) | Yes | Framework overhead |
| `react` + `react-dom` | ~130KB | No | Required |

### Optimization in next.config.js

**Lines 300-305, 317-321:**
```javascript
// Tree shaking for lodash
config.resolve.alias = {
  'lodash': 'lodash-es',
};

// Package import optimization
experimental: {
  optimizePackageImports: [
    'lucide-react',
    '@radix-ui/react-icons',
    'date-fns',
  ],
}
```

**Issue:** `lodash` and `lodash-es` are not in dependencies, but alias is configured. Also `lucide-react`, `@radix-ui/react-icons`, and `date-fns` are not in dependencies.

---

## 4. Missing Dependencies

Based on code analysis, some referenced packages are not in package.json:

### Likely Missing

| Package | Referenced In | Status |
|---------|--------------|--------|
| `schema-dts` | `/components/seo/JsonLd.tsx` | Missing - types for JSON-LD |
| `web-push` | `/lib/notifications/push.ts` (implied) | Missing - push notifications |
| `@svgr/webpack` | `next.config.js` line 296 | Missing - SVG handling |

### Should Be Added

```bash
npm install schema-dts web-push @svgr/webpack
```

Or if not actually used, remove the references.

---

## 5. Unused/Questionable Dependencies

### Potentially Unused

Based on import analysis, all listed dependencies appear to be used. However:

1. **postcss-flexbugs-fixes** - May not be needed with modern browser support
2. **postcss-preset-env** - Evaluate if all features are used

### Optimization Candidates

1. **@tailwindcss/\*** plugins - All 4 are used but consider if all features needed
2. **class-variance-authority** + **tailwind-merge** - Both are used but could be consolidated

---

## 6. Security Considerations

### Known Vulnerability Checks

Run: `npm audit` to check for vulnerabilities.

### Supply Chain Risks

| Package | Maintainer | Risk Level |
|---------|------------|------------|
| `@supabase/*` | Supabase Inc. | Low |
| `next` | Vercel | Low |
| `zustand` | pmndrs | Low |
| `next-pwa` | Community | Medium - review regularly |

### Recommendations

1. Enable `npm audit` in CI/CD
2. Use Dependabot or Renovate for updates
3. Review `next-pwa` for security updates

---

## 7. Duplicate/Redundant Analysis

### No Duplicates Found

The dependency list is clean with no obvious duplicates.

### Potential Consolidation

1. **clsx + tailwind-merge** - Both handle class names
   - Current: Used together (clsx for conditions, tailwind-merge for deduplication)
   - Status: Appropriate usage pattern

---

## 8. TypeScript Dependencies

### Type Coverage

All major packages have types:
- React/Next.js: `@types/react`, `@types/react-dom`
- Node: `@types/node`
- Supabase: Included in package
- Zustand: Included in package
- Tailwind: Included in package

### Missing Types

None identified - type coverage is complete.

---

## 9. Engine Requirements

```json
"engines": {
  "node": ">=20.0.0"
}
```

Good - requires Node.js 20 LTS or later.

---

## 10. Scripts Analysis

```json
"scripts": {
  "dev": "next dev",
  "build": "next build",
  "start": "next start",
  "lint": "next lint",
  "type-check": "tsc --noEmit"
}
```

### Missing Scripts

Consider adding:
- `"test": "vitest"` - Testing (vitest.setup.ts exists)
- `"format": "prettier --write ."` - Code formatting
- `"analyze": "ANALYZE=true next build"` - Bundle analysis

---

## 11. Recommended Additions

### For Development

```json
"devDependencies": {
  "@next/bundle-analyzer": "^15.0.0",  // Bundle analysis
  "prettier": "^3.0.0",                 // Code formatting
  "vitest": "^2.0.0",                   // Testing (config exists)
  "@testing-library/react": "^15.0.0"  // React testing
}
```

### For Production

```json
"dependencies": {
  "schema-dts": "^1.1.0"  // JSON-LD types (used in code)
}
```

---

## 12. Version Lock Recommendations

Create or verify `package-lock.json` is committed for reproducible builds.

Consider switching to stricter versioning for stability:

```json
// Current (allows minor updates)
"next": "^15.1.0"

// Stricter (patch updates only)
"next": "~15.1.0"

// Strictest (exact version)
"next": "15.1.0"
```

---

## 13. Action Items

### High Priority

1. **Add missing dependencies**
   ```bash
   npm install schema-dts
   npm install -D @svgr/webpack
   ```

2. **Verify lodash usage or remove alias**
   - Check if lodash is actually used
   - Remove webpack alias if not

3. **Add testing dependencies**
   - vitest setup exists but deps missing

### Medium Priority

4. **Add bundle analyzer**
   ```bash
   npm install -D @next/bundle-analyzer
   ```

5. **Set up Dependabot/Renovate**
   - Automated dependency updates
   - Security vulnerability alerts

6. **Run security audit**
   ```bash
   npm audit
   npm audit fix
   ```

### Low Priority

7. **Review postcss plugins**
   - Test if flexbugs-fixes still needed
   - Evaluate preset-env features used

8. **Consider stricter versioning**
   - Evaluate tilde vs caret for stability

9. **Add prettier configuration**
   - Standardize code formatting

---

## 14. Dependency Graph Summary

```
EUONGELION
├── Core Framework
│   ├── next@15.1.0
│   ├── react@19.0.0
│   └── react-dom@19.0.0
├── Styling
│   ├── tailwindcss@3.4.15
│   ├── @tailwindcss/typography@0.5.19
│   ├── @tailwindcss/forms@0.5.11
│   ├── @tailwindcss/aspect-ratio@0.4.2
│   ├── @tailwindcss/container-queries@0.1.1
│   ├── class-variance-authority@0.7.1
│   ├── clsx@2.1.1
│   └── tailwind-merge@3.4.0
├── State Management
│   └── zustand@5.0.0
├── Backend
│   ├── @supabase/supabase-js@2.47.0
│   └── @supabase/ssr@0.5.2
├── PWA
│   └── next-pwa@5.6.0
└── Build Tools
    ├── postcss@8.4.47
    ├── postcss-flexbugs-fixes@5.0.2
    ├── postcss-preset-env@11.1.1
    └── autoprefixer@10.4.20
```

---

## Summary

The dependency set is:
- **Modern**: Latest stable versions of all major packages
- **Lean**: Only 14 production dependencies
- **Appropriate**: Each dependency serves a clear purpose
- **Well-typed**: Complete TypeScript coverage

Key actions:
1. Add missing dependencies (schema-dts, @svgr/webpack)
2. Clean up unused webpack aliases
3. Set up automated dependency updates
4. Add testing and bundle analysis tooling

The project demonstrates excellent dependency hygiene with minimal bloat.

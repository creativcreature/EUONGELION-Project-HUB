# EUONGELION Local Development Guide

## Overview

This guide walks you through setting up EUONGELION for local development, from cloning the repository to running the application.

---

## Prerequisites

### Required Software

| Software | Version | Purpose |
|----------|---------|---------|
| Node.js | >= 20.0.0 | JavaScript runtime |
| npm | >= 9.0.0 | Package manager |
| Git | Latest | Version control |

### Optional Software

| Software | Purpose |
|----------|---------|
| VS Code | Recommended IDE |
| Docker | Running local Supabase |
| Supabase CLI | Database migrations |

### System Requirements

- **OS**: macOS, Linux, or Windows (WSL recommended)
- **RAM**: 8GB minimum, 16GB recommended
- **Disk**: 2GB free space

---

## Quick Start

```bash
# 1. Clone the repository
git clone https://github.com/your-org/euongelion.git
cd euongelion

# 2. Navigate to the app directory
cd app

# 3. Install dependencies
npm install

# 4. Copy environment file
cp .env.example .env.local

# 5. Configure environment variables (see below)

# 6. Start development server
npm run dev

# 7. Open browser
open http://localhost:3333
```

---

## Detailed Setup

### Step 1: Clone Repository

```bash
# Using HTTPS
git clone https://github.com/your-org/euongelion.git

# Using SSH (recommended)
git clone git@github.com:your-org/euongelion.git

# Navigate to project
cd euongelion
```

### Step 2: Understand Project Structure

```
euongelion/
├── app/                    # Next.js application
│   ├── api/               # API routes
│   ├── components/        # React components
│   ├── lib/               # Utility libraries
│   ├── src/               # Source files
│   │   ├── app/          # App router pages
│   │   └── components/   # Page components
│   ├── stores/           # Zustand stores
│   ├── types/            # TypeScript definitions
│   ├── package.json      # Dependencies
│   └── .env.example      # Environment template
├── content/               # Devotional content
│   ├── reference/        # Reference materials
│   └── drafts/           # Draft content
├── database/              # Database files
│   └── migrations/       # SQL migrations
├── supabase/             # Supabase configuration
│   └── migrations/       # Supabase migrations
└── tools/                # Development tools
    ├── project-hub.html  # Project dashboard
    └── overnight-reports/# Documentation
```

### Step 3: Install Dependencies

```bash
cd app
npm install
```

This installs:
- Next.js 15
- React 19
- Supabase client libraries
- Tailwind CSS
- Zustand
- TypeScript
- And other dependencies

### Step 4: Configure Environment

Copy the example environment file:
```bash
cp .env.example .env.local
```

Edit `.env.local` with your values:

```env
# Application
NEXT_PUBLIC_APP_NAME=EUONGELION
NEXT_PUBLIC_APP_URL=http://localhost:3333
NEXT_PUBLIC_APP_ENV=development
NODE_ENV=development

# Supabase (Required)
NEXT_PUBLIC_SUPABASE_URL=https://your-project.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key
SUPABASE_SERVICE_ROLE_KEY=your-service-role-key

# Development Settings
DEBUG=true
LOG_LEVEL=debug
```

#### Getting Supabase Credentials

1. Go to [supabase.com](https://supabase.com)
2. Create a free account
3. Create a new project
4. Go to Settings > API
5. Copy:
   - Project URL -> `NEXT_PUBLIC_SUPABASE_URL`
   - anon public key -> `NEXT_PUBLIC_SUPABASE_ANON_KEY`
   - service_role key -> `SUPABASE_SERVICE_ROLE_KEY`

### Step 5: Set Up Database

#### Option A: Use Supabase Cloud (Recommended for beginners)

1. Create a Supabase project (if not already done)
2. Run migrations:
   ```bash
   # Install Supabase CLI
   npm install -g supabase

   # Link to your project
   supabase link --project-ref your-project-ref

   # Push migrations
   supabase db push
   ```

#### Option B: Run Local Supabase (Advanced)

```bash
# Start local Supabase
supabase start

# This will output local credentials
# Update .env.local with local URLs

# Apply migrations
supabase db reset
```

### Step 6: Start Development Server

```bash
npm run dev
```

**Important**: EUONGELION runs on **port 3333** (ports 3000-3005 are occupied).

Open [http://localhost:3333](http://localhost:3333) in your browser.

---

## Available Scripts

| Command | Description |
|---------|-------------|
| `npm run dev` | Start development server |
| `npm run build` | Build for production |
| `npm run start` | Start production server |
| `npm run lint` | Run ESLint |
| `npm run type-check` | Run TypeScript compiler |

---

## IDE Setup

### VS Code (Recommended)

#### Extensions

Install these extensions for the best experience:

1. **ES7+ React/Redux/React-Native snippets**
2. **Tailwind CSS IntelliSense**
3. **Prettier - Code formatter**
4. **ESLint**
5. **TypeScript Importer**
6. **Auto Rename Tag**
7. **Error Lens**

#### Settings

Create `.vscode/settings.json`:

```json
{
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": "explicit"
  },
  "typescript.tsdk": "node_modules/typescript/lib",
  "tailwindCSS.experimental.classRegex": [
    ["cva\\(([^)]*)\\)", "[\"'`]([^\"'`]*).*?[\"'`]"],
    ["cn\\(([^)]*)\\)", "(?:'|\"|`)([^']*)(?:'|\"|`)"]
  ],
  "files.associations": {
    "*.css": "tailwindcss"
  }
}
```

---

## Development Workflow

### 1. Create Feature Branch

```bash
git checkout -b feature/your-feature-name
```

### 2. Make Changes

Edit files in `/app/src/` and `/app/components/`.

### 3. Test Locally

```bash
# Run development server
npm run dev

# Check for TypeScript errors
npm run type-check

# Check for linting errors
npm run lint
```

### 4. Commit Changes

```bash
git add .
git commit -m "feat: add your feature description"
```

Follow conventional commits:
- `feat:` - New feature
- `fix:` - Bug fix
- `docs:` - Documentation
- `style:` - Formatting
- `refactor:` - Code refactoring
- `test:` - Tests
- `chore:` - Maintenance

### 5. Push and Create PR

```bash
git push origin feature/your-feature-name
```

Then create a pull request on GitHub.

---

## Testing

### Running Tests

```bash
# Run all tests
npm test

# Run with coverage
npm run test:coverage

# Run in watch mode
npm run test:watch
```

### Manual Testing Checklist

- [ ] Test on mobile viewport (Chrome DevTools)
- [ ] Test with slow network (DevTools throttling)
- [ ] Test with no network (offline mode)
- [ ] Test dark/light theme
- [ ] Test with different user roles

---

## Debugging

### Browser DevTools

1. Open Chrome DevTools (F12)
2. Use React DevTools extension
3. Check Network tab for API calls
4. Check Console for errors

### VS Code Debugging

Create `.vscode/launch.json`:

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Next.js: debug server-side",
      "type": "node-terminal",
      "request": "launch",
      "command": "npm run dev"
    },
    {
      "name": "Next.js: debug client-side",
      "type": "chrome",
      "request": "launch",
      "url": "http://localhost:3333"
    }
  ]
}
```

### Common Debug Commands

```typescript
// Log state
console.log(JSON.stringify(state, null, 2));

// Debug API response
console.log('API Response:', await response.json());

// Check authentication
const { data: { user } } = await supabase.auth.getUser();
console.log('Current user:', user);
```

---

## Environment-Specific Notes

### macOS

```bash
# If you get permission errors
sudo chown -R $(whoami) ~/.npm

# If node-gyp fails
xcode-select --install
```

### Windows (WSL)

```bash
# Ensure WSL2 is installed
wsl --install

# Run all commands in WSL terminal
```

### Linux

```bash
# If you get ENOSPC error
echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf
sudo sysctl -p
```

---

## Troubleshooting

### Port Already in Use

```bash
# Find process using port 3333
lsof -i :3333

# Kill process
kill -9 <PID>
```

### Node Modules Issues

```bash
# Clear node_modules and reinstall
rm -rf node_modules
rm package-lock.json
npm install
```

### TypeScript Errors

```bash
# Check for type errors
npm run type-check

# Restart TypeScript server in VS Code
Cmd+Shift+P > "TypeScript: Restart TS Server"
```

### Supabase Connection Issues

1. Check `.env.local` values are correct
2. Verify Supabase project is running
3. Check network connectivity
4. Verify RLS policies allow access

### Hot Reload Not Working

```bash
# Restart development server
Ctrl+C
npm run dev

# Clear Next.js cache
rm -rf .next
npm run dev
```

---

## Quick Reference

### File Locations

| What | Where |
|------|-------|
| Pages | `/app/src/app/` |
| Components | `/app/components/` |
| API Routes | `/app/api/` |
| Stores | `/app/stores/` |
| Types | `/app/types/` |
| Styles | `/app/src/app/globals.css` |
| Config | `/app/tailwind.config.ts` |

### Key Files

| File | Purpose |
|------|---------|
| `package.json` | Dependencies and scripts |
| `next.config.js` | Next.js configuration |
| `tailwind.config.ts` | Tailwind configuration |
| `tsconfig.json` | TypeScript configuration |
| `.env.local` | Environment variables |

### Useful Commands

```bash
# Development
npm run dev           # Start dev server
npm run build         # Build for production
npm run lint          # Run linter
npm run type-check    # Check types

# Git
git status            # Check status
git pull              # Pull latest
git push              # Push changes

# Supabase
supabase status       # Check status
supabase db reset     # Reset database
supabase gen types    # Generate types
```

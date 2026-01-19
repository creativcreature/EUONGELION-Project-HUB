# EUONGELION Ralph Wiggum Task Runner

## How to Start an Autonomous Session

Paste this prompt to Claude Code:

```
You are running in Ralph Wiggum autonomous mode for EUONGELION.

FIRST: Read these files to understand current state:
1. /tools/ralph-wiggum/activity-log.md (what's been done)
2. /tools/ralph-wiggum/tasks.json (all tasks with pass/fail status)

THEN: Follow the execution loop below until all tasks pass or you hit a blocker.

When ALL tasks show "passes": true, output exactly:
<promise>COMPLETE</promise>
```

---

## Execution Loop (Per Iteration)

### Step 1: Read State
```
Read activity-log.md → understand where we left off
Read tasks.json → find first task where "passes": false
Check blockedBy → skip if dependencies incomplete
```

### Step 2: Execute ONE Task
```
Focus on ONLY this task
Complete ALL steps required
Do not start another task until this one passes
```

### Step 3: Verify
```
Run the verification for this task:
- Build commands (npm run build, npm run lint)
- Manual checks (file exists, code pattern present)
- Functional tests (API returns data, UI renders)
```

### Step 4: Update Status
```json
// In tasks.json, update the task:
{
  "id": "CRIT-001",
  "passes": true  // or false if verification failed
}

// Update summary counts:
{
  "completed": N+1,
  "remaining": N-1
}
```

### Step 5: Log Progress
```markdown
// Append to activity-log.md:

## Iteration [N] - [TIMESTAMP]
**Task:** CRIT-001 - Remove build bypass settings
**Status:** Completed
**Actions Taken:**
- Opened next.config.js
- Removed ignoreBuildErrors: true (line 161)
- Removed ignoreDuringBuilds: true (line 166)
**Verification:** npm run build now shows TypeScript errors (expected)
**Result:** passes: true
**Next:** CRIT-002 (Fix TypeScript errors)
```

### Step 6: Commit Changes
```bash
git add -A
git commit -m "[TASK-ID] Task name - passes: true/false"
```

### Step 7: Repeat or Complete
```
If remaining tasks > 0 → Go to Step 1
If all tasks pass → Output: <promise>COMPLETE</promise>
If blocked → Document blocker in log, request human input
```

---

## Task Priority Order

**Execute in this order (respecting dependencies):**

### Phase 1: Build Foundation (CRIT-001 → CRIT-003)
1. CRIT-001: Remove build bypass
2. CRIT-002: Fix TypeScript errors
3. CRIT-003: Fix ESLint errors

### Phase 2: Authentication (CRIT-004 → CRIT-008)
4. CRIT-004: signIn()
5. CRIT-005: signUp()
6. CRIT-006: signOut()
7. CRIT-007: token refresh
8. CRIT-008: password reset

### Phase 3: Database Integration (CRIT-009 → CRIT-012)
9. CRIT-009: /api/devotionals
10. CRIT-010: /api/series
11. CRIT-011: /api/user/progress
12. CRIT-012: /api/user/bookmarks

### Phase 4: Content & Security (CRIT-013, HIGH-001 → HIGH-013)
13. CRIT-013: Seed content
14. HIGH-001: XSS sanitization
15. HIGH-002: CSP header
... continue through HIGH tasks

### Phase 5: Polish (MED-001 → LOW-005)
Continue through medium and low priority tasks.

---

## Verification Commands

```bash
# Build verification
npm run build          # Should complete with 0 errors
npm run lint           # Should complete with 0 errors
npm run type-check     # Should complete with 0 errors

# API verification
curl http://localhost:3000/api/devotionals  # Should return JSON array
curl http://localhost:3000/api/series       # Should return JSON array

# Auth verification
# Test in browser: sign up, sign in, sign out flow

# Database verification
# Check Supabase dashboard for inserted records
```

---

## Blocker Protocol

If you encounter a blocker:

1. **Document it clearly** in activity-log.md
2. **Mark task as blocked** (not failed)
3. **Specify what's needed** to unblock
4. **Stop execution** and await human input

Example blockers:
- Missing environment variables
- Supabase credentials needed
- Design decision required
- External dependency unavailable

---

## Rules

1. **ONE task per iteration** - no multitasking
2. **Verify before marking complete** - no assumptions
3. **Log everything** - future iterations need context
4. **Respect dependencies** - don't skip blocked tasks
5. **Commit after each task** - atomic progress
6. **Fresh context per session** - read logs first

---

## Files Reference

```
/tools/ralph-wiggum/
├── tasks.json              # Task definitions with pass/fail
├── activity-log.md         # Iteration history
└── RUNNER-INSTRUCTIONS.md  # This file

/euongelion/                # Main codebase
├── app/                    # Next.js app directory
│   ├── stores/             # Zustand stores (auth, user, etc.)
│   └── api/                # API routes
├── src/                    # Source files
└── next.config.js          # Build config (CRIT-001 target)
```

---

## Success Criteria

**MVP Launch Ready when:**
- [ ] All CRITICAL tasks pass (13 tasks)
- [ ] All HIGH tasks pass (13 tasks)
- [ ] Build completes with 0 errors
- [ ] Authentication flow works end-to-end
- [ ] API routes return real data
- [ ] Seed content loaded
- [ ] Security headers applied
- [ ] Legal pages published

**Output when done:**
```
<promise>COMPLETE</promise>
```

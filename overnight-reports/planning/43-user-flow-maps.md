# EUONGELION User Flow Maps

**Purpose:** Document every user path through the application
**Last Updated:** 2026-01-19
**Version:** 1.0

---

## Flow Diagram Legend

```
[Page/Screen]     = Page or major screen
(Decision)        = User decision point
{Action}          = User action
->                = Navigation flow
=>                = Conditional flow
|                 = Alternative path
...               = Flow continues
```

---

## 1. NEW USER ONBOARDING

### 1.1 First Visit - Anonymous User

```
[Landing/Home Page]
    |
    v
(User sees app for first time)
    |
    +---> {Browse devotionals} -> [Devotional List/Cards]
    |                                    |
    |                                    v
    |                             [Read Devotional]
    |                                    |
    |                                    v
    |                             {Attempt to bookmark}
    |                                    |
    |                                    v
    |                             [Sign Up Prompt]
    |                                    |
    +---> {Take Soul Audit} -----------+
    |                                   |
    |                                   v
    |                             [Soul Audit Page]
    |                                   |
    |                                   v
    |                             {Enter response}
    |                                   |
    |                                   v
    |                             [Results/Recommendations]
    |                                   |
    |                                   v
    |                             {Click recommended content}
    |                                   |
    |                                   v
    |                             [Devotional Page]
    |
    +---> {Sign Up} -> [Flow 1.2]
    |
    +---> {Install PWA} -> [PWA Install Prompt] -> {Confirm} -> [Home Screen Icon]
```

### 1.2 Sign Up Flow

```
[Any Page] -> {Click Sign Up}
    |
    v
[Sign Up Page]
    |
    v
{Enter email address}
    |
    v
{Enter password}
    |
    v
{Click "Create Account"}
    |
    +---> (Validation Error?) --Yes--> [Error Message] -> {Fix input}
    |
    +---> (Success?)
          |
          +--> Yes --> [Email Verification Sent]
          |                   |
          |                   v
          |            {Open email}
          |                   |
          |                   v
          |            {Click verification link}
          |                   |
          |                   v
          |            [Account Verified]
          |                   |
          |                   v
          |            [Home Page - Logged In]
          |                   |
          |                   v
          |            (Previous Soul Audit?)
          |                   |
          |                   +--Yes--> [Personalized Home]
          |                   |
          |                   +--No---> [Prompt: Take Soul Audit?]
          |
          +--> No --> [Error Message] -> {Retry or get help}
```

### 1.3 First Devotional Experience (New User)

```
[Home Page]
    |
    v
{Scroll to featured/first devotional}
    |
    v
{Tap devotional card}
    |
    v
[Devotional Page]
    |
    +---> {Read title}
    |
    +---> {Read Scripture reference}
    |
    +---> {Read Scripture text}
    |
    +---> {Read devotional body}
    |
    +---> {Read reflection questions}
    |
    v
(Reached end of content)
    |
    +---> {Tap "Next" in series} -> [Next Devotional]
    |
    +---> {Tap "Share"} -> [Share Options]
    |                           |
    |                           +---> {Native Share}
    |                           +---> {Copy Link}
    |                           +---> {Share to Twitter}
    |                           +---> {Share to Facebook}
    |
    +---> {Tap "Bookmark"} -> (Logged in?)
    |                              |
    |                              +-Yes-> [Bookmarked!]
    |                              |
    |                              +-No--> [Sign Up Prompt]
    |
    +---> {Navigate back} -> [Previous Page]
```

---

## 2. RETURNING USER FLOWS

### 2.1 Returning User - Continue Reading

```
[App Launch/Open]
    |
    v
(Logged in?)
    |
    +-No--> [Home Page - Guest] -> {Sign In}
    |
    +-Yes-> [Home Page - Personalized]
                 |
                 v
           (Has reading progress?)
                 |
                 +-No--> [Show recommendations based on Soul Audit]
                 |
                 +-Yes-> [Show "Continue Reading" section]
                              |
                              v
                        {Tap "Continue" on in-progress series}
                              |
                              v
                        [Next unread devotional in series]
                              |
                              v
                        {Read devotional}
                              |
                              v
                        (Series complete?)
                              |
                              +-No--> {Tap "Next"} -> [Next Devotional]
                              |
                              +-Yes-> [Series Complete Celebration]
                                           |
                                           v
                                     {View next series recommendation}
```

### 2.2 Returning User - Check Bookmarks

```
[Home Page]
    |
    v
{Navigate to Bookmarks}
    |
    v
[Bookmarks Page]
    |
    v
(Has bookmarks?)
    |
    +-No--> [Empty State: "No bookmarks yet"]
    |              |
    |              v
    |        {Tap "Browse Devotionals"}
    |              |
    |              v
    |        [Devotional List]
    |
    +-Yes-> [List of bookmarked devotionals]
                 |
                 v
           {Tap any bookmark}
                 |
                 v
           [Devotional Page]
                 |
                 +---> {Remove bookmark} -> [Confirmation] -> [Updated Bookmarks]
                 |
                 +---> {Read and return} -> [Bookmarks Page]
```

### 2.3 Returning User - Browse Series

```
[Home Page]
    |
    v
{Navigate to Series}
    |
    v
[Series Listing Page]
    |
    v
{Browse available series}
    |
    v
(Filter/sort available?)
    |
    +-Yes-> {Apply filter} -> [Filtered Series List]
    |
    v
{Select a series}
    |
    v
[Series Detail Page]
    |
    +---> {View series description}
    |
    +---> {See progress: "X of Y complete"}
    |
    +---> {View devotional list}
    |
    v
{Select devotional to read}
    |
    v
[Devotional Page]
    |
    v
(Reading from series context)
    |
    +---> {Back to series} -> [Series Detail Page]
    |
    +---> {Next in series} -> [Next Devotional]
```

---

## 3. SOUL AUDIT FLOWS

### 3.1 Complete Soul Audit - Standard Path

```
[Home Page or Navigation]
    |
    v
{Tap "Soul Audit" or "Take Assessment"}
    |
    v
[Soul Audit Welcome/Intro]
    |
    v
{Tap "Begin" or "Start"}
    |
    v
[Soul Audit Question Page]
    |
    +---> Question: "What are you wrestling with?"
    |
    +---> Supporting copy displayed
    |
    v
{Type response in text area}
    |
    v
(Character count check)
    |
    +--> 0 chars: [Blocked - "Please share something"]
    |
    +--> 1-9 chars: [Nudge - "Would you like to share more?"]
    |                    |
    |                    +---> {Continue anyway} -> [Processing]
    |                    +---> {Add more text} -> {Continue typing}
    |
    +--> 10+ chars: {Tap "Continue"} -> [Processing]
                         |
                         v
                   [Processing Indicator]
                   "Finding the right words for you..."
                         |
                         v
                   (Confidence level?)
                         |
                         +--> High (>70%): [Results Page - Direct Match]
                         |
                         +--> Low (<70%): [Clarifying Options Page]
                                               |
                                               v
                                         {Select clarifying option}
                                               |
                                               v
                                         [Results Page]
```

### 3.2 Soul Audit Results and Follow-Through

```
[Soul Audit Results Page]
    |
    +---> Primary category displayed
    |     (e.g., "Rest & Renewal")
    |
    +---> Scripture theme shown
    |     (e.g., Matthew 11:28)
    |
    +---> Description of the category
    |
    +---> Recommended series/devotionals
    |
    v
{User reviews recommendations}
    |
    +---> {Tap recommended series} -> [Series Detail]
    |                                      |
    |                                      v
    |                                 {Start reading}
    |
    +---> {Tap recommended devotional} -> [Devotional Page]
    |
    +---> {Browse all in category} -> [Category Browse Page]
    |
    +---> {Retake Soul Audit} -> [Flow 3.1]
    |
    +---> {Return home} -> [Home Page - Updated recommendations]
```

### 3.3 Soul Audit - Crisis Path

```
[Soul Audit Question Page]
    |
    v
{User types crisis-indicating content}
(Contains: "don't want to live", "end my life", etc.)
    |
    v
{Tap "Continue"}
    |
    v
[Crisis Detection Triggered]
    |
    v
[Crisis Response Screen]
    |
    +---> "We hear you."
    |
    +---> "What you're carrying sounds incredibly heavy..."
    |
    +---> [Crisis Resources Box]
    |          |
    |          +---> 988 Suicide Prevention Lifeline
    |          |     {Tap to call}
    |          |
    |          +---> Crisis Text Line (741741)
    |          |     {Tap to text}
    |          |
    |          +---> National Domestic Violence Hotline
    |                {Tap to call}
    |
    +---> "God sees you. He hasn't forgotten you."
    |
    +---> {When ready to continue}
    |          |
    |          v
    |     [Gentle content recommendations]
    |     (Comfort-focused, hope-themed)
    |
    +---> {Request prayer} -> [Prayer Request Form]
```

### 3.4 Retake Soul Audit (Existing User)

```
[Profile or Settings]
    |
    v
{Tap "Retake Soul Audit"}
    |
    v
[Confirmation: "Take new assessment?"]
    |
    v
{Confirm}
    |
    v
[Soul Audit Question Page]
    |
    v
(Previous response shown for reference? - Design decision)
    |
    v
{Enter new response}
    |
    v
[Flow continues as 3.1]
    |
    v
[New Results]
    |
    +---> (Comparison to previous available?)
    |          |
    |          +-Yes-> [Show journey/progress]
    |
    +---> [New recommendations saved]
```

---

## 4. READING & PROGRESS FLOWS

### 4.1 Complete a Series

```
[Series with 1 devotional remaining]
    |
    v
{Read final devotional}
    |
    v
(Reached end of content)
    |
    v
{Mark as complete / Auto-complete on scroll}
    |
    v
[Series Completion Celebration]
    |
    +---> Congratulations message
    |
    +---> Progress stats shown
    |     (e.g., "7 devotionals in X days")
    |
    +---> Milestone awarded (if applicable)
    |
    +---> Suggested next series
    |
    v
{Choose next action}
    |
    +---> {Start suggested series} -> [New Series First Devotional]
    |
    +---> {Browse other series} -> [Series Listing]
    |
    +---> {Return home} -> [Home Page]
```

### 4.2 Reading Streak Flow

```
[Daily App Open]
    |
    v
(Has user read today?)
    |
    +-Yes-> [Streak maintained] -> (Streak milestone?)
    |                                   |
    |                                   +-Yes-> [Celebration/Badge]
    |                                   |
    |                                   +-No--> [Normal home]
    |
    +-No--> [Show: "Continue your streak!"]
                 |
                 v
           {Tap to read}
                 |
                 v
           [Today's devotional or Continue series]
                 |
                 v
           {Complete reading}
                 |
                 v
           [Streak counter increments]
                 |
                 v
           (New streak milestone?)
                 |
                 +-7 days-> [Week Streak Badge]
                 |
                 +-30 days-> [Month Streak Badge]
                 |
                 +-etc.
```

---

## 5. SETTINGS & ACCOUNT FLOWS

### 5.1 Change Account Settings

```
[Home Page]
    |
    v
{Navigate to Settings}
    |
    v
[Settings Page]
    |
    +---> Account section
    |          |
    |          +---> {Change email} -> [Email Change Form]
    |          |                            |
    |          |                            v
    |          |                       {Enter new email}
    |          |                            |
    |          |                            v
    |          |                       {Confirm password}
    |          |                            |
    |          |                            v
    |          |                       [Verification sent to new email]
    |          |
    |          +---> {Change password} -> [Password Change Form]
    |          |                               |
    |          |                               v
    |          |                         {Enter current password}
    |          |                               |
    |          |                               v
    |          |                         {Enter new password}
    |          |                               |
    |          |                               v
    |          |                         [Password updated]
    |          |
    |          +---> {Sign out} -> [Flow 5.3]
    |          |
    |          +---> {Delete account} -> [Flow 5.4]
    |
    +---> Appearance section
    |          |
    |          +---> {Toggle dark mode}
    |          |
    |          +---> {Adjust text size} (if available)
    |
    +---> Notifications section
    |          |
    |          +---> {Toggle daily reminder}
    |          |
    |          +---> {Set reminder time}
    |
    +---> Privacy section
           |
           +---> {View Privacy Policy}
           |
           +---> {View Terms of Service}
           |
           +---> {Download my data}
```

### 5.2 Sign In (Returning User)

```
[Any Page] -> {Click Sign In}
    |
    v
[Sign In Page]
    |
    +---> {Enter email}
    |
    +---> {Enter password}
    |
    +---> {Click "Sign In"}
    |          |
    |          v
    |     (Valid credentials?)
    |          |
    |          +-Yes-> [Logged In] -> [Return to previous page or Home]
    |          |
    |          +-No--> [Error: "Invalid email or password"]
    |                       |
    |                       v
    |                  {Retry or Forgot Password}
    |
    +---> {Forgot Password?}
               |
               v
          [Password Reset Page]
               |
               v
          {Enter email}
               |
               v
          {Submit}
               |
               v
          [Check your email message]
               |
               v
          {Open email, click link}
               |
               v
          [Reset Password Page]
               |
               v
          {Enter new password}
               |
               v
          [Password Reset Success]
               |
               v
          [Sign In Page]
```

### 5.3 Sign Out Flow

```
[Settings Page]
    |
    v
{Tap "Sign Out"}
    |
    v
[Confirmation Dialog]
"Are you sure you want to sign out?"
    |
    +---> {Cancel} -> [Settings Page]
    |
    +---> {Confirm Sign Out}
               |
               v
          [Session cleared]
               |
               v
          [Home Page - Guest mode]
               |
               v
          (Local data handling)
               |
               +---> Cached content remains (devotionals)
               +---> User data cleared (bookmarks, progress local copy)
               +---> Sign in prompt on protected actions
```

### 5.4 Delete Account Flow

```
[Settings Page]
    |
    v
{Tap "Delete Account"}
    |
    v
[Warning Screen]
"This will permanently delete your account and all data"
    |
    +---> List of what will be deleted:
    |     - Reading progress
    |     - Bookmarks
    |     - Soul Audit history
    |     - Account information
    |
    v
{Type "DELETE" to confirm}
    |
    v
{Enter password}
    |
    v
{Tap "Delete My Account"}
    |
    v
[Processing...]
    |
    v
[Account Deleted Confirmation]
    |
    v
[Redirect to Home - Guest]
```

---

## 6. PWA-SPECIFIC FLOWS

### 6.1 PWA Installation (Mobile)

```
[First Visit to Site]
    |
    v
(Criteria met for install prompt?)
    |
    +-No--> [Continue as web]
    |
    +-Yes-> (After engagement threshold)
                 |
                 v
            [Install Banner/Prompt appears]
            "Add EUONGELION to Home Screen"
                 |
                 +---> {Dismiss} -> [Banner hidden]
                 |                       |
                 |                       v
                 |                  (Show again later?)
                 |
                 +---> {Install}
                            |
                            v
                       [Installing...]
                            |
                            v
                       [Success: "Added to Home Screen"]
                            |
                            v
                       [App icon on device home screen]
```

### 6.2 Offline Usage

```
[User opens app - NO NETWORK]
    |
    v
[Service Worker intercepts]
    |
    v
(Is content cached?)
    |
    +-Yes-> [Load from cache]
    |            |
    |            v
    |       [Offline indicator shown]
    |            |
    |            v
    |       [User can browse cached devotionals]
    |            |
    |            v
    |       {Attempt to load uncached content}
    |            |
    |            v
    |       [Friendly offline message]
    |       "This content isn't available offline"
    |
    +-No--> [Offline error page]
                 |
                 v
            "You're offline. Please connect to continue."
                 |
                 v
            {Retry when connected}
```

### 6.3 Background Sync (if implemented)

```
[User completes devotional - OFFLINE]
    |
    v
[Action queued in IndexedDB]
    |
    v
[Sync badge/indicator shown]
"Will sync when online"
    |
    v
...time passes...
    |
    v
[Network connection restored]
    |
    v
[Background sync triggered]
    |
    v
[Queued actions sent to server]
    |
    v
[Sync complete - badge removed]
```

---

## 7. CONTENT DISCOVERY FLOWS

### 7.1 Search Flow (if implemented)

```
[Home Page]
    |
    v
{Tap search icon/bar}
    |
    v
[Search Interface]
    |
    v
{Type search query}
    |
    v
[Real-time results appear]
    |
    +---> Devotionals matching query
    |
    +---> Series matching query
    |
    +---> Scripture references matching
    |
    v
{Tap a result}
    |
    v
[Devotional or Series Page]
```

### 7.2 Category Browse Flow

```
[Home Page or Discovery]
    |
    v
{Tap "Browse by Category" or category card}
    |
    v
[Category List/Grid]
    |
    +---> Faith Foundations
    +---> Emotional Healing
    +---> Purpose & Direction
    +---> Relationships
    +---> Spiritual Practices
    +---> Doubt & Questions
    +---> Rest & Renewal
    +---> Growth & Discipleship
    |
    v
{Select category}
    |
    v
[Category Page]
    |
    +---> Category description
    +---> Scripture theme
    +---> Related series
    +---> Related devotionals
    |
    v
{Select content to read}
```

---

## 8. SHARE & SOCIAL FLOWS

### 8.1 Share Devotional

```
[Devotional Page]
    |
    v
{Tap Share button}
    |
    v
[Share Options Sheet]
    |
    +---> {Native Share} (mobile)
    |          |
    |          v
    |     [OS Share Sheet]
    |          |
    |          v
    |     {Select app to share to}
    |          |
    |          v
    |     [App opens with pre-filled content]
    |
    +---> {Copy Link}
    |          |
    |          v
    |     [Link copied to clipboard]
    |          |
    |          v
    |     [Toast: "Link copied!"]
    |
    +---> {Share to Twitter}
    |          |
    |          v
    |     [Twitter compose opens]
    |     (Pre-filled with quote + link)
    |
    +---> {Share to Facebook}
               |
               v
          [Facebook share dialog]
```

### 8.2 Invite Friend Flow (if implemented)

```
[Settings or Home]
    |
    v
{Tap "Invite Friends"}
    |
    v
[Invite Screen]
    |
    +---> Personal message option
    |
    +---> Share methods:
           |
           +---> {Text message}
           +---> {Email}
           +---> {Copy invite link}
           +---> {Share to social}
```

---

## Flow Testing Checklist

For each flow, verify:

| Flow | Happy Path | Error Handling | Edge Cases | Accessibility |
|------|------------|----------------|------------|---------------|
| 1.1 First Visit | [ ] | [ ] | [ ] | [ ] |
| 1.2 Sign Up | [ ] | [ ] | [ ] | [ ] |
| 1.3 First Devotional | [ ] | [ ] | [ ] | [ ] |
| 2.1 Continue Reading | [ ] | [ ] | [ ] | [ ] |
| 2.2 Check Bookmarks | [ ] | [ ] | [ ] | [ ] |
| 2.3 Browse Series | [ ] | [ ] | [ ] | [ ] |
| 3.1 Soul Audit | [ ] | [ ] | [ ] | [ ] |
| 3.3 Crisis Path | [ ] | [ ] | [ ] | [ ] |
| 4.1 Complete Series | [ ] | [ ] | [ ] | [ ] |
| 5.2 Sign In | [ ] | [ ] | [ ] | [ ] |
| 6.1 PWA Install | [ ] | [ ] | [ ] | [ ] |
| 6.2 Offline Usage | [ ] | [ ] | [ ] | [ ] |

---

## Notes

- All flows should be tested on mobile, tablet, and desktop
- Flows involving authentication should be tested both logged in and logged out
- Error states and loading states should be visible during testing
- Accessibility: all flows should work with keyboard-only navigation

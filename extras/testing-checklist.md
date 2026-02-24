# ✅ Testing Checklist

> A comprehensive pre-launch verification checklist. Complete every item before considering your project done.

---

## 📖 Table of Contents

- [🧪 Functional Testing](#-functional-testing)
- [🎨 UI Testing](#-ui-testing)
- [⚡ Performance Testing](#-performance-testing)
- [🚀 Deployment Testing](#-deployment-testing)
- [🌐 Cross-Browser Testing](#-cross-browser-testing)
- [⚡ Quick Test Protocol](#-quick-test-protocol)
- [📋 Reporting Issues](#-reporting-issues)

---

## 🧪 Functional Testing

### Authentication

| # | Test Case | Steps | Expected Result | Pass |
|:--|:----------|:------|:----------------|:-----|
| 1 | Sign up with valid credentials | Enter name, email, password → Submit | Account created, redirect to dashboard | ☐ |
| 2 | Sign up with existing email | Use already registered email | Error message shown | ☐ |
| 3 | Sign up with weak password | Use password < 6 characters | Error message shown | ☐ |
| 4 | Sign up with invalid email | Enter "notanemail" | Error message shown | ☐ |
| 5 | Sign in with valid credentials | Enter registered email + password | Logged in, redirect to dashboard | ☐ |
| 6 | Sign in with wrong password | Enter correct email, wrong password | Error message shown | ☐ |
| 7 | Sign in with non-existent email | Enter unregistered email | Error message shown | ☐ |
| 8 | Sign out | Click sign out button | Redirected to home or auth page | ☐ |
| 9 | Auth persistence | Sign in → close tab → reopen | Still logged in | ☐ |
| 10 | Protected route (unauthenticated) | Visit /dashboard while logged out | Redirected to /auth | ☐ |

### CRUD Operations

| # | Test Case | Steps | Expected Result | Pass |
|:--|:----------|:------|:----------------|:-----|
| 11 | Create item | Fill form → submit | New item appears in list | ☐ |
| 12 | Create with empty required field | Leave title empty → submit | Validation error shown | ☐ |
| 13 | Read items on load | Navigate to dashboard | All user's items displayed | ☐ |
| 14 | Update item (toggle complete) | Click complete button | Item status changes | ☐ |
| 15 | Delete item | Click delete button | Item removed from list | ☐ |
| 16 | Data persistence | Create item → refresh page | Item still exists | ☐ |
| 17 | User data isolation | Log in as User A | Cannot see User B's data | ☐ |

### Navigation

| # | Test Case | Steps | Expected Result | Pass |
|:--|:----------|:------|:----------------|:-----|
| 18 | Home page loads | Visit `/` | Landing page renders | ☐ |
| 19 | Auth page loads | Visit `/auth` | Login/signup form renders | ☐ |
| 20 | Dashboard loads | Visit `/dashboard` (logged in) | Dashboard renders | ☐ |
| 21 | Nav links work | Click each nav link | Navigates to correct page | ☐ |
| 22 | Logo link | Click logo | Returns to home page | ☐ |
| 23 | 404 handling | Visit `/nonexistent` | 404 page or redirect | ☐ |

---

## 🎨 UI Testing

### Layout

| # | Test Case | Expected Result | Pass |
|:--|:----------|:----------------|:-----|
| 24 | No horizontal scroll | No content overflows viewport | ☐ |
| 25 | Navbar is visible | Fixed/sticky at top of page | ☐ |
| 26 | Footer is at bottom | Below all content, not floating | ☐ |
| 27 | Content is readable | Text has sufficient contrast | ☐ |
| 28 | Images load | No broken image icons | ☐ |

### Responsive Design

| # | Viewport | Test | Pass |
|:--|:---------|:-----|:-----|
| 29 | 360px (mobile) | All content visible and usable | ☐ |
| 30 | 375px (iPhone SE) | No overlapping elements | ☐ |
| 31 | 768px (tablet) | Layout adjusts appropriately | ☐ |
| 32 | 1024px (small laptop) | Full desktop layout active | ☐ |
| 33 | 1440px (desktop) | Content centered, max-width applied | ☐ |

### Interactive Elements

| # | Test Case | Expected Result | Pass |
|:--|:----------|:----------------|:-----|
| 34 | Buttons have hover states | Visual change on hover | ☐ |
| 35 | Inputs have focus states | Border/ring change on focus | ☐ |
| 36 | Loading states shown | Spinner or skeleton during async ops | ☐ |
| 37 | Empty states shown | Message when list is empty | ☐ |
| 38 | Error states shown | User-friendly error messages | ☐ |
| 39 | Mobile menu works | Hamburger toggles nav menu | ☐ |

---

## ⚡ Performance Testing

| # | Test Case | Method | Target | Pass |
|:--|:----------|:-------|:-------|:-----|
| 40 | Page load time | Browser DevTools → Network | < 3 seconds | ☐ |
| 41 | No layout shift | Visually observe page load | No jumping content | ☐ |
| 42 | No console errors | Browser DevTools → Console | Zero errors | ☐ |
| 43 | No console warnings | Browser DevTools → Console | Minimal warnings | ☐ |
| 44 | Build succeeds | `npm run build` | Zero build errors | ☐ |

---

## 🚀 Deployment Testing

| # | Test Case | Method | Pass |
|:--|:----------|:-------|:-----|
| 45 | Live URL accessible | Open Vercel URL in browser | ☐ |
| 46 | HTTPS working | Check for padlock in browser bar | ☐ |
| 47 | All pages work in production | Navigate through all routes | ☐ |
| 48 | Auth works in production | Sign up + sign in on live URL | ☐ |
| 49 | Data operations work in production | Create + read + delete on live URL | ☐ |
| 50 | Mobile works in production | Open live URL on phone or mobile emulator | ☐ |

---

## 🌐 Cross-Browser Testing

| Browser | Version | Works | Pass |
|:--------|:--------|:------|:-----|
| Chrome | Latest | ☐ | ☐ |
| Firefox | Latest | ☐ | ☐ |
| Safari | Latest | ☐ | ☐ |
| Edge | Latest | ☐ | ☐ |
| Mobile Safari (iOS) | Latest | ☐ | ☐ |
| Chrome (Android) | Latest | ☐ | ☐ |

---

## ⚡ Quick Test Protocol

For rapid verification, run through these **10 critical checks**:

| # | Check | Pass |
|:--|:------|:-----|
| 1 | Open live URL — home page loads | ☐ |
| 2 | Click "Get Started" — navigate to auth | ☐ |
| 3 | Sign up with new account — redirects to dashboard | ☐ |
| 4 | Create a new item — appears in list | ☐ |
| 5 | Toggle item complete — status updates | ☐ |
| 6 | Delete an item — removed from list | ☐ |
| 7 | Refresh page — data still present | ☐ |
| 8 | Sign out — redirected away from dashboard | ☐ |
| 9 | Visit `/dashboard` directly — redirected to auth | ☐ |
| 10 | Open on mobile — responsive and usable | ☐ |

> [!TIP]
> Run the Quick Test Protocol after every deployment to catch regressions fast.

---

## 📋 Reporting Issues

If a test fails, document it using this template:

```markdown
### Bug Report

**Test #:** [number]
**Description:** [what failed]
**Steps to Reproduce:**
1. [step 1]
2. [step 2]
3. [step 3]

**Expected:** [what should happen]
**Actual:** [what actually happened]
**Screenshot:** [if applicable]
**Browser/Device:** [Chrome 120 / iPhone 15 / etc.]
**Severity:** [Critical / High / Medium / Low]
```

---

<div align="center">

**[⬆ Back to Top](#-testing-checklist)** · **[🏠 Return to README](../README.md)**

</div>

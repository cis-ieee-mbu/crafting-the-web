# 🔒 Security Practices

> Essential security measures for your web application. Follow these before deploying to production.

---

## 📖 Table of Contents

- [🔑 Environment Variables](#-environment-variables)
- [🛡️ Authentication Protection](#️-authentication-protection)
- [📜 Firestore Security Rules](#-firestore-security-rules)
- [✅ Input Validation](#-input-validation)
- [📋 Production Safety Checklist](#-production-safety-checklist)
- [🔍 Quick Security Audit](#-quick-security-audit)

---

## 🔑 Environment Variables

### Rules

- **NEVER** commit API keys, secrets, or credentials to Git
- **ALWAYS** use `.env.local` for local development
- **ALWAYS** add `.env.local` to `.gitignore`
- **ALWAYS** use `NEXT_PUBLIC_` prefix for client-side variables

### Verify .gitignore

```gitignore
# .gitignore
.env
.env.local
.env.production
.env*.local
node_modules/
.next/
```

### Check for Leaked Secrets

```bash
# Search your codebase for hardcoded keys
grep -r "AIzaSy" src/
grep -r "apiKey" src/ --include="*.js" --include="*.jsx"
```

If any results point to actual keys (not `process.env` references), move them to `.env.local`.

> [!WARNING]
> If you accidentally committed a secret, **rotate the key immediately**:
> 1. Firebase Console → Project Settings → regenerate API key
> 2. Update `.env.local` and Vercel env vars with the new key
> 3. The old key remains in Git history — consider it compromised

---

## 🛡️ Authentication Protection

### Protect Client-Side Routes

Every page that requires authentication should check auth state:

```javascript
"use client";

import { useEffect } from "react";
import { useRouter } from "next/navigation";
import { useAuth } from "@/context/AuthContext";

export default function ProtectedPage() {
  const { user, loading } = useAuth();
  const router = useRouter();

  useEffect(() => {
    if (!loading && !user) {
      router.push("/auth");
    }
  }, [user, loading, router]);

  // Show nothing while checking auth
  if (loading || !user) return null;

  return <div>{/* Protected content */}</div>;
}
```

### Auth State Persistence

Firebase Auth persists sessions by default using browser IndexedDB. Users stay logged in across tabs and browser restarts. To explicitly sign out:

```javascript
import { signOut } from "firebase/auth";
import { auth } from "@/lib/firebase";

await signOut(auth);
```

---

## 📜 Firestore Security Rules

### Principle of Least Privilege

> [!IMPORTANT]
> Grant only the **minimum access** needed. Deny everything by default.

### Production Rules Template

```text
rules_version = '2';

service cloud.firestore {
  match /databases/{database}/documents {

    // Users can only read/write their own data
    match /tasks/{taskId} {
      // Anyone logged in can create, but userId must match
      allow create: if isAuthenticated()
                    && incomingData().userId == currentUserId();

      // Only the owner can read, update, or delete
      allow read, update, delete: if isAuthenticated()
                                  && existingData().userId == currentUserId();
    }

    // Deny everything else
    match /{document=**} {
      allow read, write: if false;
    }
  }
}

// Helper functions
function isAuthenticated() {
  return request.auth != null;
}

function currentUserId() {
  return request.auth.uid;
}

function existingData() {
  return resource.data;
}

function incomingData() {
  return request.resource.data;
}
```

### Common Rule Mistakes

| Mistake | Risk | Fix |
|:--------|:-----|:----|
| `allow read, write: if true` | Anyone can read/write all data | Always require `request.auth != null` |
| No `userId` check | Users can access other users' data | Always match `userId == request.auth.uid` |
| Forgetting `match /{document=**}` deny | Unlisted collections are open | Add catch-all deny rule |
| Test mode left on in production | Full database access without auth | Replace with proper rules |

---

## ✅ Input Validation

### Client-Side Validation

Always validate user input before sending to the database:

```javascript
function validateTask(taskData) {
  const errors = [];

  if (!taskData.title || taskData.title.trim().length === 0) {
    errors.push("Title is required");
  }

  if (taskData.title && taskData.title.length > 200) {
    errors.push("Title must be under 200 characters");
  }

  if (!["work", "personal", "school"].includes(taskData.category)) {
    errors.push("Invalid category");
  }

  if (!["low", "medium", "high"].includes(taskData.priority)) {
    errors.push("Invalid priority");
  }

  return errors;
}
```

### Server-Side Validation (Firestore Rules)

Add data validation in security rules:

```text
match /tasks/{taskId} {
  allow create: if isAuthenticated()
                && incomingData().userId == currentUserId()
                && incomingData().title is string
                && incomingData().title.size() > 0
                && incomingData().title.size() <= 200
                && incomingData().category in ["work", "personal", "school"]
                && incomingData().priority in ["low", "medium", "high"];
}
```

> [!TIP]
> Always validate on **both** client and server. Client validation improves UX; server validation (Firestore rules) enforces security.

---

## 📋 Production Safety Checklist

### Before Going Live

#### Environment
- [ ] All API keys are in environment variables
- [ ] `.env.local` is in `.gitignore`
- [ ] No secrets in source code
- [ ] Vercel environment variables are set

#### Authentication
- [ ] Firebase authorized domains include your Vercel URL
- [ ] Login/signup forms have proper error handling
- [ ] Protected routes redirect unauthenticated users
- [ ] Sign out clears all user state

#### Database
- [ ] Firestore security rules are deployed (not test mode)
- [ ] Rules enforce user-level data isolation
- [ ] Rules validate data types and constraints
- [ ] Users cannot read/write other users' data

#### Frontend
- [ ] No sensitive data rendered in HTML source
- [ ] Error messages don't expose system internals
- [ ] Forms prevent double-submission (disable button while loading)
- [ ] XSS-safe: no `dangerouslySetInnerHTML` with user content

#### General
- [ ] HTTPS enforced (Vercel does this automatically)
- [ ] No open `console.log` with sensitive data
- [ ] Dependencies are up to date (`npm audit`)

---

## 🔍 Quick Security Audit

Run these checks periodically:

```bash
# Check for known vulnerabilities in dependencies
npm audit

# Fix automatically where possible
npm audit fix

# Search for hardcoded secrets
grep -rn "password\|secret\|apiKey\|AIza" src/ --include="*.js" --include="*.jsx"
```

---

<div align="center">

**[⬆ Back to Top](#-security-practices)** · **[🏠 Return to README](../README.md)**

</div>

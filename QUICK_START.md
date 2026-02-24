# ⚡ Quick Start

Build and deploy a web application in the fastest path possible. This guide skips deep planning and focuses on execution.

**Estimated time: 3–5 hours**

---

## 📖 Table of Contents

- [Prerequisites](#-prerequisites)
- [Step 1 — Define Your App](#-step-1--define-your-app-10-minutes)
- [Step 2 — Scaffold the Project](#-step-2--scaffold-the-project-5-minutes)
- [Step 3 — Build the UI](#-step-3--build-the-ui-12-hours)
- [Step 4 — Set Up Firebase](#-step-4--set-up-firebase-30-minutes)
- [Step 5 — Deploy to Vercel](#-step-5--deploy-to-vercel-15-minutes)
- [Step 6 — Verify](#-step-6--verify)

---

## 📋 Prerequisites

Ensure you have installed:

```bash
node --version    # v18 or higher required
npm --version     # v9 or higher
git --version     # any recent version
```

Accounts needed:

| Service | Purpose | Link |
|:--------|:--------|:-----|
| GitHub | Code hosting | [github.com](https://github.com) |
| Firebase | Backend | [console.firebase.google.com](https://console.firebase.google.com) |
| Vercel | Deployment | [vercel.com](https://vercel.com) |

> [!IMPORTANT]
> Make sure Node.js **v18+** is installed before proceeding. Run `node --version` to verify.

---

## 💡 Step 1 — Define Your App (10 minutes)

Write down three things:

```text
App Name:     _______________
What it does: _______________
Core feature: _______________
```

**Example:**

```text
App Name:     TaskFlow
What it does: Simple task manager for students
Core feature: Create, complete, and delete tasks
```

> [!TIP]
> Keep it simple. A focused app with one core feature is better than a complex app with many half-built features.

---

## 🏗️ Step 2 — Scaffold the Project (5 minutes)

```bash
npx create-next-app@latest my-app --tailwind --eslint --app --src-dir
cd my-app
npm install firebase react-icons
npm run dev
```

Open `http://localhost:3000` to verify it works.

---

## 🎨 Step 3 — Build the UI (1–2 hours)

Use an AI tool (Cursor, V0, Claude, ChatGPT) to generate components.

**Prompt template:**

```text
Build a React component for [component name] using Tailwind CSS.
It should [describe what it does].
Include [specific requirements].
Export as a default function component.
```

**Build in this order:**

1. `Navbar` — logo + navigation links
2. `HeroSection` — headline + CTA button
3. Main feature area (your core feature UI)
4. `Footer` — simple footer

Place files in:

```text
src/components/Navbar.jsx
src/components/HeroSection.jsx
src/components/TaskList.jsx    ← (your core feature)
src/components/Footer.jsx
```

Assemble in `src/app/page.js`:

```jsx
import Navbar from "@/components/Navbar";
import HeroSection from "@/components/HeroSection";
import TaskList from "@/components/TaskList";
import Footer from "@/components/Footer";

export default function Home() {
  return (
    <>
      <Navbar />
      <HeroSection />
      <TaskList />
      <Footer />
    </>
  );
}
```

---

## 🔥 Step 4 — Set Up Firebase (30 minutes)

### 4a — Create Firebase Project

1. Go to [Firebase Console](https://console.firebase.google.com)
2. Create new project
3. Add Web App → copy config
4. Enable **Authentication** → Email/Password
5. Enable **Cloud Firestore** → Start in test mode

### 4b — Configure in Code

```bash
touch .env.local
```

```env
NEXT_PUBLIC_FIREBASE_API_KEY=your_key
NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN=your_domain
NEXT_PUBLIC_FIREBASE_PROJECT_ID=your_id
NEXT_PUBLIC_FIREBASE_STORAGE_BUCKET=your_bucket
NEXT_PUBLIC_FIREBASE_MESSAGING_SENDER_ID=your_sender
NEXT_PUBLIC_FIREBASE_APP_ID=your_app_id
```

> [!WARNING]
> Never commit `.env.local` to Git. Make sure it's listed in your `.gitignore` file.

Create `src/lib/firebase.js`:

```javascript
import { initializeApp } from "firebase/app";
import { getAuth } from "firebase/auth";
import { getFirestore } from "firebase/firestore";

const firebaseConfig = {
  apiKey: process.env.NEXT_PUBLIC_FIREBASE_API_KEY,
  authDomain: process.env.NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN,
  projectId: process.env.NEXT_PUBLIC_FIREBASE_PROJECT_ID,
  storageBucket: process.env.NEXT_PUBLIC_FIREBASE_STORAGE_BUCKET,
  messagingSenderId: process.env.NEXT_PUBLIC_FIREBASE_MESSAGING_SENDER_ID,
  appId: process.env.NEXT_PUBLIC_FIREBASE_APP_ID,
};

const app = initializeApp(firebaseConfig);
export const auth = getAuth(app);
export const db = getFirestore(app);
```

### 4c — Add Auth + Data Functions

Use AI to generate:
- `src/lib/auth.js` — signUp, signIn, logOut
- `src/lib/firestore.js` — addItem, getItems, deleteItem

### 4d — Connect UI to Firebase

Wire your core feature component to read/write from Firestore.

> [!TIP]
> Restart your dev server (`Ctrl+C` then `npm run dev`) after adding environment variables.

---

## 🚀 Step 5 — Deploy to Vercel (15 minutes)

```bash
# Push to GitHub
git init
git add .
git commit -m "complete app"
git branch -M main
git remote add origin https://github.com/YOU/YOUR-REPO.git
git push -u origin main
```

Then:

1. Go to [vercel.com](https://vercel.com)
2. Import your GitHub repo
3. Add environment variables (same as `.env.local`)
4. Click **Deploy**

Your app is now live. 🎉

> [!IMPORTANT]
> After deploying, add your Vercel domain (e.g., `your-app.vercel.app`) to Firebase → Authentication → Settings → **Authorized domains**. Without this, authentication will fail in production.

---

## ✅ Step 6 — Verify

- [ ] Home page loads
- [ ] Can sign up / log in
- [ ] Core feature works (CRUD)
- [ ] Works on mobile
- [ ] Live URL is accessible

---

## 🏁 Done

You now have a deployed web application. For deeper understanding of each phase, follow the [full Learning Path](./LEARNING_PATH.md).

---

<div align="center">

**[⬆ Back to Top](#-quick-start)** · **[🏠 Return to README](./README.md)**

</div>

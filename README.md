<div align="center">

# 🌐 Crafting the Web — AI Assisted Web Development Pipeline

**A complete, step-by-step workshop for building and deploying web applications using AI-assisted tooling.**

*From idea to production in a structured, repeatable pipeline.*

[![Next.js](https://img.shields.io/badge/Next.js-000000?style=for-the-badge&logo=nextdotjs&logoColor=white)](https://nextjs.org/)
[![React](https://img.shields.io/badge/React-61DAFB?style=for-the-badge&logo=react&logoColor=black)](https://react.dev/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-06B6D4?style=for-the-badge&logo=tailwindcss&logoColor=white)](https://tailwindcss.com/)
[![Firebase](https://img.shields.io/badge/Firebase-FFCA28?style=for-the-badge&logo=firebase&logoColor=black)](https://firebase.google.com/)
[![Vercel](https://img.shields.io/badge/Vercel-000000?style=for-the-badge&logo=vercel&logoColor=white)](https://vercel.com/)

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg?style=flat-square)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)
[![Beginner Friendly](https://img.shields.io/badge/Beginner-Friendly-orange?style=flat-square)](#prerequisites)

</div>

---

## 📖 Table of Contents

- [What Is This?](#-what-is-this)
- [The Pipeline](#-the-pipeline)
- [System Architecture](#-system-architecture)
- [Tech Stack](#-tech-stack)
- [Repository Navigation](#-repository-navigation)
- [How to Use This Repo](#-how-to-use-this-repo)
- [Prerequisites](#-prerequisites)
- [License](#-license)

---

## 🎯 What Is This?

This repository contains the full documentation and workflow guide for the **Crafting the Web** workshop. Students follow a **10-phase pipeline** to build a real, deployed web application — using AI tools at every stage.

**You will build:**

- ✅ A fully functional web application
- ✅ Connected to a real backend (Firebase)
- ✅ Deployed to a live URL (Vercel)
- ✅ Using AI to accelerate every step

> [!TIP]
> New to web development? Start with [Phase 1 — Overview](./01-overview/overview.md) and follow each phase in order. Each phase builds on the previous one.

---

## 🔄 The Pipeline

```mermaid
flowchart LR
    A["Idea"] --> B["Research"]
    B --> C["Architecture"]
    C --> D["UI Design"]
    D --> E["Build"]
    E --> F["Backend"]
    F --> G["Deploy"]

    A -.- A1["Define Problem"]
    B -.- B1["Identify Components"]
    C -.- C1["System Structure"]
    D -.- D1["Layout Specs"]
    E -.- E1["Working Frontend"]
    F -.- F1["Auth + Database"]
    G -.- G1["Live URL"]
```

---

## 🏛️ System Architecture

```mermaid
flowchart TB
    subgraph CLIENT["CLIENT - Browser"]
        direction TB
        subgraph NEXTJS["Next.js + React + Tailwind"]
            Pages["Pages"]
            Components["Components"]
            State["State / Context"]
        end
        SDK["Firebase SDK"]
    end

    subgraph FIREBASE["FIREBASE - Google Cloud"]
        Auth["Authentication<br/>Email/Pass"]
        Firestore["Cloud Firestore<br/>NoSQL Database"]
    end

    subgraph VERCEL["VERCEL - Deployment"]
        Build["Build Pipeline"]
        CDN["CDN / Edge Network"]
        URL["Live URL<br/>your-app.vercel.app"]
    end

    Pages --> SDK
    Components --> SDK
    State --> SDK
    SDK -->|HTTPS| Auth
    SDK -->|HTTPS| Firestore
    CLIENT --> Build
    Build --> CDN
    CDN --> URL
```

---

## 🛠️ Tech Stack

| Layer | Technology | Purpose |
|:------|:-----------|:--------|
| **Frontend** | Next.js, React, Tailwind CSS | UI rendering & styling |
| **Backend** | Firebase (Auth + Firestore) | Authentication & data storage |
| **Deployment** | Vercel | Hosting & CI/CD |
| **AI Tools** | Claude, ChatGPT, Cursor, V0, Bolt | Development acceleration |

---

## 🗂️ Repository Navigation

### 📋 Core Pipeline

| S.No | Phase | Documentation | Time Estimate |
|:-:|:------|:--------------|:--------------|
| 1 | 🌍 Overview | [01-overview/overview.md](./01-overview/overview.md) | 15 min |
| 2 | 💡 Ideation | [02-ideation/ideation.md](./02-ideation/ideation.md) | 30 min |
| 3 | 🔍 Research | [03-research/research.md](./03-research/research.md) | 30 min |
| 4 | 🏗️ Architecture | [04-architecture/architecture.md](./04-architecture/architecture.md) | 45 min |
| 5 | 🎨 UI Design | [05-ui-design/ui-design.md](./05-ui-design/ui-design.md) | 30 min |
| 6 | ⚙️ Frontend Build | [06-frontend-build/frontend.md](./06-frontend-build/frontend.md) | 2–4 hrs |
| 7 | 🤖 AI Workflow | [07-workflow-optimization/ai-workflow.md](./07-workflow-optimization/ai-workflow.md) | Ongoing |
| 8 | 🔥 Firebase Backend | [08-firebase-backend/firebase.md](./08-firebase-backend/firebase.md) | 1–2 hrs |
| 9 | 🚀 Deployment | [09-deployment/vercel.md](./09-deployment/vercel.md) | 30 min |
| 10 | ✅ Final Output | [10-final-output/deliverables.md](./10-final-output/deliverables.md) | 30 min |

### ⚡ Quick Access

| Document | Purpose |
|:---------|:--------|
| [📚 LEARNING_PATH.md](./LEARNING_PATH.md) | Recommended study order |
| [⚡ QUICK_START.md](./QUICK_START.md) | Skip to building fast |

### 📦 Extras

| Document | Purpose |
|:---------|:--------|
| [🐛 Common Errors](./extras/common-errors.md) | Troubleshooting guide |
| [🔒 Security Practices](./extras/security-practices.md) | Production safety |
| [✅ Testing Checklist](./extras/testing-checklist.md) | Pre-launch verification |

---

## 🧭 How to Use This Repo

### 🐢 Sequential Path (Recommended for Beginners)

Follow phases 1 through 10 in order. Each phase builds on the previous one.

### 🏃 Fast Track

Jump to [QUICK_START.md](./QUICK_START.md) for a condensed build-and-deploy workflow.

### 📖 Reference Mode

Use individual phase docs as reference while building your own project.

> [!NOTE]
> The **Sequential Path** is recommended for first-time users. It provides the deepest understanding of how all the pieces fit together.

---

## 📋 Prerequisites

Before starting, make sure you have:

- ✅ Basic understanding of HTML, CSS, JavaScript
- ✅ A code editor installed ([VS Code](https://code.visualstudio.com/) or [Cursor](https://cursor.sh/) recommended)
- ✅ [Node.js 18+](https://nodejs.org/) installed
- ✅ A [GitHub](https://github.com/) account
- ✅ A [Google](https://accounts.google.com/) account (for Firebase)
- ✅ A [Vercel](https://vercel.com/) account (free tier)

> [!IMPORTANT]
> Verify your Node.js version by running `node --version` in your terminal. You need **v18 or higher**.

---

## 📄 License

This workshop documentation is open source and available for educational use.

---

<div align="center">

*Built for the Crafting the Web Workshop*

**[⬆ Back to Top](#-crafting-the-web--ai-assisted-web-development-pipeline)**

</div>

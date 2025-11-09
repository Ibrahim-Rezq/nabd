# 🕌 Nabd (نَبْض) – Muslim Routine Tracker

> _"Reflect daily, improve consistently."_  
> **Nabd** (نَبْض) is a serene, minimal web application designed to help Muslims maintain balance and consistency in their worship (`ʿibādāt`) and worldly (`dunyā`) habits.

It allows you to track your daily prayers, remembrance, good deeds, and productive routines — encouraging self-reflection and mindful improvement.

---

## 🌟 Overview

**Nabd** is a Muslim routine tracker that visualizes your spiritual and personal progress across four main categories:

| Category                  | Description                                                           |
| ------------------------- | --------------------------------------------------------------------- |
| **Ṣalāh (Prayer)**        | Track your five daily prayers with pre/post steps and punctuality.    |
| **Adhkār (Remembrances)** | Morning and evening adhkār and post-prayer dhikr.                     |
| **General ʿIbādāt**       | Voluntary fasting, charity, Qur’an recitation, and duʿāʾ.             |
| **Dunyā (Worldly life)**  | Reading, studying, exercising, journaling — balancing faith and life. |

Each activity has a three-state tracking system:

-   ⬜ Not done
-   🟨 Done (late)
-   🟩 Done (on time)

---

## 🗺️ Roadmap (MVP Phases Overview)

Nabd will evolve through several **MVP stages**, each expanding on functionality while maintaining simplicity.  
This roadmap outlines the _conceptual development path_ — not specific technical tasks.

---

### **MVP 0 – Salah Tracker (Local Only)**

> _Core functionality and UX validation_

-   Build the foundation of the app using React, Vite, and TailwindCSS (with ShadCN UI).
-   Implement a simple checklist for the five daily prayers.
-   Store data locally via `localStorage`.
-   Minimal, mobile-friendly user experience.

---

### **MVP 1 – Enhanced Salah Tracking**

> _Introduce structured progress tracking_

-   Add three-state logic (not done / late / on time).
-   Add daily summaries and progress insights.
-   Introduce global state management with Zustand.
-   Improve feedback and design polish.

---

### **MVP 2 – Adhkār Tracker**

> _Expand scope to remembrance_

-   Introduce Morning and Evening Adhkār sections.
-   Combine Adhkār and Salah dashboards.
-   Optionally allow users to customize adhkār lists.

---

### **MVP 3 – Dunyā & General ʿIbādāt + Early Backend Setup**

> _Introduce worldly balance and begin backend integration_

-   Add Dunyā tasks (reading, working, studying, exercising).
-   Add General ʿIbādāt (Qur’an, Sadaqah, fasting, duʿāʾ).
-   Begin setting up **Supabase** for authentication and persistent storage.
-   Define data models using Prisma.
-   Connect app to a live database while still maintaining local caching for offline support.

---

### **MVP 4 – Full Cloud Sync and Analytics**

> _Enable multi-device experience and user data visualization_

-   Complete Supabase authentication (email + OAuth).
-   Sync progress across devices using PostgreSQL.
-   Implement backend APIs using NestJS for extended control.
-   Add personalized analytics and history tracking.

---

### **MVP 5 – Reflections & Insights**

> _Bring meaning into your data_

-   Add journaling and daily reflection prompts.
-   Optional AI-based reflection suggestions.
-   Weekly and monthly progress summaries.
-   Achievements and soft gamification (non-competitive).

---

## ⚙️ Tech Stack

| Layer                | Technology                             | Description                                                    |
| -------------------- | -------------------------------------- | -------------------------------------------------------------- |
| **Frontend**         | React + Vite + TailwindCSS + ShadCN UI | Fast, modular, and aesthetic UI framework.                     |
| **State Management** | Zustand                                | Lightweight, persistent store for app-wide state.              |
| **Backend**          | NestJS + Prisma ORM + PostgreSQL       | Scalable and type-safe architecture.                           |
| **Auth & Database**  | Supabase                               | Authentication, database, and storage in one unified platform. |
| **Hosting**          | Vercel (frontend) + Supabase (backend) | Seamless CI/CD with reliable free-tier options.                |

---

## 🚀 Deployment Plan

| Layer        | Platform                         | Description                                           |
| ------------ | -------------------------------- | ----------------------------------------------------- |
| **Frontend** | [Vercel](https://vercel.com)     | CI/CD integration, preview deploys, and edge caching. |
| **Backend**  | [Supabase](https://supabase.com) | PostgreSQL, Auth, and Storage combined.               |

> ⚙️ Note: Supabase setup starts as early as MVP 3 to minimize architecture shifts later.

---

## 🧭 Vision

> **Nabd** aims to help Muslims stay consistent, reflective, and intentional — using modern tools to nurture timeless faith and discipline.

The goal is not just productivity, but balance:

> _Faith and life, both tended with care._

---

## 🧑‍💻 Author

**Developer:** Ibrahim  
**Stack:** React, NestJS, PostgreSQL, Prisma, Supabase  
**License:** [MIT License](./LICENSE.md)

---

> _“Indeed, Allah does not change the condition of a people until they change what is in themselves.”_  
> **— Qur’an, 13:11**

> **“إِنَّ ٱللَّهَ لَا يُغَيِّرُ مَا بِقَوْمٍ حَتَّىٰ يُغَيِّرُوا۟ مَا بِأَنفُسِهِمْ”**  
> **— الرعد 11**

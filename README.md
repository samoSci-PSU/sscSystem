# SSC — Science Student Central System

> A centralized web platform for the Science Faculty Student Union and its affiliated clubs at Prince of Songkla University, designed to reduce paper usage and streamline student activity management.

---

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [User Roles](#user-roles)
- [Tech Stack](#tech-stack)
- [Infrastructure](#infrastructure)
- [Deployment](#deployment)
- [Team](#team)
- [Roadmap](#roadmap)

---

## Overview

SSC (Science Student Central System / ระบบศูนย์กลางนักศึกษาคณะวิทยาศาสตร์) is a multi-module web system serving approximately **3,000 students** across the Science Faculty. It connects three groups — students, club members, and the student union — through five core subsystems.

**Key goals:**
- Eliminate paper-based processes for equipment lending, project submissions, and document distribution
- Provide a single platform for all clubs under the Science Faculty Student Union
- Standardize club operations and document templates across academic years
- Enable the union president to digitally sign and approve club projects from anywhere

---

## Features

### Module 1 — Equipment Borrowing System
Allows clubs to manage their equipment inventory and process borrow/return requests digitally.

- Browse available equipment with status and quantity
- Submit borrow requests (item, date range, purpose)
- Approve or reject requests with notes
- Track return status and send overdue notifications
- Export borrow history reports (CSV / PDF)

### Module 2 — Online Shop
Enables the student union and affiliated clubs to create their own shop for selling merchandise or event-related products.

- Each club can create and manage its own shop
- List products with images, price, stock, and order deadline
- Students and external buyers can browse and place orders
- Order status tracking (pending → ready → received)
- Inventory management and order closing

### Module 3 — Document Templates & Staff Directory
A centralized resource hub for clubs to access standardized documents and faculty contact information.

- Download official document templates (project forms, budget forms, etc.)
- Browse faculty staff and administrators with contact details
- Upload and categorize templates (managed by union staff)

### Module 4 — Digital Project Approval & Signing
Allows clubs to submit project proposals and get them digitally signed by the union president — no physical visit required.

- Submit project documents (PDF upload or form-based)
- Track approval status in real time
- Union president signs or returns with comments
- Notification system for all status changes

### Module 5 — Project Archive
A searchable archive of all projects from every club across academic years.

- Browse and search by club, academic year, or keyword
- View project details, budget summaries, and attached documents
- Clubs upload completed projects to the archive

---

## User Roles

SSC uses a role-based access control system. A single user account can hold multiple roles simultaneously.

| Role | Description | Permissions |
|---|---|---|
| `student` | Any Science Faculty student | Browse shop, view archive, download templates, view staff directory |
| `club_member` | Student who is a member of an affiliated club | + Borrow equipment, submit projects, upload to archive |
| `union_staff` | Science Faculty Student Union team member | + Manage equipment, manage shop, manage documents and staff info |
| `president` | Union president (subset of union_staff) | + Sign and approve club project submissions |

> A user can be both `student + club_member` or `student + union_staff` at the same time. Role assignment is managed by union staff via the admin panel.

---

## Tech Stack

| Layer | Technology | Notes |
|---|---|---|
| **Framework** | Next.js 14 (App Router) | TypeScript, server components by default |
| **Styling** | Tailwind CSS | Utility-first, consistent design system |
| **Database** | Supabase (PostgreSQL) | Managed DB with row-level security |
| **Auth** | Supabase Auth | Email-based login (university email) |
| **File Storage** | Supabase Storage | PDFs, images, document templates |
| **Hosting** | Cloudflare Pages | Unlimited bandwidth, free tier |
| **AI-assisted Dev** | Cursor + Gemini 2.5 Pro | AI-directed coding workflow via Google AI Studio API |

---

## Infrastructure

### Capacity Planning

Designed for ~3,000 students with a peak of 1,500 daily active users.

| Metric | Estimate |
|---|---|
| Daily active users (peak) | 1,500 |
| Requests per day | ~22,500 |
| Bandwidth per month | ~30–45 GB |
| File storage growth | ~500 MB / academic year |

### Supabase Plan

| Phase | Plan | Notes |
|---|---|---|
| Development / Demo | Free tier | Sufficient for dev; projects pause after 7 days of inactivity |
| Production (June 2025+) | Pro ($25/month) | 8 GB DB, 250 GB bandwidth, no project pause |

### Cloudflare Pages

Chosen over Vercel for production due to:
- Unlimited bandwidth on free tier
- Permits non-commercial organizational use
- No usage-based overage charges

> **Note:** Next.js deployment on Cloudflare requires `@cloudflare/next-on-pages` adapter. All API routes must use `export const runtime = 'edge'`.

---


---

## Getting Started

### Prerequisites

- Node.js 18+
- A [Supabase](https://supabase.com) project
- A [Cloudflare](https://pages.cloudflare.com) account (for deployment)
- [Cursor](https://cursor.sh) editor with Gemini API key (recommended for development)


---

---

## Deployment

### Development → Staging

```bash
git checkout -b feature/your-feature
# ... make changes ...
git push origin feature/your-feature
# Open a Pull Request to dev branch
```

### Production (Cloudflare Pages)

```bash
# Install Cloudflare adapter
npm install @cloudflare/next-on-pages

# Build for Cloudflare
npm run build:cloudflare

# Deploy via Cloudflare Pages dashboard or CLI
npx wrangler pages deploy .vercel/output/static
```

### Branch Strategy

```
main      ← production (protected)
dev       ← staging / integration
feature/* ← individual features
hotfix/*  ← urgent production fixes
```

---

## Team

| Member | Role | Responsibilities |
|---|---|---|
| Member 1 | Project Lead + Fullstack | Architecture, Auth, Project signing system (Modules 3, 4, 5) |
| Member 2 | Frontend Focus | UI components, Equipment borrowing, Shop (Modules 1, 2) |
| Member 3 | Backend Focus | API design, DB schema, File storage, Notifications, DevOps |

**Development workflow:** Figma → Prompt → Cursor → Debug → Pull Request → Review

---

## Roadmap

| Date | Milestone |
|---|---|
| Mar 28–30, 2025 | Team training: Git/GitHub, Figma, Cursor + Next.js + Supabase |
| Mar 31 – Apr 4 | Design Sprint: Figma wireframes + DB schema |
| **Apr 5, 2025** | **🎯 Mockup / Demo release** |
| Apr 6 – Apr 25 | Phase 1: Auth, Dashboard, Equipment Borrowing |
| Apr 26 – May 16 | Phase 2: Shop, Project Submission, Digital Signing |
| May 17 – May 31 | Phase 3: Document Templates, Staff Directory, Project Archive |
| Jun 1 – Jun 5 | UAT, final bug fixes, production deployment |
| **Jun 6, 2025** | **🚀 Production Launch** |

---

## License

This project is developed for the Science Faculty Student Union at Prince of Songkla University. All rights reserved.
# Maktab Student Management System

> **This project is the origin of [Labbaik](https://uselabbaik.com)** — a purpose-built management platform for Islamic educational institutions worldwide. What started here as a single-school deployment for Masjid Irshad Luton evolved into a multi-tenant SaaS product serving maktabs, madrasahs, and Darul Ulooms globally. This repo represents that first iteration.

---

## 📚 Overview

A student management system built for Islamic madrasahs and maktabs, centralising student records, attendance, academic progress, and payments in one place. Originally deployed for Masjid Irshad Luton, it supports multiple curriculum tracks (Qaidah, Quran, Hifz), role-based access for admins, teachers, and parents, and gives parents real-time visibility into their child's progress — replacing paper registers and spreadsheets entirely.

**Tech Stack:** React 18 · Vite · TypeScript · Tailwind CSS · shadcn/ui · Supabase (Postgres + RLS + Edge Functions) · Stripe · Resend

---

## 🎓 Core Student Management

### Student Directory

- Centralised student list with search and filters
- Filter by maktab (Boys / Girls), status, and curriculum group

### Student Curriculum Groups

- **Group A — Qaidah:** Levels 1–13 + Duas Books 1 & 2
- **Group B — Quran:** Juz 1–30, Tajweed Levels 1–7, Duas
- **Group C — Hifz:** Juz Amma surahs, Sabak, Sabak Para, Daur tracking

### Graduation & Promotion

- Promote students between groups with automatic progress reset

---

## ✅ Attendance Tracking

- Mobile-first one-tap interface for teachers
- Teacher is automatically marked present when recording student attendance (DB trigger)
- Per-group attendance history with date filters
- Monthly reports highlighting low and perfect attendance

<table>
  <tr>
    <td><img src="docs/screenshots/Registration.png" width="380" alt="Registration" /></td>
    <td><img src="docs/screenshots/attendance2.png" width="380" alt="Attendance" /></td>
  </tr>
</table>

---

## 📈 Progress Tracking

- Monthly progress prompts built into the post-attendance flow
- Historical snapshots stored per student per month
- Milestone tracking across Qaidah, Tajweed, Quran, and Hifz
- Parent notifications triggered on every update

---

## 💳 Payments (Stripe)

- Separate Stripe accounts for Boys and Girls maktabs
- Admission fee + recurring subscription per class
- Automatic 10% sibling discount; manual concessions supported
- Webhook-driven student activation on payment completion
- Customer billing portal for parents
- In production, Stripe integration eliminated missed and delayed payments — observed ~**133% increase** in monthly teacher income post-rollout

---

## 👨‍👩‍👧 Parent Portal

- Passwordless magic-link authentication (separate Supabase client to avoid session collisions)
- Dashboard with progress and attendance charts (7-day to 12-month views)
- Notifications feed and profile self-management
- PWA-installable with push notifications

<img src="docs/screenshots/Parent-portal.png" width="600" alt="Parent Portal" />

---

## 🛠️ Admin Panel

- User management: create, reset, and disable teacher accounts
- Registration queue: review and approve/reject pending applications
- Announcements: email + in-portal, image attachments, scheduled or immediate
- Full audit logs across students, attendance, progress, and payments
- Ghost mode: view the app as any teacher or parent
- Email template preview and testing
- Public website event manager

<img src="docs/screenshots/Admin-Panel.png" width="600" alt="Admin Panel" />

---

## 🔐 Security & Access Control

- Role-based access: Admin, Teacher, Parent — stored in a dedicated `user_roles` table (never on profiles)
- Row-Level Security enforced on every Postgres table
- `has_role()` security-definer function prevents recursive RLS issues
- All sensitive operations (Stripe webhooks, payment links, magic links) handled in authenticated Edge Functions
- Comprehensive audit logging throughout

---

## 🌱 What This Became

This codebase was the proof of concept that validated the product. The insights from running it in production at Masjid Irshad — attendance behaviour, payment friction, teacher workflows, parent expectations — directly shaped the architecture of [Labbaik](https://uselabbaik.com).

Labbaik is the multi-tenant evolution: a global platform for Islamic educational institutions with multi-currency payment processing, a donor/sponsor-a-child module, a WhatsApp bot, a Hafiz oversight dashboard, and support for institutions across the UK, Malaysia, Pakistan, and beyond.

---

## License

Business Source License (BUSL-1.1) — see [LICENSE](LICENSE) for details.

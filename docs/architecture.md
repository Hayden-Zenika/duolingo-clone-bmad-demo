# Architecture Documentation

## Executive Summary
This project is a Duolingo clone built with Next.js, TypeScript, and PostgreSQL. It features a comprehensive language learning platform with lessons, quizzes, progress tracking, and a shop system.

## Technology Stack
- **Framework:** Next.js (App Router)
- **Language:** TypeScript
- **Database:** PostgreSQL (Neon)
- **ORM:** Drizzle ORM
- **UI:** Tailwind CSS, Shadcn UI, Radix UI
- **Authentication:** Clerk
- **State Management:** Zustand
- **Payments:** Stripe

## Architecture Pattern
The application follows a **Monolithic** architecture using the **Next.js App Router**.
- **Frontend:** React Server Components (RSC) and Client Components.
- **Backend:** Next.js API Routes (Serverless Functions).
- **Database:** Relational data model managed by Drizzle ORM.

## Data Architecture
The database schema is defined in `db/schema.ts` and includes tables for:
- Courses and Units
- Lessons and Challenges
- User Progress and Subscriptions

## API Design
The API is RESTful, with endpoints organized by resource (e.g., `/api/courses`, `/api/lessons`).
- **Authentication:** Protected by Clerk middleware.
- **Validation:** Input validation using Zod (implied).

## Component Overview
The UI is built with reusable components from `components/ui` (Shadcn UI) and feature-specific components in `components/`.
- **Layouts:** `sidebar.tsx`, `mobile-header.tsx`
- **Features:** `user-progress.tsx`, `quests.tsx`
- **Modals:** Managed by Zustand stores (`store/`).

## Development Workflow
- **Package Manager:** npm
- **Linting:** ESLint
- **Formatting:** Prettier
- **Database Management:** Drizzle Kit

## Deployment Architecture
- **Platform:** Vercel (implied by Next.js)
- **Database:** Neon (Serverless PostgreSQL)
- **CI/CD:** GitHub Actions (implied)

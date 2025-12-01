# Development Guide

## Prerequisites
- Node.js (v20+)
- npm or yarn or pnpm
- PostgreSQL database (Neon recommended)

## Installation
1. Clone the repository
2. Install dependencies:
   ```bash
   npm install
   ```
3. Set up environment variables:
   - Copy `.env.example` to `.env` (if available) or create `.env`
   - Configure `DATABASE_URL`
   - Configure Clerk keys (`NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY`, `CLERK_SECRET_KEY`)
   - Configure Stripe keys (`STRIPE_API_KEY`, `STRIPE_WEBHOOK_SECRET`)

## Development
Start the development server:
```bash
npm run dev
```
Access the app at `http://localhost:3000`.

## Database
- Push schema changes: `npm run db:push`
- Open Drizzle Studio: `npm run db:studio`
- Seed database: `npm run db:prod`

## Linting and Formatting
- Lint: `npm run lint`
- Format: `npm run format`
- Fix formatting: `npm run format:fix`

## Build
Build for production:
```bash
npm run build
```
Start production server:
```bash
npm run start
```

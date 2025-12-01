# Source Tree Analysis

## Project Structure

```
duolingo-clone-bmad-demo/
├── actions/             # Server actions for data mutation
├── app/                 # Next.js App Router pages and layouts
│   ├── (auth)/          # Authentication routes (sign-in, sign-up)
│   ├── (main)/          # Main application routes (learn, courses, leaderboard, quests, shop)
│   ├── (marketing)/     # Marketing landing page
│   ├── admin/           # Admin dashboard (React Admin)
│   ├── api/             # API routes
│   └── lesson/          # Lesson player interface
├── components/          # Reusable UI components
│   ├── modals/          # Application modals
│   └── ui/              # Shadcn UI primitive components
├── config/              # Application configuration
├── db/                  # Database schema and queries (Drizzle)
├── lib/                 # Utility functions and shared logic
├── public/              # Static assets
├── scripts/             # Database seeding and maintenance scripts
└── store/               # Global state management (Zustand)
```

## Critical Directories

- **app/**: Contains the application routing logic and page components.
- **components/**: Houses reusable UI components, ensuring consistency across the app.
- **db/**: Defines the database schema and provides query helpers.
- **lib/**: Contains utility functions, including Stripe integration and admin helpers.
- **store/**: Manages global state for modals and other application-wide data.
- **actions/**: Server actions for handling user interactions and data updates.

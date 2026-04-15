# Next.js Dashboard - AI Agent Instructions

This is a **Next.js 15+** educational dashboard application using modern patterns.

## Project Context

**Type**: Educational Next.js App Router dashboard  
**Stack**: TypeScript, React 18+, PostgreSQL, NextAuth 5.0.0-beta, Tailwind CSS, Zod  
**Package Manager**: pnpm

## Build & Development

```bash
pnpm dev          # Start dev server (Turbopack-powered)
pnpm build        # Production build
pnpm start        # Run production build
pnpm seed         # Initialize database (via app/seed/route.ts)
```

**Note**: No test or lint scripts configured. Development-focused learning project.

## Architecture & Key Patterns

### Data Flow

- **Server-side async functions** in [app/lib/data.ts](app/lib/data.ts) query PostgreSQL directly
- **No ORM** — raw postgres driver for learning purposes
- Database types manually defined in [app/lib/definitions.ts](app/lib/definitions.ts)
- Database initialization via [app/seed/route.ts](app/seed/route.ts)
- Query utilities in [app/query/route.ts](app/query/route.ts)

### Components

- Located in [app/ui/](app/ui/) organized by feature (buttons, forms, tables, charts, customers, dashboard, invoices)
- Functional React components with hooks
- Styled with **Tailwind CSS** + Tailwind Forms
- Icons from **@heroicons/react**
- Debouncing via **use-debounce**

### Routes & Pages

- App Router pattern in [app/](app/)
- Dashboard main pages in [app/dashboard/](app/)
- Feature routes (invoices, customers) in [app/dashboard/invoices/](app/dashboard/invoices/), etc.
- Authentication managed by NextAuth 5.0.0-beta with bcrypt password hashing

### Form Validation

- **Zod** for schema validation
- Forms in [app/ui/invoices/](app/ui/invoices/) (create-form.tsx, edit-form.tsx)

### Styling & Layout

- **Tailwind CSS** for styling with custom config in [tailwind.config.ts](tailwind.config.ts)
- Global styles in [app/ui/global.css](app/ui/global.css)
- **PostCSS** configured in [postcss.config.js](postcss.config.js)

## Code Conventions

- **TypeScript**: Strict mode enabled, ES2017 target
- **Imports**: Use path alias `@/*` (configured in [tsconfig.json](tsconfig.json))
- **Component exports**: Named exports with TypeScript interfaces/types
- **Server components**: Preferred for data fetching; mark client components with `'use client'`
- **Async operations**: Use async/await with proper error handling
- **Database connection**: Re-establish per request (stateless, serverless-friendly)

## File Structure Reference

```
app/
├── lib/                    # Business logic & data access
│   ├── data.ts           # Server-side async functions querying DB
│   ├── definitions.ts    # TypeScript database types
│   ├── utils.ts          # Utility functions
│   └── placeholder-data.ts
├── ui/                     # Reusable components
│   ├── dashboard/        # Dashboard-specific components (cards, charts, nav)
│   ├── invoices/         # Invoice-specific components (forms, tables)
│   ├── customers/        # Customer table component
│   ├── *.tsx             # Global components (buttons, forms, search, etc.)
│   └── global.css
├── dashboard/             # Dashboard routes & pages
├── invoices/              # Invoice management routes
├── seed/                  # Database seeding endpoint
├── query/                 # Query utilities endpoint
└── page.tsx              # Root page / login
```

## Important Notes

- This is a **learning project** — not production-hardened
- Database queries use `postgres` driver directly; no connection pooling configured
- Authentication is NextAuth 5.0.0-beta (beta version)
- When adding features, follow existing patterns (server functions in lib/, UI in app/ui/)
- Always use Zod for form validation
- Prefer server components; use `'use client'` only when necessary (interactivity, hooks)

## Documentation

- [README.md](README.md) — Project overview and setup
- Inline code examples in [app/lib/data.ts](app/lib/data.ts) show how to query the database

---

**Last updated**: April 2026  
**Maintainer notes**: For questions about Next.js patterns or this codebase, refer to the Next.js 15+ docs and the code examples in app/lib/data.ts.

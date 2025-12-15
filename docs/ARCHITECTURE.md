# Project Architecture – Next.js 13+ with App Router

This document describes the architecture, folder structure, and conventions used in this Next.js project. It serves as a reference for developers joining the project and for maintaining a clean and scalable codebase.

---

## Overview

**Architecture Type:** Modular / Layered by Responsibility
**Framework:** Next.js 13+
**Router:** App Router (`src/app/`)
**Source Folder:** `src/`
**Goal:** Clear separation of concerns, modularity, and scalability.

---

## Folder Structure

```
my-next-app/
├─ src/
│  ├─ app/                     # App Router pages and API routes
│  │  ├─ layout.tsx            # Root layout shared across pages
│  │  ├─ page.tsx              # Entry page for the route
│  │  ├─ api/                  # API routes
│  │  │  ├─ users/
│  │  │  │  └─ route.ts        # /api/users
│  │  │  └─ auth/
│  │  │     └─ login/
│  │  │        └─ route.ts     # /api/auth/login
│  │  ├─ dashboard/            # Nested route example
│  │  │  └─ page.tsx
│  │  └─ components/           # Route-specific UI components
│  │
│  ├─ components/              # Reusable global UI components
│  │  ├─ Button.tsx
│  │  └─ Card.tsx
│  │
│  ├─ styles/                  # CSS/SCSS global and module files
│  │  ├─ globals.css
│  │  └─ button.module.css
│  │
│  ├─ lib/                     # Helpers, utilities, API clients, DB connection
│  │  ├─ db.ts
│  │  └─ fetcher.ts
│  │
│  ├─ hooks/                   # Custom React hooks
│  │  └─ useAuth.ts
│  │
│  ├─ context/                 # React context providers for global state
│  │  └─ AuthContext.tsx
│  │
│  └─ types/                   # Global TypeScript types and interfaces
│     └─ index.d.ts
│
├─ public/                      # Static assets (images, favicon, fonts)
├─ ARCHITECTURE.md              # This file
├─ README.md                     # Project overview and instructions
├─ package.json
├─ tsconfig.json
└─ next.config.js
```

---

## Folder Responsibilities

### `src/app/`

- Contains **pages and routes** using App Router.
- `layout.tsx` defines shared layout for pages.
- `page.tsx` defines the default page for the route.
- `api/` contains **API endpoints**, each folder represents a route with `route.ts`.
- Route-specific components go in `app/<route>/components/`.

### `src/components/`

- **Reusable UI components** across the app.
- Keep generic; route-specific components go inside route folders.

### `src/styles/`

- Global styles (`globals.css`) and CSS modules for components (`*.module.css`).

### `src/lib/`

- Utilities, helper functions, database or API clients.
- Reusable functions that do not belong to UI logic.

### `src/hooks/`

- Custom React hooks.
- Naming convention: `use<Name>.ts`.

### `src/context/`

- React context providers for global state.
- Each context should provide a hook for consumption.

### `src/types/`

- Global TypeScript types/interfaces.
- Centralized to prevent duplication and improve type safety.

### `public/`

- Static assets served directly from the root (`/`).

---

## Principles and Conventions

1. **Modularity:** Each folder has a single responsibility.
2. **Reusability:** Global components, hooks, and utilities are separated from route-specific code.
3. **Scalability:** Easy to add new routes, pages, and API endpoints.
4. **Clarity:** Folder names and structure follow Next.js conventions for easier onboarding.
5. **Consistency:** TypeScript and naming conventions applied across modules.

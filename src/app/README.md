# App Directory (`app/`)

Contains all routes using Next.js App Router.

## Structure

- `layout.tsx`: Root layout shared across pages.
- `page.tsx`: Entry page for the route.
- `api/`: API routes.
    - Each folder represents a route with a `route.ts` file.
    - Example: `api/users/route.ts` defines `/api/users`.
- Route folders can contain their own `components/` for local UI components.

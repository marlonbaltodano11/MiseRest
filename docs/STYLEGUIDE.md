# Style Guide – Next.js 13+ Project

This guide defines coding conventions, folder structure practices, and standards for the project to ensure consistency, readability, and maintainability across the team.

---

## 1. **Folder Structure Conventions**

- **`src/app/`**
    - Pages and route folders follow App Router conventions.
    - Each route can have a `page.tsx`, optional `layout.tsx`, and `components/` for local components.
    - API routes must have `route.ts` inside a folder matching the endpoint name.

- **`src/components/`**
    - Reusable global components.
    - Use PascalCase for component file names (e.g., `Button.tsx`).

- **`src/lib/`**
    - Utilities, helper functions, API clients, database clients.
    - Avoid UI logic here.

- **`src/hooks/`**
    - Custom hooks.
    - File naming: `use<Name>.ts` (e.g., `useAuth.ts`).

- **`src/context/`**
    - React context providers for global state.
    - Each file exports the provider and a custom hook.

- **`src/types/`**
    - Global TypeScript types and interfaces.

- **`src/styles/`**
    - Global styles: `globals.css`.
    - Component-level styles: CSS Modules (`*.module.css`).

---

## 2. **Naming Conventions**

| Type              | Convention                      | Example                     |
| ----------------- | ------------------------------- | --------------------------- |
| Components        | PascalCase                      | `Navbar.tsx`, `Card.tsx`    |
| React Hooks       | `useCamelCase`                  | `useAuth.ts`                |
| Context Providers | PascalCase + `Context`          | `AuthContext.tsx`           |
| API Routes        | snake-case folders + `route.ts` | `api/users/route.ts`        |
| Files (general)   | kebab-case or PascalCase        | `fetcher.ts`, `Button.tsx`  |
| CSS Modules       | `camelCase.module.css`          | `button.module.css`         |
| Types/Interfaces  | PascalCase                      | `User.ts`, `AuthPayload.ts` |

---

## 3. **Code Style**

- **Language:** TypeScript.
- **React:** Functional components only.
- **Formatting:** Prettier and ESLint enforced.
- **Quotes:** Single quotes `'` for JS/TS.
- **Semi-colons:** Always use semicolons.
- **Line length:** 100-120 characters max.
- **Imports:** Group by:
    1. External libraries
    2. Internal utilities (`lib/`, `hooks/`, `context/`, `types/`)
    3. Components
    4. Styles

Example:

```ts
import React from "react";
import { fetcher } from "@/lib/fetcher";
import { Button } from "@/components/Button";
import styles from "./card.module.css";
```

---

## 4. **Component Guidelines**

- Keep components **small and focused** (single responsibility).
- Use props for configuration; avoid hardcoded logic.
- Components should be **reusable whenever possible**.
- Route-specific components go inside `app/<route>/components/`.
- Always type props with TypeScript.

Example:

```ts
interface ButtonProps {
  label: string;
  onClick: () => void;
}

export const Button: React.FC<ButtonProps> = ({ label, onClick }) => {
  return <button onClick={onClick}>{label}</button>;
};
```

---

## 5. **API Routes Guidelines**

- Folder name matches the endpoint.
- File must be named `route.ts`.
- Export functions for HTTP methods: `GET`, `POST`, etc.
- Keep handlers small; delegate logic to `lib/` functions.

Example:

```ts
// src/app/api/users/route.ts
import { NextResponse } from "next/server";
import { getUsers } from "@/lib/users";

export async function GET() {
    const users = await getUsers();
    return NextResponse.json(users);
}
```

---

## 6. **Hooks Guidelines**

- Prefix with `use`.
- Should encapsulate reusable logic, not UI.
- Return data and functions in an object for clarity.

Example:

```ts
export function useAuth() {
    const [user, setUser] = React.useState<User | null>(null);

    const login = async (credentials: LoginPayload) => {
        const user = await fetcher("/api/auth/login", credentials);
        setUser(user);
    };

    return { user, login };
}
```

---

## 7. **Context Guidelines**

- Each context exports provider + hook for consumption.
- Keep state minimal; avoid storing large objects unnecessarily.

Example:

```ts
const AuthContext = React.createContext<AuthContextType | undefined>(undefined);

export const AuthProvider: React.FC = ({ children }) => {
  const [user, setUser] = React.useState<User | null>(null);
  return <AuthContext.Provider value={{ user, setUser }}>{children}</AuthContext.Provider>;
};

export const useAuthContext = () => React.useContext(AuthContext);
```

---

## 8. **Testing Guidelines**

- Use **Jest** and **React Testing Library** for unit and component tests.
- Test files mirror component paths: `Button.test.tsx`.
- Use descriptive test names and cover critical paths.

---

## 9. **Miscellaneous Conventions**

- **Comments:** Only explain **why**, not **what**.
- **Error handling:** Always catch errors in API routes and async functions.
- **Environment variables:** Use `.env` with `NEXT_PUBLIC_` prefix for frontend variables.
- **Strict TypeScript:** Enable `strict` mode in `tsconfig.json`.

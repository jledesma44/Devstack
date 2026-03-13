# Devstack

A developer knowledge hub for snippets, command, prompts, notes, files, images, links,and custom types.

## Commands

- `npm run dev` — start dev server at <http://localhost:3000>
- `npm run build` — production build (must pass before committing)
- `npm run lint` — run ESLint
- `npm run start` — run production server

## Context Files

Read the following to get the full context of the project:

- @context/project-overview.md
- @context/coding-standards.md
- @context/ai-interactions.md
- @context/current-feature.md

## Architecture

### Framework & Config

- **Next.js 16** with App Router (`src/app/`) — server components by default
- **React 19** with React Compiler enabled (`reactCompiler: true` in `next.config.ts`)
- **TypeScript** strict mode; path alias `@/*` → `src/*`
- **Tailwind CSS v4** — configured via CSS only (`src/app/globals.css`); **no `tailwind.config.js/ts`**
  - Theme customization goes in `@theme {}` block inside `globals.css`

### Planned Stack (not yet installed)

- **Database**: Neon PostgreSQL + Prisma ORM
- **Auth**: NextAuth v5 (email + GitHub OAuth)
- **UI components**: shadcn/ui
- **File storage**: Cloudflare R2
- **AI**: OpenAI gpt-5-nano
- **Payments**: Stripe

### File Organization (follow as features are added)

```
src/
  app/          # Next.js App Router pages and layouts
  components/   # [feature]/ComponentName.tsx
  actions/      # Server Actions — [feature].ts
  types/        # TypeScript types — [feature].ts
  lib/          # Utilities — [utility].ts
```

### Key Conventions

- `'use client'` only when needed (interactivity, hooks, browser APIs)
- Server Actions for mutations; API routes only for webhooks, file uploads, or external integrations
- Prisma migrations via `prisma migrate dev` (not `db push`)
- Return shape from Server Actions: `{ success, data, error }`

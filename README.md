# Frontend Scaffold Playbook

A lightweight AI-guided playbook for creating consistent Next.js frontend scaffold projects.

This repository is intentionally designed to work in **README-only mode**. An AI coding assistant should be able to read this file, ask the right questions, create a scaffold specification, generate a new project, and verify the result.

Use this with AI coding assistants such as ChatGPT Codex, Claude Code, GitHub Copilot, Cursor, or similar tools.

---

## Purpose

This repo helps an AI coding assistant create a frontend scaffold in a repeatable and controlled way.

The AI should not immediately generate code. It should first:

1. Read this README.
2. Ask scaffold questions.
3. Create `scaffold-spec.md`.
4. Follow the 9-step generation playbook.
5. Verify the generated project.
6. Produce a handoff summary.

The goal is to reduce AI guessing and avoid over-engineering.

---

## Default Stack

| Area | Technology |
| --- | --- |
| Framework | Next.js App Router |
| UI Runtime | React |
| Language | TypeScript |
| Styling | Tailwind CSS |
| UI Components | shadcn/ui |
| Icons | lucide-react |
| Forms | React Hook Form |
| Validation | Zod |
| Server State | TanStack Query |
| Client State | Zustand |
| Authentication | MSAL.js / Azure MSAL |

Default libraries:

```text
next
react
react-dom
typescript
tailwindcss
shadcn/ui
lucide-react
react-hook-form
zod
@hookform/resolvers
@tanstack/react-query
zustand
@azure/msal-browser
@azure/msal-react
```

---

## Expected Output

The generated frontend project should include:

- Next.js App Router setup
- TypeScript setup
- Tailwind CSS setup
- shadcn/ui setup
- Basic app shell layout
- Initial pages from `scaffold-spec.md`
- Clean folder structure
- `.env.example`
- Root `AGENTS.md` with AI behavioral guidelines
- Optional `.github/copilot-instructions.md` if GitHub Copilot is used
- Optional `.agents/*` context files if the project needs stronger AI guidance
- Local verification result

Keep the scaffold small. Do not generate full business features unless explicitly requested.

---

## Recommended AI Workflow

```text
User
  ↓
AI reads this README
  ↓
AI asks scaffold questions
  ↓
AI creates scaffold-spec.md
  ↓
AI initializes the Next.js project
  ↓
AI installs dependencies and initializes shadcn/ui
  ↓
AI optionally applies agent skills
  ↓
AI skips or documents the database schema step
  ↓
AI creates only necessary AI context files
  ↓
AI creates the frontend folder structure and app shell
  ↓
AI applies AI Code Discipline
  ↓
AI runs verification checks
  ↓
AI summarizes generated output
```

The AI must not start generating code before asking the required scaffold questions, unless the user has already provided enough information.

---

## Scaffold Questions

Ask only what is needed. Do not ask questions that the user has already answered.

### 1. Project Identity

- What is the project name?
- What is the short description of the app?
- Is this for POC, MVP, or production?
- Is this an internal app or customer-facing app?

### 2. Application Type

Choose one or more:

- Internal dashboard
- Admin portal
- Review / approval workflow
- AI-assisted workflow
- Data management app
- Public website
- Other

### 3. Stack

- Use the default stack from this playbook?
- Any library to add?
- Any library to avoid?
- Preferred package manager: npm, pnpm, yarn, or bun?

### 4. Authentication

- Does the app need authentication?
- Should it use Azure MSAL?
- Are roles required now?
- For POC, should admin users be hard-coded by email?

Default enterprise assumption:

```text
Azure MSAL authentication is required.
Dynamic role management is optional.
For POC, hard-coded admin emails are acceptable if documented clearly.
```

### 5. Backend Integration

- Is there a backend API?
- What is the API base URL?
- Is OpenAPI / Swagger available?
- Should the scaffold include a mock API layer?
- What is the standard API response format?

### 6. Pages and Features

- What pages should be created initially?
- Which page is the landing page after login?
- What feature modules are needed for the initial scaffold?

Example pages:

- Dashboard
- Upload
- Review Result
- History
- Settings

### 7. UI Direction

- Preferred UI style?
  - Clean enterprise
  - Premium dashboard
  - Minimal SaaS
  - Clinical / compliance
  - Developer tool
- Sidebar layout or top navigation?
- Dark mode required?
- Any brand color?

### 8. Deployment Target

- Local only
- Docker
- AKS
- Vercel
- Static hosting
- Other

Also ask only if relevant:

- Is a Dockerfile needed?
- Is CI/CD needed now?

---

## Scaffold Specification

After asking questions, create `scaffold-spec.md` before generating code.

Suggested format:

```md
# Scaffold Specification

## Project Identity

- Project name:
- Description:
- Phase:
- Audience:
- Application type:

## Selected Stack

- Framework:
- Language:
- Styling:
- UI components:
- Icons:
- Forms:
- Validation:
- Server state:
- Client state:
- Auth:
- Package manager:

## Architecture Decisions

- Routing:
- Folder structure:
- Auth strategy:
- API strategy:
- State management strategy:
- Styling strategy:

## Backend and Data Ownership

- Backend owner:
- API base URL:
- OpenAPI / Swagger available:
- Database owned by frontend project: No
- Database schema required in this scaffold: No

## Initial Pages

- `/`
- `/dashboard`
- `/settings`

## Initial Features

- App shell
- Auth preparation
- API client placeholder
- Query provider
- Layout components

## Environment Variables

```env
NEXT_PUBLIC_APP_NAME=
NEXT_PUBLIC_API_BASE_URL=
NEXT_PUBLIC_AZURE_AD_CLIENT_ID=
NEXT_PUBLIC_AZURE_AD_TENANT_ID=
NEXT_PUBLIC_AZURE_AD_REDIRECT_URI=
```

## Assumptions

-
-
-

## Out of Scope

-
-
-


---

## 9-Step Generation Playbook

After creating `scaffold-spec.md`, follow these steps.

| Step | Name | Status | Purpose |
| --- | --- | --- | --- |
| 1 | Initialize Next.js Project | Required | Create the base project using the official generator. |
| 2 | Install Core Dependencies | Required | Lock the selected frontend stack in `package.json`. |
| 3 | Initialize shadcn/ui | Required | Set up the base UI component system. |
| 4 | Apply Agent Skills | Optional / Recommended | Run external AI skill CLIs only if available. |
| 5 | Database Schema First | Skipped / Optional | Skip for frontend-only scaffolds. Document backend ownership instead. |
| 6 | Create AI Context Files | Recommended | Create only the AI instruction files that are useful for this project. |
| 7 | Create Folder Structure | Required | Create the agreed frontend architecture. |
| 8 | Create Core App Shell | Required | Create providers, layout, initial pages, and `.env.example`. |
| 9 | AI Code Discipline, Verification, and Handoff | Required | Apply behavioral rules, run checks, and summarize the result. |

---

### Step 1: Initialize Next.js Project

Use the official Next.js generator.

```bash
npx create-next-app@latest {{project_name}} \
  --typescript \
  --tailwind \
  --eslint \
  --app \
  --src-dir \
  --import-alias "@/*"
```

Why this matters:

- App Router is enabled from the start.
- TypeScript is enabled from the start.
- Tailwind CSS is installed from the start.
- `src/` directory is used consistently.
- `@/*` import alias avoids messy relative imports.

Adjust the command if the user selected another package manager.

---

### Step 2: Install Core Dependencies

Install the selected frontend libraries before generating feature code.

Default command:

```bash
npm install \
  lucide-react \
  react-hook-form \
  zod \
  @hookform/resolvers \
  @tanstack/react-query \
  zustand \
  clsx \
  tailwind-merge \
  class-variance-authority \
  next-themes \
  @azure/msal-browser \
  @azure/msal-react
```

Why this matters:

- The AI can see the selected libraries in `package.json`.
- The AI is less likely to introduce unwanted libraries.
- Generated code should naturally use the approved stack.

---

### Step 3: Initialize shadcn/ui

```bash
npx shadcn@latest init
```

Recommended base components:

```bash
npx shadcn@latest add button card input textarea label form dialog dropdown-menu table badge tabs separator
```

Use shadcn/ui as the default base component system.

---

### Step 4: Apply Agent Skills

Status: **Optional / Recommended**

This step is useful when the environment allows external scaffold CLIs.

Run:

```bash
npx @dan/agent-patterns init
```

Optionally apply UI/UX skill support for AI assistants:

```bash
npx uipro init --ai all
```

If these commands are unavailable, blocked, or not desired, skip this step and continue with Step 6.

Do not treat this step as the source of truth. The required guidance should still be captured in `README.md`, `scaffold-spec.md`, and the generated `AGENTS.md`.

---

### Step 5: Database Schema First

Status: **Skipped for frontend-only scaffold**

This scaffold guide intentionally skips database schema generation because the frontend usually does not own the database.

Use this step only when the generated project owns the database or includes full-stack responsibilities.

Frontend default:

```text
The frontend does not own the database schema.
The frontend consumes backend APIs through a typed API client.
Database schema generation is out of scope for this scaffold.
```

Document backend and data ownership in `scaffold-spec.md` instead.

---

### Step 6: Create AI Context Files

Status: **Recommended**

Create only the files that are useful for the target project.

Minimum recommended file:

```text
AGENTS.md
```

Optional files:

```text
.github/copilot-instructions.md
.agents/CONTEXT.md
.agents/DESIGN_SYSTEM.md
.agents/FOLDER_STRUCTURE.md
.agents/CODING_RULES.md
.agents/API_CONTRACT.md
.agents/AUTH_SPEC.md
```

Rules:

- `AGENTS.md` should include the AI Behavioral Guidelines from Step 9.
- `.github/copilot-instructions.md` is useful only if GitHub Copilot is used.
- `.agents/*` files are useful when the project needs stronger AI guidance or will be maintained by multiple AI assistants.
- Do not create unused documentation files just to fill a structure.

---

### Step 7: Create Folder Structure

Recommended structure:

```text
src/
├── app/
│   ├── layout.tsx
│   ├── page.tsx
│   ├── providers.tsx
│   ├── globals.css
│   ├── dashboard/
│   │   └── page.tsx
│   └── settings/
│       └── page.tsx
│
├── components/
│   ├── ui/
│   ├── layout/
│   └── shared/
│
├── features/
│   ├── auth/
│   ├── dashboard/
│   └── settings/
│
├── hooks/
├── lib/
│   ├── api/
│   ├── auth/
│   ├── query-client.ts
│   └── utils.ts
│
├── stores/
├── types/
├── constants/
└── config/
```

Naming conventions:

- Components: PascalCase
- Hooks: camelCase prefix `use`
- Stores: camelCase suffix `Store`
- Folders: kebab-case

Folder rules:

- `components/ui` is reserved for shadcn/ui components.
- `components/layout` is for shell, sidebar, header, and navigation.
- `components/shared` is for reusable project components.
- `features/*` is for feature-specific components, hooks, schemas, and types.
- `lib/api` is for API client and fetcher logic.
- `lib/auth` is for Azure MSAL setup.
- `stores` is for Zustand stores.
- `types` is for shared TypeScript types.

---

### Step 8: Create Core App Shell

Create only the basic app shell required for the scaffold.

Core files:

```text
src/app/providers.tsx
src/lib/query-client.ts
src/lib/auth/msal-config.ts
src/lib/api/client.ts
src/components/layout/app-shell.tsx
src/components/layout/sidebar.tsx
src/components/layout/topbar.tsx
src/components/layout/nav-items.tsx
.env.example
```

Default pages:

```text
/
/dashboard
/settings
```

Each page should include:

- Clear title
- Short description
- Placeholder content
- Basic layout using shadcn/ui cards

Default `.env.example`:

```env
NEXT_PUBLIC_APP_NAME=
NEXT_PUBLIC_API_BASE_URL=http://localhost:8000
NEXT_PUBLIC_AZURE_AD_CLIENT_ID=
NEXT_PUBLIC_AZURE_AD_TENANT_ID=
NEXT_PUBLIC_AZURE_AD_REDIRECT_URI=http://localhost:3000/auth/callback
```

---

### Step 9: AI Code Discipline, Verification, and Handoff

Before generating or modifying scaffold code, apply the AI behavioral guidelines below.

These guidelines should also be written into the generated project's root `AGENTS.md` file.

Recommended `AGENTS.md` baseline:

```md
# AGENTS.md

## AI Behavioral Guidelines

### 1. Think Before Coding

- State assumptions explicitly. If uncertain, ask.
- If multiple interpretations exist, present them — don't pick silently.
- If a simpler approach exists, say so. Push back when warranted.
- If something is unclear, stop. Name what's confusing. Ask.

### 2. Simplicity First

- No features beyond what was asked.
- No abstractions for single-use code.
- No "flexibility" or "configurability" that wasn't requested.
- No error handling for impossible scenarios.
- If you write 200 lines and it could be 50, rewrite it.

### 3. Surgical Changes

- Don't "improve" adjacent code, comments, or formatting.
- Don't refactor things that aren't broken.
- Match existing style, even if you'd do it differently.
- Remove imports, variables, and functions that your changes made unused.
- Don't remove pre-existing dead code unless asked.

### 4. Goal-Driven Execution

- Transform tasks into verifiable goals:
  - "Add validation" → "Write tests for invalid inputs, then make them pass"
  - "Fix the bug" → "Write a test that reproduces it, then make it pass"
  - "Refactor X" → "Ensure tests pass before and after"
- For multi-step tasks, state a brief plan with verification checks.
```

Run verification:

```bash
npm run lint
npm run build
npm run dev
```

Fix issues related to:

- TypeScript errors
- ESLint errors
- Missing imports
- Broken aliases
- Invalid client/server component usage
- Missing environment variables

Final handoff summary should include:

- Project name
- Stack used
- Dependencies installed
- Agent skills applied or skipped
- Database step status: skipped or applied
- Folder structure created
- Key files created
- Commands used
- Verification result
- Assumptions
- Recommended next prompt

---

## Coding Rules for Generated Projects

### General

- Use TypeScript.
- Do not use `any`.
- Use named exports.
- Use `@/*` imports.
- Keep files small and focused.
- Do not introduce new dependencies unless requested.

### Next.js

- Use App Router only.
- Do not use Pages Router.
- Prefer Server Components by default.
- Add `"use client"` only when required.

### React

- Use functional components.
- Keep business logic out of UI components.
- Extract reusable hooks only when useful.

### Styling

- Use Tailwind CSS.
- Use shadcn/ui components.
- Use `cn()` for conditional classes.
- Do not create random CSS files unless necessary.

### Forms

- Use React Hook Form.
- Use Zod for validation.
- Use `@hookform/resolvers/zod`.

### Server State

- Use TanStack Query.
- Do not fetch directly inside visual components.

### Client State

- Use Zustand only for lightweight UI state.
- Do not use Redux unless explicitly requested.

### Authentication

- Keep auth config in `src/lib/auth`.
- Do not hard-code secrets.
- Use environment variables.
- For POC, hard-coded admin emails are acceptable only if documented clearly.

---

## Recommended First Prompt

```text
You are a senior frontend architect and AI scaffold assistant.

Read README.md first.

Do not generate code yet.

First, ask me the scaffold questions from the README in grouped sections.

After I answer, summarize my answers into scaffold-spec.md.

Then follow the 9-step Generation Playbook in README.md to create the frontend scaffold project.

Use the default stack unless I explicitly override it.

Keep the scaffold small and avoid over-engineering.
```

---

## Recommended Prompt After User Answers

```text
Based on my answers, create scaffold-spec.md first.

Then generate the Next.js frontend scaffold by following the 9-step Generation Playbook.

Apply Agent Skills only if the commands are available:

npx @dan/agent-patterns init
npx uipro init --ai all

Skip the Database Schema First step unless this project owns the database or I explicitly ask for full-stack setup.

Create AGENTS.md with the AI Behavioral Guidelines from Step 9.

Do not skip verification.

At the end, provide a handoff summary including files created, dependencies installed, commands used, verification result, and remaining assumptions.
```

---

## Positioning

This repository is best described as:

> A lightweight AI-guided frontend scaffold playbook for generating consistent Next.js applications through structured questions, scaffold specifications, and repeatable generation steps.

It is useful for:

- Internal enterprise apps
- POC web applications
- Admin portals
- AI-assisted review workflows
- Dashboard-style applications
- Reusable frontend architecture setup
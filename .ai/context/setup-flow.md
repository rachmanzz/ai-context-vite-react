# Setup Flow

This document defines the step-by-step flow for setting up a new project. Follow these instructions in order.

## 1. Check Existing Clarification

Look inside `.ai/clarification/` for these files:
- `project-setup.md` — contains answers from `@.ai/quest/setup.md`
- `project-learning.md` — contains answers from `@.ai/quest/learning.md`

### If both files exist AND contain complete answers:
- Skip all questions
- Read their contents and use them directly
- Proceed to step 3

### If either file is missing or incomplete:
- Ask the user the questions from `@.ai/quest/setup.md`
- Ask the user the questions from `@.ai/quest/learning.md`
- Generate `./.ai/clarification/project-setup.md` with the answers
- Generate `./.ai/clarification/project-learning.md` with the answers
- Proceed to step 2

## 2. Validate Clarification

Confirm the generated files are saved correctly in `.ai/clarification/`.

## 3. Check Vite Installation

Check if Vite is already installed in the project:
- Look for `vite.config.ts` or `vite.config.js` in the project root
- Check `package.json` for `vite` in `devDependencies` or `dependencies`

### If Vite is NOT installed:
- Read `@.ai/context/skills/vite-react-setup.md` for scaffolding instructions
- Follow the guide to create a new Vite + React + TypeScript project

### If Vite IS already installed:
- Skip scaffolding
- Proceed to step 4

## 4. Read Clarification Context

Read the following clarification files:
- `.ai/clarification/project-setup.md`
- `.ai/clarification/project-learning.md`

Extract:
- **Package Manager** (bun, npm, yarn, deno)
- **Additional Libraries** list

## 5. Standardize Package Manager Across Context

Search all `.ai/context/` files for any hardcoded package manager commands (bun, npm, yarn, deno).

Replace EVERY occurrence of a different package manager with the one specified in `project-setup.md`.

**Rules:**
- ONLY modify package manager references (e.g., `bun add` → `npm install`, `bun run` → `npm run`)
- Do NOT change any other content in those files
- This standardization happens ONLY at the beginning of setup

## 6. Install Additional Libraries

Read the `Additional Libraries` field from `.ai/clarification/project-setup.md`.

For each library listed:
- Install using the standardized package manager
- Example: if package manager is `npm`, run `npm install <library-name>`
- Example: if package manager is `bun`, run `bun add <library-name>`

## 7. Install Required Stack Libraries

Based on `project-learning.md`, install the agreed tech stack if not already present:

Common examples:
- `tailwindcss @tailwindcss/vite` — always needed
- State management (e.g., `zustand`, `@reduxjs/toolkit`, etc.)
- Routing (e.g., `@tanstack/react-router`, `react-router-dom`)
- Data fetching (e.g., `@tanstack/react-query`)
- UI components (e.g., `shadcn` via `npx shadcn init`)
- Validation (e.g., `zod`, `react-hook-form`)

## 8. Verify Setup

- Confirm `package.json` contains all expected dependencies
- Confirm `vite.config.ts` exists and is configured
- Run a dry build or dev server check to ensure no errors

## 9. Check API Documentation

Check `.ai/work/api.docs.md`:
- If it contains real API documentation (content beyond the placeholder `[ do not delete this line... ]`), proceed to step 10
- If it is empty or only has the placeholder line:
  - Ask the user: **"Do you want to add API documentation first? You'll need to manually edit `.ai/work/api.docs.md`."**
  - **If yes**: Say "I will stop execution. After you fill in the API docs, type `lanjutkan eksekusi` to continue." Then STOP — do not proceed further. Wait for the user to type `lanjutkan eksekusi` before continuing.
  - **If no**: Proceed to step 10 without API docs. During implementation, create mock data on the frontend side as needed.

## 10. Create Workflow & Strategy

Create or update these files:

### `.ai/work/workflow.md`
- Write a step-by-step execution plan based on the project learning context
- Each step must be clearly defined and validated before moving to the next

### `.ai/work/strategy.md`
- Document the implementation strategy based on facts (not assumptions)
- Reference `.ai/work/api.docs.md` if it exists with real content
- If no API docs exist, note that frontend mocking will be used
- Wait for user validation of the strategy before executing

## 11. Execute Strategy

- After the user validates the strategy, implement the frontend features
- If API endpoints are not yet available, create mock data/functions on the frontend side to demonstrate functionality
- Ensure all components, state management, and API service layers are properly connected
- Run final checks to confirm no errors were introduced

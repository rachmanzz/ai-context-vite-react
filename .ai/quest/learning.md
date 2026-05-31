# Project Learning Quest

AI **must** ask these questions to deeply understand the project before generating a learning document.

## Questions

### 1. Project Overview
- What is the core purpose of this project?
- Who are the target users?
- What problem does it solve?

### 2. Tech Stack
- Framework: React
- Build tool: Vite
- Language: TypeScript
- Styling: Tailwind CSS
- State management: Zustand, Redux, Context API, or none? (required)
- PWA support needed?

### 3. Architecture & Data Flow
- How does data flow within the app? (e.g., component → state → API → render)
- Any key architectural decisions? (e.g., PWA, offline-first, encryption, Web Workers)
- Authentication flow: JWT, session, OAuth, passphrase-based, or none?

### 4. Security & Privacy
- Storage: IndexedDB, localStorage, session-only (Zustand), or none?

### 5. API & Backend
- REST API (no other choice)
- What endpoints does the frontend consume?

### 6. Key Business Logic
- What are the core features/modules?
- Any complex algorithms or validations?

### 7. Deployment & Infrastructure
- Platform: Vercel, Cloudflare, Docker, self-hosted?
- Environment variables needed?
- CI/CD setup?

## Example User Clarification

```
Project Overview: Frontend for task management dashboard with real-time collaboration
Tech Stack: React 19, Vite 8, TypeScript, Tailwind CSS v4, Zustand
Architecture: SPA with Zustand state management, JWT auth, localStorage caching
Security: JWT token stored in memory, no encryption at rest
API: REST with axios interceptors for auth and error handling
Deployment: Vercel with environment variables for API base URL
```

## Output

After user answers, AI creates `./.ai/clarification/project-learning.md` with the filled template:

```markdown
# Project Learning: [Project Name]

## Main Principles

### 1. ...
### 2. ...
### 3. ...

---

## Data Flow

### Feature A
```
flow diagram
```

### Feature B
```
flow diagram
```

---

## Storage Architecture

### Storage Type
```typescript
{
  key: value,
}
```

---

## Key Business Logic

---

```

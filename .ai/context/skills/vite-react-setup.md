# Vite React Setup Skill

Vite version: 8.x+

This skill defines the standard procedure for scaffolding a new Vite React project.

## Scaffold Project

Choose your package manager:

```bash
# bun (preferred)
bun create vite ./ --template react-ts

# deno
deno init --npm vite

# yarn
yarn create vite ./ --template react-ts

# npm
npm create vite@latest ./ -- --template react-ts
```

## Install Dependencies

```bash
bun install
```

## Recommended First Steps

After scaffold, install core tooling:

```bash
# Tailwind CSS
bun add tailwindcss @tailwindcss/vite

# TypeScript types
bun add -D @types/node
```

## Dev Server

```bash
bun run dev
```

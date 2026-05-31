# Tailwind CSS Setup Skill

Tailwind support version: 4.3+

This skill defines the standard procedure for setting up Tailwind CSS 4.3+ in a Vite-based React project, optimized for visual excellence and modern CSS features.

## Prerequisites
- Vite-based project (React/TypeScript preferred)
- Node.js environment with `bun` (preferred) or `npm`

## Installation
Install the core Tailwind packages and the Vite plugin:

```bash
bun add tailwindcss @tailwindcss/vite
```

## Configuration

### 1. Vite Integration
Update `vite.config.ts` to include the Tailwind plugin:

```typescript
import { defineConfig } from 'vite'
import tailwindcss from '@tailwindcss/vite'

export default defineConfig({
  plugins: [
    tailwindcss(),
  ],
})
```

### 2. CSS Entry Point
In your main CSS file (e.g., `src/index.css`), import Tailwind:

```css
@import "tailwindcss";

/* Optional: Shadcn integration if used */
/* @import "shadcn/tailwind.css"; */
```

## Best Practices
- **OKLCH Colors**: Use `oklch` for more consistent and vibrant colors across different displays.
- **Modern CSS**: Favor standard CSS features and variables over complex Tailwind configuration files.
- **Visual Polish**: Use Tailwind's utility classes to implement refined shadows, transitions, and interactive states (hover, focus, active).
- **Dark Mode**: Use the `@custom-variant dark (&:is(.dark *));` pattern or the standard `dark:` variant for consistent dark mode implementation.

## Validation
- Verify that Tailwind classes are being processed correctly by checking for generated styles in the browser's developer tools.
- Ensure that custom theme variables are correctly applied to the UI elements.

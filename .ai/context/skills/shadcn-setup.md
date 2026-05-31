# Shadcn Setup Skill

Shadcn version: 4.x+
Style: Radix Nova
Tailwind version: 4.3+

This skill defines the standard procedure for setting up shadcn in a Vite-based React project.

> **Note:** `baseUrl` in tsconfig is deprecated in TypeScript 5.5+. Use `paths` directly instead.

## AI Interaction Flow

Before starting setup, AI **must** ask the user:

1. **"Do you want to use a shadcn preset?"**
   - If yes: ask the user to open https://ui.shadcn.com/create?template=vite and customize the theme.
   - **Note:** AI currently only handles **radix-ui** based themes. If the user chooses base-ui, some components may be misconfigured.
   - Ask the user to copy the preset code (either just the code or the full command) and paste it into the prompt.
   - Once the code is provided, proceed to the init step.

2. If no preset, use the default init command below.

## Prerequisites
- Vite-based project (React/TypeScript)
- Tailwind CSS 4.3+ already configured (see `tailwind-setup.md`)
- Node.js environment with `bun` (preferred) or `npm`

### 1. tsconfig Paths (No baseUrl)

In `tsconfig.json` (root solution file), set up project references and paths:

```json
{
  "files": [],
  "references": [
    { "path": "./tsconfig.app.json" },
    { "path": "./tsconfig.node.json" }
  ],
  "compilerOptions": {
    "paths": {
      "@/*": ["./src/*"]
    }
  }
}
```

In `tsconfig.app.json`, add paths WITHOUT `baseUrl`:

```json
{
  "compilerOptions": {
    "paths": {
      "@/*": ["./src/*"]
    }
  },
  "include": ["src"]
}
```

> **Why no `baseUrl`?** TypeScript 5.5+ deprecated `baseUrl`. Paths are resolved relative to the tsconfig file location, so `"./src/*"` works correctly without it.

### 2. Vite Resolve Alias

In `vite.config.ts`, add the `@` alias so Vite resolves imports at build time:

```typescript
import { resolve } from 'path'

export default defineConfig({
  resolve: {
    alias: {
      '@': resolve(__dirname, 'src'),
    },
  },
  // ...
})
```

## Init

- **With preset** (user provided code): `bunx --bun shadcn@latest init --preset [CODE] --template vite`
- **Without preset** (default): `bunx --bun shadcn@latest init --preset b0 --template vite --pointer`

This auto-generates:
- `components.json` in project root
- CSS `@import` statements in `src/index.css` (`tw-animate-css`, `shadcn/tailwind.css`)
- `@custom-variant dark` and `@theme inline` in `src/index.css`
- `src/lib/utils.ts` with `cn()` utility

## Available Components

All components are installed via `bun shadcn add <name>` to `src/components/ui/`.

| Component | Description |
|-----------|-------------|
| Accordion | Collapsible stacked sections for displaying content |
| Alert | Notification banner for important messages |
| Alert Dialog | Modal dialog for confirmations/alerts |
| Aspect Ratio | Container with fixed aspect ratio |
| Avatar | User profile image component |
| Badge | Small label for status/counts |
| Breadcrumb | Navigation trail showing page hierarchy |
| Button | Interactive button with variants/sizes |
| Button Group | Grouped button layout |
| Calendar | Date calendar picker |
| Card | Content container with header/body/footer |
| Carousel | Sliding image/content carousel |
| Chart | Data visualization charts |
| Checkbox | Multi-select input control |
| Collapsible | Expandable/collapsible content area |
| Combobox | Autocomplete input with dropdown |
| Command | Command palette / search interface |
| Context Menu | Right-click context menu |
| Data Table | Sortable, filterable table with pagination |
| Date Picker | Date selection component |
| Dialog | Modal overlay dialog |
| Drawer | Slide-out panel (mobile-friendly) |
| Dropdown Menu | Click-triggered dropdown menu |
| Empty | Empty state placeholder |
| Field | Form field wrapper with label/error/message |
| Hover Card | Preview card on hover |
| Input | Text input field |
| Input Group | Grouped input with addons |
| Input OTP | One-time password input |
| Kbd | Keyboard key visual indicator |
| Label | Form label component |
| Menubar | Horizontal menu bar |
| Native Select | Native browser select dropdown |
| Navigation Menu | Responsive navigation menu |
| Pagination | Page navigation control |
| Popover | Floating content popup |
| Progress | Progress/loading bar |
| Radio Group | Single-select radio button group |
| Resizable | Draggable panel resizer |
| Scroll Area | Custom scrollbar container |
| Select | Custom styled select dropdown |
| Separator | Horizontal/vertical divider |
| Sheet | Slide-in panel (like Drawer) |
| Sidebar | Application sidebar navigation |
| Skeleton | Loading placeholder |
| Slider | Range slider input |
| Sonner | Toast notification (via sonner) |
| Spinner | Loading spinner indicator |
| Switch | Toggle switch control |
| Table | Data table layout |
| Tabs | Tabbed content panels |
| Textarea | Multi-line text input |
| Toast | Notification toast (alternative) |
| Toggle | On/off toggle button |
| Toggle Group | Grouped toggle buttons |
| Tooltip | Tooltip on hover |
| Typography | Text/heading style utilities |

## Validation
- Run `bun tsc` and verify no path resolution errors.
- Run `bun run build` and verify Vite resolves `@/` imports.
- Import and render a shadcn component to verify styling works (dark/light mode, animations).

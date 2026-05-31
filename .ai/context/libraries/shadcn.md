# UI Library Standards: Shadcn UI & Tailwind CSS

This document defines the standards for UI development within the Project, focusing on visual excellence, accessibility, and performance.

## Core Stack
- **Styling**: Tailwind CSS 4.3+
- **Components**: Shadcn UI (Latest)
- **State & Navigation**: TanStack Query & TanStack Router (Preferred)

## Implementation Rules

### 1. Component Usage
- **Shadcn First**: Always prefer Shadcn components for UI elements. 
- **Visual Polish**: Every component should be styled to look "cool" and modern. Use gradients, shadows, and refined typography where appropriate.
- **Table Constraint**: **STRICT RULE**: Do not use complex `data-table` abstractions unless explicitly requested. Use standard `Table` components.
- **Consistency**: Maintain a cohesive visual language across the entire application.

### 2. Integration with State Management
- **Asynchronous States**: Use established state management (e.g., TanStack Query) for loading states within UI components (e.g., Skeleton loaders).
- **Navigation**: Use the project's router for all navigation between views.

### 3. Accessibility & UX
- **ARIA Compliance**: Ensure all components maintain accessibility.
- **Interactive Feedback**: Provide visual feedback for all user actions (hover states, loading spinners, success toasts).
- **Responsive Design**: Ensure the UI looks great across all device sizes.

### 4. Tailwind Usage
- **Modern Features**: Utilize latest Tailwind CSS features.
- **Customization**: Use the Tailwind configuration to define a polished color palette and theme tokens.

By adhering to these standards, we ensure the Project has a professional, accessible, and stunning interface.

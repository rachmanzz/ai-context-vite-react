# TanStack Query Setup Skill

TanStack Query version: 5.x

This skill defines the standard procedure for setting up TanStack Query (React Query) in a Vite-based React project.

## Prerequisites
- Vite-based project (React/TypeScript)
- shadcn set up (optional, for UI integration)

## Installation

```bash
bun add @tanstack/react-query
bun add -D @tanstack/eslint-plugin-query
```

## Provider Setup

Create `QueryClient` with no custom options and wrap the app:

```tsx
// src/main.tsx
import { QueryClient, QueryClientProvider } from '@tanstack/react-query'

const queryClient = new QueryClient()

root.render(
  <QueryClientProvider client={queryClient}>
    <App />
  </QueryClientProvider>
)
```

## Custom Hook Pattern

Encapsulate all queries and mutations inside custom hooks in `src/hooks/`. This keeps data-fetching logic isolated from components.

### Query Hook

```typescript
// src/hooks/use-entities.ts
import { useQuery } from '@tanstack/react-query'

export function useEntities(page = 1) {
  return useQuery({
    queryKey: ['entities', page],
    queryFn: () => listEntities(page),
  })
}

export function useEntity(id: string | undefined) {
  return useQuery({
    queryKey: ['entity', id],
    queryFn: () => getEntity(id!),
    enabled: !!id,
  })
}
```

### Mutation Hook

```typescript
// src/hooks/use-entities.ts
import { useMutation, useQueryClient } from '@tanstack/react-query'

export function useCreateEntity() {
  const queryClient = useQueryClient()

  return useMutation({
    mutationFn: (body: { name: string }) => createEntity(body),
    onSuccess: () => {
      queryClient.invalidateQueries({ queryKey: ['entities'] })
    },
  })
}

export function useDeleteEntity() {
  const queryClient = useQueryClient()

  return useMutation({
    mutationFn: (id: string) => deleteEntity(id),
    onSuccess: () => {
      queryClient.invalidateQueries({ queryKey: ['entities'] })
    },
  })
}
```

## Query Key Convention

Use inline flat arrays (no factory needed):

| Pattern | Key | Use Case |
|---------|-----|----------|
| Plural list | `['entities']` | Entity list queries |
| Paginated list | `['entities', page]` | Paginated list |
| Scoped list | `['entities', parentId, page]` | List scoped to a parent |
| Singular detail | `['entity', id]` | Single entity detail |

> **Convention:** Plural keys for lists, singular keys for details. This differentiates list vs detail queries naturally.

## Conditional Fetching

Use `enabled` to prevent queries from firing when dependencies are missing:

```typescript
export function useEntity(id: string | undefined) {
  return useQuery({
    queryKey: ['entity', id],
    queryFn: () => getEntity(id!),
    enabled: !!id,
  })
}
```

## Consuming in Components

### Queries

```tsx
function EntityList() {
  const { data, isLoading } = useEntities()

  if (isLoading) return <Skeleton />
  return data?.map(entity => <div key={entity.id}>{entity.name}</div>)
}
```

### Mutations (Async)

Use `mutateAsync` with try/catch for form submissions:

```tsx
function CreateForm({ onSuccess }: { onSuccess: () => void }) {
  const createEntity = useCreateEntity()

  async function onSubmit(data: { name: string }) {
    try {
      await createEntity.mutateAsync(data)
      onSuccess()
    } catch (error) {
      // handle error
    }
  }

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <Button type="submit" disabled={createEntity.isPending}>
        {createEntity.isPending ? 'Creating...' : 'Create'}
      </Button>
    </form>
  )
}
```

### Mutations (Fire-and-Forget)

Use `.mutate()` for delete/actions where no follow-up is needed:

```tsx
<Button onClick={() => deleteEntity.mutate(id)} disabled={deleteEntity.isPending}>
  {deleteEntity.isPending ? 'Deleting...' : 'Delete'}
</Button>
```

## Scoped Invalidation

When mutations affect resources scoped to a parent, pass the parent ID and scope invalidation:

```typescript
export function useCreateChild(parentId: string | undefined) {
  const queryClient = useQueryClient()

  return useMutation({
    mutationFn: (body: Body) => createChild(parentId!, body),
    onSuccess: () => {
      queryClient.invalidateQueries({ queryKey: ['children', parentId] })
    },
  })
}
```

## Error Handling

### Query Errors

Handle errors via the `error` return value or a global error boundary:

```tsx
const { data, isLoading, error } = useEntities()
if (error) return <div>Error: {error.message}</div>
```

### Mutation Errors

Always wrap `mutateAsync` in try/catch in forms. For `.mutate()`, attach a catch handler:

```typescript
deleteEntity.mutate(id, {
  onError: (error) => {
    toast.error(error.message)
  },
})
```

## ESLint Plugin

```bash
bun add -D @tanstack/eslint-plugin-query
```

> ESLint config is handled automatically by the project's ESLint setup.

## Validation
- Run `bun tsc` to verify types.
- Verify query keys are consistent between hooks and invalidation calls.
- Test loading, error, and success states for each query/mutation.

# React Form Setup Skill

Shadcn Form + React Hook Form + Zod

This skill defines the standard procedure for building forms using React Hook Form with shadcn Field components and Zod validation.

## Prerequisites
- shadcn already set up (see `shadcn-setup.md`)
- Field component installed (`bun shadcn add field`)

## Installation

```bash
bun add react-hook-form @hookform/resolvers zod
```

## Anatomy

Uses `useForm` from React Hook Form, `<Controller />` for controlled inputs, and shadcn `<Field />` components for layout & error display. Zod schema with `zodResolver` for validation.

```typescript
import { zodResolver } from "@hookform/resolvers/zod"
import { useForm, Controller } from "react-hook-form"
import * as z from "zod"

import {
  Field,
  FieldDescription,
  FieldError,
  FieldGroup,
  FieldLabel,
} from "@/components/ui/field"
```

## Schema & Form Setup

```typescript
const formSchema = z.object({
  title: z.string().min(5).max(32),
  description: z.string().min(20).max(100),
})

export function MyForm() {
  const form = useForm<z.infer<typeof formSchema>>({
    resolver: zodResolver(formSchema),
    defaultValues: {
      title: "",
      description: "",
    },
  })

  function onSubmit(data: z.infer<typeof formSchema>) {
    console.log(data)
  }

  return (
    <form onSubmit={form.handleSubmit(onSubmit)}>
      {/* fields */}
    </form>
  )
}
```

## Field Types

### Input
```typescript
<Controller
  name="title"
  control={form.control}
  render={({ field, fieldState }) => (
    <Field data-invalid={fieldState.invalid}>
      <FieldLabel htmlFor={field.name}>Title</FieldLabel>
      <Input {...field} id={field.name} aria-invalid={fieldState.invalid} />
      {fieldState.invalid && <FieldError errors={[fieldState.error]} />}
    </Field>
  )}
/>
```

### Textarea
```typescript
<Controller
  name="description"
  control={form.control}
  render={({ field, fieldState }) => (
    <Field data-invalid={fieldState.invalid}>
      <FieldLabel htmlFor={field.name}>Description</FieldLabel>
      <Textarea {...field} id={field.name} aria-invalid={fieldState.invalid} />
      {fieldState.invalid && <FieldError errors={[fieldState.error]} />}
    </Field>
  )}
/>
```

### Select
```typescript
<Controller
  name="language"
  control={form.control}
  render={({ field, fieldState }) => (
    <Field data-invalid={fieldState.invalid}>
      <FieldLabel htmlFor={field.name}>Language</FieldLabel>
      <Select name={field.name} value={field.value} onValueChange={field.onChange}>
        <SelectTrigger id={field.name} aria-invalid={fieldState.invalid}>
          <SelectValue placeholder="Select" />
        </SelectTrigger>
        <SelectContent>
          <SelectItem value="en">English</SelectItem>
        </SelectContent>
      </Select>
      {fieldState.invalid && <FieldError errors={[fieldState.error]} />}
    </Field>
  )}
/>
```

### Checkbox (Array)
```typescript
<Controller
  name="items"
  control={form.control}
  render={({ field, fieldState }) => (
    <FieldSet>
      <FieldLegend>Items</FieldLegend>
      <FieldGroup data-slot="checkbox-group">
        {items.map((item) => (
          <Field key={item.id} orientation="horizontal" data-invalid={fieldState.invalid}>
            <Checkbox
              id={item.id}
              checked={field.value.includes(item.id)}
              onCheckedChange={(checked) => {
                const newValue = checked
                  ? [...field.value, item.id]
                  : field.value.filter((v) => v !== item.id)
                field.onChange(newValue)
              }}
            />
            <FieldLabel htmlFor={item.id}>{item.label}</FieldLabel>
          </Field>
        ))}
      </FieldGroup>
      {fieldState.invalid && <FieldError errors={[fieldState.error]} />}
    </FieldSet>
  )}
/>
```

### Radio Group
```typescript
<Controller
  name="plan"
  control={form.control}
  render={({ field, fieldState }) => (
    <FieldSet>
      <FieldLegend>Plan</FieldLegend>
      <RadioGroup name={field.name} value={field.value} onValueChange={field.onChange}>
        {plans.map((plan) => (
          <FieldLabel key={plan.id} htmlFor={plan.id}>
            <Field orientation="horizontal" data-invalid={fieldState.invalid}>
              <FieldContent>
                <FieldTitle>{plan.title}</FieldTitle>
                <FieldDescription>{plan.description}</FieldDescription>
              </FieldContent>
              <RadioGroupItem value={plan.id} id={plan.id} aria-invalid={fieldState.invalid} />
            </Field>
          </FieldLabel>
        ))}
      </RadioGroup>
      {fieldState.invalid && <FieldError errors={[fieldState.error]} />}
    </FieldSet>
  )}
/>
```

### Switch
```typescript
<Controller
  name="twoFactor"
  control={form.control}
  render={({ field, fieldState }) => (
    <Field orientation="horizontal" data-invalid={fieldState.invalid}>
      <FieldContent>
        <FieldLabel htmlFor={field.name}>Multi-factor auth</FieldLabel>
        <FieldDescription>Enable MFA to secure your account.</FieldDescription>
        {fieldState.invalid && <FieldError errors={[fieldState.error]} />}
      </FieldContent>
      <Switch
        id={field.name}
        checked={field.value}
        onCheckedChange={field.onChange}
        aria-invalid={fieldState.invalid}
      />
    </Field>
  )}
/>
```

## Validation Modes

```typescript
const form = useForm({
  resolver: zodResolver(formSchema),
  mode: "onChange", // "onChange" | "onBlur" | "onSubmit" | "onTouched" | "all"
})
```

| Mode | Triggers |
|------|----------|
| `onSubmit` (default) | On submit |
| `onChange` | On every change |
| `onBlur` | On blur |
| `onTouched` | First blur, then every change |
| `all` | Blur and change |

## Array Fields (useFieldArray)

```typescript
import { useFieldArray } from "react-hook-form"

const { fields, append, remove } = useFieldArray({
  control: form.control,
  name: "emails",
})
```

```typescript
<FieldSet>
  <FieldLegend>Email Addresses</FieldLegend>
  <FieldGroup>
    {fields.map((field, index) => (
      <Controller
        key={field.id}
        name={`emails.${index}.address`}
        control={form.control}
        render={({ field: cf, fieldState }) => (
          <Field orientation="horizontal" data-invalid={fieldState.invalid}>
            <Input {...cf} aria-invalid={fieldState.invalid} />
            {fields.length > 1 && (
              <Button type="button" variant="ghost" onClick={() => remove(index)}>
                Remove
              </Button>
            )}
            {fieldState.invalid && <FieldError errors={[fieldState.error]} />}
          </Field>
        )}
      />
    ))}
  </FieldGroup>
  <Button type="button" variant="outline" onClick={() => append({ address: "" })}>
    Add Email
  </Button>
</FieldSet>
```

### Array Schema

```typescript
const formSchema = z.object({
  emails: z
    .array(z.object({ address: z.string().email("Invalid email.") }))
    .min(1, "Add at least one email.")
    .max(5, "Max 5 emails."),
})
```

## Reset Form

```typescript
<Button type="button" variant="outline" onClick={() => form.reset()}>
  Reset
</Button>
```

## Validation
- Run `bun tsc` to verify types.
- Test form submit with invalid data to confirm error display.
- Verify `aria-invalid` and `data-invalid` attributes are correct for accessibility.

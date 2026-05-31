# Project Setup Quest

AI **must** ask the user these questions before scaffolding:

## Questions

### 1. Project Name
- Default: folder name or `name` from `package.json` if available
- Ask: "What is the project name?"

### 2. Project Description
- Ask: "What is the project description?"

### 3. Package Manager
- Options: `bun`, `npm`, `yarn`, `deno`
- Default: `bun`
- Ask: "Which package manager to use?"

### 4. Additional Libraries
- Ask: "Any additional libraries needed? (e.g., zustand, firebase, etc.)"
- Free text input

## Example User Clarification

```
Project Name: my-awesome-app
Project Description: A modern web app for managing tasks
Package Manager: bun
Additional Libraries: zustand, firebase, @tanstack/react-query
```

## Output

After user answers, AI creates `./.ai/clarification/project-setup.md` with the filled template:

```markdown
# Project Setup Clarification

- **Project Name:** {{project-name}}
- **Project Description:** {{project-description}}
- **Package Manager:** {{package-manager}}
- **Additional Libraries:** {{additional-libraries}}
```

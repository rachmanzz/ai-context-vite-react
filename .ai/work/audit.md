# Audit Checklist

Run this audit after each execution phase to verify quality and consistency.

## Code Quality
- [ ] No TypeScript errors (`npx tsc --noEmit`)
- [ ] No lint warnings (`npx lint`)
- [ ] All imports are correct and used
- [ ] No `any` types (unless unavoidable and justified)
- [ ] Functions follow Single Responsibility Principle

## Dependencies
- [ ] No missing dependencies in `package.json`
- [ ] No unused imports or variables
- [ ] All installed libraries are actually used

## Components & UI
- [ ] Components use Shadcn where applicable
- [ ] Tailwind classes follow project conventions
- [ ] Responsive layout works across breakpoints
- [ ] Loading, empty, and error states are handled

## State & Data Flow
- [ ] State management pattern is consistent (as agreed in clarification)
- [ ] API service layer is properly abstracted
- [ ] Mock data (if used) is clearly separated from real logic

## Routing & Navigation
- [ ] All routes are defined and linked correctly
- [ ] Navigation guards / auth checks are in place (if needed)

## Build & Deploy
- [ ] `npm run build` (or equivalent) passes without errors
- [ ] Environment variables are properly typed and documented

## File Structure
- [ ] No dead code or commented-out blocks
- [ ] Files follow the established naming conventions
- [ ] Related files are grouped in the same directory

AI may also add custom audit findings beyond this checklist. These notes can capture issues, improvements, or observations that become input for the next strategy iteration.

[ do not delete this line, mark items as done with `[x]` during audit]

## Custom Audit Notes

Use this section to document additional findings discovered during audit. These findings can inform the next strategy and workflow.

### Findings
- (Add findings here as needed)

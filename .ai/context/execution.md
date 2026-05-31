# Execution and Implementation Workflow

This document establishes the mandatory protocol for developing and maintaining the Project.

## Strategy-First Requirement

A comprehensive strategy must be documented before any implementation.

1.  **Mandatory Documentation**: All proposed changes must be written to `.task/work/strategy.md`.
2.  **No Immediate Execution**: After documenting the strategy, stop and wait for a specific command to proceed.
3.  **Security & Excellence Review**: Every strategy must explicitly state how it maintains core project principles and visual/technical excellence.

## Implementation Boundaries and Standards

- **Visual Excellence**: **STRICT RULE**: Prioritize high-quality, modern, and polished UI components. Every change should contribute to a refined and interactive experience.
- **Technology Stack Consistency**: Adhere to the established technologies and APIs used in the project.
- **Integrity**: Ensure the app passes relevant audits and follows best practices for its platform.
- **Validation**: 
    - Verify that sensitive data is never logged to the console.
    - Confirm the UI remains responsive and attractive across all screen sizes.

## Build and Distribution

- **Build Tooling**: Leverage modern build tools (e.g., Vite) for fast development and optimized production builds.
- **Package Manager**: **STRICT RULE**: Always use the project's preferred package manager (e.g., `bun`) for installing dependencies and executing binaries.
- **Deployment**: Follow the established deployment pipeline.
- **Cleanup**: Delete the strategy entry from `.task/work/strategy.md` once the task is successfully implemented and verified.

By following this workflow, we maintain a controlled, transparent, and high-quality development process.

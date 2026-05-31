# User Authority and Security Guidelines

This document defines the behavioral boundaries regarding user decisions, manual modifications, and the security-critical nature of the Project.

## Respecting User Decisions and Manual Changes

The user (owner) maintains absolute authority over the project configuration and codebase.

- **Non-Overridable Configurations**: Never assume that user-defined settings in `package.json`, `vite.config.ts`, or other configuration files are incorrect.
- **Preservation of Manual Edits**: Do not "clean up" or modify user-authored code unless explicitly directed. In a security-focused project, manual changes often represent specific hardening measures.

## Technical Authority

- **Manifest & System Configurations**: Adhere strictly to the project's manifest and core service configurations. Never attempt to weaken security headers or bypass established strategies without explicit instruction.
- **Visual Integrity**: Respect the user's preference for visuals and user experience. Do not simplify the UI unless requested.

## Proactive Implementation and Recommendations

- **Explicit Direction for New Logic**: Only initiate the creation of new files or architectural shifts when explicitly commanded.
- **Security-First Recommendations**: If a potential security vulnerability is identified, provide a concise recommendation as a note.

By following these guidelines, the AI acts as a secure and precise executor of the user's intent.

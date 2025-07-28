# Coding Style Guide

This document outlines the coding standards and conventions for this project. Consistency is key to maintainability, and this guide serves as the single source of truth.

## 1. Code Formatting
-   **Tooling:** All code MUST be formatted using [Prettier](https://prettier.io/). We use the standard configuration with minimal overrides.
-   **Line Length:** Maximum line length is 80 characters.
-   **Indentation:** Use 2 spaces for indentation. Do not use tabs.

## 2. Naming Conventions
-   **Variables and Functions:** Use `camelCase`.
    -   `const maxRetries = 3;`
    -   `function calculateTotal() {}`
-   **Components (React/Vue/Svelte):** Use `PascalCase`. The filename should match the component name.
    -   `component UserProfile.tsx` -> `<UserProfile />`
-   **Constants:** Use `UPPER_SNAKE_CASE` for global or exported constants that are hard-coded and immutable.
    -   `export const API_BASE_URL = 'https://api.example.com';`
-   **Boolean Variables:** Prefix with `is`, `has`, or `should`.
    -   `const isVisible = true;`
    -   `const hasPermission = false;`

## 3. Component Design (Frontend)
-   **Props:** All props must have explicit types (using TypeScript or PropTypes).
-   **Structure:** Keep components small and focused on a single responsibility.
-   **State:** Prefer local state. Lift state up only when necessary. For complex global state, use the designated state management library.

## 4. Comments
-   Write comments for *why*, not *what*. The code should be self-explanatory about what it does. Comments should explain the reasoning behind complex or non-obvious logic.
    ```javascript
    // We fetch user data on the client-side to ensure it's always fresh,
    // even on pages that use static generation.
    useEffect(() => {
      fetchUserData();
    }, []);
    ```

## 5. Tooling and Automation
-   **Linter:** [ESLint](https://eslint.org/) is configured to enforce these rules.
-   **Pre-commit Hooks:** A pre-commit hook is set up to run the linter and formatter before any code is committed to the repository. Do not bypass these hooks.

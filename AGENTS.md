# Repository Guidelines

## Project Structure & Module Organization

- Source lives in `src/`; `src/main.tsx` mounts `<App />`, and `src/App.tsx` handles LIFF initialization and UI copy. Styles are in `src/App.css`; Vite HTML shell is `index.html`.
- LIFF requires `VITE_LIFF_ID` in a `.env` file. Vite only exposes env vars prefixed with `VITE_`; avoid committing secrets.
- Keep new components co-located with related styles/assets under `src/`, and use PascalCase filenames for React components.

## Build, Test, and Development Commands

- Install: `npm install`.
- Develop: `npm run dev` (Vite dev server; add `-- --host` if testing on device/emulator).
- Build: `npm run build` (TypeScript type-check via `tsc`, then Vite build output).
- Preview: `npm run preview` (serves the production build locally).
- Lint: `npm run lint` (ESLint on JS/TS/TSX).
- Format: `npm run format` (Prettier write on JS/TS/TSX/JSON/CSS/SCSS/MD).
- Tests: `npm test` currently exits with an error placeholder—add real tests before relying on it.

## Coding Style & Naming Conventions

- TypeScript strict; prefer typed props/state and avoid `any`.
- Formatting is enforced by Prettier (2-space indent, double quotes per current code). Run `npm run format` before commits.
- Follow React conventions: components in PascalCase, hooks in camelCase, and obey ESLint rules of hooks. Keep imports minimal and ordered logically.

## Testing Guidelines

- No tests exist yet. When adding, colocate with source (e.g., `src/__tests__/App.test.tsx`) and use descriptive test names that mirror the behavior under test.
- Aim for coverage on LIFF initialization edge cases (failed init, missing env) and render expectations. Wire new tests into `npm test` once implemented.

## Commit & Pull Request Guidelines

- Git history uses short, imperative messages (e.g., “Create a LIFF app”, “Format code using prettier”). Keep following this style.
- For PRs, include: scope/intent, key changes, how to validate (commands and expected UI states), and note any env prerequisites like `VITE_LIFF_ID`.
- Attach screenshots or brief notes for UI-facing changes, and mention any dependency or config updates.

## Environment & Configuration Tips

- Create `.env` with `VITE_LIFF_ID=<your-liff-id>` for local/dev/preview runs; do not commit secrets.
- When debugging on mobile LINE clients, run `npm run dev -- --host` and ensure the device can reach your dev host.

## Code Design Principles

Follow Robert C. Martin's SOLID and Clean Code principles:

### SOLID Principles

1. **SRP (Single Responsibility)**: One reason to change per class; separate concerns (e.g., storage vs formatting vs calculation)
2. **OCP (Open/Closed)**: Open for extension, closed for modification; use polymorphism over if/else chains
3. **LSP (Liskov Substitution)**: Subtypes must be substitutable for base types without breaking expectations
4. **ISP (Interface Segregation)**: Many specific interfaces over one general; no forced unused dependencies
5. **DIP (Dependency Inversion)**: Depend on abstractions, not concretions; inject dependencies

### Clean Code Practices

- **Naming**: Intention-revealing, pronounceable, searchable names (`daysSinceLastUpdate` not `d`)
- **Functions**: Small, single-task, verb names, 0-3 args, extract complex logic
- **Classes**: Follow SRP, high cohesion, descriptive names
- **Error Handling**: Exceptions over error codes, no null returns, provide context, try-catch-finally first
- **Testing**: TDD, one assertion/test, FIRST principles (Fast, Independent, Repeatable, Self-validating, Timely), Arrange-Act-Assert pattern
- **Code Organization**: Variables near usage, instance vars at top, public then private functions, conceptual affinity
- **Comments**: Self-documenting code preferred, explain "why" not "what", delete commented code
- **Formatting**: Consistent, vertical separation, 88-char limit, team rules override preferences
- **General**: DRY, KISS, YAGNI, Boy Scout Rule, fail fast

## Development Methodology

Follow Martin Fowler's Refactoring, Kent Beck's Tidy Code, and t_wada's TDD principles:

### Core Philosophy

- **Small, safe changes**: Tiny, reversible, testable modifications
- **Separate concerns**: Never mix features with refactoring
- **Test-driven**: Tests provide safety and drive design
- **Economic**: Only refactor when it aids immediate work

### TDD Cycle

1. **Red** → Write failing test
2. **Green** → Minimum code to pass
3. **Refactor** → Clean without changing behavior
4. **Commit** → Separate commits for features vs refactoring

### Practices

- **Before**: Create TODOs, ensure coverage, identify code smells
- **During**: Test-first, small steps, frequent tests, two hats rule
- **Refactoring**: Extract function/variable, rename, guard clauses, remove dead code, normalize symmetries
- **TDD Strategies**: Fake it, obvious implementation, triangulation

### When to Apply

- Rule of Three (3rd duplication)
- Preparatory (before features)
- Comprehension (as understanding grows)
- Opportunistic (daily improvements)

### Key Rules

- One assertion per test
- Separate refactoring commits
- Delete redundant tests
- Human-readable code first

> "Make the change easy, then make the easy change." - Kent Beck

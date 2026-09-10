---
description: 'Shared commenting, documentation, and TypeScript coding standards'
applyTo: '**/*.{ts,astro,css}'
---

# Coding Standards

## Comments and documentation

- Comment intent, constraints, and non-obvious decisions — explain **why**, not what the next line already says.
- Do not add comments that merely paraphrase code. Prefer clear names and small functions for explaining mechanics.
- Keep comments accurate. Update or remove a comment in the same change when the related code changes; an outdated comment is a bug.
- Use comments sparingly for complex algorithms, compatibility workarounds, security considerations, and decisions that are not obvious from the implementation.

## Data-layer API documentation

Every exported function in `db/` and `src/lib/` must have a TSDoc/JSDoc comment that:

- States the function's purpose and important behavior.
- Documents every parameter with `@param`, including the injectable `db` argument used by data-access helpers.
- Documents the return value with `@returns`, including meaningful `null` or error behavior.

Keep pure transforms free of database concerns, and explain determinism or ordering guarantees when they are part of the public behavior.

```ts
/**
 * Returns games ordered by title for deterministic static builds.
 *
 * @param db - The database client to query.
 * @returns All games mapped to the app-facing type.
 */
export async function getAllGames(db: Database): Promise<Game[]> {
  // ...
}
```

## Astro component contracts

Every reusable `.astro` component must define a `Props` interface in its frontmatter. Add a short TSDoc comment to the interface when the contract is not self-explanatory, and document non-obvious props with property comments. Keep the interface accurate when the component API changes.

```astro
---
/** The heading and optional supporting content shown by the hero. */
interface Props {
  /** Text rendered as the primary heading. */
  title: string;
  description?: string;
}
---
```

## TypeScript formatting

- Use four spaces for indentation, single quotes for strings, semicolons, and trailing commas in multiline literals and parameter lists.
- Prefer `const`, explicit parameter and return types for data-layer functions, and `import type` for type-only imports.
- Keep lines readable; split long expressions at meaningful boundaries instead of relying on dense formatting.
- ESLint enforces the repository's recommended JavaScript/TypeScript rules, the unused-variable convention, and semicolons. Keep indentation and quote style consistent with the surrounding TypeScript and Astro files, and run the `quality-checks` skill before submitting changes.

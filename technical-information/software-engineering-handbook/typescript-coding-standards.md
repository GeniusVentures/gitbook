# SuperGenius TypeScript Coding Standards

Revision 1.0 — July 2026

Adapted from the SuperGenius C++ Coding Standards (Rev 2.0), restated for
TypeScript 5.x / ECMAScript 2022+ codebases.

* * *

## 1. Scope

This document defines the coding standards for SuperGenius TypeScript and
JavaScript source files (frontends, Node services, tooling). Rules are
classified as:

| Classification | Meaning | Enforcement |
| --- | --- | --- |
| **Required** | Mandatory. Deviations must be approved by the team lead. | `eslint` check (should pass clean) |
| **Recommended** | Should be followed unless there is a compelling reason to deviate. | `eslint` check (warnings may exist) |

The automated enforcement configuration lives in `eslint.config.js`,
`.prettierrc`, and `tsconfig.json` at the repository root. See §12 Tooling
for usage. `prettier` + `eslint` + `tsc --strict` play the roles of
`clang-format` and `clang-tidy` in the C++ standard.

### 1.1 General Principles

The primary goal is **maintainability**. Other considerations in priority
order: correctness, readability, consistency, clarity, portability,
simplicity, and finally efficiency. When in doubt, strive for clarity first,
then efficiency.

Think of the reader. Keep it simple. Break down complexity. Be explicit —
avoid implicit or obscure language features. Be consistent. Minimize scope,
both logical and visual.

* * *

## 2. Comments

### 2.1 File Comments

**Required:** Every source file shall have a top-of-file comment. Use
TSDoc/JSDoc-compatible format.

```
/**
 * @fileoverview Brief description of the file's purpose.
 * @author Jane Smith
 */
```

### 2.2 Function and Interface Comments

**Required:** All exported functions, classes, interfaces, and type aliases
shall have TSDoc comments. The comment size should match the function's size
and complexity.

```
/**
 * Attaches a rendering window to the context.
 * @param rendWin The window to attach.
 * @returns false on failure.
 */
attachRenderWindow(rendWin: RenderWindow): boolean;
```

**Required:** Use `//` single-line comments for inline comments.

**Recommended:** Prefer block comments (on their own line) over trailing
comments. Use trailing comments only for special annotations (e.g.
`// eslint-disable-next-line`, `// istanbul ignore next`).

**Required:** Block comments are at the same indentation level as the code
they describe.

**Recommended:** Document workarounds and non-obvious decisions with a
linked issue or spec reference, not folklore.

* * *

## 3. Code Layout

### 3.1 Braces

**Required:** Opening braces go on the **same line** as the statement
(1TBS / K&R style). Allman braces are *not* used in TypeScript code.

```
function doSomething(): void {
  if (x !== y) {
    y = x;
  } else {
    // ...
  }
}
```

> Enforced by: `prettier` (default `bracketSameLine` behavior for control
> statements).

**Required:** Always use braces on `if`, `for`, `while`, and `do`/`while`
statements, even when the body is a single statement.

```
// Correct
if (condition) {
  doWork();
}

// Incorrect
if (condition) doWork();
```

> Enforced by: `eslint` (`curly: ["error", "all"]`) [Required]

**Required:** Arrow function bodies that exceed one expression use a block
with an explicit `return`; single-expression bodies omit braces and return.

### 3.2 Indentation and Spacing

**Required:** Indentation is 2 spaces. Do not use tabs. (This matches the
dominant TypeScript ecosystem convention; the C++ 4-space rule does not
carry over.)

> Enforced by: `prettier` (`tabWidth: 2`, `useTabs: false`)

**Required:** No space between a function name and the opening parenthesis.
Single space after keywords (`if`, `for`, `while`, `switch`, `catch`).

**Required:** Balance spacing on either side of binary operators. Do not
space before separators (semicolon, comma) but do space after them.

**Recommended:** Use semicolons at statement ends. Be consistent — never
mix styles within a file.

> Enforced by: `prettier` (`semi: true`)

### 3.3 Column Limit

**Recommended:** Lines should not exceed 100 columns.

> Enforced by: `prettier` (`printWidth: 100`)

### 3.4 Line Wrapping

**Required:** When wrapping a line, indent the continuation past the current
indent column. Wrap conditional expressions after the logical operators.

```
if (theNameOfTheGame === aGameName &&
    theTimeBeingPlayed > aLimit) {
  // ...
}
```

**Required:** Wrap long function signatures after a parameter comma, with
indentation.

```
function setValues(a1: ObjectRef, a2: ObjectRef, aName: string,
                   aValue: number): void {
  // ...
}
```

### 3.5 Declarations

**Required:** Start each declaration on a new line. One statement per line.

**Required:** Use `const` by default; `let` only when reassignment is
required; `var` is never permitted.

> Enforced by: `eslint` (`prefer-const`, `no-var`) [Required]

### 3.6 Switch Statements

**Required:** All `switch` statements shall have a `default` case.

**Required:** Each non-empty `case` shall end with `break`, `return`,
`throw`, or an explicit `// fallthrough` comment documenting intent.

> Enforced by: `eslint` (`default-case`, `no-fallthrough`) [Required]

### 3.7 Blank Lines

**Recommended:** Use blank lines before and after block comments and
between logical sections to visually separate code chunks. At most one
consecutive blank line.

* * *

## 4. Naming Conventions

### 4.1 Summary Table

| Entity | Case | Example | Enforced |
| --- | --- | --- | --- |
| Classes / Interfaces / Types / Enums | PascalCase | `ProcessingNode` | Required |
| Enum members | `UPPER_CASE` | `DatabaseError.NotFound` | Recommended |
| Functions / methods | camelCase, verb-noun | `getValue()` | Required |
| Variables / parameters | camelCase | `nodeId` | Required |
| Compile-time constants | `UPPER_CASE` | `MAX_RETRY_COUNT` | Required |
| Module-level constants | `UPPER_CASE` | `DEFAULT_PORT` | Required |
| Files (component/class) | kebab-case | `processing-node.ts` | Recommended |
| Boolean variables/functions | `is`/`has`/`can` prefix | `isReady` | Recommended |

> Enforced by: `eslint` (`@typescript-eslint/naming-convention`) [Recommended]

### 4.2 Type Names

**Required:** Types, classes, and interfaces start with an uppercase letter
and use PascalCase.

**Required:** Do **not** prefix interfaces with `I` (`IUserService` is
incorrect; `UserService` is correct). No Hungarian notation or type
prefixes anywhere.

### 4.3 Variables and Parameters

**Recommended:** Local variables and parameters use camelCase.

**Required:** Make all identifiers unique within a function. Avoid
similar-sounding names within a scope.

**Recommended:** Boolean names read as predicates: `isReady`, `hasError`,
`canRetry`, `shouldUpdate`.

### 4.4 Constants

**Required:** Compile-time and module constants use `UPPER_CASE` (the
analogue of the C++ `k` prefix rule). Do not use magic numbers; wire-format
and protocol constants shall be named exactly once in a dedicated constants
module, imported by every producer and consumer of the format.

```
export const MAX_RETRY_COUNT = 3;
export const PUBLIC_KEY_SIZE = 32;
```

### 4.5 Functions and Methods

**Required:** Functions and methods use camelCase with a verb-noun pattern:
`getName`, `isEmpty`, `createThread`, `destroyThread`. Accessor/mutator/
factory verb conventions match the C++ standard: `get*`/`set*` pairs,
`is*`/`has*` for booleans, `create*`/`destroy*` for factories.

### 4.6 Spelling and Clarity

**Required:** Use correct English spelling. Avoid abbreviations except for
well-known domain terms.

* * *

## 5. Language Usage

### 5.1 Strictness

**Required:** `strict: true` in `tsconfig.json`. No new file may disable
strict flags (`strictNullChecks`, `noImplicitAny`, etc.) locally or
globally.

**Required:** `any` is not permitted in new code. Use `unknown` and narrow
explicitly. `// @ts-ignore` / `@ts-expect-error` require a comment
explaining why and a linked issue.

> Enforced by: `eslint` (`@typescript-eslint/no-explicit-any`) [Required]

### 5.2 Initialization

**Required:** All variables must be initialized at the point of
declaration (the analogue of the C++ init rule).

**Required:** Use `readonly` on class members and object properties that
are not reassigned (the analogue of C++ `const` correctness).

### 5.3 Null and Undefined

**Required:** Use `undefined` for absent values; reserve `null` for
interoperability with APIs that require it. Never use `==` / `!=`; always
`===` / `!==`. The only tolerated loose comparison is `== null` where both
`null` and `undefined` are meant — prefer explicit `x === null || x === undefined`.

> Enforced by: `eslint` (`eqeqeq: ["error", "always"]`) [Required]

**Recommended:** Prefer optional chaining (`?.`) and nullish coalescing
(`??`) over `&&` chains and `||` defaults when the value may be
`0`, `""`, or `false`.

### 5.4 Casts and Type Assertions

**Required:** Avoid type assertions (`as T`). When unavoidable (e.g. after
narrowing the compiler cannot follow), add a comment justifying the
invariant. Double assertions (`as unknown as T`) are effectively never
permitted.

> Enforced by: `eslint` (`@typescript-eslint/consistent-type-assertions`) [Recommended]

### 5.5 Immutability and `const` Correctness

**Required:** Function parameters shall not be reassigned.

> Enforced by: `eslint` (`no-param-reassign`) [Required]

**Recommended:** Prefer immutable patterns: spread over mutation,
`Readonly<T>` / `ReadonlyArray<T>` in public signatures where mutation by
callers would be a bug.

### 5.6 Enums and Union Types

**Required:** Prefer `const` objects with `as const` plus a union type, or
string enums, over numeric enums. Closed value sets shall be explicit —
bare numbers/strings with a comment are not an enum (the analogue of the
C++ `enum class` rule).

```
export const CodeMode = { Fp4Affine: 0, T158Affine: 1 } as const;
export type CodeMode = typeof CodeMode[keyof typeof CodeMode];
```

### 5.7 Conditionals and Truthiness

**Required:** All non-boolean conditional expressions shall use an explicit
comparison. Do not rely on implicit truthiness for numbers, strings, or
nullable values whose falsy state is ambiguous (the analogue of the C++
implicit-bool rule).

```
if (count !== 0) { ... }          // correct
if (count) { ... }                // incorrect
if (node !== undefined) { ... }   // correct
if (node) { ... }                 // incorrect for nullable objects
```

**Recommended:** Minimize negative comparisons; prefer positive logic.
Use `if`/`else` over nested ternaries; a single simple ternary for value
selection is acceptable.

### 5.8 Loops and Iteration

**Recommended:** Prefer `for...of` and array methods (`map`, `filter`,
`reduce`, `find`) over index loops. Count index loops ascending.

**Recommended:** Minimize `break` in loops; use it only for abnormal early
exit. Use `continue` sparingly with a comment.

**Required:** Never use `for...in` on arrays.

### 5.9 Asynchronous Code

**Required:** Use `async`/`await` over raw `.then()` chains. Every promise
chain must have error handling; floating promises are not permitted.

> Enforced by: `eslint` (`@typescript-eslint/no-floating-promises`,
> `@typescript-eslint/no-misused-promises`) [Required]

**Required:** In async iteration, prefer `for await...of`. Do not fire-and-
forget promises without an explicit `void` operator and a comment.

**Recommended:** Default to pre-increment (`++i`) where a choice exists,
matching the C++ convention.

### 5.10 Regular `function` vs Arrow

**Recommended:** Use arrow functions for callbacks and inline functions;
use named `function` declarations for top-level functions (hoisting,
stack-trace readability). Do not use `this` in module-scope arrow
functions.

### 5.11 goto, Labels, and Obscure Features

**Required:** Labeled statements (the JS `goto` analogue) are never
permitted. The comma operator, `with`, and implicit globals are never
permitted.

### 5.12 Floating-Point

**Required:** Do not compare floating-point numbers for equality. Compare
against an epsilon or use integer/fixed-point representations.

### 5.13 Globals and Side Effects

**Required:** No mutable module-level state. Configuration and shared
state are injected via constructors or parameters (dependency injection),
never imported as mutable singletons.

* * *

## 6. Class Design

### 6.1 Interfaces

**Required:** Program to an interface: depend on `interface` types (or
abstract classes) at module boundaries, not concrete implementations.

**Required:** Keep class interfaces minimal and complete. A developer
should only need the type declarations to use the class.

**Required:** Data members shall never be public without a reason. Use
`private`/`protected` and accessors. `#private` fields are acceptable;
`private` (compile-time) is preferred for ecosystem compatibility.

> Enforced by: `eslint` (`@typescript-eslint/explicit-member-accessibility`) [Required]

**Required:** Explicit accessibility modifiers on all class members.

**Recommended:** Prefer non-member, non-friend free functions over member
functions when private access is not needed (matches the C++ standard).

### 6.2 Special Member Functions

**Recommended:** Rule of Zero applies: classes that manage no resources
directly need no explicit lifecycle methods. Resource-owning classes
implement explicit cleanup (`close()`, `dispose()`, or
`Symbol.dispose`/`Symbol.asyncDispose` where supported) and document the
ownership contract.

**Recommended:** Use `using` declarations for `Disposable` resources where
the runtime supports them (the RAII analogue).

### 6.3 Inheritance

**Required:** Public inheritance shall model "is-a" relationships. Never
redefine an inherited non-virtual method without `override` semantics —
use the `override` keyword.

> Enforced by: `tsc` (`noImplicitOverride: true`) [Required]

**Recommended:** Prefer composition over implementation inheritance (the
C++ standard applies unchanged).

### 6.4 Encapsulation

**Required:** Do not traverse multiple links in a single statement. Use
named temporaries.

```
// Incorrect — hard to read and debug
const name = obj.getDepartment().getManager().getName();

// Correct
const dept = obj.getDepartment();
const mgr = dept.getManager();
const name = mgr.getName();
```

* * *

## 7. Error Handling

### 7.1 Exceptions and Result Types

**Required:** Throw `Error` subclasses, never string or object literals.
Define a small custom error hierarchy per package
(`class Sgf4FormatError extends Error`).

**Recommended:** In hot paths and at API boundaries, a `Result<T, E>`
discriminated union return (the analogue of the C++ `outcome::result<T>`
rule) is preferred over throwing. One style per module — do not mix
throwing and result-returning for the same failure modes.

```
type Result<T, E> = { ok: true; value: T } | { ok: false; error: E };
```

### 7.2 Assertions

**Recommended:** Use assertions (`invariant`-style helpers, Node `assert`)
liberally to document invariants and detect programming errors.

**Required:** Assertions document invariants only. Input validation at
trust boundaries uses explicit checks with typed errors.

### 7.3 Exception Safety

**Required:** Cleanup paths (`finally`, `dispose`) must never throw
unhandled exceptions. Catch and handle anything that could escape.

**Required:** A failed constructor leaves no partially-usable object:
prefer factory functions returning `Result<T, E>` over throwing
constructors for fallible construction.

* * *

## 8. File and Module Layout

### 8.1 Files

**Required:** One primary class/component per file. Closely related helper
types may be co-located.

**Recommended:** Files should not exceed roughly 400 lines; functions
should fit within approximately 100 lines (the C++ §8.4 rule applies
unchanged).

### 8.2 Import Order

**Required:** Order imports as: (1) node/built-in modules, (2) third-party
packages, (3) project-internal modules, (4) relative imports. Alphabetize
within groups.

> Enforced by: `eslint` (`import/order`) [Required]

**Required:** No circular imports. Shared constants/types live in a leaf
module that imports nothing from the package.

### 8.3 Exports

**Required:** Package entry points (`index.ts`) define the public surface
explicitly. Avoid `export *` except in deliberate barrel files.

**Recommended:** Use named exports over default exports (refactor-safe
renaming, clearer imports).

### 8.4 Side Effects

**Required:** Importing a module shall not trigger observable side effects
(network, filesystem, global mutation) other than constant initialization.
Initialization happens in an explicit `init()`/`main()` called by the
entry point.

* * *

## 9. Type Design

### 9.1 Interfaces vs Type Aliases

**Recommended:** Use `interface` for object shapes that may be extended;
use `type` for unions, intersections, mapped types, and function types.

### 9.2 Narrowing

**Required:** Validate untrusted input (network, filesystem, user) with
runtime schema validators (e.g. `zod`, `valibot`) and let types flow from
the schema (`z.infer`). Never cast `JSON.parse` output directly.

### 9.3 Generics

**Recommended:** Name generic parameters meaningfully (`TValue`, `TError`)
when a single letter is unclear. Constrain generics
(`<T extends Foo>`) rather than accepting everything.

### 9.4 Utility Types

**Recommended:** Prefer built-in utility types (`Partial`, `Required`,
`Pick`, `Omit`, `Record`, `Readonly`) over hand-rolled mapped types.

* * *

## 10. Platform Abstraction

**Required:** Do not scatter environment checks (`typeof window`,
`process.env`, `Deno`, `Bun`) through source files. Isolate platform and
environment differences behind a single `platform` module, selected at
build time or via dependency injection (the C++ §10 rule applies
unchanged).

**Required:** Environment variables are read exactly once, in a typed
config module with validation and defaults — never ad hoc `process.env.*`
throughout the code.

* * *

## 11. Testing

**Required:** New logic ships with tests in the same change (vitest or
jest, colocated `*.test.ts` or a `tests/` tree matching source layout).

**Recommended:** Tests are deterministic: seeded RNGs, fake timers, no
network. Binary-format code shall include hand-constructed golden
vectors, not only round-trip self-consistency checks.

**Recommended:** Name tests as behavior statements
(`it("decodes a MIXED record via the split map")`).

* * *

## 12. Tooling

### 12.1 prettier

The repository root contains `.prettierrc` encoding the formatting rules
from §3. Run:

```
prettier --write <file>      # apply formatting
prettier --check <file>      # check only
```

All code shall be formatted before commit. Most editors can format on
save.

### 12.2 eslint

The repository root contains `eslint.config.js` (flat config) encoding
the static analysis rules from §4–§7, with `@typescript-eslint`
type-checked rules enabled. Each rule is annotated `[Required]` or
`[Recommended]`. Run:

```
eslint <file>
```

Required rules should pass clean on new and modified code. Recommended
rules may produce warnings; address them where practical.

### 12.3 TypeScript compiler

```
tsc --noEmit
```

Type checking is part of every build. `strict` mode is non-negotiable.

### 12.4 Build Verification

Before committing, always:

1. Format with prettier
2. Run eslint on changed files
3. Run `tsc --noEmit` without errors
4. Run tests

* * *

## 13. References

- SuperGenius C++ Coding Standards, Revision 2.0 (this document's parent).
- Microsoft. _TypeScript Handbook_.
- Google. _TypeScript Style Guide_.
- typescript-eslint project. _Recommended and stylistic rule sets_.

* * *

_Revision 1.0 — July 2026._
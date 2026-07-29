# Dart / Flutter Coding Standards

Revision 1.0 — July 2026

This is a **delta document** against the
[C++ Coding Standards](c++-coding-standards.md). Everything not restated here
applies unchanged: general principles (§1.1), comment discipline (§2), error
handling philosophy (§7), and tooling expectations (§12). Where Dart idiom
conflicts with the C++ rule, **this document wins for Dart code**.

The primary reference is the official
[Dart style guide](https://dart.dev/effective-dart) — Effective Dart is the
baseline; this document only records where the workspace deviates from it.

---

## 1. Scope

Applies to all Dart code in the workspace: Flutter apps (GeniusWallet,
genius-tube UI), reusable packages under `GeniusWallet/packages/`, and
generated-code templates that emit Dart.

Rules keep the same classifications as the C++ standard: **Required** /
**Recommended**.

---

## 2. Deltas from the C++ Standard

### 2.1 Bracing — Allman does NOT apply

**Required:** Dart uses **K&R / same-line braces** (the dartfmt default), not
Allman. This is the single biggest visual delta from the C++ standard.

```dart
// Dart — correct
if (isReady) {
  play();
} else {
  buffer();
}

// NOT the C++ Allman style:
// if (isReady)
// {
//     play();
// }
```

**Required:** Never hand-format around dartfmt. Run `dart format` (or have the
IDE apply it) before commit. If dartfmt's output looks wrong, the code is too
clever — simplify the code, not the formatter's output.

### 2.2 Naming

Dart has its own naming conventions; follow them rather than the C++ table:

| Construct | Style | Example | Classification |
|---|---|---|---|
| Types (classes, enums, typedefs, mixins, extensions) | PascalCase | `PlaybackLease` | Required |
| Functions, methods, variables, parameters | camelCase | `resolveEntitlement()` | Required |
| Members (fields) | camelCase, no prefix | `nodeId` | Required |
| Private members | leading `_` | `_contentKey` | Required |
| Constants (`const`/`static const`) | camelCase | `defaultEpochLength` | Required |
| Files and directories | snake_case | `playback_lease.dart` | Required |
| Packages | snake_case | `genius_api` | Required |

Deltas to note explicitly:

* **No `m_` prefix.** Dart marks privacy with leading `_`, not scope with a
  prefix. A private field is `_nodeId`; a public one is `nodeId`.
* **No `k` prefix on constants.** Dart style is plain camelCase
  (`defaultEpochLength`, not `kDefaultEpochLength`).
* **Functions are camelCase**, where the C++ standard uses PascalCase.
* **Files are snake_case**, matching the C++ standard's file rule.

### 2.3 Types and null safety

**Required:** Sound null safety everywhere. No `// @dart=2.x` opt-outs, no
`late` without an initializer in the constructor path, no `!` unless the
alternative is measurably worse. Prefer making the type honest (nullable or
not) over asserting at use sites.

**Required:** Prefer `final` fields and `const` constructors where the object
is immutable — view models and event/command structs crossing the FFI boundary
should be immutable value types.

**Recommended:** Use Dart 3 records and sealed classes for the typed
command/event envelopes that mirror the C++ core's FFI structs. Sealed classes
give exhaustive `switch` checking for free.

### 2.4 Error handling

Mirrors C++ §7 with Dart mechanics:

**Required:** Errors that cross the FFI boundary arrive as values (the
`GeniusTubeError`-style struct via ffigen), not exceptions. Convert them to
typed Dart results or throw typed exceptions **at the repository/facade
layer** — widgets should never see raw FFI error structs.

**Required:** Exceptions thrown in Dart use typed exception classes
(`class EntitlementException implements Exception`), never bare strings or
generic `Exception()` instances.

**Recommended:** Retryability comes from the core's error-code functions via
FFI. Do not hand-maintain a Dart copy of the error taxonomy — the C++ core is
the single source of truth.

### 2.5 Comments

Same as C++ §2 with Dart syntax, **using Doxygen-style comments** rather than
dartdoc. Our documentation pipeline (gendoc-template) is Doxygen-based; the
`///` dartdoc convention is not consumed by our tooling, so we standardize on
Doxygen format for all workspace languages including Dart.

**Required:** Every file has a top-of-file Doxygen comment. Public APIs have
Doxygen `/** ... */` block comments in the declaring file.

```dart
/**
 * @file playback_lease.dart
 * @brief Playback-lease resolution against the on-chain entitlement registry.
 */

/**
 * @brief Resolves the current holder's entitlement for [assetId] against the
 *        chain, returning a lease ready for playback.
 * @param assetId  The asset whose entitlement is being resolved.
 * @return A [Future] completing with the resolved [PlaybackLease].
 * @throws [EntitlementException] when ownership cannot be proven.
 */
Future<PlaybackLease> resolveEntitlement(String assetId) { ... }
```

**Recommended:** Inline comments use `//`, same as C++.

### 2.6 Flutter-specific rules

**Required:** Widgets contain no protocol, ledger, DRM, or CRDT logic. A
widget reads a view model, renders it, and dispatches a typed command. All
state transitions happen in the C++ core and arrive as typed events.

**Required:** State management is `provider` with immutable view models.
Avoid adding heavier frameworks (bloc, riverpod, getx) — one pattern
workspace-wide.

**Recommended:** Keep widgets small; extract a new widget before a build
method exceeds a screen of code, same spirit as the C++ function-size rule.

**Recommended:** `const` constructors on widgets wherever possible — it is
the cheapest Flutter performance win and costs nothing.

---

## 3. Generated Dart

FFI bindings and schema-driven Dart are generated (ffigen / Jinja2) and are
never committed. Do not hand-edit generated files — change the template or
the config and regenerate. Generated files carry the source-schema and
generator-version header, same as generated C++.

---

## 4. Tooling

| Tool | Purpose |
|---|---|
| `dart format` | Formatting — run before commit, no config debates |
| `dart analyze` (`analysis_options.yaml` with `package:flutter_lints`) | Static analysis — Required-clean |
| `flutter test` | Unit/widget tests |
| ffigen | FFI binding regeneration (driven by CMake stamp targets) |

`analysis_options.yaml` lives at the package root and includes
`package:flutter_lints/flutter.yaml`. Deviations from a lint require a
`// ignore: <lint>` comment with a reason on the same line — same discipline
as the C++ standard's clang-tidy suppression rule.

---

## 5. References

* [Effective Dart](https://dart.dev/effective-dart) — the baseline this
  document deltas from
* [C++ Coding Standards](c++-coding-standards.md) — parent document
* `GeniusWallet/packages/genius_api/` — reference package structure and
  ffigen consumption pattern

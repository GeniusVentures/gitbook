## Python Coding Standards

This section extends the SuperGenius C++ Coding Standards to Python source
files (e.g. `gnus-poc/`, tooling, test harnesses). The classifications are
identical: **Required** rules must be followed (enforced by `ruff` + `mypy`,
which play the roles of `clang-format` and `clang-tidy`); **Recommended**
rules should be followed unless there is a compelling reason to deviate.

The §1.1 General Principles apply unchanged: maintainability first, think of
the reader, be explicit, minimize scope.

### 1 Comments and Docstrings

**Required:** Every module shall have a top-of-file docstring stating its
purpose (the analogue of the §2.1 top-of-file comment).

**Required:** All public classes, functions, and modules shall have docstrings
(Google style). Comment size should match the function's size and complexity.

**Required:** Use `#` single-line comments for inline comments. Block comments
sit on their own line, at the same indentation level as the code they describe.

### 2 Code Layout

**Required:** Indentation is 4 spaces. Never tabs (PEP 8; enforced by `ruff format`).

**Recommended:** Lines should not exceed 100 columns (the C++ limit of 120 is
acceptable where the team prefers consistency with C++).

**Required:** One statement per line. Each declaration on a new line.

**Required:** Break long lines inside parentheses, brackets, or braces rather
than with backslash continuations. Indent the continuation past the current
indent column. Wrap conditional expressions after the logical operators.

**Recommended:** Two blank lines between top-level definitions, one between
method definitions. At most one blank line within a function body.

### 3 Naming Conventions

| Entity | Case | Example | Enforced |
| --- | --- | --- | --- |
| Modules / packages | snake_case | `sgfp4_format.py` | Required |
| Classes / Exceptions | PascalCase | `QuadtreeEncoder` | Required |
| Functions / methods | snake_case, verb-noun | `decode_v2()` | Required |
| Variables / parameters | snake_case | `leaf_index` | Required |
| Compile-time constants | `UPPER_CASE` | `SPLIT_MAP_BYTES` | Required |
| Enum types | PascalCase | `class CodeMode(IntEnum)` | Required |
| Enum members | `UPPER_CASE` | `FP4_AFFINE` | Recommended |
| Non-public members | single leading `_` | `_build_split_map` | Required |

**Required:** No Hungarian notation or type prefixes.

**Recommended:** Boolean-returning functions start with `is_` or `has_`
(the analogue of §4.6). Factory functions start with `create_`; teardown
functions with `destroy_`.

**Required:** Wire-format and protocol "magic numbers" shall be named exactly
once in a dedicated constants module (the analogue of §4.5
`avoid-magic-numbers`), imported by every producer and consumer of the format.
Do not duplicate literal masks, shifts, or sizes across files.

### 4 Language Usage

**Required:** Use `enum.Enum` / `enum.IntEnum` for closed sets of values.
Bare integer constants with a comment are not an enum (analogue of §5.9
`enum class`).

**Required:** All non-boolean conditional expressions shall be explicit
(analogue of §5.12). Test `None` with `is` / `is not`; test bit flags with
`!= 0`; do not rely on truthiness of objects whose falsy value is ambiguous.

```
if flags & RESERVED_MASK != 0:   # correct
if flags & RESERVED_MASK:        # incorrect
if node is None:                 # correct
if not node:                     # incorrect
```

**Required:** No mutable default arguments (`def f(items=[])`). Use
`Optional[...] = None` and initialize in the body.

**Required:** Acquire resources with context managers (`with`) — the RAII
analogue. Files, sockets, and locks shall not rely on `__del__`.

**Required:** Type hints on all public function signatures. `mypy` (or
equivalent) must pass on new code.

**Recommended:** Prefer `pathlib.Path` over `os.path` string manipulation.
Prefer f-strings over `%` or `.format()`. Prefer dataclasses for simple
data carriers.

**Recommended:** Use `nonlocal`/`class` state instead of single-element list
closure hacks (`idx = [0]`).

**Recommended:** Minimize `break`/`continue` in loops, as in §5.13. Count
loops ascending.

### 5 Class Design

**Required:** Data members shall not be public (§6.1 analogue): prefix with
`_`; expose behavior through methods or `@property`.

**Recommended:** Prefer composition over inheritance (§6.4 applies unchanged).
Use `abc.ABC` for interfaces.

**Required:** A class's public surface shall be documented in its docstring;
`__all__` shall be defined in package `__init__.py` files that re-export.

### 6 Error Handling

**Required:** Raise specific exception types, never bare `except:` and never
`except Exception` without re-raising or wrapping. Define a small custom
exception hierarchy per package (e.g. `SGFP4FormatError(ValueError)`).

**Required:** `assert` documents invariants only (§7.2 analogue). Never use
`assert` for input validation or error handling — it is stripped under
`python -O`.

**Recommended:** Functions should document raised exceptions in their
docstrings.

### 7 Module and File Layout

**Required:** Import order: (1) standard library, (2) third-party,
(3) project-local (the analogue of §8.3; enforced by `ruff` isort rules).

**Required:** No circular imports. Shared constants/types live in a leaf
module (e.g. `*_format.py`) that imports nothing from the package.

**Required:** Executable module code guarded by `if __name__ == "__main__":`.

**Recommended:** Functions should fit within approximately 100 lines (§8.4
applies unchanged). Extract helpers rather than nesting logic.

**Recommended:** Avoid monkey-patching and runtime modification of other
modules' objects.

### 8 Platform Abstraction

**Required:** No scattered `sys.platform` checks in source files (§10
analogue). Isolate platform differences in a single `platform_utils` module.

### 9 Testing

**Required:** New logic ships with `pytest` tests in the same change.

**Recommended:** Tests use seeded RNGs (`np.random.default_rng(seed)`) for
determinism. Binary-format code shall include hand-constructed golden
vectors, not only round-trip self-consistency checks.

### 10 Tooling

| C++ tool | Python analogue | Purpose |
| --- | --- | --- |
| clang-format | `ruff format` (or `black`) | Layout enforcement |
| clang-tidy | `ruff check` | Static analysis, naming, import order |
| — | `mypy` | Type checking (Required checks must pass clean) |

Before committing, always: format, lint, type-check, and run tests
(§12.3 applies unchanged).
# SuperGenius C++ Coding Standards

Revision 2.0 — June 2026

Adapted from the Corelinux Consortium C++ Coding Standards (2000), modernized for C++17.

---

## 1. Scope

This document defines the coding standards for the SuperGenius C++ codebase. Rules are classified as:

| Classification | Meaning | Enforcement |
|---|---|---|
| **Required** | Mandatory. Deviations must be approved by the team lead. | clang-tidy check (should pass clean) |
| **Recommended** | Should be followed unless there is a compelling reason to deviate. | clang-tidy check (warnings may exist) |

The automated enforcement configuration lives in `.clang-tidy` and `.clang-format` at the repository root. See [§12 Tooling](#12-tooling) for usage.

### 1.1 General Principles

The primary goal is **maintainability**. Other considerations in priority order: correctness, readability, consistency, clarity, portability, simplicity, and finally efficiency. When in doubt, strive for clarity first, then efficiency.

Think of the reader. Keep it simple. Break down complexity. Be explicit — avoid implicit or obscure language features. Be consistent. Minimize scope, both logical and visual.

---

## 2. Comments

### 2.1 File Headers

**Required:** Every source and header file shall have a top-of-file comment. Use Doxygen-compatible format.

```cpp
/**
 * @file MyClass.hpp
 * @brief Brief description of the file's purpose.
 * @author Jane Smith
 */
```

### 2.2 Function and Interface Comments

**Required:** All public functions and interfaces shall have header comments in the `.hpp` file. The comment size should match the function's size and complexity.

```cpp
/**
 * @brief Attaches a rendering window to the context.
 * @param rendWin  The window to attach.
 * @return false on failure.
 */
virtual bool AttachRenderWindow(IRenderWindow *rendWin) = 0;
```

### 2.3 Inline Comments

**Required:** Use C++ single-line comments (`//`) for inline comments.

**Recommended:** Prefer block comments (on their own line) over trailing comments. Use trailing comments only for special annotations.

**Required:** Trailing comments at a closing brace are indented one level from the brace.

**Required:** Block comments are at the same indentation level as the code they describe.

---

## 3. Code Layout

### 3.1 Braces

**Required:** Use Allman / Ullman brace style. Braces are always on their own line, at the same indentation level as the statement that precedes them. The code within braces is indented one level.

```cpp
void DoSomething()
{
    if ( x != y )
    {
        y = x;
    }
    else
    {
        // ...
    }
}
```

> **Enforced by:** `clang-format` (`BreakBeforeBraces: Allman`)

**Required:** Always use braces on `if`, `for`, `while`, and `do`/`while` statements, even when the body is a single statement.

```cpp
// Correct
if ( condition )
{
    DoWork();
}

// Incorrect
if ( condition )
    DoWork();
```

> **Enforced by:** `clang-tidy` (`readability-braces-around-statements`) [Required]

**Required:** Put the `while` in a `do`/`while` statement on the same line as the closing brace.

```cpp
do
{
    ++x;
} while ( x < y );
```

### 3.2 Indentation and Spacing

**Required:** Indentation is 4 spaces. Do not use tabs.

> **Enforced by:** `clang-format` (`IndentWidth: 4`, `UseTab: Never`)

**Required:** Balance spacing inside parentheses — space after `(` and before `)` when arguments are present. No spaces in empty argument lists.

```cpp
void DoFunction();                  // no args — no spaces
void DoFunction( ObjectRef aRef );  // args — spaces inside parens
```

**Required:** Do not space between a function name and the opening parenthesis.

```cpp
DoFunction( arg );   // correct
DoFunction ( arg );  // incorrect
```

> **Enforced by:** `clang-format` (`SpacesInParentheses: true`, `SpaceBeforeParens: ControlStatements`)

**Required:** Do not use spaces between a dereference operator and its operand.

```cpp
val = *pFoo;   // correct
val = * pFoo;  // incorrect
```

> **Enforced by:** `clang-format` (`PointerAlignment: Left`)

**Required:** Balance spacing on either side of binary operators.

**Required:** Do not space before separators (semicolon, comma) but do space after them.

### 3.3 Column Limit

**Recommended:** Lines should not exceed 120 columns.

> **Enforced by:** `clang-format` (`ColumnLimit: 120`)
>
> *Historical note: The original 2000 standard specified 78 columns. This was revised to 120 for modern displays and C++17 code density.*

### 3.4 Line Wrapping

**Required:** When wrapping a line, indent the continuation past the current indent column.

**Required:** Wrap conditional expressions after the logical operators.

```cpp
if ( theNameOfTheGame == aGameName &&
     theTimeBeingPlayed > aLimit )
{
    // ...
}
```

> **Enforced by:** `clang-format` (`BreakBeforeBinaryOperators: None`)

**Required:** Wrap long function signatures after a parameter comma, with indentation.

```cpp
void ClassMethod::SetValues( ObjectCref a1, ObjectCref a2, StringCref aName,
                             IntCref aValue )
{
    // ...
}
```

> **Enforced by:** `clang-format` (`BinPackParameters: false`)

### 3.5 Declarations

**Required:** Start each declaration on a new line.

**Required:** Put one statement per line (except for trivial in-line accessors in headers).

### 3.6 Switch Statements

**Required:** All `switch` statements shall have a `default` case.

**Required:** Indent `case` labels one level from the `switch`. Indent the case body one level from the `case`. The `break` is at the same indentation as the body.

```cpp
switch ( variable )
{
    case 1:
        DoSomething();
        break;
    case 2:
        DoOther();
        break;
    default:
        break;
}
```

> **Enforced by:** `clang-format` (`IndentCaseLabels: true`)

### 3.7 Access Modifiers

**Required:** `public`, `protected`, and `private` appear flush with the `class` keyword (no additional indentation).

> **Enforced by:** `clang-format` (`AccessModifierOffset: 0`)

**Required:** Access controls appear in this order: `public`, `protected`, `private` (methods), then `protected`, `private` (data members). Empty access-control sections may be omitted.

### 3.8 Namespaces

**Required:** Namespace bodies are indented one level. Use nested namespace syntax (C++17).

```cpp
namespace sgns::storage
{
    // indented one level
}
```

> **Enforced by:** `clang-format` (`NamespaceIndentation: All`, `CompactNamespaces: false`)

### 3.9 Blank Lines

**Recommended:** Use blank lines before and after block comments to visually separate code chunks.

> **Enforced by:** `clang-format` (`MaxEmptyLinesToKeep: 1`)

---

## 4. Naming Conventions

### 4.1 Summary Table

| Entity | Case | Prefix | Example | Enforced |
|---|---|---|---|---|
| Classes | PascalCase | — | `ProcessingNode` | Required |
| Structs | PascalCase | — | `CrdtOptions` | Required |
| Enums | PascalCase | — | `DatabaseError` | Required |
| Enum constants | `UPPER_CASE` | — | `NOT_FOUND` | Recommended |
| Functions (free) | PascalCase | — | `CreateLogger` | Recommended |
| Methods (member) | PascalCase | — | `GetValue()` | Recommended |
| Variables (local) | camelCase | — | `localVar` | Recommended |
| Parameters | camelCase | — | `nodeId` | Recommended |
| Member variables | camelCase | `m_` | `m_nodeId` | Recommended |
| Compile-time constants | PascalCase | `k` | `kMaxRetryCount` | Recommended |
| Global constants | PascalCase | `k` | `kDefaultPort` | Recommended |

> **Enforced by:** `clang-tidy` (`readability-identifier-naming`) [Recommended]
>
> *Note: Naming is classified as Recommended because the codebase is transitioning. Some files still use trailing-underscore members (`node_id_`) or camelCase free functions (`createLogger`). New code shall follow this table.*

### 4.2 Type Names

**Required:** Types start with an uppercase letter and use PascalCase (also known as UpperCamelCase).

```cpp
class TokenAmount { };
struct CrdtOptions { };
enum class DatabaseError : uint8_t { };
```

### 4.3 Variables and Parameters

**Recommended:** Local variables and parameters use camelCase (lowerCamelCase) — first word lowercase, subsequent words capitalized.

```cpp
int itemCount = 0;
void Process( const std::string &nodeId );
```

**Recommended:** Do not use Hungarian notation or type prefixes (`a`, `p`, `l`, etc.).

### 4.4 Member Variables

**Recommended:** Non-public member variables use `m_` prefix followed by camelCase.

```cpp
class ProcessingNode
{
private:
    std::string m_nodeId;
    std::chrono::seconds m_ttl;
};
```

**Recommended:** Do not use `m_` prefix for public members of simple structs used as data carriers.

```cpp
struct Point
{
    double x;
    double y;
};
```

### 4.5 Compile-Time Constants

**Recommended:** Compile-time constants use `k` prefix followed by PascalCase.

```cpp
constexpr int kMaxRetryCount = 3;
inline constexpr size_t kPublicKeySize = 32;
static constexpr uint64_t kDefaultPort = 3000;
```

Do not use `#define` for value constants. Do not use `UPPER_CASE` for constants.

> **Enforced by:** `clang-tidy` (`cppcoreguidelines-avoid-magic-numbers`) [Required], with `0`, `1`, `-1`, and `2` allowed in trivial contexts.

### 4.6 Functions and Methods

**Recommended:** Functions and methods use PascalCase with a verb-noun pattern.

```cpp
void SetName( const std::string &name );
bool IsEmpty() const;
int GetCount() const;
std::shared_ptr<Thread> CreateThread();
void DestroyThread( std::shared_ptr<Thread> t );
```

**Required:** Accessor methods (returning a value) start with `Get` and should be `const`.

**Recommended:** Boolean accessor methods start with `Is` or `Has` and return `bool`.

**Required:** Mutator methods (setting a value) start with `Set` and do not return values.

**Required:** Factory creation functions start with `Create`. Factory destruction functions start with `Destroy`.

### 4.7 Spelling and Clarity

**Required:** Use correct English spelling. Avoid abbreviations except for well-known domain terms.

**Recommended:** Make names clearly unique within their scope. Avoid similar-sounding names.

**Required:** Make all identifiers unique within a function.

---

## 5. Language Usage

### 5.1 C++ Standard

**Required:** Code targets C++17. Do not use C++20 (or later) features.

### 5.2 Initialization

**Required:** All variables must be initialized at the point of declaration. If the value is not yet known, initialize pointers to `nullptr` and arithmetic types to `0`.

```cpp
int count = 0;
std::string name;
Logger logger = nullptr;
```

> **Enforced by:** `clang-tidy` (`cppcoreguidelines-init-variables`) [Required]

**Recommended:** Prefer member initializer lists over assignment in the constructor body.

```cpp
// Preferred
MyClass::MyClass( int value, const std::string &name )
    : m_value( value )
    , m_name( name )
{ }

// Acceptable but not preferred
MyClass::MyClass( int value, const std::string &name )
{
    m_value = value;
    m_name = name;
}
```

> **Enforced by:** `clang-tidy` (`cppcoreguidelines-prefer-member-initializer`) [Recommended]

**Required:** List members in a constructor initialization list in the order they are declared in the class header.

> **Enforced by:** `clang-format` (`BreakConstructorInitializers: BeforeComma`, `ConstructorInitializerIndentWidth: 4`)

### 5.3 Pointers and Null

**Required:** Use `nullptr`, never `NULL`, `0`, or `NULLPTR` for null pointers.

> **Enforced by:** `clang-tidy` (`modernize-use-nullptr`) [Required]

### 5.4 Casts

**Required:** Use explicit C++-style casts. Never rely on implicit compiler conversions for pointer or arithmetic narrowing.

```cpp
auto value = static_cast<uint32_t>( rawValue );
auto ptr = dynamic_cast<Derived *>( basePtr );
```

> **Enforced by:** `clang-tidy` (`google-readability-casting`) [Required]

### 5.5 `const` Correctness

**Required:** Use `const` on every function, parameter, return value, and variable that will not be modified.

**Recommended:** All accessor (getter) member functions should be `const`.

> **Enforced by:** `clang-tidy` (`readability-make-member-function-const`) [Recommended]

**Required:** Pass non-modifiable objects by `const` reference, not by value.

```cpp
void Process( const Transaction &txn );
```

**Required:** Never return handles (references, pointers, iterators) to private object internals from `const` member functions. If a handle must be returned, make it `const`.

### 5.6 `noexcept`

**Recommended:** Declare functions `noexcept` if they are guaranteed not to throw. This is especially important for move constructors, move assignment, destructors, and simple accessors.

```cpp
uint64_t Value() const noexcept;
~MyClass() = default;  // destructors are implicitly noexcept
```

> **Enforced by:** `clang-tidy` (`modernize-use-noexcept`) [Recommended]
>
> *Note: The project uses `outcome::result<T>` for error propagation rather than exceptions in hot paths. Functions using `outcome::result` should still be declared `noexcept` when they don't throw.*

### 5.7 `auto`

**Recommended:** Prefer `auto` for variable declarations where the type is obvious from the initializer. Avoid `auto` where the type is not immediately clear to the reader.

```cpp
auto logger = base::createLogger( "Tag" );          // clear
auto it = map.find( key );                           // clear
uint64_t count = GetCount();                          // better than auto when type matters
```

### 5.8 Range-Based `for` and Algorithms

**Recommended:** Prefer range-based `for` loops over iterator-based loops where possible.

**Recommended:** Prefer standard algorithms over hand-written loops.

### 5.9 Enums

**Required:** Prefer `enum class` (scoped enumerations) over unscoped `enum`.

**Recommended:** Specify the underlying type for `enum class` when size matters.

```cpp
enum class DatabaseError : uint8_t
{
    OK,
    NOT_FOUND,
    CORRUPTION
};
```

**Recommended:** Enum constant names use `UPPER_CASE`.

> **Enforced by:** `clang-tidy` (`readability-identifier-naming.EnumConstantCase`) [Recommended]
>
> *Note: Some code uses PascalCase for scoped enum constants (e.g., `ParseMode::Strict`). This produces warnings under the current tooling; new code should use `UPPER_CASE`.*

### 5.10 `goto`

**Required:** `goto` is never permitted.

> **Enforced by:** `clang-tidy` (`cppcoreguidelines-avoid-goto`) [Required]

### 5.11 Switch Statements

**Required:** All `switch` statements shall have a `default` case.

**Required:** Each non-empty `case` shall end with a `break`, `return`, or explicit comment documenting intentional fall-through.

### 5.12 Conditional Expressions

**Required:** All non-boolean comparison expressions shall use an explicit comparison operator. Do not rely on implicit conversion to `bool`.

```cpp
if ( ptr != nullptr )  // correct
if ( ptr )             // incorrect
```

> **Enforced by:** `clang-tidy` (`readability-implicit-bool-conversion`) [Required]

**Recommended:** Minimize negative comparisons; prefer positive logic.

**Recommended:** Use `if`/`else` blocks rather than the ternary operator (`?:`) when the intent is to execute code for side effects, not just to select a value.

### 5.13 Loops

**Recommended:** Use `for` loops when the loop control needs initialization or recalculation; otherwise use `while`.

**Recommended:** Count `for` loops in ascending order.

**Recommended:** Minimize use of `break` in loops. Use it only for abnormal early exit.

**Recommended:** Use `continue` sparingly, with a comment explaining why.

### 5.14 Operators

**Recommended:** Default to pre-increment (`++i`) and pre-decrement (`--i`) unless post-increment/decrement semantics are logically required.

### 5.15 Floating-Point

**Required:** Do not compare floating-point numbers for equality.

**Recommended:** Use floating-point numbers only where necessary (graphics, physics).

### 5.16 Macros

**Required:** Replace `#define` value constants with `constexpr` or `inline constexpr`. Use macros only for include guards and unavoidable platform/compiler integration.

**Required:** Multi-statement macros shall have one statement per line, properly backslash-continued.

### 5.17 Stack vs Heap

**Required:** Match `new` with `delete` and `new[]` with `delete[]`.

**Required:** Prefer stack allocation. When heap allocation is needed, use `std::unique_ptr` (or `std::shared_ptr` when shared ownership is required). Never use raw `new`/`delete` in application code — wrap in smart pointers at the point of allocation.

---

## 6. Class Design

### 6.1 Interfaces

**Required:** Program to an interface, not an implementation. Define abstract interfaces (pure virtual classes) and depend on them.

**Required:** Keep class interfaces minimal and complete. A developer should only need the `.hpp` file to use the class.

**Required:** Data members shall never be `public`.

> **Enforced by:** `clang-tidy` (`misc-non-private-member-variables-in-classes`) [Required]

**Required:** Prefer non-member, non-friend free functions over member functions to increase encapsulation. Member functions should only be used when they need access to private data.

### 6.2 Special Member Functions

**Recommended:** Follow the Rule of Zero/Five:
- **Rule of Zero:** If a class does not manage resources directly, do not declare any of the special member functions (destructor, copy/move constructors, copy/move assignment). Let the compiler generate them.
- **Rule of Five:** If a class manages resources directly, declare all five: destructor, copy constructor, copy assignment, move constructor, and move assignment.

> **Enforced by:** `clang-tidy` (`cppcoreguidelines-special-member-functions`) [Recommended]

**Required:** Declare destructors `virtual` in all polymorphic base classes.

> **Enforced by:** `clang-tidy` (`bugprone-*` virtual-destructor checks) [Required]

### 6.3 Inheritance

**Required:** Public inheritance shall model "is-a" relationships.

**Required:** Never redefine an inherited non-virtual function.

> **Enforced by:** `clang-tidy` (`modernize-use-override`) [Required]

**Required:** Never redefine an inherited default parameter value.

**Recommended:** Differentiate between inheritance of interface and inheritance of implementation. Prefer composition over implementation inheritance.

### 6.4 Composition over Inheritance

**Recommended:** Favor object composition over class inheritance. Composition allows behavior to be combined at runtime and reduces rigid dependencies.

### 6.5 Encapsulation

**Required:** Keep internal class structure hidden. Do not expose implementation details in the public interface.

**Required:** Do not traverse multiple links or member functions in a single statement. Use named temporaries.

```cpp
// Incorrect — hard to read and debug
auto name = obj->GetDepartment()->GetManager()->GetName();

// Correct
auto *dept = obj->GetDepartment();
auto *mgr = dept->GetManager();
auto name = mgr->GetName();
```

---

## 7. Error Handling

### 7.1 Outcome Pattern

**Required:** The project uses `outcome::result<T>` for fallible operations rather than C++ exceptions in hot paths.

```cpp
outcome::result<Blob<32>> Blob::fromHex( std::string_view hex );
```

All functions returning `outcome::result<T>` shall be declared `noexcept` unless they have a specific reason to throw.

### 7.2 Assertions

**Recommended:** Use assertions liberally to document invariants and detect programming errors.

### 7.3 Exception Safety

**Required:** Destructors must never throw exceptions. Catch and handle any exceptions that could escape a destructor.

**Required:** If a constructor fails, it shall leave the object in a well-defined state. In `outcome::result`-based code, use factory functions that return `outcome::result<T>` rather than throwing from constructors.

---

## 8. File Layout

### 8.1 File Extensions

**Required:** Use `.hpp` for C++ header files and `.cpp` for C++ source files.

**Recommended:** Use `.h` and `.c` for C-style files only (discouraged).

### 8.2 One Class Per Header

**Required:** A class shall have a single header file. Closely related helper types may be co-located.

**Recommended:** Classes with a large number of member functions may split their implementation across multiple `.cpp` files organized by functional area.

### 8.3 Include Order

**Recommended:** Order includes as: (1) own header, (2) project headers, (3) third-party headers, (4) standard library headers.

> **Enforced by:** `clang-format` (`SortIncludes: true`, `IncludeBlocks: Preserve`)

**Required:** Minimize header file interdependence. Use forward declarations where possible instead of `#include`.

### 8.4 Function Length

**Recommended:** Functions should fit within approximately 100 lines.

**Recommended:** Module files should not exceed 10–15 pages.

---

## 9. Header File Layout

### 9.1 Include Guards

**Required:** All headers must be guarded against multiple inclusion.

```cpp
#ifndef SUPERGENIUS_MYCLASS_HPP
#define SUPERGENIUS_MYCLASS_HPP
// ...
#endif // SUPERGENIUS_MYCLASS_HPP
```

`#pragma once` is an acceptable alternative for headers that are not part of the public API, but traditional guards are preferred for portability.

### 9.2 Header Content

**Required:** Do not allocate memory (define static storage) in header files.

**Required:** Include only what the header directly needs. Forward-declare types that are used only by reference or pointer.

### 9.3 Order Within a Class

**Required:** Within a class definition, members appear in this order:

1. `public:` — constructors, destructor, operator overloads, accessors, mutators
2. `protected:` — protected methods
3. `private:` — private methods
4. `protected:` — protected data members
5. `private:` — private data members

---

## 10. Platform Abstraction

**Required:** Do not use `#ifdef` OS-specific checks (`WINDOWS`, `OSX`, `ANDROID`, etc.) in source files. Instead, include a `Platform.hpp` header that provides platform-specific abstractions.

```cpp
// Incorrect
#ifdef WINDOWS
    // Windows-specific code
#elif __APPLE__
    // Mac-specific code
#endif

// Correct
#include "Platform.hpp"
// Platform.hpp handles the OS-specific includes
```

Use the build system (CMake) to select per-platform include directories and source files.

---

## 11. Includes

**Required:** Use project-root-relative paths for internal includes.

```cpp
#include "base/logger.hpp"
#include "storage/face/readable.hpp"
```

**Required:** Use angle-bracket includes for third-party and standard library headers.

```cpp
#include <spdlog/spdlog.h>
#include <boost/asio.hpp>
#include <string>
```

---

## 12. Tooling

### 12.1 clang-format

The repository root contains `.clang-format` encoding the formatting rules from [§3 Code Layout](#3-code-layout) and [§8–9 File Layout](#8-file-layout). Run:

```bash
clang-format -i <file>           # apply formatting
clang-format --dry-run <file>    # check only
```

All code shall be formatted before commit. Most IDEs can be configured to run clang-format on save.

### 12.2 clang-tidy

The repository root contains `.clang-tidy` encoding the static analysis rules from [§4–7](#4-naming-conventions). Each check is annotated as `[Required]` or `[Recommended]` and mapped to the corresponding standard section. Run:

```bash
clang-tidy <file> -- -std=c++17
```

For full project analysis, use the CMake-generated `compile_commands.json`:

```bash
cd build/OSX/Debug
cmake .. -G "Ninja" -DCMAKE_EXPORT_COMPILE_COMMANDS=ON
ninja
run-clang-tidy -p .
```

Required checks should pass clean on new and modified code. Recommended checks may produce warnings; developers should address warnings where practical but are not required to clear all warnings in legacy files.

### 12.3 Build Verification

Before committing, always:

1. Format with clang-format
2. Run clang-tidy on changed files
3. Build without errors or warnings
4. Run tests

Use the repository's build instructions in `README.md` for platform-specific commands.

---

## 13. References

- The Corelinux Consortium. *The Corelinux C++ Coding Standards*. Version 1.6, May 2000.
- Gamma, E., Helm, R., Johnson, R., and Vlissides, J. *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison Wesley, 1995.
- Meyers, S. *Effective C++*, *More Effective C++*, *Effective STL*, and *Effective Modern C++*. Addison Wesley.
- Reddy, M. *API Design for C++*. Morgan Kaufmann, 2011.
- ISO/IEC 14882:2017 — *Programming Language C++* (C++17 Standard).

---

*Revision 2.0 — June 2026. This document supersedes Revision 1.0 (June 2000, last revised March 2020).*

# How to Build a Native App on the GNUS / SuperGenius Platform

This is the recipe for creating a new application (like Genius Tube, Genius AI Boss,
or GeniusWallet) that runs as a native peer on the GNUS and SuperGenius networks.
It is written for both humans and LLM agents: follow it top to bottom and you get a
buildable, correctly-integrated app.

## 1. What an app is

An app is a **native C++17 core plus an optional Flutter presentation layer**.
The C++ core owns networking, identity, cryptography, distributed state, payments,
and protocol validation by linking the platform libraries. Flutter (if present)
renders screens and forwards user intent across an FFI boundary.

The app talks to the world through SuperGenius (peer network, GlobalDB/CRDT,
transactions) and GeniusSDK (the C ABI apps consume), and reads
entitlement/ownership truth from the TokenContracts on EVM.

**Golden rule (from MASTER_ARCHITECTURE.md):** when a capability already exists in
SuperGenius, GeniusSDK, GeniusWallet, or thirdparty, link it. Apps own their
domain logic and build everything else from the platform.

## 2. Workspace layout

Apps live in a shared workspace next to the platform repos:

```
GeniusNetwork/                <- workspace root ("super root")
  SuperGenius/                <- peer network, GlobalDB, accounts, processing
  GeniusSDK/                  <- C ABI + cmake umbrella for platform deps
  GeniusWallet/               <- Flutter wallet, reusable packages, ffigen configs
  TokenContracts/             <- EVM contracts (entitlement truth)
  thirdparty/                 <- ALL dependencies, pinned commits, built from source
  documentation/              <- platform docs (you are here)
  apps/
    your-app/                 <- the new app
    genius-ai-boss/           <- reference app (plugin framework, codegen patterns)
```

Every dependency comes from `thirdparty/` at a pinned commit and is built by CMake,
which makes builds auditable and identical across macOS, Linux, Windows, Android,
and iOS.

## 3. The universal build pattern

Every repo in the workspace — libraries and apps alike — builds the same way:

```bash
cd build/<Platform>          # OSX | Linux | Windows | iOS | Android
mkdir Debug && cd Debug      # or Release, RelWithDebInfo
cmake .. -G Ninja -DCMAKE_BUILD_TYPE=Debug
ninja
ninja install
```

`build/` is the **cmaketemplate** submodule shared by all repos. Its
`build/<Platform>/CMakeLists.txt` is the configure entry point; it sets the
toolchain, platform variables, and `PROJECT_ROOT`, then includes
`cmake/CommonBuildParameters.cmake` from the repo, which descends into `src/`.

Build order for a fresh machine: `thirdparty` -> `SuperGenius` -> `GeniusSDK`
-> your app.

## 4. App repository skeleton

```
your-app/
  build/                      <- cmaketemplate submodule
  cmake/
    CommonBuildParameters.cmake   <- project settings; included by build/<Platform>
    GeniusDependencies.cmake      <- locates workspace (GeniusSDK/SuperGenius/thirdparty)
  include/your_app/           <- public headers, snake_case dir
  src/
    CMakeLists.txt
    platform/<OS>/platform/Platform.hpp   <- one dir per OS, names match build/<Platform>
    generated/CMakeLists.txt              <- codegen targets; output regenerates at build time
    ffi/                        <- C ABI facade (.h + .cpp)
  tools/ffigen/               <- ffigen yaml configs
  tests/
```

Key conventions:

* **Naming**: targets `your_app_*`, include root `include/your_app/`.
* **C++17** — set in the root cmake for every target.
* **Platform abstraction**: source does `#include "platform/Platform.hpp"`. The
  `build/<Platform>/` entry point adds exactly one `src/platform/<OS>/` include
  dir, so platform knowledge lives in one directory per OS.
* **Generated code** regenerates under `src/generated/` via CMake stamp-file
  targets on every build that needs it; the tree stays out of git.

## 5. Consuming the platform

Your `cmake/CommonBuildParameters.cmake` locates the workspace (walk up from the
checkout until a dir containing GeniusSDK, SuperGenius, and thirdparty is found),
then includes `GeniusSDK/cmake/CommonBuildParameters.cmake`, which imports every
thirdparty package and the installed SuperGenius/GeniusSDK CMake configs.
Your targets then link the imported targets (e.g. `GeniusSDK::GeniusSDK`).

Rules of engagement:

* **Wire messages and signing authority come from the platform.** Chain signed
  transactions are the signature of record. App-persisted values are plain C++
  structs; use nlohmann/json (from thirdparty) where serialization is needed.
* **Errors**: follow SuperGenius's `outcome::result<T>` + per-service error enums.
  Retryability is a fixed property of each error code, declared with the enum.
* **Logging**: spdlog for all diagnostic output.
* **Extensibility**: register capabilities as plugins keyed by the FNV-1a hash of
  a versioned string (e.g. `hpke/x25519/aes256gcm/v1`), looked up through a typed
  service locator — see `apps/genius-ai-boss/backend/scaffold/src/singleton/`
  for the pattern.

## 6. Flutter (optional)

Add Flutter when the app has a UI.

* Flutter owns screens, navigation, and rendering.
* The C++ core exposes a **C ABI** (`extern "C"` facade header under
  `include/your_app/ffi/`). All exceptions are caught at the boundary and returned
  as error structs.
* Dart bindings are generated by **ffigen** from that C header. Copy the config
  pattern from `GeniusWallet/packages/genius_api/gen_sgns_ffi.yaml`; drive it from
  a `src/generated/` CMake target. Error codes and strings are exposed as FFI
  functions so Dart reads the taxonomy straight from the core.
* For wallet flows, the reusable **GeniusWallet packages** cover first-party
  identity; **reown_appkit** (the maintained WalletConnect successor) covers
  external EVM wallets.

## 7. Testing and quality gates

* Google Test (from thirdparty), >= 80% coverage target.
* Use the project wait-condition templates (condition_variable/polling) for
  asynchronous test synchronization.
* Crypto test vectors are deterministic and run in both the C++ and Dart harnesses
  from shared versioned fixtures.
* FFI boundary tests run under ASan/UBSan; LeakSanitizer watches key buffers.
  Fuzz the parsers and validators your app owns.
* clang-format / clang-tidy before commit (Allman braces, workspace naming).

## 8. Checklist for a new app

1. Create `apps/your-app/` with the skeleton above; add the cmaketemplate
   submodule at `build/`.
2. Set C++17, target naming, and the platform-include selection in
   `cmake/CommonBuildParameters.cmake`.
3. Add `src/platform/<OS>/platform/Platform.hpp` for each target OS.
4. Verify: `cd build/OSX && mkdir Debug && cd Debug && cmake .. -G Ninja
   -DCMAKE_BUILD_TYPE=Debug && ninja && ninja install` on a clean checkout.
5. Add the C ABI facade + ffigen config (if Flutter), regenerate bindings.
6. Register your app's plugins/services through the locator; write the smoke
   test that assembles your versioned capability strings.
7. Then start domain phases (data model, services, UI).

## Where to read more

* `documentation/MASTER_ARCHITECTURE.md` — repo ownership, trust boundaries,
  how the platform fits together.
* `documentation/docs/technical-information/super-genius-blockchain-technical-details/`
  — GlobalDB key grammar, account/address derivation, ElGamal keys.
* `apps/genius-ai-boss/` — plugin/singleton framework and Jinja2 codegen patterns.
* `GeniusWallet/packages/genius_api/` — ffigen + Flutter FFI consumption pattern.
* `apps/genius-tube/.planning/phases/00-architecture-schema-freeze/00-CONTEXT.md`
  — a worked example of freezing these decisions for a real app.

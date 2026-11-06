<p align="center">
  <a href="https://github.com/vex-graph"><img src="https://raw.githubusercontent.com/vex-graph/vex-graph/main/resources/vexgraph.png" alt="vexgraph" width="48%"></a>
  <img src="https://raw.githubusercontent.com/vex-graph/vex-graph/main/resources/ecosystem.png" alt="ecosystem" width="48%">
</p>

# vex-lib

My own ecosystem for relentless dogfooding.

A vertically integrated, multi-repository systems engineering ecosystem built in
C23 with Rust-owned storage and native C processing. Everything is a pointer.

> **Work in progress — not a finished product suite.** Repositories range from
> implemented slices to partial foundations and empty declared homes. The apps in
> particular are unfinished: their descriptions are goals, not shipped IDE, DAW,
> drawing-studio or game capabilities. Consult the
> [readiness Gist](https://gist.github.com/vex-graph/6943f92acb931b25dad1073c46da6ce7) — see all [gists](https://gist.github.com/vex-graph).

I am a solo developer + I have an AI pair-programming pipeline that treats dense,
explicit, machine-readable architecture as a first-class artifact. No arrow
sugar. No hidden allocations on steady-state paths. No secrets in the arena.

## Current State

**Implemented:** the repository set, the `b`-driven build entry, every component
at mixed readiness, the shared test suite, and the constitution plus its Gists.
**Proven:** macOS builds and the scoped test suites recorded in the workspace test
checklist; see the readiness Gist. **Not finished:** the apps are shells,
scaffolds or blueprints, `meld` (the scene framework) is an empty home, and
`anti`, `drawling` and `impedance` carry little or no source. Windows and Linux
runtime proof is outstanding.

## Scope and Limitations

**Scope:** a vertically integrated C23/Rust ecosystem in four roles — lifetime
(substrate), core (libraries), app (programs with a `main`) and optional tools —
plus the personal `b`, `func` and `job` tools. **Deliberately not covered:** no
monorepo (each repository is independent) and no platform promise beyond the
stated floor. **Known limits and gaps:** Windows/Linux runtime proof, GPU and
audio runtime proof, and application completion are outstanding; nothing here is
a finished product suite.

## Four roles, not a ladder

There are no tiers and no rank order. A role says what a component *is*, not how
important it is.

Role belongs to a **component**, not to a repository. Most repositories carry one
role; a repository with two separable components carries two — `darkbase` is a
core store plus an app, and `api-haven` is a core contract library plus a
gateway tool.

| Role | What it means |
| :--- | :--- |
| **lifetime** | The substrate. Boots first, tears down last, owns OS resources and every byte. |
| **core** | Libraries. Composed by something above them, never launched on their own. |
| **app** | Has a `main`. Nothing links it. |
| **optional tools** | Outside the runtime graph. Run and exit, or are opted into. Never a link dependency of an app that did not ask. |

## lifetime

The substrate. Boots first, tears down last, owns OS resources and every byte.

| Repo | Owns |
| :--- | :--- |
| [`lifetime`](https://github.com/vex-lib/lifetime) | Kernel host: process/application lifecycle, lifetimes, native OS windowing, capability gating and memory substrate attestation. `Kernel_run` lives here. |
| [`relational-engine`](https://github.com/vex-lib/relational-engine) | The only allocator: memory and storage, stable row chunks, variable bindings, cache and native C search over Rust-owned spans. |

`annotation` — the header-only marker vocabulary that every other component
includes — lives in-tree; it is 36 lines and has no repository of its own.

## core

Libraries. Composed by something above them, never launched on their own.

| Repo | Owns |
| :--- | :--- |
| [`vexspoke`](https://github.com/vex-lib/vexspoke) | CPU computation: math, algorithms, containers, synchronization, behavior and network protocols. |
| [`graphvex`](https://github.com/vex-lib/graphvex) | GPU: drawable, compositor, Vulkan pipelines, fonts and SDF raster. |
| [`determinant`](https://github.com/vex-lib/determinant) | Terminal: cell rendering, widgets, CLI parsing and caller-fed input. |
| [`darling-framework`](https://github.com/vex-lib/darling-framework) | Retained human UI: nodes, frame, panel, properties, input and focus. |
| [`language`](https://github.com/vex-lib/language) | Language service: lexer and project index, shipped as dylibs. |
| [`samplerate`](https://github.com/vex-lib/samplerate) | Native audio: CoreAudio/WASAPI/ALSA device output, DSP graph, render and export. |
| [`meld`](https://github.com/vex-lib/meld) | Scene framework: worlds, entities, particles, cameras and the draw list. **Empty home today** — a declared boundary, not shipped code. |
| [`darkbase`](https://github.com/vex-graph/darkbase) | The store half: engine, page chain, protocol and service. The user-facing app half is a separate role below. |
| [`api-haven`](https://github.com/vex-graph/api-haven) | The contract half: JSON-oriented connector shapes — provider registries, `WsSource`, `AiSse`, `DbSqliteFile`, `AssetBroker`. The gateway half is a tool below. |
| [`sesh`](https://github.com/vex-graph/sesh) | Session relay for the suite: sync and VPS transport, online by default. |
| [`harness`](https://github.com/vex-graph/harness) | The agent interface: the AI tool loop and the objects it drives. |

## app

Has a `main`. Nothing links it. An app may link any library, and nothing links
an app.

| Repo | Is |
| :--- | :--- |
| [`semicolon`](https://github.com/vex-suite/semicolon) | Terminal shell and IDE workflows. |
| [`primeagen`](https://github.com/vex-graph/primeagen) | Personal agent client. |
| [`darkbase`](https://github.com/vex-graph/darkbase) | The user-facing store application. Its CLI surface is empty today. |
| [`impedance`](https://github.com/vex-suite/impedance) | Bare-metal DAW over the `samplerate` engine. Two files today. |
| [`anti`](https://github.com/vex-suite/anti) | Game-engine and creative-workflow composition. No source yet. |
| [`drawling`](https://github.com/vex-suite/drawling) | Drawing and animation studio. No source yet. |

## optional tools

Outside the runtime graph. Run and exit, or are opted into. Never linked as a
library by an app that did not ask for them.

| Repo | Is |
| :--- | :--- |
| [`hotcwap`](https://github.com/vex-graph/hotcwap) | Hot-reload utility: dynamic module and executable swapping, ABI airlock. It is not the boot-first host — the Kernel and the window backends live in `lifetime`. |
| [`job`](https://github.com/vex-graph/job) | Update resolver and image publish tool. Ships with `hotcwap` whenever `hotcwap` is included. |
| [`b`](https://github.com/vex-graph/b) | The build system behind `run`, `build` and `export`. |
| [`func`](https://github.com/vex-graph/func) | Compile-time opcode orchestrator. |
| [`api-haven`](https://github.com/vex-graph/api-haven) | The gateway half: the runtime connector surface over the same shapes, for apps that opt in. |
| `vex-test` | The in-tree test host. |
| `tools/` | The workspace scripts: CI, readiness, linting, allocation gate. |

## Three edges: include down, link up, load optional

Only includes are strictly directional. An include points **down** — app may
include core, core may include lifetime, and lifetime includes nothing above
itself. A **link** points the other way: an app links the libraries it consumes.
A **load** is the one optional runtime edge (a tool or a hot-swapped module) and
never becomes a build dependency.

The build enforces all three. `core` never includes an app; `lifetime` never
includes `core`; nothing includes a tool. A repository carrying two roles splits
its includes by component: `darkbase/engine` follows core rules while the
`darkbase` app follows app rules.

**Compose down, never rebuild.** A capability that exists below is referenced,
not re-implemented beside it. Two moves are legal: reference the lower contract,
or grow it in the component that owns it. A duplicate is a defect even when its
own tests pass, and a wrapper may adapt names and defaults but not copy behavior.

**Tests are applications.** A test sits above the component it verifies: it links
that component and anything beneath it, and nothing above it.

## Three organisations, one ecosystem

The repositories are split by what they are, not by who can see them.

| Organisation | Holds |
| :--- | :--- |
| [`vex-lib`](https://github.com/vex-lib) | lifetime and core: the libraries, the shared test suite and the scene framework. |
| [`vex-graph`](https://github.com/vex-graph) | Personal account: the tools, the agent and relay components, and the parts that began personal and stayed there. |
| [`vex-suite`](https://github.com/vex-suite) | Applications: semicolon, impedance, anti and drawling. |

Some parts deliberately live in my personal account. They carry none of the
ecosystem's baggage: no boot obligation, no in-tree build requirement, no
ecosystem-wide contract to keep in step. They stand alone, ship on their own
schedule, and stay useful to someone who never clones the ecosystem. The rule is
one-directional and never a requirement: a personal part must build and run with
no ecosystem checkout; the ecosystem may reference one as an optional
dependency; a component that leans on one is itself optional and must state what
it does without it.

Ownership is not optionality: `hotcwap`, `api-haven` and `harness` are optional
*per app* but remain ecosystem-owned components with a stated role.

## The Law

Architecture is governed by a living constitution through
[preferences.md](https://gist.github.com/vex-graph/4132a6c45cb6d3797c3e8eff2e94035a).
It sets the memory invariants, the object model, and syntactic determinism.

Ownership at the bottom is not negotiable: `lifetime` owns residency and hardware
ground truth, the relational engine owns storage and its lifetimes, `graphvex`
owns shaders and GPU dispatch, and `vexspoke` owns CPU computation. A core
component may borrow either the storage or the computation contract, but a
borrowed contract is a permission, not an implemented dependency. The Vexspoke
memory/container ABI and its default allocator remain until an explicit migration
with owner proof; no C/Rust atomic-layout equivalence and no automatic schema
migration is implied.

Commit dependencies upstream-first — the relational engine before Vexspoke when
it consumes that ABI, lifetime before core, core before app. Per-file commits may
depend on other records in the same verified work cycle.

Standalone and in-tree builds are architectural obligations, not blanket
readiness claims.

## Notable non-negotiables

- `(*ptr).field` — never `->`; every dereference is explicit.
- One class per file. One problem in one file stays in one file.
- Return by value; no caller-provided destination parameters.
- Two-layer access cap. Symmetric getters and setters.
- `Memory_alloc`, `MemoryArena_alloc` and `Transient_alloc` are the only
  allocation entry points. No second allocator.
- Zero steady-state allocation. Bounded waits on every joined thread.
- Includes point down; teardown runs top-down; `Memory_freeAll` is always last.

## Reading a repository

This profile describes the **intended** ownership of an unfinished ecosystem.
Read each repository's own `## Current State` and `## Scope and Limitations`
before treating any capability as shipped, and consult the readiness Gist and
the workspace test checklist for the evidence of record.

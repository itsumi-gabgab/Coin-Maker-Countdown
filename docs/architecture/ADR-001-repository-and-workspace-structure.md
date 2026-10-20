# ADR-001: Repository and Workspace Structure

## Status

Accepted

## Context

Coin Maker Countdown consists of two related applications:

1. A local web application presenting the release countdown, official game
   information, media, development timeline and personal road-to-release
   content.

2. A Windows desktop countdown application providing a lightweight,
   always-available representation of the same release state.

Both applications share project concepts including release configuration,
release-state calculation and game metadata.

Maintaining these shared concerns independently would introduce unnecessary
duplication and increase the possibility of inconsistent behaviour.

The project is maintained by a single developer and does not require the
complexity of a large-scale monorepo orchestration platform.

## Decision

The project will use a single Git repository organised as an npm workspace
monorepo.

The top-level structure will distinguish deployable applications, reusable
packages, source assets and project documentation.

Initial structure:

CoinMakerCountdown/
├── apps/
│   ├── web/
│   └── desktop/
├── packages/
│   ├── core/
│   └── data/
├── assets/
│   ├── official/
│   └── personal/
├── docs/
│   ├── architecture/
│   ├── research/
│   └── sources/
├── package.json
├── package-lock.json
└── tsconfig.base.json

`apps` contains independently executable or distributable applications.

`packages` contains code or data intended to be consumed by more than one
application.

`assets` contains project media. Official source material must be kept
separate from personal or project-created assets.

`docs` contains information about the engineering and provenance of the
project rather than runtime application content.

npm workspaces will provide package linking and workspace-level dependency
management.

## Rationale

A monorepo reflects the fact that the web and desktop applications are two
presentations of the same underlying project rather than unrelated products.

npm workspaces provide sufficient dependency and package management without
introducing an additional orchestration framework such as Nx or Turborepo.

The structure provides explicit architectural boundaries while remaining
small enough to understand directly from the repository tree.

## Consequences

### Positive

- Shared code can be reused without publication to an external package
  registry.
- Dependencies can be managed from a common repository root.
- Changes affecting both applications can be committed atomically.
- Shared domain behaviour can be tested once.
- Architecture remains visible in the directory structure.
- A single repository tracks source code, documentation and asset provenance.

### Negative

- Workspace configuration is slightly more complex than two independent
  projects.
- Desktop-specific dependencies must be prevented from leaking into shared
  packages or the web application.
- Package boundaries must remain deliberate to avoid turning `packages/core`
  into an unstructured collection of utilities.

## Constraints

Shared packages must not depend on application packages.

`packages/core` must remain independent of browser DOM APIs and Electron APIs.

Application-specific functionality belongs in the relevant application.

Additional workspace tooling must not be introduced unless npm workspaces
become demonstrably insufficient.

## Revisit When

Reconsider this decision if:

- the applications become independently maintained products;
- workspace build dependencies become sufficiently complex to justify
  orchestration tooling;
- shared packages require independent versioning or publication;
- the repository grows beyond the scale at which npm workspaces remain
  straightforward.

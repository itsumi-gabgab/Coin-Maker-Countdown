# ADR-002: Web Technology Stack

## Status

Accepted

## Context

The Coin Maker Countdown web application is primarily an interactive
presentation and information application.

Its expected responsibilities include:

- displaying release state;
- presenting countdown information;
- displaying official game information;
- presenting press and media assets;
- presenting a development timeline;
- presenting personal road-to-release statistics;
- providing modest navigation and user interaction;
- adapting its presentation when the release state changes.

The application does not currently require complex client-side application
state, large component hierarchies, server-side rendering or a backend
application.

The project should remain lightweight, usable locally and maintainable as a
production-quality application.

## Decision

The web application will use:

- TypeScript as its implementation language;
- Vite as its development server and build tool;
- standard HTML for document structure;
- standard CSS for presentation;
- browser DOM APIs for interaction.

No client-side UI framework will be introduced initially.

Specifically, React, Vue, Angular and comparable component frameworks are
outside the initial architecture.

No CSS framework will be introduced initially.

Styling will use modern CSS, including custom properties, layout primitives
and other native platform capabilities where appropriate.

## Rationale

The current interface requirements do not justify the runtime cost,
abstraction or additional architectural model of a UI framework.

TypeScript provides static structure and maintainability while continuing to
compile to standard browser JavaScript.

Vite provides modern development and production build tooling without
dictating an application framework.

Native HTML and CSS provide direct control over the project's specialised
visual language:

medieval royal mint
×
working dungeon workshop
×
modern information dashboard.

Avoiding a general-purpose CSS framework prevents its design assumptions from
competing with the project's bespoke visual system.

The absence of a framework is an explicit architectural choice rather than an
instruction to avoid modular design.

## Module Design

Application behaviour should be divided by responsibility rather than placed
in a single entry-point script.

Expected areas include:

src/
├── application/
├── components/
├── views/
├── styles/
└── main.ts

DOM-oriented modules belong to the web application.

Release and countdown domain logic belongs to the shared core package.

Content and structured project data belongs to the shared data package.

## Browser Baseline

The application is a personal local application.

Development may therefore target current evergreen browsers rather than
legacy browser versions.

Browser requirements should be revisited before any decision to deploy the
website publicly.

## Dependencies

The initial web application should contain no production runtime dependency
unless a concrete requirement justifies one.

Initial development tooling may include:

- TypeScript;
- Vite;
- Vitest;
- ESLint;
- typescript-eslint;
- Prettier;
- Node.js type definitions where required.

Dependencies must solve an identified requirement rather than being added in
anticipation of possible future needs.

## Testing

Domain behaviour must be tested independently of the browser interface.

Vitest will be used initially for automated TypeScript tests.

Tests should prioritise behaviour where regression would affect project
correctness, particularly:

- release-window handling;
- exact-release handling;
- countdown calculations;
- transition into released state;
- calendar boundaries;
- invalid release configuration.

UI testing frameworks will not be introduced initially.

## Consequences

### Positive

- Minimal runtime footprint.
- Minimal dependency surface.
- Direct control of markup and styling.
- Fast local development cycle.
- Shared TypeScript code can be consumed by both web and desktop
  applications.
- Application architecture remains understandable without framework-specific
  knowledge.

### Negative

- Component lifecycle and state management must be designed where needed
  rather than supplied by a framework.
- Reusable UI composition requires project conventions rather than a
  framework component model.
- A sufficiently complex future interface could eventually make a dedicated
  UI framework beneficial.

## Explicitly Deferred

The following are deliberately not adopted initially:

- React;
- Vue;
- Angular;
- Tailwind CSS;
- Bootstrap;
- Sass;
- jQuery;
- dedicated state-management libraries;
- dedicated date/time libraries;
- large animation libraries;
- browser end-to-end testing frameworks.

Deferral does not prohibit future adoption when justified by an identified
requirement.

## Revisit When

Reconsider the absence of a UI framework if:

- client-side state becomes substantially more complex;
- extensive dynamic component composition develops;
- maintaining UI lifecycle manually becomes a measurable source of defects;
- future requirements fundamentally alter the application's role.

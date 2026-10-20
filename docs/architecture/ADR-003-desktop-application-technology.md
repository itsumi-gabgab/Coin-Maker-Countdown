# ADR-003: Desktop Application Technology

## Status

Accepted

## Context

Coin Maker Countdown requires a Windows desktop application that provides a
persistent lightweight representation of the game's release state.

Expected desktop capabilities include:

- compact and expanded presentations;
- a frameless window;
- window dragging;
- optional always-on-top behaviour;
- system-tray integration;
- optional launch-at-login behaviour;
- shared release configuration;
- the same release-state semantics as the web application;
- the same broad visual identity as the web application.

A native .NET/WPF application was considered.

WPF would provide strong Windows integration and a native Windows technology
stack, but would require countdown and release-domain behaviour to exist in
both TypeScript and C# or require a separate cross-language integration
mechanism.

The desktop application is primarily a presentation application rather than a
computationally intensive native application.

## Decision

The desktop application will use Electron and TypeScript.

The desktop renderer will use the same general web technology model as the web
application.

Shared release and domain behaviour will come from `packages/core`.

Shared structured project data will come from `packages/data`.

Electron-specific functionality will remain isolated from shared packages.

The intended Electron architecture is:

Electron Main Process
↓
Controlled IPC
↓
Preload Layer
↓
Renderer

The renderer will not be given unrestricted Node.js access.

Electron-specific build tooling will be selected when desktop implementation
begins.

The current preferred candidates are electron-vite for development/build
integration and electron-builder for packaging, subject to validation at the
time desktop development starts.

## Rationale

Electron allows the desktop and web applications to share TypeScript domain
logic directly.

It also allows visual design concepts and potentially suitable presentation
code to be reused without requiring the desktop application to reproduce the
same behaviour using a second UI framework.

This significantly reduces the risk that web and desktop countdown semantics
diverge.

The desktop application's requirements are sufficiently UI-oriented that the
benefit of direct TypeScript and web-technology reuse outweighs the smaller
runtime footprint that a native WPF implementation could provide.

## Security Boundary

Electron APIs must not become dependencies of shared domain code.

The renderer must communicate with privileged desktop functionality through a
deliberately constrained preload/API boundary.

Node.js or filesystem access must not be exposed wholesale to renderer code.

This maintains a meaningful separation between:

- portable application UI;
- shared domain logic;
- privileged operating-system integration.

## Code Sharing

Code should be shared because it represents the same responsibility, not
merely because two applications contain visually similar code.

Expected shared concerns include:

- release configuration types;
- release-state determination;
- countdown calculations;
- game metadata types.

Application window management, system tray behaviour and operating-system
integration belong exclusively to the desktop application.

Web-specific navigation and browser integration belong exclusively to the web
application.

## Dependencies

Electron will not be installed during the initial web/core bootstrap.

Desktop dependencies should be introduced only when active desktop
implementation begins.

This prevents Electron and its associated tooling from becoming dependencies
of repository milestones that do not require the desktop application.

## Consequences

### Positive

- One TypeScript implementation of release-domain behaviour.
- Strong reuse potential between web and desktop presentation.
- Reduced risk of behavioural divergence.
- One principal language across the project.
- Existing web tooling and developer experience transfer naturally to the
  desktop application.

### Negative

- Electron has a larger application distribution and runtime footprint than a
  native WPF implementation.
- Care is required to preserve the security boundary between renderer and
  privileged desktop APIs.
- Native Windows behaviour may occasionally require Electron-specific
  integration.
- Electron upgrades become part of ongoing project maintenance.

## Alternatives Considered

### .NET / WPF

Advantages:

- native Windows technology;
- comparatively lightweight runtime behaviour;
- strong Windows desktop integration;
- mature C# tooling.

Rejected initially because the project would either duplicate release-domain
logic across C# and TypeScript or require additional integration between the
two languages.

WPF remains a viable fallback if Electron proves unsuitable for the final
desktop experience.

## Revisit When

Reconsider Electron if:

- desktop resource consumption is unacceptable for the intended always-on
  countdown use case;
- required Windows integration is materially impaired by Electron;
- Electron packaging or lifecycle behaviour becomes disproportionate to the
  application's purpose;
- the desktop application evolves into a substantially native Windows tool
  rather than a visual companion application.

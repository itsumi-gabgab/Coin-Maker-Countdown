# Coin Maker Countdown

Coin Maker Countdown is an unofficial personal companion project for
**Coin Maker Simulator** by Studio 312.

The project is being built around the road to the game's full release and
consists of two planned applications:

- a local interactive web companion containing release information,
  official game information, media and a release countdown;
- a lightweight Windows desktop countdown application sharing the same
  release state and visual identity.

> [!IMPORTANT]
> Coin Maker Countdown is an unofficial fan/personal project and is not
> affiliated with, endorsed by, or published by Studio 312.
>
> Coin Maker Simulator, its branding, official media and related intellectual
> property belong to their respective owners.

## Release status

The currently confirmed release window for Coin Maker Simulator is:

**March 2027**

An exact release day has not been announced in the first-party sources
reviewed by this project.

Coin Maker Countdown deliberately does not infer a release date from the
month-level release window.

Until an exact date is officially announced, the application will represent
the release as a window rather than generate a fictional day-based countdown.

## Project status

**Early development / architecture and domain bootstrap**

The repository currently contains the development-tooling and architectural
baseline.

Application implementation has not yet begun.

## Planned applications

### Web

A local interactive companion site built with:

- TypeScript
- Vite
- standard HTML
- standard CSS
- browser DOM APIs

No client-side UI or CSS framework is currently planned.

### Desktop

A Windows desktop countdown application is planned using:

- Electron
- TypeScript
- a constrained main/preload/renderer security boundary

Electron dependencies will be introduced when desktop implementation begins.

## Repository structure

```text
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
└── tsconfig.base.json
```

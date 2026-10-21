# ADR-004: Release Domain Modelling

## Status

Proposed

## Decision

Release timing will be represented according to the precision of the
authoritative information available.

The domain will distinguish between:

- month-level release windows;
- exact calendar dates;
- exact release instants.

Missing precision will not be represented by inferred values.

A month-level release window must not be converted into an arbitrary date.

An exact calendar date must not be converted into an arbitrary release
time.

Only an exact release instant may drive a full
days/hours/minutes/seconds countdown.

Release presentation state will be derived from release timing rather than
stored redundantly.

The shared core domain will not depend on JSON, DOM, Node.js or Electron
APIs.

Persistence and mapping of project source data will be the responsibility
of the data package.

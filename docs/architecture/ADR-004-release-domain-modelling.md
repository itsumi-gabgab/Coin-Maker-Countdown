# ADR-004: Release Domain Modelling

## Status

Accepted

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

The domain must also represent the absence of an active known release timing.

Unknown release timing is distinct from month, day and instant precision and
may occur when previously announced timing is withdrawn or superseded without
replacement timing.

Release timing precision and release status are separate domain concepts and
must not be conflated.

A month-level release window expiring does not establish that release has
occurred.

A calendar release date beginning or expiring does not by itself establish
that release has occurred when no exact release instant is known.

Time alone may automatically establish the released state only when the
authoritative release information provides an exact release instant.

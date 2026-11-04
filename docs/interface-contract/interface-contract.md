# Sail-Link — Logical Interface Contract

**Version:** 0.1.0 (draft)  
**Protocol version:** TBD  
**Status:** Functional baseline; schema is illustrative and subject to validation

## 1. Purpose

This document defines the logical information exchanged across the Sail-Link workflow. It deliberately does not define BLE advertising frames, fragmentation, pairing, GATT characteristics, packet sizes, timing guarantees, or other transport-level details. Those decisions remain dependent on the SL-02 feasibility test.

## 2. Source of truth

Expedition is authoritative for the metric catalogue and metric values made available to Sail-Link. Sail-Link must not silently redefine the source units.

The logical contract must accommodate all metrics made available by Expedition. The final metric identifiers, names, value types, units, precision, and metadata must be derived from verified Expedition data; they are not invented in this draft.

## 3. Logical message model

A logical update represents a coherent snapshot of the currently available metric state.

The contract needs to express:

- document/schema version;
- protocol version;
- snapshot identity or sequence;
- snapshot creation/receipt context;
- a collection of metrics;
- for each metric, a stable source identifier, value where available, original unit where applicable, and explicit status.

Exact field names and timestamp semantics are provisional until real Expedition samples and SL-04/SL-06 validation are available.

## 4. Metric status

Each metric must carry an explicit status. The status vocabulary is **TBD** and must be finalized using real source behaviour and tests.

The contract must be able to distinguish at least:
- a metric with a usable value;
- a metric that is invalid;
- a metric that is unavailable;
- a metric whose last update is stale.

Whether an initial/no-value state needs a separate status is also TBD.

No enum values are frozen by this draft. The schema therefore leaves status as a string and documents the unresolved vocabulary.

## 5. Update and snapshot semantics

Internally, Sail-Link may update individual metric values as new Expedition information arrives. The logical data made available to watches must represent a coherent snapshot rather than a partially updated mixture.

The source architecture currently describes retaining the last valid value until a stale timeout. The timeout and the precise interaction between retained values and status transitions remain open.

## 6. Watch configuration contract

Watch display configuration is local to each Garmin application instance:

- configuration mode: role-based or personalized;
- role selection for role-based mode;
- selected metric identifiers;
- display order;
- maximum of four displayed metrics.

The common Sail-Link stream is not filtered separately for each watch. Role-to-metric defaults are not yet specified.

## 7. Versioning

Two version dimensions are required:

1. **Document/schema version:** semantic versioning (SemVer).
2. **Protocol version:** an integer protocol version carried by the logical message.

Initial values and compatibility policy are TBD. A schema/document revision does not automatically imply a protocol change; compatibility rules must be established before the first stable release.

## 8. Transport boundary

The logical contract is independent of the final BLE transport choice. BLE framing is deferred to SL-02. The POC requirement currently describes a unidirectional broadcast from Sail-Link to watches; the final transport feasibility and implementation path must be recorded after SL-02.

## 9. Validation sources

The contract and fixtures must be checked against:
- synthetic fixtures for predictable functional cases;
- anonymized real Expedition samples;
- replay and integration tests defined by the project roadmap.

A real sample must not be represented as validated until its source, anonymization, and mapping have been reviewed.

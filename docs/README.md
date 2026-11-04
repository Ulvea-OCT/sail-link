# Sail-Link Documentation

This directory contains the functional documentation specific to the Sail-Link POC.

The documentation focuses on the product workflow and user-visible behaviour. It intentionally avoids unnecessary implementation details and does not duplicate Ulvea organization-wide policies.

## Documents

| Document | Description |
|---|---|
| [Interface Contract](interface-contract/interface-contract.md) | Logical data contract between Expedition, Sail-Link, and Garmin applications. |
| [Metric Payload Schema](interface-contract/metric-payload.schema.json) | Draft JSON Schema for the logical metric snapshot. |
| [Mock Payloads](mock-payloads/README.md) | Synthetic examples and guidance for anonymized real Expedition samples. |
| [Open Items](decisions/open-items.md) | Requirements and decisions still awaiting confirmation or validation. |

## Functional overview

Sail-Link receives the metrics made available by Expedition and distributes a common data stream to compatible Garmin smartwatch applications. Each watch independently configures which metrics to display, using either a role-based or personalized layout.

The POC has two hardware-selected operating modes:

- **STRL:** autonomous operating mode.
- **CONF:** configuration mode, in which available Wi-Fi networks are shown for user selection.

The Garmin application handles broadcast reading and display configuration. Up to four metrics are displayed on each watch.

## Scope and status

This is a POC requirements baseline. Items marked TBD in the documents remain open and must not be treated as finalized implementation decisions.

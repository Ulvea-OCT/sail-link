# Sail-Link

Sail-Link is a sailing data gateway for making metrics available from Expedition readable on compatible Garmin smartwatches.

The POC validates the functional workflow from Expedition through Sail-Link to multiple Garmin watches. Sail-Link provides a common metric stream; each watch uses its Garmin application to configure its own display.

## POC at a glance

- **Data source:** Expedition.
- **Distribution:** common, unidirectional broadcast to compatible watches.
- **Watch configuration:** role-based or personalized.
- **Display limit:** up to four metrics per watch.
- **Operating modes:** `STRL` and `CONF`, selected by a physical two-position switch.
- **Concurrent-watch goal:** at least six watches.

## Operating modes

- **STRL:** autonomous operating mode.
- **CONF:** configuration mode; available Wi-Fi networks are shown so the user can select a network and connect.

The POC does not include a third selector position or the former `STAL` mode.

## Garmin application

The Garmin application discovers and reads the Sail-Link broadcast and configures the watch display. The user can select a predefined crew role or create a personalized metric selection and order.

The broadcast is common to all watches. Sail-Link does not create a separate metric transmission for each watch.

## Documentation

Project-specific functional documentation, the logical interface contract, schema, mock payloads, and open decisions are maintained in [`docs/`](docs/README.md).

## Project status

This repository describes a POC baseline. BLE framing, metric status vocabulary, stale timeout, role-to-metric defaults, and other unresolved items remain subject to feasibility work and validation. See [open items](docs/decisions/open-items.md).

Organization-wide security, contribution, intellectual-property, and repository policies are maintained centrally by Ulvea and are not duplicated in this repository.

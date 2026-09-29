# SailLink

**Personal telemetry for sailing crews.**

SailLink is a local telemetry bridge for racing sailboats. It receives live data from **Expedition**, processes and normalizes the telemetry, and distributes a unified data stream to **Garmin smartwatches** over local BLE.

The goal is simple:

> **One boat, one telemetry stream, personalized information for every crew member.**

SailLink is designed as a complementary system to existing onboard electronics. It does not replace the navigation system or act as a certified navigation or safety device.

---

## Overview

On a modern racing boat, large amounts of useful data are already available through navigation software and onboard electronics. The problem is that this information is usually concentrated on one or a few shared displays.

Different crew members need different information.

The helmsman, tactician, trimmer and coach may all need data from the same source, but each needs a different subset of metrics at the right time.

SailLink addresses this problem by creating a **local, personalized telemetry layer** between the boat's existing data source and the crew's smartwatches.

```text
                 Boat electronics
                        │
                        ▼
              ┌───────────────────┐
              │     Expedition    │
              │  telemetry source │
              └─────────┬─────────┘
                        │
                     UDP / Wi-Fi
                        │
                        ▼
              ┌───────────────────┐
              │      SailLink     │
              │                   │
              │ UDP receiver      │
              │ Parser            │
              │ Metric register   │
              │ BLE advertiser    │
              │ Configuration     │
              │ Diagnostics / OTA │
              └─────────┬─────────┘
                        │
                  BLE advertising
                        │
          ┌─────────────┼─────────────┐
          ▼             ▼             ▼
      Garmin #1     Garmin #2 ... Garmin #N
          │             │             │
          ▼             ▼             ▼
       Personal      Personal      Personal
       dashboard     dashboard     dashboard
```

The architecture deliberately keeps **Expedition as the authoritative telemetry source**. SailLink forwards and distributes the data rather than becoming another navigation engine.

---

## Current Product Scope

The current MVP focuses on:

* Expedition as the primary telemetry source
* UDP transport over a local Wi-Fi network
* ESP32-S3 as the initial POC hardware platform
* BLE advertising without pairing
* Garmin Connect IQ application
* Personalized metric selection on the watch
* Approximately 1 Hz telemetry updates
* Initial validation with 2–6 Garmin watches
* Local operation without cloud dependency
* Smartphone-based configuration and diagnostics

Direct NMEA 2000/0183 integration, session recording and other navigation software integrations are **not MVP requirements**. They remain possible future extensions.

---

# Repository Purpose

This repository contains the **engineering implementation of SailLink**.

It is intentionally separate from the broader Ulvea management repository.

The repository should contain:

* SailLink firmware
* Garmin Connect IQ application
* Communication protocol definitions
* Development and diagnostic tools
* Automated tests
* Hardware/firmware integration tests
* POC test evidence
* Engineering documentation
* Build and release configuration

Business plans, financial models, corporate governance and general company documentation belong in the Ulvea documentation repository rather than here.

---

# Repository Structure

The repository is organized around the product's technical boundaries.

```text
.
├── firmware/
│   ├── README.md
│   ├── src/
│   ├── include/
│   ├── components/
│   ├── tests/
│   └── sdkconfig.defaults
│
├── garmin/
│   ├── README.md
│   ├── app/
│   ├── resources/
│   └── tests/
│
├── protocol/
│   ├── README.md
│   ├── telemetry.md
│   ├── expedition.md
│   └── schemas/
│
├── tools/
│   ├── udp-generator/
│   ├── packet-analyzer/
│   ├── log-tools/
│   └── diagnostics/
│
├── tests/
│   ├── unit/
│   ├── integration/
│   ├── hardware/
│   └── fixtures/
│
├── docs/
│   ├── architecture/
│   ├── protocol/
│   ├── hardware/
│   ├── testing/
│   └── operations/
│
├── evidence/
│   ├── pcaps/
│   ├── logs/
│   ├── measurements/
│   └── screenshots/
│
├── .github/
│   ├── workflows/
│   ├── ISSUE_TEMPLATE/
│   └── pull_request_template.md
│
├── README.md
├── LICENSE
└── CHANGELOG.md
```

The exact directory structure may evolve as implementation progresses. The important principle is that **firmware, Garmin software, protocol and validation evidence remain clearly separated**.

---

# Architecture

## Data Flow

The current architecture is:

```text
Expedition
    │
    │ UDP
    ▼
SailLink Wi-Fi
    │
    ▼
Expedition parser
    │
    ▼
Unified metric register
    │
    ▼
Telemetry snapshot
    │
    ├── Fragment 0
    ├── Fragment 1
    ├── Fragment 2
    └── ...
    │
    ▼
BLE advertising
    │
    ├── Garmin watch
    ├── Garmin watch
    ├── Garmin watch
    └── Garmin watch
```

SailLink does not maintain a separate dashboard configuration for every watch.

Instead:

* SailLink publishes the unified telemetry stream.
* The Garmin application receives and caches the data.
* Each watch chooses which metrics to display.
* The user interface manages states such as `LIVE`, `STALE` and `SEARCHING`.

This keeps the central unit independent from individual crew roles.

---

# Operating Modes

SailLink currently defines three physical operating modes.

| Mode   | Network         | Purpose                                       |
| ------ | --------------- | --------------------------------------------- |
| `CONF` | SailLink SoftAP | Provisioning, recovery, diagnostics and OTA   |
| `STRL` | Wi-Fi client    | Normal operation on the boat/Starlink network |
| `STAL` | SailLink SoftAP | Standalone operation without the boat router  |

The physical selector makes the operating context explicit and simplifies installation and troubleshooting.

### CONF

Used for:

* Initial configuration
* Wi-Fi credential setup
* Credential recovery
* Diagnostics
* OTA updates

### STRL

Normal operational mode.

SailLink joins the existing boat/Starlink Wi-Fi network and receives Expedition UDP traffic.

### STAL

Standalone mode.

SailLink creates its own Wi-Fi network so that a PC/tablet running Expedition can communicate directly with the device.

---

# Firmware

The initial hardware/software POC is based on:

* **ESP32-S3**
* **ESP-IDF**
* **FreeRTOS**
* Wi-Fi station / SoftAP
* UDP receiver
* BLE advertising
* External 2.4 GHz antenna
* Local diagnostics
* Persistent configuration
* OTA update and recovery

The initial POC BOM explicitly uses ESP32-S3 and ESP-IDF/FreeRTOS, with UDP on the planned port `10110` and fragmented BLE advertising as the Garmin transport.

The firmware is responsible for:

1. Network management
2. Expedition UDP reception
3. Packet validation
4. Expedition protocol parsing
5. Metric normalization
6. Telemetry freshness management
7. BLE snapshot generation
8. BLE advertising
9. Configuration
10. Logging
11. Diagnostics
12. OTA updates
13. Fault recovery

---

# Garmin Application

The Garmin application is the personal interface for each crew member.

Its responsibilities include:

* Discovering SailLink
* Receiving BLE telemetry
* Reconstructing fragmented snapshots
* Maintaining a metric cache
* Selecting displayed metrics
* Selecting role/layout where applicable
* Displaying live telemetry
* Detecting stale telemetry
* Showing connection/search status

The initial UX targets approximately **1–4 metrics per user**, with different dashboard configurations possible for roles such as helmsman, tactician, trimmer and coach.

The first mandatory Garmin validation target is the **Vivoactive 3**, followed by a more recent model and then scaling toward 2–6 simultaneous watches.

---

# Protocol

The protocol layer is intentionally separated from the firmware implementation.

This allows:

* Firmware and Garmin code to evolve independently
* Protocol fixtures to be reused in automated tests
* Captured Expedition traffic to become versioned test vectors
* Malformed and edge-case packets to be reproduced
* Protocol changes to be reviewed independently

The MVP uses repeated full telemetry snapshots with fragmentation when required by the BLE payload constraints.

There is no requirement for delta compression in the initial implementation.

---

# Testing Strategy

SailLink is being developed as a **validation-driven hardware/software project**.

The repository should therefore preserve not only source code but also the evidence required to demonstrate that architectural assumptions are true.

The POC sequence currently covers:

1. ESP32-S3 platform
2. Starlink/local network
3. Expedition protocol
4. Garmin BLE advertising
5. Wi-Fi/BLE coexistence
6. 2–6 watch scaling
7. Power and autonomy
8. Robustness, recovery and OTA
9. Operational cockpit testing

The validation plan explicitly requires firmware/Git version, hardware identification, serial logs, PCAPs where applicable, Garmin screenshots, setup photos and electrical measurements to be attached to test sessions.

---

# Engineering Principles

## 1. Validate before industrializing

The POC exists to reduce technical risk before committing to:

* Custom PCB
* Final battery
* Endurance pack
* IP67 enclosure
* Marine connectors
* Certification

The purpose of the initial BOM is therefore **not to build the final product**, but to validate the main architectural assumptions.

## 2. Evidence over assumptions

Claims about:

* BLE reliability
* Garmin compatibility
* Wi-Fi coexistence
* latency
* packet loss
* autonomy
* thermal behavior
* environmental performance

must be supported by measurements or reproducible tests.

## 3. Keep the architecture simple

Expedition owns navigation calculations.

SailLink owns:

```text
receive → validate → normalize → distribute
```

Garmin owns:

```text
receive → cache → personalize → display
```

This separation reduces coupling between the boat data source, central hardware and user interface.

## 4. Fail explicitly

Telemetry must distinguish between states such as:

```text
SEARCHING
LIVE
STALE
```

Network failures, malformed packets, missing channels and interrupted updates must not silently produce misleading data.

## 5. Hardware decisions follow measurements

Battery size, antenna choice, enclosure and final PCB should be selected from POC measurements rather than assumptions.

---

# Current Validation Gates

The current project should not move to the next hardware stage simply because the software appears functional.

Key gates include:

| Gate              | Required evidence                                   |
| ----------------- | --------------------------------------------------- |
| Expedition        | Parser, checksum, mapping and scaling validated     |
| BLE               | Garmin receives and reconstructs telemetry reliably |
| Scaling           | 2–6 Garmin operate simultaneously                   |
| Radio             | Wi-Fi/BLE coexistence is acceptable                 |
| Power             | Real consumption and autonomy measured              |
| Robustness        | Recovery and OTA behavior validated                 |
| Field             | Operational cockpit test completed                  |
| Industrialization | Evidence supports custom PCB/enclosure decisions    |

The broader product plan also requires a repeatable Expedition → central unit → Garmin chain, at least six watches in the defined pilot context, measured autonomy and successful design-partner validation before production.

---

# Development Workflow

Changes should generally follow this path:

```text
Issue
  ↓
Implementation
  ↓
Unit tests
  ↓
Integration tests
  ↓
Hardware/POC test
  ↓
Evidence
  ↓
Review
  ↓
Merge
  ↓
Release
```

Experimental work should be kept distinguishable from validated behavior.

A POC result is not automatically a product requirement.

A product requirement is not automatically a validated technical capability.

---

# Documentation

Technical documentation belongs close to the code it describes.

Use:

```text
docs/
├── architecture/
├── protocol/
├── hardware/
├── testing/
└── operations/
```

Each major subsystem should have its own technical `README.md`.

For example:

```text
firmware/README.md
garmin/README.md
protocol/README.md
tools/README.md
tests/README.md
```

The root README explains **what SailLink is and how the repository is organized**.

Subsystem READMEs explain **how that subsystem actually works**.

This avoids turning the root README into a complete technical manual.

---

# Relationship with Ulvea Documentation

The product repository is part of the wider Ulvea project but has a deliberately narrower scope.

The Ulvea documentation repository contains higher-level material such as:

* Business plans
* Financial plans
* Company governance
* Compliance planning
* Product strategy
* Technical planning documents
* BOM planning
* POC checklists

For example, the SailLink technical planning set includes the architecture/POC document, BOM/prototyping plan and POC test checklist.

This repository should contain the **implementation and its directly associated engineering evidence**.

---

# Project Status

**Current stage:** POC / technical validation

The architecture is still subject to experimental validation.

The main open technical questions include:

* Expedition protocol details and long-term compatibility
* Reliable BLE advertising reception by Garmin Connect IQ
* Wi-Fi/BLE coexistence
* Reliable operation with multiple watches
* Antenna placement and RF behavior around carbon/metal structures
* Real power consumption
* Battery sizing
* OTA robustness
* Environmental and marine constraints

These questions are deliberately addressed through the POC sequence before final hardware decisions are made.

---

# Non-Goals

The following are **not part of the initial MVP**:

* Replacing Expedition
* Replacing professional navigation systems
* Acting as a certified navigation device
* Direct NMEA 2000 integration
* Direct NMEA 0183 integration
* Cloud-dependent telemetry during racing
* Session recording inside SailLink
* Supporting every Garmin model from day one
* Supporting arbitrary navigation software before the Expedition beachhead is validated

The product positioning is intentionally complementary to existing onboard electronics.

---

# Roadmap

### Phase 1 — Software / Radio POC

* ESP32-S3 firmware
* `CONF / STRL / STAL`
* Starlink/network validation
* Expedition packet capture and parser
* Minimal Garmin application
* BLE advertising protocol
* Snapshot fragmentation

### Phase 2 — Integrated Prototype

* External antenna
* Battery/power solution
* Garmin dashboard
* 2–6 watch testing
* Radio coexistence testing
* Cockpit testing
* Energy measurements

### Phase 3 — Pre-Series

* Custom PCB
* Protected 12V input
* USB-C charging
* Internal battery
* IP67 enclosure
* OTA and diagnostics
* Compliance validation
* Extended scalability testing

This sequencing follows the current technical roadmap and keeps industrialization behind the major technical go/no-go decisions.

---

# Contributing

Before opening a pull request:

* Keep changes focused
* Add or update tests where applicable
* Document protocol changes
* Do not commit secrets or credentials
* Do not commit unreviewed production firmware binaries
* Attach relevant test evidence for hardware changes
* Record hardware revision and firmware commit for physical tests
* Update documentation when behavior or interfaces change

For hardware/firmware validation, reproducibility is more important than simply reporting that a test passed.

---

# License

License and intellectual-property policy are defined separately for the project.

Until the licensing model is formally established, assume that the repository is **not automatically open source** merely because development tools or third-party components are open source.

---

# SailLink in One Sentence

> **SailLink is a local telemetry bridge that turns a boat's existing Expedition data into personalized, live information for every crew member's Garmin smartwatch.**

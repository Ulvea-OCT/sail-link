# sail-link Pre-Foundation Roadmap (F0 → FINAL) — v6

Single source of truth for the pre-foundation plan. The GitHub Actions workflow parses this file, schedules the work, creates/updates the GitHub Project, and populates the native GitHub Roadmap view. Tasks in the backlog are ordered chronologically (by start date, then by founder). Each task has at most 4 scope points; finer detail is added later as sub-issues.

- Team: 9 h/week operating capacity = 3 active founders × 3 h/week; Founder D provides cross-cutting supervision without adding productive capacity.
- Roles: Founder A = Technical Lead / Firmware · Founder B = Garmin UX / Test · Founder C = Product / Customer Discovery · Founder D = cross-cutting Operations / Hardware / Business supervision.
- Branches: two development branches, Garmin app (SL-03, SL-05, SL-07) and Expedition UDP (SL-04, SL-06). The p0 Sail-Link feasibility test (SL-02) is the third pipeline so that all three founders are active from the start. Task assignment is decided separately.
- Test strategy: the architecture is ESP32-based. CI contains only the ESP32 path: the firmware runs under QEMU (Docker) with replayed Expedition data, and the radio-dependent checks (Wi-Fi/BLE) run hardware-in-the-loop (HIL) on the existing ESP32 test unit. Espressif's QEMU does not model the Wi-Fi/Bluetooth radio, so keep the transport behind an interface. Garmin app tests run locally in the Connect IQ simulator and are excluded from CI. Integration tests are independent feature tests (SL-08, SL-09, SL-10) run in parallel.
- Garmin Bluetooth / Connect API study: completed in an earlier definition phase and not a roadmap task.
- Hardware: the existing ESP32 test unit is the prototype and no purchase is planned. If the sign-off (SL-12) finds it insufficient, procurement tasks are added.
- Plan B: if the no-pairing path (Plan A) fails in SL-02, the integration switches to a paired GATT link (see the Plan B section). SL-07 is blocked by SL-02 so the decision is taken first.
- Priority rule: effective Expedition UDP communication is p1; the non-pairing, unidirectional Sail-Link → smartwatch test is p0.
- Task model: keep task skeletons minimal (max 4 scope points); add concrete sub-issues progressively when the work is taken.
- Parallelism: maximum 3 active tasks, one per operating founder; Founder D supervises across workstreams.
- Effort rule: initial effort is s = 3 h, m = 6 h, l = 12 h; low/medium-risk tasks use a 3× factor and high-risk tasks use 4× (the original 1.5×/2× doubled for a wider estimate). Divide adjusted hours by the 9 h/week operating capacity, add 1 week, and round up per task before summation.
- Activity start date: 2026-10-26.
- Non-working periods: 2026-12-15 → 2027-01-15 and one Easter week (2027-03-29 → 2027-04-04).
- FINAL is the Go/No-Go decision gate.

## Scheduler configuration
```yaml
scheduler:
  max_parallel_tasks: 3
```

`max_parallel_tasks` is the maximum number of roadmap tasks that the scheduler may place in the same calendar interval. Dependencies always take precedence: a task cannot start before every task in `blocked_by` has finished.

## Phase calendar

| Phase | Dates | Duration | Gate evidence |
|---|---|---|---|
| F0 | 2026-10-26 → 2026-11-15 | calendar envelope | Security policy and project foundation in place |
| F1 | 2026-11-16 → 2027-02-07 | calendar envelope | Sail-Link feasibility proven without pairing |
| F2 | 2026-11-16 → 2027-03-28 | calendar envelope | Effective Expedition UDP communication proven |
| F3 | 2026-11-16 → 2027-03-28 | calendar envelope | Garmin app and ESP32 Bluetooth / Connect integration working |
| F4 | 2027-04-05 → 2027-05-30 | calendar envelope | End-to-end software validated and stabilized |
| F5 | 2027-05-03 → 2027-05-23 | calendar envelope | ESP32 prototype hardware signed off |
| FINAL | 2027-05-31 → 2027-06-27 | calendar envelope | Final Go/No-Go decision |

## Markers (Project Roadmap)

- 2026-10-26 — Start of F0 foundation
- 2027-02-07 — Gate F1: Sail-Link feasibility proven without pairing
- 2027-03-28 — Gate F2: Effective Expedition UDP communication proven
- 2027-03-28 — Gate F3: Garmin app and ESP32 Bluetooth / Connect integration working
- 2027-05-30 — Gate F4: End-to-end software validated and stabilized
- 2027-05-23 — Gate F5: ESP32 prototype hardware signed off
- 2027-06-27 — FINAL Go/No-Go decision

## Critical path

- Dependency chain: SL-01 → SL-02/SL-04 → SL-07 → SL-08/09/10 → SL-11 → SL-13.
- Hardware sign-off (SL-12) runs in parallel with end-to-end validation (SL-11); there is no purchase chain.
- The three pipelines (Sail-Link feasibility, Garmin app, Expedition UDP) run independently until they converge in the integration tests.
- Hardware stays downstream of software evidence; the ESP32 test unit covers all software and hardware-in-the-loop testing.

## Effort and parallelization

| Metric | Value |
|---|---:|
| Tasks | 13 (was 27 in v2) |
| Founder capacity | 9 h/week operating capacity |
| Human-hours multiplier | 3× low/medium risk; 4× high risk (doubled) |
| Per-task rounding | Round up before summation |
| Maximum simultaneous tasks | 3 |
| Adjusted effort, all tasks | 420 h |
| Base serialized rounded workload | 64 weeks |
| Scheduled working weeks | 29 plus non-working periods |
| Parallelized final date | 2027-06-27 |

> Reference note: dates come from the effort formula with doubled multipliers and are a broad, deliberately wide reference, not a commitment.

## Parallelized task calendar

| ID | Task | Weeks | Start | Target |
|---|---|---:|---|---|
| SL-01 | security-policy-and-project-foundation | 3 | 2026-10-26 | 2026-11-15 |
| SL-02 | sail-link-no-pairing-smartwatch-feasibility-test | 7 | 2026-11-16 | 2027-02-07 |
| SL-03 | garmin-environment-and-app-skeleton | 5 | 2026-11-16 | 2027-01-24 |
| SL-04 | expedition-udp-environment-esp32-qemu-and-replay | 7 | 2026-11-16 | 2027-02-07 |
| SL-05 | garmin-app-user-interface | 5 | 2027-01-25 | 2027-02-28 |
| SL-06 | real-expedition-udp-test-and-constraints | 7 | 2027-02-08 | 2027-03-28 |
| SL-07 | esp32-garmin-bluetooth-connect-integration | 7 | 2027-02-08 | 2027-03-28 |
| SL-08 | integration-test-expedition-udp-to-esp32 | 4 | 2027-04-05 | 2027-05-02 |
| SL-09 | integration-test-esp32-to-watch-ble-and-display | 4 | 2027-04-05 | 2027-05-02 |
| SL-10 | integration-test-resilience-latency-and-data-rate | 4 | 2027-04-05 | 2027-05-02 |
| SL-11 | end-to-end-software-validation-and-stabilization | 4 | 2027-05-03 | 2027-05-30 |
| SL-12 | esp32-prototype-hardware-sign-off | 3 | 2027-05-03 | 2027-05-23 |
| SL-13 | final-software-hardware-go-no-go-decision | 4 | 2027-05-31 | 2027-06-27 |

## Plan B — paired GATT link

- **Trigger:** the SL-02 decision criteria fail, for example the watch does not receive or parse the no-pairing advertising payload reliably on the target models, or the update rate/latency is too poor.
- **Plan B:** the ESP32 acts as a BLE GATT peripheral with a notify characteristic; the Garmin app scans, pairs (secure pairing/bonding) and reads notifications through the Connect IQ BluetoothLowEnergy module.
- **Impact:** SL-07 prototypes the GATT link instead of the advertising path; SL-05 adds a connection-state indicator; SL-09 and SL-10 add connect/reconnect cases. No new task; SL-07 stays high-risk.
- **If Plan B also fails:** a phone relay through Garmin Connect Mobile and the Connect IQ Mobile SDK is the last option; it adds a companion phone app and should trigger a Go/No-Go review before any work starts.

## Changes from v5

- Tasks and dependencies are unchanged.
- Effort multipliers doubled (1.5× → 3×, 2× → 4×); the +1 week per task is kept.
- All dates recomputed with dependencies, a maximum of 3 parallel tasks and the non-working periods.

## Issue backlog (machine-readable)

### SL-01 — security-policy-and-project-foundation
```yaml
id: SL-01
title: security-policy-and-project-foundation
phase: F0
gate: F0
priority: p2
workstream: foundation
risk: low
effort: m
start: 2026-10-26
target: 2026-11-15
blocked_by: []
owners: 1
```

**Objective:** protect the repository, define the working strategy and complete the minimum documentation before the parallel work starts.

**Scope:**
- [ ] Protect `main` (pull requests and reviews required, required status checks, no force-push or deletion).
- [ ] Define the security policy: secrets handling, SECURITY.md, dependency and secret scanning.
- [ ] Define the working strategy: branching, gates, 3 founder pipelines and test strategy (CI covers only the ESP32 path).
- [ ] Write the minimum documentation: README, CONTRIBUTING and the interface contract (message schema, mock payloads).

**Definition of Done:** the declared outcome is completed, the relevant evidence is documented, and the next dependent task has the required information or artifact.

### SL-02 — sail-link-no-pairing-smartwatch-feasibility-test
```yaml
id: SL-02
title: sail-link-no-pairing-smartwatch-feasibility-test
phase: F1
gate: F1
priority: p0
workstream: sail-link
risk: high
effort: l
start: 2026-11-16
target: 2027-02-07
blocked_by: ['SL-01']
owners: 1
```

**Objective:** prove or disprove the non-pairing, unidirectional Sail-Link to smartwatch path and document the decision.

**Scope:**
- [ ] Prepare the minimum test setup, the smartwatch-side path and the success/failure criteria (on the target watch models).
- [ ] Execute the unidirectional Sail-Link to smartwatch test without pairing (Plan A).
- [ ] Capture logs and evidence.
- [ ] Document the result and decide: continue with Plan A or switch to Plan B (paired GATT link).

**Definition of Done:** the declared outcome is completed, the relevant evidence is documented, and the next dependent task has the required information or artifact.

### SL-03 — garmin-environment-and-app-skeleton
```yaml
id: SL-03
title: garmin-environment-and-app-skeleton
phase: F3
gate: F3
priority: p2
workstream: garmin-app
risk: low
effort: l
start: 2026-11-16
target: 2027-01-24
blocked_by: ['SL-01']
owners: 1
```

**Objective:** create the Garmin development environment and a minimal app skeleton that builds and runs in the simulator.

**Scope:**
- [ ] Set up the Garmin development environment and toolchain.
- [ ] Create the minimal Garmin app skeleton.
- [ ] Verify it builds and runs in the local Connect IQ simulator (not in CI).
- [ ] Document build/run steps and link the earlier Garmin Bluetooth / Connect API study.

**Definition of Done:** the declared outcome is completed, the relevant evidence is documented, and the next dependent task has the required information or artifact.

### SL-04 — expedition-udp-environment-esp32-qemu-and-replay
```yaml
id: SL-04
title: expedition-udp-environment-esp32-qemu-and-replay
phase: F2
gate: F2
priority: p1
workstream: expedition-udp
risk: high
effort: l
start: 2026-11-16
target: 2027-02-07
blocked_by: ['SL-01']
owners: 1
```

**Objective:** set up the Expedition UDP environment and an ESP32-under-QEMU test bench that replays Expedition data in CI.

**Scope:**
- [ ] Set up the Expedition UDP test environment; identify the data path and required messages.
- [ ] Implement the UDP receive harness against the interface contract.
- [ ] Run a minimal ESP32 firmware under QEMU (Docker) fed by a recorded or synthetic Expedition feed.
- [ ] Add the QEMU replay test to CI (Wi-Fi and BLE radio stay on real hardware).

**Definition of Done:** the declared outcome is completed, the relevant evidence is documented, and the next dependent task has the required information or artifact.

### SL-05 — garmin-app-user-interface
```yaml
id: SL-05
title: garmin-app-user-interface
phase: F3
gate: F3
priority: p2
workstream: garmin-app
risk: medium
effort: l
start: 2027-01-25
target: 2027-02-28
blocked_by: ['SL-03']
owners: 1
```

**Objective:** design and implement the Garmin app user interface, fed by mock payloads, and verify it in the local simulator.

**Scope:**
- [ ] Define the screens and display layouts from the interface contract.
- [ ] Implement the UI and its display behavior driven by mock payloads.
- [ ] Verify rendering and behavior in the local Connect IQ simulator (not in CI).
- [ ] Document the data model and the simulator limits versus a real watch.

**Definition of Done:** the declared outcome is completed, the relevant evidence is documented, and the next dependent task has the required information or artifact.

### SL-06 — real-expedition-udp-test-and-constraints
```yaml
id: SL-06
title: real-expedition-udp-test-and-constraints
phase: F2
gate: F2
priority: p1
workstream: expedition-udp
risk: high
effort: l
start: 2027-02-08
target: 2027-03-28
blocked_by: ['SL-04']
owners: 1
```

**Objective:** run the effective Expedition UDP communication test and document the result and interface constraints.

**Scope:**
- [ ] Run the real Expedition UDP communication test.
- [ ] Compare behavior with the Docker replay fixture.
- [ ] Document results and interface constraints.
- [ ] Feed findings back into the interface contract.

**Definition of Done:** the declared outcome is completed, the relevant evidence is documented, and the next dependent task has the required information or artifact.

### SL-07 — esp32-garmin-bluetooth-connect-integration
```yaml
id: SL-07
title: esp32-garmin-bluetooth-connect-integration
phase: F3
gate: F3
priority: p2
workstream: bluetooth
risk: high
effort: l
start: 2027-02-08
target: 2027-03-28
blocked_by: ['SL-03', 'SL-02', 'SL-04']
owners: 1
```

**Objective:** prototype and implement the Bluetooth / Connect link between the ESP32 and the Garmin app on the path chosen in SL-02 (Plan A or Plan B).

**Scope:**
- [ ] Prototype message exchange between the ESP32 test unit and the Garmin app skeleton.
- [ ] Implement the integration path against the interface contract.
- [ ] Keep the firmware logic runnable under QEMU in CI; run the BLE radio checks as a HIL script on the ESP32 test unit.
- [ ] Document constraints and open risks.

**Definition of Done:** the declared outcome is completed, the relevant evidence is documented, and the next dependent task has the required information or artifact.

### SL-08 — integration-test-expedition-udp-to-esp32
```yaml
id: SL-08
title: integration-test-expedition-udp-to-esp32
phase: F4
gate: F4
priority: p1
workstream: integration-tests
risk: high
effort: m
start: 2027-04-05
target: 2027-05-02
blocked_by: ['SL-06', 'SL-07']
owners: 1
```

**Objective:** integration test: Expedition UDP data flowing through the ESP32 path.

**Scope:**
- [ ] Define it as an independent feature test.
- [ ] Run it in QEMU CI with the replay fixture.
- [ ] Confirm it with real Expedition data on the ESP32 test unit.
- [ ] Record results and add it to the regression set.

**Definition of Done:** the declared outcome is completed, the relevant evidence is documented, and the next dependent task has the required information or artifact.

### SL-09 — integration-test-esp32-to-watch-ble-and-display
```yaml
id: SL-09
title: integration-test-esp32-to-watch-ble-and-display
phase: F4
gate: F4
priority: p1
workstream: integration-tests
risk: high
effort: m
start: 2027-04-05
target: 2027-05-02
blocked_by: ['SL-05', 'SL-07']
owners: 1
```

**Objective:** integration test: ESP32 data transferred over BLE and shown correctly on the watch.

**Scope:**
- [ ] Define it as an independent feature test.
- [ ] Run it on the ESP32 test unit with the Garmin app on a real watch.
- [ ] Record results and defects.
- [ ] Add it to the regression set.

**Definition of Done:** the declared outcome is completed, the relevant evidence is documented, and the next dependent task has the required information or artifact.

### SL-10 — integration-test-resilience-latency-and-data-rate
```yaml
id: SL-10
title: integration-test-resilience-latency-and-data-rate
phase: F4
gate: F4
priority: p1
workstream: integration-tests
risk: high
effort: m
start: 2027-04-05
target: 2027-05-02
blocked_by: ['SL-04', 'SL-07']
owners: 1
```

**Objective:** integration test: behavior on disconnects, bad or missing data, latency and data-rate limits.

**Scope:**
- [ ] Define fault-injection cases (drop, reconnect, malformed or missing data).
- [ ] Run the functional fault cases in QEMU CI.
- [ ] Measure latency and data-rate budget on the ESP32 test unit.
- [ ] Record results and add the tests to the regression set.

**Definition of Done:** the declared outcome is completed, the relevant evidence is documented, and the next dependent task has the required information or artifact.

### SL-11 — end-to-end-software-validation-and-stabilization
```yaml
id: SL-11
title: end-to-end-software-validation-and-stabilization
phase: F4
gate: F4
priority: p1
workstream: integration-tests
risk: high
effort: m
start: 2027-05-03
target: 2027-05-30
blocked_by: ['SL-08', 'SL-09', 'SL-10']
owners: 1
```

**Objective:** validate and stabilize the end-to-end software path once the three integration tests pass.

**Scope:**
- [ ] Review the three integration test results.
- [ ] Fix and re-run failing cases.
- [ ] Run the full regression set end to end.
- [ ] Declare the software baseline for the final decision.

**Definition of Done:** the declared outcome is completed, the relevant evidence is documented, and the next dependent task has the required information or artifact.

### SL-12 — esp32-prototype-hardware-sign-off
```yaml
id: SL-12
title: esp32-prototype-hardware-sign-off
phase: F5
gate: F5
priority: p2
workstream: hardware-readiness
risk: medium
effort: m
start: 2027-05-03
target: 2027-05-23
blocked_by: ['SL-02', 'SL-06', 'SL-07']
owners: 1
```

**Objective:** confirm the existing ESP32 test unit is sufficient as the prototype and document the hardware requirements proven by the interfaces.

**Scope:**
- [ ] Confirm the existing ESP32 test unit is sufficient as the prototype (no purchase planned).
- [ ] Define ESP32 hardware requirements from the Sail-Link, UDP and BLE results (variant, antenna, power, I/O).
- [ ] Define wearable compatibility from the BLE integration.
- [ ] Record the sign-off and open hardware risks for the final review.

**Definition of Done:** the declared outcome is completed, the relevant evidence is documented, and the next dependent task has the required information or artifact.

### SL-13 — final-software-hardware-go-no-go-decision
```yaml
id: SL-13
title: final-software-hardware-go-no-go-decision
phase: FINAL
gate: FINAL
priority: p0
workstream: final-validation
risk: high
effort: m
start: 2027-05-31
target: 2027-06-27
blocked_by: ['SL-11', 'SL-12']
owners: 1
```

**Objective:** make the final software/hardware Go/No-Go decision from the evidence generated by the roadmap.

**Scope:**
- [ ] Compile the final evidence from F0-F5.
- [ ] Review technical feasibility, software status and hardware readiness.
- [ ] Run the final founder Go/No-Go review.
- [ ] Record the final decision and next steps.

**Definition of Done:** the declared outcome is completed, the relevant evidence is documented, and the next dependent task has the required information or artifact.

## Recommendations

1. **Test the target watch models early.** Connect IQ BLE scanning has user-reported defects with advertising data on some devices; run the SL-02 test on the watch you intend to ship on, not only the simulator.
2. **Keep the transport behind an interface in the firmware.** QEMU then runs the message parsing, encoding and state machines with injected frames, while real Wi-Fi/BLE is exercised only in the HIL checks.
3. **Treat the interface contract as code.** Keep the message schema and mock payloads in the repo as versioned files, reused by the QEMU replay, the Garmin UI mock data and the ESP32 tests.
4. **Run the HIL checks on one self-hosted runner** with a job lock and timeouts, and keep the watch-in-the-loop test (SL-09) as a manual trigger.
5. **Keep security light but real.** Protected `main`, one required review, secret scanning and dependency alerts are enough at this stage.

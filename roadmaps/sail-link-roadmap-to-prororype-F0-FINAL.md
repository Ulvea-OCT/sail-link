# sail-link Pre-Foundation Roadmap (F0 → FINAL)

Single source of truth for the pre-foundation plan. The GitHub Actions workflow parses this file, schedules the work, creates/updates the GitHub Project, and populates the native GitHub Roadmap view.

- Team: 4 founders × 3 h/week = 12 h/week gross.
- Roles: Founder A = Technical Lead / Firmware · Founder B = Garmin UX / Test · Founder C = Product / Customer Discovery · Founder D = Operations / Hardware / Business.
- Hardware purchase rule: hardware work starts only after software feasibility and interface evidence justify the purchase.
- Priority rule: effective Expedition UDP communication is p1; the non-pairing, unidirectional Sail-Link → smartwatch test is p0.
- Connect/Bluetooth sequence: setup environment → Garmin app development → study Bluetooth API → implementation; implementation is blocked by the API study.
- Task model: keep activity/task skeletons minimal; add concrete sub-issues progressively when the work is taken.
- Parallelism: maximum 4 active tasks/subtasks.
- Effort rule: human-hours are multiplied by 2, divided by the 12 h/week team capacity, then increased by 1 week and rounded up per task.
- Activity start date: 2026-10-05.
- Non-working periods: 2026-12-15 → 2027-01-15 and one Easter week.
- FINAL is the Go/No-Go decision gate.

## Scheduler configuration
```yaml
scheduler:
  max_parallel_tasks: 4
```

`max_parallel_tasks` is the maximum number of roadmap tasks that the scheduler may place in the same calendar interval. Dependencies always take precedence: a task cannot start before every task in `blocked_by` has finished.

## Phase calendar

| Phase | Dates | Duration | Gate evidence |
|---|---|---|---|
| F0 | 2026-10-05 → 2026-10-18 | calendar envelope | Foundation and constraints defined |
| F1 | 2026-10-19 → 2027-01-20 | calendar envelope | Sail-Link feasibility proven without pairing |
| F2 | 2026-10-19 → 2027-02-10 | calendar envelope | Effective Expedition UDP communication proven |
| F3 | 2026-10-19 → 2026-11-29 | calendar envelope | Garmin app path working in development environment |
| F4 | 2026-11-02 → 2027-02-03 | calendar envelope | Bluetooth / Connect API understood and integration path proven |
| F5 | 2027-02-11 → 2027-04-21 | calendar envelope | End-to-end software validated and stabilized |
| F6 | 2027-04-22 → 2027-06-09 | calendar envelope | Hardware requirements and BOM ready |
| F7 | 2027-06-10 → 2027-08-11 | calendar envelope | Prototype hardware selected and ordered |
| FINAL | 2027-08-12 → 2027-08-25 | calendar envelope | Final Go/No-Go decision |

## Markers (Project Roadmap)

- 2026-10-05 — Start of F0 foundation
- 2027-01-20 — Sail-Link feasibility gate F1
- 2027-02-10 — Expedition UDP gate F2
- 2026-11-29 — Garmin development gate F3
- 2027-02-03 — Bluetooth / Connect gate F4
- 2027-04-21 — Software stabilization gate F5
- 2027-06-09 — Hardware readiness gate F6
- 2027-08-11 — Prototype hardware order gate F7
- 2027-08-25 — FINAL Go/No-Go decision

## Critical path

- Dependency-consistent critical chain: SL-01 → SL-11 → SL-14 → SL-15 → SL-16 → SL-17 → SL-18 → SL-19 → SL-20 → SL-21 → SL-22 → SL-23 → SL-24 → SL-25 → SL-26 → SL-27.
- Parallel workstreams: Sail-Link feasibility, Expedition UDP, and Garmin / Bluetooth can progress independently until their dependencies converge.
- Hardware is intentionally downstream of the software evidence; no hardware purchase is required to progress through the feasibility, Expedition UDP, Garmin development, or Bluetooth study stages.

## Effort and parallelization

| Metric | Value |
|---|---:|
| Founder capacity | 12 h/week gross |
| Human-hours multiplier | 2× |
| Per-task rounding | Round up before summation |
| Maximum simultaneous tasks | 4 |
| Base serialized rounded workload | 65 weeks |
| Parallelized critical-path duration | 40 weeks |
| Parallelized final date | 2027-08-25 |

## Parallelized task calendar

| ID | Task | Weeks | Start | Target | Primary founder |
|---|---|---:|---|---|---|
| SL-01 | project-foundation-and-constraints | 2 | 2026-10-05 | 2026-10-18 | Founder A |
| SL-02 | define-sail-link-feasibility-test-setup | 2 | 2026-10-19 | 2026-11-01 | Founder A |
| SL-06 | set-up-expedition-udp-development-test-environment | 2 | 2026-10-19 | 2026-11-01 | Founder B |
| SL-11 | create-garmin-development-environment | 2 | 2026-10-19 | 2026-11-01 | Founder C |
| SL-03 | prepare-no-pairing-smartwatch-test-path | 2 | 2026-11-02 | 2026-11-15 | Founder A |
| SL-07 | identify-expedition-udp-data-path-and-message-requirements | 2 | 2026-11-02 | 2026-11-15 | Founder B |
| SL-12 | create-minimal-garmin-app-skeleton | 2 | 2026-11-02 | 2026-11-15 | Founder C |
| SL-14 | study-garmin-bluetooth-connect-api | 3 | 2026-11-02 | 2026-11-22 | Founder D |
| SL-04 | execute-unidirectional-sail-link-to-smartwatch-test | 3 | 2026-11-16 | 2026-12-06 | Founder A |
| SL-08 | implement-expedition-udp-receive-test-harness | 3 | 2026-11-16 | 2026-12-06 | Founder B |
| SL-13 | implement-minimal-garmin-app-data-path | 2 | 2026-11-16 | 2026-11-29 | Founder C |
| SL-15 | prototype-bluetooth-connect-communication | 3 | 2026-11-23 | 2026-12-13 | Founder D |
| SL-05 | document-sail-link-feasibility-result-and-decision | 2 | 2026-12-07 | 2027-01-20 | Founder A |
| SL-09 | execute-effective-expedition-udp-communication-test | 3 | 2026-12-07 | 2027-01-27 | Founder B |
| SL-16 | implement-bluetooth-connect-integration-path | 3 | 2026-12-14 | 2027-02-03 | Founder C |
| SL-10 | document-expedition-udp-result-and-interface-constraints | 2 | 2027-01-28 | 2027-02-10 | Founder A |
| SL-17 | integrate-sail-link-data-into-software-path | 3 | 2027-02-11 | 2027-03-03 | Founder A |
| SL-18 | integrate-garmin-display-output-behavior | 2 | 2027-03-04 | 2027-03-17 | Founder A |
| SL-19 | run-end-to-end-software-validation-and-stabilization | 4 | 2027-03-18 | 2027-04-21 | Founder A |
| SL-20 | define-hardware-requirements-from-proven-software-interfaces | 2 | 2027-04-22 | 2027-05-05 | Founder A |
| SL-21 | define-hardware-compatibility-and-procurement-constraints | 2 | 2027-05-06 | 2027-05-19 | Founder A |
| SL-22 | prepare-hardware-bom-and-selection-criteria | 3 | 2027-05-20 | 2027-06-09 | Founder A |
| SL-23 | evaluate-candidate-prototype-hardware | 3 | 2027-06-10 | 2027-06-30 | Founder A |
| SL-24 | select-prototype-hardware-and-prepare-order | 2 | 2027-07-01 | 2027-07-14 | Founder A |
| SL-25 | approve-hardware-purchase-gate | 2 | 2027-07-15 | 2027-07-28 | Founder A |
| SL-26 | order-prototype-hardware | 2 | 2027-07-29 | 2027-08-11 | Founder A |
| SL-27 | final-software-hardware-go-no-go-decision | 2 | 2027-08-12 | 2027-08-25 | Founder A |

## Issue backlog (machine-readable)

### SL-01 — project-foundation-and-constraints
```yaml
id: SL-01
title: project-foundation-and-constraints
phase: F0
gate: F0
priority: p2
workstream: foundation
risk: low
effort: s
start: 2026-10-05
target: 2026-10-18
blocked_by: []
owners: 1
```

**Objective:** establish the project foundation, constraints and working rules for the Sail-Link pre-foundation programme.

**Scope:**
- [ ] Confirm repository/project conventions and the F0–FINAL progression.
- [ ] Document the software-first and hardware-gating rules.
- [ ] Confirm the four-founder ownership model and maximum four active tasks.
- [ ] Confirm the machine-readable roadmap conventions used by the automation.

**Definition of Done:** the declared outcome is completed, the relevant evidence is documented, and the next dependent task has the required information or artifact.

### SL-02 — define-sail-link-feasibility-test-setup
```yaml
id: SL-02
title: define-sail-link-feasibility-test-setup
phase: F1
gate: F1
priority: p1
workstream: sail-link
risk: medium
effort: m
start: 2026-10-19
target: 2026-11-01
blocked_by: ['SL-01']
owners: 1
```

**Objective:** define a reproducible Sail-Link feasibility test setup before committing to prototype hardware.

**Scope:**
- [ ] Define the minimum setup needed to test Sail-Link communication.
- [ ] Identify the interfaces and test equipment required.
- [ ] Define the success/failure observations for the feasibility test.
- [ ] Avoid hardware procurement until the test requirements are understood.

**Definition of Done:** the declared outcome is completed, the relevant evidence is documented, and the next dependent task has the required information or artifact.

### SL-03 — prepare-no-pairing-smartwatch-test-path
```yaml
id: SL-03
title: prepare-no-pairing-smartwatch-test-path
phase: F1
gate: F1
priority: p0
workstream: smartwatch
risk: medium
effort: m
start: 2026-11-02
target: 2026-11-15
blocked_by: ['SL-02']
owners: 1
```

**Objective:** prepare the no-pairing smartwatch test path so the key feasibility question can be tested with minimal infrastructure.

**Scope:**
- [ ] Prepare the smartwatch-side development/test environment.
- [ ] Define the minimum Sail-Link advertising/output needed for the test.
- [ ] Verify that the test path does not require pairing.
- [ ] Prepare repeatable logging and evidence capture.

**Definition of Done:** the declared outcome is completed, the relevant evidence is documented, and the next dependent task has the required information or artifact.

### SL-04 — execute-unidirectional-sail-link-to-smartwatch-test
```yaml
id: SL-04
title: execute-unidirectional-sail-link-to-smartwatch-test
phase: F1
gate: F1
priority: p0
workstream: smartwatch
risk: high
effort: m
start: 2026-11-16
target: 2026-12-06
blocked_by: ['SL-03']
owners: 1
```

**Objective:** execute the non-pairing, unidirectional Sail-Link → smartwatch feasibility test.

**Scope:**
- [ ] Run the Sail-Link → smartwatch test without pairing.
- [ ] Verify the path is unidirectional from Sail-Link to smartwatch.
- [ ] Record discovery, reception and data observations.
- [ ] Capture evidence to support a binary feasibility decision.

**Definition of Done:** the declared outcome is completed, the relevant evidence is documented, and the next dependent task has the required information or artifact.

### SL-05 — document-sail-link-feasibility-result-and-decision
```yaml
id: SL-05
title: document-sail-link-feasibility-result-and-decision
phase: F1
gate: F1
priority: p0
workstream: sail-link
risk: medium
effort: m
start: 2026-12-07
target: 2027-01-20
blocked_by: ['SL-04']
owners: 1
```

**Objective:** record the Sail-Link feasibility result and the resulting technical decision.

**Scope:**
- [ ] Document test results and observed constraints.
- [ ] Record confirmed limitations and assumptions.
- [ ] Decide whether the feasibility gate is sufficiently evidenced.
- [ ] Feed the result into the next roadmap phase.

**Definition of Done:** the declared outcome is completed, the relevant evidence is documented, and the next dependent task has the required information or artifact.

### SL-06 — set-up-expedition-udp-development-test-environment
```yaml
id: SL-06
title: set-up-expedition-udp-development-test-environment
phase: F2
gate: F2
priority: p1
workstream: expedition-udp
risk: medium
effort: m
start: 2026-10-19
target: 2026-11-01
blocked_by: ['SL-01']
owners: 1
```

**Objective:** set up the Expedition UDP development and test environment.

**Scope:**
- [ ] Set up the development/test environment for Expedition UDP.
- [ ] Define repeatable capture and replay conditions.
- [ ] Document network configuration and test endpoints.
- [ ] Keep the environment independent of prototype hardware where possible.

**Definition of Done:** the declared outcome is completed, the relevant evidence is documented, and the next dependent task has the required information or artifact.

### SL-07 — identify-expedition-udp-data-path-and-message-requirements
```yaml
id: SL-07
title: identify-expedition-udp-data-path-and-message-requirements
phase: F2
gate: F2
priority: p1
workstream: expedition-udp
risk: medium
effort: s
start: 2026-11-02
target: 2026-11-15
blocked_by: ['SL-06']
owners: 1
```

**Objective:** identify the actual Expedition UDP data path, framing and message requirements.

**Scope:**
- [ ] Identify UDP endpoint, port, framing and message structure.
- [ ] Identify required telemetry fields and message semantics.
- [ ] Record unknowns that must be resolved by testing.
- [ ] Produce an interface note for implementation.

**Definition of Done:** the declared outcome is completed, the relevant evidence is documented, and the next dependent task has the required information or artifact.

### SL-08 — implement-expedition-udp-receive-test-harness
```yaml
id: SL-08
title: implement-expedition-udp-receive-test-harness
phase: F2
gate: F2
priority: p1
workstream: expedition-udp
risk: medium
effort: m
start: 2026-11-16
target: 2026-12-06
blocked_by: ['SL-07']
owners: 1
```

**Objective:** implement a minimal receive/test harness for Expedition UDP traffic.

**Scope:**
- [ ] Implement a minimal UDP receive harness.
- [ ] Log received datagrams and basic protocol diagnostics.
- [ ] Support repeatable test/replay inputs.
- [ ] Keep parsing separate from the receive path.

**Definition of Done:** the declared outcome is completed, the relevant evidence is documented, and the next dependent task has the required information or artifact.

### SL-09 — execute-effective-expedition-udp-communication-test
```yaml
id: SL-09
title: execute-effective-expedition-udp-communication-test
phase: F2
gate: F2
priority: p1
workstream: expedition-udp
risk: high
effort: m
start: 2026-12-07
target: 2027-01-27
blocked_by: ['SL-08']
owners: 1
```

**Objective:** prove effective Expedition UDP communication with an actual working data flow.

**Scope:**
- [ ] Connect the test harness to an effective Expedition UDP source.
- [ ] Verify actual packets are received and interpreted.
- [ ] Record evidence of stable communication.
- [ ] Document the conditions under which the test succeeds.

**Definition of Done:** the declared outcome is completed, the relevant evidence is documented, and the next dependent task has the required information or artifact.

### SL-10 — document-expedition-udp-result-and-interface-constraints
```yaml
id: SL-10
title: document-expedition-udp-result-and-interface-constraints
phase: F2
gate: F2
priority: p1
workstream: expedition-udp
risk: medium
effort: m
start: 2027-01-28
target: 2027-02-10
blocked_by: ['SL-09']
owners: 1
```

**Objective:** document the proven Expedition UDP interface and its constraints.

**Scope:**
- [ ] Document the proven UDP interface.
- [ ] Record framing, fields, constraints and failure cases.
- [ ] Identify implications for the Garmin/software path.
- [ ] Use the result as the input to software integration.

**Definition of Done:** the declared outcome is completed, the relevant evidence is documented, and the next dependent task has the required information or artifact.

### SL-11 — create-garmin-development-environment
```yaml
id: SL-11
title: create-garmin-development-environment
phase: F3
gate: F3
priority: p2
workstream: garmin-app
risk: low
effort: m
start: 2026-10-19
target: 2026-11-01
blocked_by: ['SL-01']
owners: 1
```

**Objective:** create the Garmin development environment required for app work.

**Scope:**
- [ ] Install the Garmin/Connect IQ development environment.
- [ ] Verify a minimal app can be built and run.
- [ ] Document SDK/tool versions and setup.
- [ ] Keep development independent of prototype hardware.

**Definition of Done:** the declared outcome is completed, the relevant evidence is documented, and the next dependent task has the required information or artifact.

### SL-12 — create-minimal-garmin-app-skeleton
```yaml
id: SL-12
title: create-minimal-garmin-app-skeleton
phase: F3
gate: F3
priority: p2
workstream: garmin-app
risk: low
effort: m
start: 2026-11-02
target: 2026-11-15
blocked_by: ['SL-11']
owners: 1
```

**Objective:** create the minimal Garmin app skeleton in the development environment.

**Scope:**
- [ ] Create the minimal application structure.
- [ ] Implement only the required skeleton and navigation.
- [ ] Add a minimal data placeholder path.
- [ ] Prepare the app for progressive integration.

**Definition of Done:** the declared outcome is completed, the relevant evidence is documented, and the next dependent task has the required information or artifact.

### SL-13 — implement-minimal-garmin-app-data-path
```yaml
id: SL-13
title: implement-minimal-garmin-app-data-path
phase: F3
gate: F3
priority: p2
workstream: garmin-app
risk: medium
effort: s
start: 2026-11-16
target: 2026-11-29
blocked_by: ['SL-12']
owners: 1
```

**Objective:** implement the minimal Garmin application data path against the proven software interfaces.

**Scope:**
- [ ] Implement the minimal application data path.
- [ ] Connect the app to the agreed software data contract.
- [ ] Verify rendering of representative telemetry.
- [ ] Keep implementation minimal until Bluetooth behavior is proven.

**Definition of Done:** the declared outcome is completed, the relevant evidence is documented, and the next dependent task has the required information or artifact.

### SL-14 — study-garmin-bluetooth-connect-api
```yaml
id: SL-14
title: study-garmin-bluetooth-connect-api
phase: F4
gate: F4
priority: p2
workstream: bluetooth-connect
risk: medium
effort: m
start: 2026-11-02
target: 2026-11-22
blocked_by: ['SL-11']
owners: 1
```

**Objective:** study the Garmin Bluetooth / Connect API and document its usable capabilities and constraints.

**Scope:**
- [ ] Study the available Bluetooth / Connect APIs.
- [ ] Document discovery, scanning, advertising and data constraints.
- [ ] Identify API/version limitations relevant to the target device.
- [ ] Record the findings before implementation starts.

**Definition of Done:** the declared outcome is completed, the relevant evidence is documented, and the next dependent task has the required information or artifact.

### SL-15 — prototype-bluetooth-connect-communication
```yaml
id: SL-15
title: prototype-bluetooth-connect-communication
phase: F4
gate: F4
priority: p2
workstream: bluetooth-connect
risk: high
effort: l
start: 2026-11-23
target: 2026-12-13
blocked_by: ['SL-14']
owners: 1
```

**Objective:** prototype the Bluetooth / Connect communication path after the API study.

**Scope:**
- [ ] Prototype communication using the studied API.
- [ ] Validate discovery and data transfer behavior.
- [ ] Test the smallest viable payload.
- [ ] Record API limitations and implementation constraints.

**Definition of Done:** the declared outcome is completed, the relevant evidence is documented, and the next dependent task has the required information or artifact.

### SL-16 — implement-bluetooth-connect-integration-path
```yaml
id: SL-16
title: implement-bluetooth-connect-integration-path
phase: F4
gate: F4
priority: p2
workstream: bluetooth-connect
risk: high
effort: l
start: 2026-12-14
target: 2027-02-03
blocked_by: ['SL-15', 'SL-13']
owners: 1
```

**Objective:** implement the Bluetooth / Connect integration path based on the proven API behavior.

**Scope:**
- [ ] Implement the validated Bluetooth / Connect integration.
- [ ] Handle reception and basic data validation.
- [ ] Integrate with the Garmin app data path.
- [ ] Document any remaining platform constraints.

**Definition of Done:** the declared outcome is completed, the relevant evidence is documented, and the next dependent task has the required information or artifact.

### SL-17 — integrate-sail-link-data-into-software-path
```yaml
id: SL-17
title: integrate-sail-link-data-into-software-path
phase: F5
gate: F5
priority: p1
workstream: software-integration
risk: high
effort: m
start: 2027-02-11
target: 2027-03-03
blocked_by: ['SL-10', 'SL-16']
owners: 1
```

**Objective:** connect the proven Sail-Link data path to the Garmin software path.

**Scope:**
- [ ] Connect the proven Expedition/Sail-Link data path to Garmin.
- [ ] Verify data reaches the application consistently.
- [ ] Preserve clear boundaries between transport and presentation.
- [ ] Prepare the integrated path for stabilization.

**Definition of Done:** the declared outcome is completed, the relevant evidence is documented, and the next dependent task has the required information or artifact.

### SL-18 — integrate-garmin-display-output-behavior
```yaml
id: SL-18
title: integrate-garmin-display-output-behavior
phase: F5
gate: F5
priority: p2
workstream: software-integration
risk: medium
effort: s
start: 2027-03-04
target: 2027-03-17
blocked_by: ['SL-17']
owners: 1
```

**Objective:** implement the Garmin-side display and output behavior for the integrated data.

**Scope:**
- [ ] Implement the required Garmin display/output behavior.
- [ ] Display representative telemetry clearly.
- [ ] Handle missing or stale data explicitly.
- [ ] Keep the UI scope limited to the validated prototype needs.

**Definition of Done:** the declared outcome is completed, the relevant evidence is documented, and the next dependent task has the required information or artifact.

### SL-19 — run-end-to-end-software-validation-and-stabilization
```yaml
id: SL-19
title: run-end-to-end-software-validation-and-stabilization
phase: F5
gate: F5
priority: p1
workstream: software-integration
risk: high
effort: l
start: 2027-03-18
target: 2027-04-21
blocked_by: ['SL-18']
owners: 1
```

**Objective:** validate and stabilize the complete software path end to end.

**Scope:**
- [ ] Run repeatable end-to-end software tests.
- [ ] Exercise communication failures and recovery.
- [ ] Fix integration defects discovered during validation.
- [ ] Record the stable software baseline.

**Definition of Done:** the declared outcome is completed, the relevant evidence is documented, and the next dependent task has the required information or artifact.

### SL-20 — define-hardware-requirements-from-proven-software-interfaces
```yaml
id: SL-20
title: define-hardware-requirements-from-proven-software-interfaces
phase: F6
gate: F6
priority: p2
workstream: hardware-readiness
risk: medium
effort: m
start: 2027-04-22
target: 2027-05-05
blocked_by: ['SL-05', 'SL-19']
owners: 1
```

**Objective:** derive concrete hardware requirements from the software interfaces that have actually been proven.

**Scope:**
- [ ] Translate proven software interfaces into hardware requirements.
- [ ] Identify required radios, power, connectors and interfaces.
- [ ] Separate mandatory requirements from optional improvements.
- [ ] Produce a hardware requirement baseline.

**Definition of Done:** the declared outcome is completed, the relevant evidence is documented, and the next dependent task has the required information or artifact.

### SL-21 — define-hardware-compatibility-and-procurement-constraints
```yaml
id: SL-21
title: define-hardware-compatibility-and-procurement-constraints
phase: F6
gate: F6
priority: p2
workstream: hardware-readiness
risk: medium
effort: m
start: 2027-05-06
target: 2027-05-19
blocked_by: ['SL-20']
owners: 1
```

**Objective:** define hardware compatibility and procurement constraints from the validated software architecture.

**Scope:**
- [ ] Define hardware compatibility constraints.
- [ ] Define procurement and supplier constraints.
- [ ] Identify risks that could invalidate the software baseline.
- [ ] Document constraints for candidate evaluation.

**Definition of Done:** the declared outcome is completed, the relevant evidence is documented, and the next dependent task has the required information or artifact.

### SL-22 — prepare-hardware-bom-and-selection-criteria
```yaml
id: SL-22
title: prepare-hardware-bom-and-selection-criteria
phase: F6
gate: F6
priority: p2
workstream: hardware-readiness
risk: medium
effort: m
start: 2027-05-20
target: 2027-06-09
blocked_by: ['SL-21']
owners: 1
```

**Objective:** prepare the hardware BOM and objective selection criteria without prematurely purchasing hardware.

**Scope:**
- [ ] Create the prototype hardware BOM.
- [ ] Define objective selection criteria.
- [ ] Compare required specifications against available candidates.
- [ ] Prepare the package needed for hardware evaluation.

**Definition of Done:** the declared outcome is completed, the relevant evidence is documented, and the next dependent task has the required information or artifact.

### SL-23 — evaluate-candidate-prototype-hardware
```yaml
id: SL-23
title: evaluate-candidate-prototype-hardware
phase: F7
gate: F7
priority: p2
workstream: prototype-hardware
risk: medium
effort: m
start: 2027-06-10
target: 2027-06-30
blocked_by: ['SL-22']
owners: 1
```

**Objective:** evaluate candidate prototype hardware against the proven requirements.

**Scope:**
- [ ] Evaluate candidate prototype hardware.
- [ ] Check candidates against the approved requirements.
- [ ] Record technical, availability and procurement observations.
- [ ] Produce an evidence-based candidate comparison.

**Definition of Done:** the declared outcome is completed, the relevant evidence is documented, and the next dependent task has the required information or artifact.

### SL-24 — select-prototype-hardware-and-prepare-order
```yaml
id: SL-24
title: select-prototype-hardware-and-prepare-order
phase: F7
gate: F7
priority: p2
workstream: prototype-hardware
risk: medium
effort: m
start: 2027-07-01
target: 2027-07-14
blocked_by: ['SL-23']
owners: 1
```

**Objective:** select the prototype hardware and prepare the procurement order.

**Scope:**
- [ ] Select the prototype hardware candidate.
- [ ] Confirm compatibility with the validated software interfaces.
- [ ] Prepare the order and required procurement information.
- [ ] Record the selection rationale and evidence.

**Definition of Done:** the declared outcome is completed, the relevant evidence is documented, and the next dependent task has the required information or artifact.

### SL-25 — approve-hardware-purchase-gate
```yaml
id: SL-25
title: approve-hardware-purchase-gate
phase: F7
gate: F7
priority: p2
workstream: prototype-hardware
risk: high
effort: s
start: 2027-07-15
target: 2027-07-28
blocked_by: ['SL-24']
owners: 1
```

**Objective:** approve the hardware purchase only after the preceding feasibility and selection evidence is complete.

**Scope:**
- [ ] Review the complete pre-purchase evidence.
- [ ] Confirm feasibility and hardware requirements are satisfied.
- [ ] Approve or reject the purchase gate based on documented criteria.
- [ ] Record the gate decision.

**Definition of Done:** the declared outcome is completed, the relevant evidence is documented, and the next dependent task has the required information or artifact.

### SL-26 — order-prototype-hardware
```yaml
id: SL-26
title: order-prototype-hardware
phase: F7
gate: F7
priority: p2
workstream: prototype-hardware
risk: medium
effort: s
start: 2027-07-29
target: 2027-08-11
blocked_by: ['SL-25']
owners: 1
```

**Objective:** order the selected prototype hardware.

**Scope:**
- [ ] Place the prototype hardware order.
- [ ] Record supplier, parts, cost and expected delivery.
- [ ] Confirm the ordered configuration matches the approved BOM.
- [ ] Track procurement status.

**Definition of Done:** the declared outcome is completed, the relevant evidence is documented, and the next dependent task has the required information or artifact.

### SL-27 — final-software-hardware-go-no-go-decision
```yaml
id: SL-27
title: final-software-hardware-go-no-go-decision
phase: FINAL
gate: FINAL
priority: p0
workstream: final-validation
risk: high
effort: m
start: 2027-08-12
target: 2027-08-25
blocked_by: ['SL-26']
owners: 1
```

**Objective:** make the final software/hardware Go-No-Go decision using the evidence generated by the roadmap.

**Scope:**
- [ ] Compile the final evidence from F0–F7.
- [ ] Review technical feasibility, software status and hardware readiness.
- [ ] Run the final founder Go/No-Go review.
- [ ] Record the final decision and next steps.

**Definition of Done:** the declared outcome is completed, the relevant evidence is documented, and the next dependent task has the required information or artifact.

````

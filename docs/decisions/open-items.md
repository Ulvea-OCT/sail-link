# Sail-Link POC — Open decisions and clarifications

This list preserves unresolved points rather than filling them with assumptions.

| ID | Topic | Current position | Required follow-up |
|---|---|---|---|
| OI-01 | Power-on behaviour | Not explicitly answered in requirements collection | Define startup behaviour with physical selector in STRL/CONF |
| OI-02 | CONF Wi-Fi selection UI | Networks are to be shown and user selects one | Specify where/how the list is presented and how selection is made |
| OI-03 | Metric status vocabulary | Explicit status per metric required | Define values and exact semantics from real Expedition data |
| OI-04 | STALE timeout | Preliminary expectation around 2–3 seconds; tests decide | Measure and choose timeout |
| OI-05 | BLE framing/transport | Unidirectional broadcast is the functional direction; framing deferred | Complete SL-02 feasibility test and record Plan A/Plan B |
| OI-06 | Role-to-metric defaults | Seven role labels supplied | Define the default metric set and order for each role |
| OI-07 | Role terminology | English working labels proposed | Confirm terminology with sailing users |
| OI-08 | Metric catalogue details | All Expedition-available metrics; Expedition authoritative | Extract and validate identifiers, types, units, precision |
| OI-09 | Version initial values | SemVer document/schema version and integer protocol version required | Set initial versions and compatibility policy |
| OI-10 | Six-watch acceptance vs Q36 | Q34 and Q35 require at least six simultaneous watches; Q36 selected A (software/simulation testing) | Reconcile whether six physical watches are needed for acceptance or whether the six-watch requirement is a target for a later test |
| OI-11 | Source-loss presentation | Hide value and show unavailable; timing preliminary 2–3 seconds | Verify transition and recovery behaviour |
| OI-12 | Real sample fixtures | Both synthetic and anonymized real samples desired | Supply and review real Expedition captures |

## Confirmed POC boundaries

- Physical selector has two positions only: STRL and CONF.
- STAL and a third selector position are outside the POC.
- STRL is the autonomous operating mode.
- CONF presents available Wi-Fi networks for user selection and connection.
- Garmin app handles discovery/reading of the broadcast and per-watch display configuration.
- Role-based and personalized display modes are required.
- Personalized mode supports metric selection and ordering.
- Maximum four displayed metrics per watch.
- At least six simultaneous watches are a POC goal.
- Expedition is authoritative for the metric catalogue; original units are retained.
- The stream is common to all watches; Sail-Link does not tailor transmissions per watch.

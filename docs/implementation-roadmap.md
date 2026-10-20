# Implementation Roadmap

The repository is currently a documentation scaffold aligned with the invention-disclosure draft. The original Arduino sketches and complete wiring/configuration files have not yet been added.

## 1. Reproducible source package

- [ ] Add the helmet transmitter sketch.
- [ ] Add the vehicle-side receiver sketch.
- [ ] Add any shared protocol / threshold header files.
- [ ] Document Arduino IDE version, board package, and required libraries.
- [ ] Record the exact transmitter and receiver board models.

## 2. Hardware documentation

- [ ] Add an approved, as-built wiring diagram.
- [ ] Record sensor module variants (especially MQ-3 vs MQ-135 and SW-420 vs MH-series references).
- [ ] Clarify the AD8232 / AD620AN signal chain and whether the measured source is intended to be ECG, EEG, or another biopotential input.
- [ ] Document electrode setup, signal conditioning, ADC sampling, and signal-quality checks, if cleared for publication.
- [ ] Record nRF24L01 power, channel, data-rate, payload, retry, and timeout settings.
- [ ] Document GPS serial configuration and critical-event acquisition logic.

## 3. Safer decision logic

- [ ] Define a single safety-state table and precedence for helmet, alcohol, fatigue, crash, and sensor-fault states.
- [ ] Default to a disabled simulated-motor state for missing, stale, or malformed data.
- [ ] Add explicit radio-loss and receiver-reset handling.
- [ ] Include a watchdog / timeout plan if supported by the implementation.
- [ ] Keep the bench motor clearly separate from any real vehicle ignition.

## 4. Measurement and test evidence

- [ ] Save representative, unedited transmitter and receiver serial logs.
- [ ] Create repeatable test cases for each scenario.
- [ ] Calibrate sensor thresholds and document environmental dependencies.
- [ ] Test communication range, packet loss, and latency.
- [ ] Measure GPS time-to-fix and coordinate behavior.
- [ ] Use labelled datasets and qualified review before making fatigue-detection accuracy claims.
- [ ] Record failures as well as successful demonstrations.

## 5. Intellectual property and publication

The source draft is an invention-disclosure document marked ©VIT IPR&TTCELL. Before publishing detailed implementation files, claims, complete circuit diagrams, or additional images from that document, obtain clearance from the relevant institution / IP team. This repository currently gives a technical overview rather than reproducing the full disclosure form or its proposed protection claims.

# Implementation Roadmap

The repository currently provides the technical overview for the smart-helmet prototype, including the AD620AN instrumentation amplifier in the EEG-oriented acquisition chain. The original Arduino sketches and complete wiring/configuration files have not yet been added.

## 1. Reproducible source package

- [ ] Add the helmet transmitter sketch.
- [ ] Add the vehicle-side receiver sketch.
- [ ] Add any shared protocol / threshold header files.
- [ ] Document Arduino IDE version, board package, and required libraries.
- [ ] Record the exact transmitter and receiver board models.

## 2. Hardware documentation

- [ ] Add an approved, as-built wiring diagram.
- [ ] Confirm the actual alcohol and vibration sensor modules (project notes refer to MQ-3/MQ-135 and SW-420/MH-series variants).
- [ ] Document how the ECG-oriented sensor/front-end was configured for scalp EEG acquisition.
- [ ] Record the actual signal path through the sensor module and AD620AN, including gain-setting resistor, supply rails, bias/reference, and filter network.
- [ ] Document electrode placement, ADC sampling, and signal-quality checks, if cleared for publication.
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

Before publishing proprietary implementation files, patent claims, complete circuit diagrams, or protected project material, obtain clearance from the relevant institution / IP team. This repository is intended to provide a technical overview of the project.

# Prototype Validation Notes

This page summarizes examples reported in the invention-disclosure draft. It is not an independent re-test of the prototype.

## Scenarios shown in the draft

| Scenario | Example readings / states in draft | Receiver action described |
|---|---|---|
| Normal condition | EEG-related raw readings around 492–515; alcohol-sensor values around 300–311; alcohol NO, crash NO, helmet YES | Simulated motor ON when required conditions are satisfied |
| Alcohol-related unsafe condition | Example alcohol-sensor values around 451–487, with alcohol YES and helmet YES; some EEG-related readings around 233–280 | Simulated motor remains OFF |
| Critical unsafe condition | Example alcohol-sensor values around 505–517, crash YES, low EEG-related readings around 213–260, helmet YES | Simulated motor remains OFF and emergency state is reported |
| Helmet not worn / weak input | Helmet NO and an EEG weak-signal condition; some sensor values absent | Simulated motor remains OFF until required inputs are valid |

**Units caution:** the table's values are copied as reported serial / example values in the draft. The document does not consistently establish a calibrated physical unit for these readings. Treat them as prototype raw values, not clinically meaningful EEG amplitudes or calibrated alcohol concentrations.

## Other observations stated in the draft

- The Arduino Serial Plotter figure shows a signal varying approximately from 257 to 267 raw values and is described as a low-frequency/resting-state variation.
- One section explicitly states that EEG fatigue detection does not work when EEG data is missing; the receiver may show a weak-signal condition unless missing input is handled in code.
- The document describes transmitter and receiver serial output for normal, unsafe, critical, and helmet-not-worn scenarios.

These observations demonstrate a prototype workflow and serial-status reporting, not an established detection accuracy.

## Validation still needed

The draft does not provide a consolidated quantitative report for the following:

- Sensitivity, specificity, false alarms, or missed events for fatigue detection.
- Clinically validated EEG acquisition or fatigue labels.
- Calibrated alcohol concentration or calibration procedure for MQ-3 readings.
- Crash-detection confusion matrix across road vibration / pothole / drop / impact tests.
- Radio packet-loss rate, interference resilience, range, or end-to-end alert latency.
- GPS time-to-fix, location error, or emergency-alert delivery time.
- Receiver safe-state behavior under lost packets, stale payloads, reset, or disconnected sensors.
- Long-duration reliability, power consumption, and helmet comfort / impact-safety effects.

## Recommended repeatable test record

For each run, record the firmware commit, board and module versions, wiring, calibration / threshold settings, scenario applied, transmitter output, receiver output, motor-driver state, timestamp, and any failures. Keep raw logs and label the actual result PASS / FAIL / NOT RUN only after execution.

## Safety statement

The reported motor is a bench demonstrator. Do not infer that this prototype is approved for real-road use, certified crash detection, validated impairment detection, or a medically reliable fatigue assessment.

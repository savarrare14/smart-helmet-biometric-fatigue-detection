# Non-Invasive Smart Helmet with Integrated Biometric Fatigue Detection

An Arduino-based smart-helmet **prototype** that combines rider/helmet status sensing, alcohol-sensor input, vibration-based crash indication, EEG-oriented biopotential acquisition, GPS location capture, and wireless communication with a vehicle-side safety-check unit.

> **Status:** Prototype / proof of concept. This repository contains a public-facing technical summary aligned with the invention-disclosure draft and the project clarification that the AD620 instrumentation amplifier was used in the EEG signal chain. The original firmware source, exact wiring files, and calibrated test dataset have not yet been added. The system is not a certified road-safety product or a clinically validated fatigue detector.

## Project overview

Traditional helmets provide passive impact protection. This prototype explores adding electronic checks that can flag selected unsafe conditions and prevent a **simulated** ignition from being enabled until the receiver-side safety conditions are satisfied.

The helmet-side transmitter is described around an Arduino Uno; a second Arduino Uno acts as the vehicle-side receiver. A pair of nRF24L01 2.4 GHz radio modules transfers helmet status, alcohol-sensor state, vibration/crash flag, and fatigue-related signal/status. A NEO-6M GPS module is used for location capture during critical events.

The ECG-oriented sensor module/front-end was repurposed for EEG-oriented acquisition using scalp biopotential input, with an **AD620 instrumentation amplifier** used to amplify the low-level signal for the prototype's fatigue-related processing. The sensor signal depends on electrode placement; the AD620 amplifies the signal but does not itself convert ECG into EEG.

## System architecture

```mermaid
flowchart TD
  subgraph Helmet["Helmet-side transmitter"]
    IR["IR helmet-wear sensor"]
    MQ3["MQ-3 alcohol sensor"]
    VIB["SW-420 vibration sensor"]
    BIO["ECG-oriented sensor/front-end with scalp electrodes for EEG acquisition"]
    AD620["AD620 instrumentation amplifier"]
    GPS["NEO-6M GPS"]
    TX["Arduino Uno transmitter"]
    IR --> TX
    MQ3 --> TX
    VIB --> TX
    BIO --> AD620 --> TX
    GPS --> TX
    ALARM["Local LED / buzzer / vibration alert"]
    TX --> ALARM
    RADIO1["nRF24L01 transmitter"]
    TX --> RADIO1
  end
  RADIO1 -. 2.4 GHz wireless status payload .-> RADIO2["nRF24L01 receiver"]
  subgraph Vehicle["Vehicle-side receiver / bench demo"]
    RADIO2 --> RX["Arduino Uno receiver"]
    BUTTON["Push-button / key input"] --> RX
    RX --> LOGIC{"Safety conditions all satisfied?"}
    LOGIC -- Yes --> DRIVER["L298N motor driver"]
    DRIVER --> MOTOR["12 V DC motor: simulated ignition"]
    LOGIC -- No --> OFF["Motor remains OFF"]
    RX --> STATUS["Serial status output"]
  end
  TX -. critical-event coordinates .-> GPS
```

This diagram summarizes the intended signal path; it is not an as-built wiring diagram. Confirm actual pin assignments, signal conditioning, radio payload fields, and control flow from the firmware before attempting to reproduce the prototype.

## Hardware described in the draft and project clarification

| Component | Role in the prototype |
|---|---|
| Arduino Uno × 2 | Helmet transmitter and vehicle-side receiver |
| MQ-3 alcohol sensor | Alcohol-related sensor input |
| SW-420 vibration sensor | Abrupt vibration / crash-like event indication |
| IR sensor module | Helmet-wear status input |
| ECG-oriented sensor module/front-end with scalp electrodes | Repurposed for EEG-oriented biopotential acquisition |
| AD620 instrumentation amplifier | Amplifies the low-level biopotential signal used in the EEG/fatigue input chain |
| nRF24L01 modules × 2 | Helmet-to-vehicle wireless status transmission |
| NEO-6M GPS module | Location capture for critical-event handling |
| LED / buzzer / vibration alert | Local warning indication (as implemented) |
| L298N motor driver + 12 V DC motor | Bench-top ignition simulation |
| Push button | Simulated ignition/key input |

**Signal-chain note:** EEG refers to electrical activity acquired from scalp electrodes; ECG refers to cardiac electrical activity. The ECG-oriented front-end was repurposed in this prototype for EEG-oriented acquisition, and the AD620 was used for amplification. The exact gain, filter network, electrode placement, sampling settings, and final analog interconnection should be documented from the actual circuit before making performance claims.

The draft also mentions different alcohol/vibration sensor variants in different sections. The table above reflects the main component list; verify MQ-3 versus MQ-135 and SW-420 versus MH-series references against the hardware that was actually used.

## Operating sequence described in the draft

1. Read helmet-wear status through the IR sensor.
2. Read the MQ-3 alcohol-sensor input and evaluate the configured status/threshold.
3. Monitor vibration input for a crash-like event.
4. Acquire the scalp biopotential signal through the repurposed ECG-oriented front-end and AD620 amplification chain; flag weak or missing signal conditions where supported.
5. Package sensor/status information and transmit it using the nRF24L01 link.
6. On the receiver, evaluate the incoming safety states. The demo motor is enabled only when the required checks pass; otherwise it remains off.
7. On a critical event, the draft describes acquiring GPS coordinates and issuing local/wireless alerts.

The exact threshold values, packet format, timeout behavior, and fail-safe behavior must be verified in the source code; they are not fully specified here.

## Prototype observations

The draft includes serial-output scenarios for a normal condition, an alcohol-related unsafe condition, a combined critical condition, and a helmet-not-worn / weak-signal condition. In the examples, the receiver keeps the simulated motor off when unsafe or incomplete inputs are reported.

The draft also describes an Arduino Serial Plotter trace with small variations in raw readings and explicitly notes one setup where EEG input is absent or weak. These observations show proof-of-concept integration, not validated physiological fatigue detection or real-world crash classification. See [Prototype validation notes](docs/prototype-validation.md).

## Repository contents

- [System architecture](docs/system-architecture.md) — transmitter/receiver flow and decision logic.
- [Hardware and sensors](docs/hardware-and-sensors.md) — component roles and analog front-end notes.
- [Prototype validation](docs/prototype-validation.md) — scenarios reported in the draft, caveats, and tests still needed.
- [Implementation roadmap](docs/implementation-roadmap.md) — source files and measurements to add next.

## Safety, validation, and IP notes

- This is a student engineering prototype, not a certified motorcycle helmet, medical device, or production ignition interlock.
- Do not rely on the prototype to determine whether a rider is sober, alert, or safe to drive.
- Do not connect the demonstrator to a real vehicle's ignition system. The described motor is a bench-top simulation.
- The draft does not establish clinical performance, calibrated alcohol concentration, sensitivity/specificity, crash-detection accuracy, wireless reliability, GPS response latency, or long-duration reliability.
- The uploaded source is an invention-disclosure draft marked ©VIT IPR&TTCELL. This repository summarizes the technical project only; it does not reproduce the full disclosure, internal forms, or detailed proposed protection claims. Obtain institutional/IP-team clearance before publishing additional patent-specific material, detailed schematics, or source files.

## Current repository status

The repository is being documented from the invention-disclosure draft and the clarified AD620 use. The original Arduino sketches, radio packet definitions, pin map, sensor calibration data, and reproducible test logs still need to be added and reviewed. No source implementation should be inferred from this documentation alone.

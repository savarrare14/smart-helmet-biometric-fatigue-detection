# Hardware and Sensor Notes

The table below consolidates the component list and description in the invention-disclosure draft. The draft contains a few naming differences, so the final hardware configuration should be checked against the actual prototype.

| Item | Model / quantity in draft | Described role | Verification note |
|---|---|---|---|
| Controller | Arduino Uno × 2 | One transmitter and one receiver | Confirm exact boards and software versions |
| Alcohol sensor | MQ-3; MQ-135 is also mentioned in one section | Alcohol-related input / unsafe-state flag | Draft's component table specifies MQ-3; verify what was physically used |
| Vibration sensor | SW-420; MH-series vibration sensor mentioned elsewhere | Detect abrupt vibration / crash-like events | Confirm module type and trigger/calibration method |
| Helmet-wear sensor | IR sensor module | Detect whether helmet is worn | Document mounting position and false-positive handling |
| Biopotential front end | AD8232 module + AD620AN amplifier | Signal chain described as EEG / fatigue input | AD8232 is called an ECG module elsewhere in the draft; verify electrodes, signal chain, and intended measurement |
| Radio link | nRF24L01 × 2 | Helmet-to-vehicle status transfer | Add configuration and packet format from firmware |
| GPS | NEO-6M | Location capture during critical events | Capture test fix time and location behavior |
| Alert output | LED; buzzer / vibration alert also described | Local alert for selected states | Include only outputs actually fitted and tested |
| Motor driver | L298N | Drive a simulated ignition load | This is a demonstrator; do not connect to a real vehicle |
| Load | 12 V DC motor | Simulated engine / ignition state | Bench-top prototype only |
| User input | Tactile push button | Simulated ignition-key input | Verify exact receiver logic |

## Biopotential sensing clarification

The draft title and several sections describe EEG-based fatigue detection. The components section lists an AD8232 module and an AD620AN amplifier and describes using their output for brain-activity monitoring. Other sections refer to ECG / EEG interchangeably, and one validation note records a weak or missing EEG signal.

Before publishing implementation specifics, the project should document which sensor front end was actually used, electrode placement, gain / filtering, ADC settings, sampling rate, signal-quality checks, and how fatigue thresholds were derived. The prototype readings in the draft do not establish a clinically valid EEG measurement or fatigue classification.

## Electrical and safety notes

- Check logic levels, common ground, supply requirements, and module pinouts before reconnecting hardware.
- MQ-series sensor readings depend on heater warm-up, calibration, environment, and sensor module design. Do not label raw ADC values as a calibrated blood/breath alcohol concentration.
- A vibration switch can respond to road shocks or handling as well as crash-like impacts; a crash classifier needs additional validation.
- Do not use this demonstrator as a medical diagnostic device or real vehicle ignition interlock.

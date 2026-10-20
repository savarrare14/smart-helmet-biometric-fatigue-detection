# Hardware and Sensor Notes

This page consolidates the component list in the invention-disclosure draft and the project's clarification that the AD620 instrumentation amplifier was used to amplify the signal in the EEG-oriented acquisition chain. The draft has a few differences in sensor naming, so the final bill of materials should be checked against the actual prototype.

| Item | Model / quantity | Described role | Verification note |
|---|---|---|---|
| Controller | Arduino Uno × 2 | One transmitter and one receiver | Confirm exact boards and software versions |
| Alcohol sensor | MQ-3; MQ-135 is also mentioned in one section | Alcohol-related input / unsafe-state flag | The draft's component table specifies MQ-3 |
| Vibration sensor | SW-420; MH-series vibration sensor mentioned elsewhere | Abrupt vibration / crash-like events | Confirm the fitted module and trigger/calibration method |
| Helmet-wear sensor | IR sensor module | Detect whether helmet is worn | Document mounting position and false-positive handling |
| ECG-oriented sensor module/front-end | AD8232 is listed in the draft | Front-end reused for EEG-oriented acquisition through scalp-electrode placement | Document the actual connections and which module's output feeds the AD620 |
| Instrumentation amplifier | AD620AN | Amplification of the low-level biopotential signal for the EEG/fatigue input chain | Add the actual gain-setting resistor, supply, filtering and output range from the circuit |
| Radio link | nRF24L01 × 2 | Helmet-to-vehicle status transfer | Add configuration and packet format from firmware |
| GPS | NEO-6M | Location capture during critical events | Capture test fix time and location behavior |
| Alert output | LED; buzzer / vibration alert also described | Local alert for selected states | Include only outputs actually fitted and tested |
| Motor driver | L298N | Drive a simulated ignition load | Bench demonstrator only; do not connect to a real vehicle |
| Load | 12 V DC motor | Simulated engine / ignition state | Bench-top prototype only |
| User input | Tactile push button | Simulated ignition-key input | Verify exact receiver logic |

## ECG-oriented sensor setup used for EEG acquisition

In this prototype, the ECG-oriented sensor/front-end was repurposed to acquire a scalp biopotential signal for EEG-oriented fatigue monitoring. The **AD620AN instrumentation amplifier** was used to amplify the low-amplitude signal in that chain before it was read by the microcontroller.

Technically, the AD620 does not convert ECG into EEG. The signal being measured is determined by the source and electrode placement: electrodes on the scalp are used for EEG acquisition, while ECG electrodes are normally placed to measure cardiac electrical activity. The amplifier provides gain; it does not change the physiological source of the signal.

For reproducibility, document the actual circuit topology, electrode placement, AD620 gain-setting resistor, supply rails, bias/reference, filtering, ADC input range, sample rate, and signal-quality checks from the build. Do not infer those values from the amplifier model alone.

The prototype readings in the disclosure draft do not establish a clinically validated EEG measurement or fatigue classification.

## Electrical and safety notes

- Check logic levels, common ground, supply requirements, and module pinouts before reconnecting hardware.
- MQ-series sensor readings depend on heater warm-up, calibration, environment, and sensor module design. Do not label raw ADC values as a calibrated blood/breath alcohol concentration.
- A vibration switch can respond to road shocks or handling as well as crash-like impacts; a crash classifier needs additional validation.
- Do not use this demonstrator as a medical diagnostic device or real vehicle ignition interlock.

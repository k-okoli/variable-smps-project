# Variable Benchtop Power Supply (Flyback SMPS, BLE Control)

Mains-powered variable benchtop power supply built around an isolated flyback
SMPS with a multi-output transformer. The flyback secondaries supply a
continuously adjustable CV/CC main output plus two auxiliary USB charge
ports, all derived from a single transformer rather than separate supplies.

Architecture reference: [`docs/system-block-diagram.drawio`](docs/system-block-diagram.drawio)
(import into [diagrams.net](https://app.diagrams.net)).

## Specification

| Parameter | Value |
|---|---|
| Main output | 0-24 V / 0-2 A, continuously adjustable, CV and CC modes |
| Main output power | 48 W max |
| USB-C output | 5 V / 3 A fixed (15 W) — v1. USB-PD up to 60 W reserved as a v2 option (STUSB4500 footprint, not populated in v1) |
| USB-A output | Fast-charge profile (QC3.0 / BC1.2), ~18 W |
| Protection | OVP (crowbar), OCP (shunt + comparator), OTP (thermistor) |
| Input | 230 VAC mains |
| Isolation | Flyback transformer, SELV secondary side |
| Total system power budget (v1) | ~130 W |

The main output spec supersedes earlier figures (15 V / 3 A, 45 W) quoted
during initial scoping — current design point is 0-24 V / 0-2 A.

## Architecture

Single flyback transformer with four secondaries:

1. **Main bus** (~30 V / 2.5 A) → tracking buck pre-regulator (tracks ~2-3 V
   above the commanded output to limit linear dissipation) → CV/CC control
   core (DAC setpoints, shunt current sense, error amp + linear post-reg) →
   0-24 V / 0-2 A output terminals.
2. **USB-C bus** (~22 V / 3 A capacity) → CC logic resistors (Type-C current
   advertisement) → fixed 5 V buck + VBUS current-limit switch → USB-C
   connector. Bus voltage/current headroom is kept above the v1 load so a v2
   PD upgrade (STUSB4500 + PD-capable buck) drops in without a transformer
   respin.
3. **USB-A bus** (~12 V / 2 A) → QC3.0/BC1.2 controller + buck → USB-A
   connector.
4. **Control/aux bus** (~12 V / 1 A) → 5 V / 3.3 V regulation → STM32, BLE
   module, LCD, rotary encoders, status LEDs, fan.

Primary side: mains switch, fuse, NTC inrush limiter, EMI filter (CM choke +
X/Y caps), bridge rectifier + bulk cap, quasi-resonant/active-clamp flyback
controller. Feedback to the primary controller is opto-isolated off the
secondary side (SSR control loop). Output enable/sequencing and fault
handling are managed by the STM32.

## Hardware

- **Topology**: Flyback SMPS, quasi-resonant or active-clamp controller,
  multi-output transformer (single primary, four secondaries)
- **MCU**: STM32 — setpoint DAC control, ADC sensing, supervisory logic, UI,
  BLE link
- **Wireless**: Bluetooth Low Energy (dedicated module + antenna). Wi-Fi is
  not in scope for this design.
- **EDA**: [KiCad](https://www.kicad.org/)
- **Enclosure**: Plastic (chosen for BLE range; requires internal EMI
  shielding consideration given the flyback's switching noise)

## Status

Architecture and power budget defined (see block diagram above); USB-C PD
explicitly deferred to a later revision. Currently in schematic capture and
transformer design.

## Roadmap

- **Schematic + transformer design** — flyback secondary sizing, CV/CC
  control loop, protection circuitry
- **First PCB prototype** — SMPS core, CV/CC control, control/aux rail
- **Firmware skeleton** — setpoint control, ADC sensing, basic UI, BLE
- **Refined prototype** — USB-A/USB-C outputs, enclosure integration
- **Validation** — CV/CC transition response, load regulation, thermal,
  OVP/OCP/OTP trip testing
- **Documentation + release**

## Development Practices

- **Version control**: Git/GitHub for schematics, firmware, and docs
- **Simulation**: SPICE for flyback loop stability before prototyping
- **Testing**: low-voltage isolated bring-up first, then load testing with
  electronic loads, oscilloscope validation of CV/CC transitions and
  protection trip points

## Safety

This is a mains-voltage project. The primary side carries lethal voltages
and must be treated as hazardous at all times. Isolation, creepage/clearance,
and fusing should follow IEC 62368-1 practice; do not operate the primary
side outside an enclosed, isolated test setup.

## Team

Two-person build: power electronics/hardware design, and firmware/UI/
wireless integration, with overlap on system integration and test.

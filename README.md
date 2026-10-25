<h1 align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="Logos/Dark%20Logo.png">
    <source media="(prefers-color-scheme: light)" srcset="Logos/Light%20Logo.png">
    <img alt="Ringwraith" src="Logos/Light%20Logo.png" width="420">
  </picture>
</h1>

<div align="center">

A home-built 5-inch 6S freestyle quad on a Mark4 HD frame, flown with a Radiomaster Pocket over ExpressLRS.<br>
Parts ordered September 2026, built and first flown October 2026.

[![Stars](https://img.shields.io/github/stars/manojeetc/Ringwraith?style=for-the-badge&logo=github&color=F77032)](https://github.com/manojeetc/Ringwraith/stargazers)
[![Forks](https://img.shields.io/github/forks/manojeetc/Ringwraith?style=for-the-badge&logo=github&color=F77032)](https://github.com/manojeetc/Ringwraith/forks)
[![Watchers](https://img.shields.io/github/watchers/manojeetc/Ringwraith?style=for-the-badge&logo=github&color=F77032)](https://github.com/manojeetc/Ringwraith/watchers)
![Views](https://komarev.com/ghpvc/?username=manojeetc-ringwraith&label=views&color=F77032&style=for-the-badge)
[![Last commit](https://img.shields.io/github/last-commit/manojeetc/Ringwraith/main?style=for-the-badge&color=F77032)](https://github.com/manojeetc/Ringwraith/commits/main)
[![Repo size](https://img.shields.io/github/repo-size/manojeetc/Ringwraith?style=for-the-badge&color=F77032)](https://github.com/manojeetc/Ringwraith)

[![Status: flying](https://img.shields.io/badge/status-flying-F77032?style=flat-square&labelColor=0A0A0A)](#flying)
[![Class: 5" freestyle](https://img.shields.io/badge/class-5%22%20freestyle-F77032?style=flat-square&labelColor=0A0A0A)](#at-a-glance)
[![Power: 6S LiPo](https://img.shields.io/badge/power-6S%20LiPo-F77032?style=flat-square&labelColor=0A0A0A)](#battery-care)
[![Build cost: $338](https://img.shields.io/badge/build%20cost-%24338-F77032?style=flat-square&labelColor=0A0A0A)](#bill-of-materials)
[![Firmware: Betaflight](https://img.shields.io/badge/firmware-Betaflight-555555?style=flat-square&labelColor=0A0A0A)](https://betaflight.com)
[![FC: STM32F722](https://img.shields.io/badge/FC-STM32F722-555555?style=flat-square&labelColor=0A0A0A)](#flight-controller-highlights-jhemcu-gf30f722-icm)
[![Link: ExpressLRS 2.4GHz](https://img.shields.io/badge/link-ExpressLRS%202.4GHz-555555?style=flat-square&labelColor=0A0A0A)](https://www.expresslrs.org)
[![Radio: Radiomaster Pocket](https://img.shields.io/badge/radio-Radiomaster%20Pocket-555555?style=flat-square&labelColor=0A0A0A)](#radio-setup-radiomaster-pocket-edgetx)

[Parts](#bill-of-materials) · [Wiring](#wiring) · [Betaflight](#betaflight-setup) · [Radio](#radio-setup-radiomaster-pocket-edgetx) · [Flying](#flying) · [Lessons learned](#lessons-learned) · [Upgrades](#upgrade-ideas)

</div>

## At a glance

| | |
| --- | --- |
| Type | 5" freestyle quadcopter (H-style frame) |
| Battery | 6S LiPo, 1300mAh, XT60 |
| Motors | 2207 1800KV |
| Props | 5" tri-blade |
| Flight controller | STM32F722, Betaflight |
| ESC | 4-in-1, BLHeli_S, 3-6S |
| Radio link | ExpressLRS 2.4GHz (CRSF) |
| Video | None yet (flown line of sight) |
| Expected flight time | About 3 to 4 minutes per pack |
| All-up weight | TBD |

## Bill of materials

| Part | Item | Price |
| --- | --- | --- |
| Frame | MARK4-HD 5" 240mm carbon fiber, frame only | $19.18 |
| Motors | iFlight XING-E Pro 2207 1800KV, x4 | $81.53 |
| Stack | JHEMCU F722 stack: GF30F722-ICM flight controller + RuiBet BLHeli_S 4-in-1 ESC | $75.88 |
| Receiver | SpeedyBee Nano 2.4GHz ELRS | $18.28 |
| Props | iFlight Nazgul F5 5" tri-blade, 5mm shaft, 8 pcs | $11.97 |
| Flight batteries | Ovonic 6S 1300mAh 130C XT60, 2-pack | $30.23 |
| **Drone subtotal** | | **$237.07** |
| Radio | Radiomaster Pocket, ELRS (FCC), Hall gimbals | $78.47 |
| Radio batteries | 18650 3.7V 3200mAh | $22.58 |
| **Total** | | **$338.12** |

Plus shop supplies: XT60 pigtail, low-ESR capacitor, silicone wire, solder, flux, heat shrink, zip ties and hardware.

Full spreadsheet: [Miscellaneous/Ringwraith BOM.xlsx](Miscellaneous/Ringwraith%20BOM.xlsx)

Note: the ESC was ordered as a 55A stack, but the board is marked RuiBet 45A. That's still enough for these motors on 6S in normal flying.

## Flight controller highlights (JHEMCU GF30F722-ICM)

- STM32F722 processor, ICM-42688-P gyro
- 3-8S input, 5V/2.5A and 10V/2A regulators (10V is switched by USER1, meant for an HD video unit)
- 16MB blackbox, barometer, AT7456E analog OSD chip
- 6 UARTs, I2C, LED strip and buzzer pads, HD port, USB-C, boot button
- 30.5 x 30.5mm mounting

## Wiring

```
6S LiPo --XT60--> 4-in-1 ESC (BLHeli_S) ---> 4x XING-E Pro 2207 1800KV
                    |  capacitor across the battery pads
                    |  8-pin harness
                    v
          JHEMCU GF30F722-ICM (F722)
            |  UART, CRSF          |  BZ+ / BZ-
            v                      v
     SpeedyBee Nano ELRS       Buzzer (optional)
            ^
            :  2.4GHz ELRS link
     Radiomaster Pocket
```

**Wiring diagrams** (click to open full size)

<p align="center">
  <a href="Wiring%20Diagrams/FC%20to%20ELRS%20Wiring.svg"><img src="Wiring%20Diagrams/FC%20to%20ELRS%20Wiring.svg" alt="Wiring diagram: flight controller to ExpressLRS receiver" width="48%"></a>
  <a href="Wiring%20Diagrams/FC%20to%20Motor%20Wiring.svg"><img src="Wiring%20Diagrams/FC%20to%20Motor%20Wiring.svg" alt="Wiring diagram: flight controller and ESC to motors" width="48%"></a>
</p>

**Receiver to FC**

| Receiver | FC pad |
| --- | --- |
| 5V | 5V |
| GND | GND |
| TX | RX of UART `TBD` |
| RX | TX of UART `TBD` |

- TX and RX cross over.
- Use thin signal wire (28-30 AWG). Thick wire won't take solder on pads this small.
- The FC's 5V pad is only powered from the battery, not USB. The receiver stays dark on USB alone; that's normal.

## Stack orientation

- **ESC:** harness connector side up, battery pads (+/-) facing the rear.
- **FC:** printed arrow up and pointing forward.
- With the battery pads at the rear, the ESC's motor pads match Betaflight's default layout, so no motor remapping was needed.

## Motor layout and props

```
            FRONT
   M4 (CW)          M2 (CCW)
        \            /
         \  [stack] /
         /          \
        /            \
   M3 (CCW)         M1 (CW)
            REAR
```

Spin directions shown are Betaflight's default (props-in). If "Motor direction is reversed" is turned on, every arrow flips. Always confirm in the Motors tab.

**Props**

- Match the arrow on each prop to its motor's spin. Props marked **R** have a clockwise arrow and go on the clockwise motors.
- Text side up.
- Flanged M5 nylon-insert nut, flange down, tightened snug with an 8mm wrench. Push through the stiff point where the nylon grips, then stop.
- Props only go on or off with no battery and no USB connected.

## Betaflight setup

Configured with the Betaflight App at app.betaflight.com (Chrome or Edge).

| Setting | Value |
| --- | --- |
| Accelerometer | Calibrated with the FC mounted, quad level |
| Ports | Serial RX on the receiver's UART |
| Receiver | Serial (via UART), CRSF |
| ESC protocol | DShot300 |
| Motor poles | 14 (12N14P) |
| Bidirectional DShot | Off (stock BLHeli_S) |
| Battery | Warning 3.5V/cell, minimum 3.3V/cell |
| Throttle limit | Scale, 60-70% while learning |
| Failsafe | Stage 2: Drop (tested: radio off with props off, motors stop) |
| PIDs and rates | Defaults |

**Modes**

| Mode | Switch | Channel | Notes |
| --- | --- | --- | --- |
| ARM | SA (far left, 2-pos) | AUX1 / CH5 | Off at startup. ELRS expects arm on CH5. |
| ANGLE | SB (3-pos) | AUX2 / CH6 | Up and middle positions. Down = acro (no mode). |
| BEEPER | SC (3-pos) | AUX3 / CH7 | One end. Optional turtle mode on the other end. |
| Spare | SD (far right, 2-pos) | AUX4 / CH8 | Unused |

Always click **Save** on each tab, then back up with `diff all` (see Backups).

## Radio setup (Radiomaster Pocket, EdgeTX)

- **Model:** the built-in "Pocket" profile (internal ELRS on, switches already mapped).
- **Internal module:** CRSF.
- **ExpressLRS script** (hold SYS for Tools): packet rate 250Hz, TX Power with Dynamic on, max 250mW.
- **Binding:** receiver and radio on the same major ELRS version. Receiver LED: slow blink = waiting, double blink = bind mode, solid = connected, fast blink = WiFi mode.
- **Battery range:** 6.4V to 8.2V (Li-ion).
- **Timer 1:** 2:30 countdown, runs while the arm switch is in the armed position, voice or beep countdown. Long-press the wheel on the main screen to reset.
- **Throttle curve CV1** (5-point, smooth), applied to the Thr input as a custom curve. It flattens the response around the hover point:

| Point | Stick | Output |
| --- | --- | --- |
| 1 | Bottom | -100 |
| 2 | 1/4 | -60 |
| 3 | Middle | -35 |
| 4 | 3/4 | +10 |
| 5 | Top | +100 |

If hover sits outside the flat zone, nudge point 3. Don't stack this with Betaflight's Throttle MID/EXPO.

Charging: bottom USB-C port. Top USB-C port is for the computer and simulators (choose USB Joystick).

## Flying

**Before every flight**

- [ ] Props tight, undamaged, arrows matching motor spin
- [ ] Battery charged and strapped down firmly
- [ ] Receiver antenna clear of the props
- [ ] Arm switch off, radio on, **then** plug in the battery
- [ ] Receiver LED solid
- [ ] Timer reset

**After landing:** disarm, unplug the battery, **then** turn off the radio. Feel the motors: warm is fine, too hot to hold means something's wrong.

**Flying tips**

- Fly in ANGLE mode, nose pointing away, in a big open field with nobody around.
- Take off decisively to waist or head height; hovering inches off the ground is wobbly.
- Hover throttle is low. Make small, early throttle corrections.
- If it gets away: ease throttle back toward hover and let go of the right stick. If control is lost over open ground, disarm.
- After a crash: disarm immediately, then check props, motor spin, screws and battery.

## Battery care

| Situation | Rule |
| --- | --- |
| Charging | Balance mode at 1C (1.3A), in a LiPo bag, never unattended |
| Full | 4.2V/cell (25.2V). Don't leave packs full for days. |
| Storage | 3.8V/cell (charger storage mode) |
| Landing | Before 3.5V/cell under load |
| Damage | Puffed, dented or punctured packs get recycled, never trashed |

## Lessons learned

- **Signal wire gauge:** 18 AWG wouldn't solder to the receiver pads. Thin 28-30 AWG worked right away.
- **The 3.3V short:** after the receiver work, the FC wasn't detected over USB and one part got hot. 3V3 to GND measured 0.00 ohms on the resistance setting, even though continuity mode didn't beep. A stray solder blob was the cause. Cleaning it off with flux and a clean iron tip fixed it.
- **USB detection test:** a radio prompt on the same cable and port proved the cable and computer were fine, which narrowed the problem to the FC.
- **Modes reset:** settings that aren't saved are lost. Click Save, then keep a `diff all` backup.
- **First flight climb-away:** the throttle is very sensitive on 6S. Fixed with the radio throttle curve and a throttle limit.
- **Never power up with props on indoors.**

## Legal (US)

| Item | Status |
| --- | --- |
| TRUST certificate | TBD |
| FAA DroneZone registration (number marked on the frame) | TBD |
| Remote ID (broadcast module, or fly only at a FRIA) | TBD |

Check airspace with B4UFLY, stay under 400 feet, keep the quad in sight, and use a spotter when flying with goggles.

## Upgrade ideas

- **FPV:** analog for cheap, or digital HD using the FC's HD port and 10V supply
- **ELRS telemetry:** drone battery voltage on the radio with a low-voltage voice callout
- **LED strip:** different colors front and back for line-of-sight orientation
- **GPS:** GPS Rescue, plus Altitude and Position Hold (Betaflight 2025.12 or newer, flashed with those options)
- **Action camera** on the top plate, stabilized with Gyroflow
- **Bluejay** ESC firmware for bidirectional DShot and RPM filtering
- **Blackbox tuning**

## Backups

After any configuration change:

1. Betaflight CLI tab, type `diff all`, press Enter.
2. Save the output as a text file next to this README.

To restore, paste the file into the CLI and type `save`.

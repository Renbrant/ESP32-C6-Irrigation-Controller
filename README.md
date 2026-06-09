# irriBRANT - Advanced 9-Zone Smart Irrigation Controller

<p align="center">
  <img src="docs/banner2.png" alt="irriBRANT Banner">
</p>

<p align="center">
  <strong>Professional-grade ESPHome smart irrigation controller with local scheduling, offline operation, and native Home Assistant integration</strong>
</p>

---

## Overview

**irriBRANT** is a professional-grade smart irrigation controller designed to replace traditional irrigation timers with a modern, automation-first, locally controlled solution.

The project is built around a **Seeed Studio XIAO ESP32-C6**, powered by **ESPHome**, and designed to integrate natively with **Home Assistant** while keeping the core irrigation logic inside the ESP32.

Unlike simple relay-based irrigation controllers, irriBRANT was designed to support:

* Local irrigation scheduling
* Offline operation without Home Assistant
* 9 independent irrigation zones
* 3 configurable irrigation programs
* Zone runtime control
* Repeat cycles
* Persistent settings inside the ESP32
* Native Home Assistant dashboard integration
* Weather-aware automation
* Rain and snow lockout logic
* Future soil moisture and flow monitoring

The result is a flexible, reliable, and expandable irrigation platform for smart homes, DIY automation, and maker projects.

---

# 🚀 Project Status: ACTIVE VALIDATION PHASE

The irriBRANT project has moved beyond concept and prototype design.

The hardware has already been designed, fabricated, assembled, and tested with real firmware. The current development focus is on firmware refinement, dashboard usability, long-term reliability, and weather-aware scheduling.

## Current Progress

* [x] Schematic Design
* [x] PCB Layout & Routing
* [x] Gerber Generation
* [x] PCB Fabrication
* [x] PCB Assembly
* [x] ESPHome Firmware Development
* [x] MCP23017 I/O Expansion Working
* [x] 9-Zone Output Addressing Validated
* [x] Local Zone Control Implemented
* [x] Home Assistant Integration Implemented
* [x] Dashboard Development Started
* [x] ESP32-Based Scheduling Architecture Defined
* [x] 3-Program Irrigation Logic Planned / In Development
* [x] Offline-Capable Architecture Selected
* [ ] Long-Term Field Testing
* [ ] Weather Forecast / Rain / Snow Logic Finalization
* [ ] Enclosure Design
* [ ] Flow Sensor Support
* [ ] Soil Moisture Sensor Support
* [ ] Final Documentation Package

---

# 🧠 Firmware Architecture

irriBRANT is being developed as an **ESPHome standalone irrigation controller**.

Home Assistant is used for dashboard, monitoring, configuration, and remote control, but the long-term design goal is for the ESP32 to remain responsible for the actual irrigation logic.

## ESP32 Responsibilities

The ESP32 is responsible for:

* Zone execution
* Program storage
* Irrigation scheduling
* Runtime logic
* Repeat logic
* Zone enable / disable state
* Irrigation status tracking
* Local persistence
* Manual start / stop actions
* Safety lockouts
* Offline operation

## Home Assistant Responsibilities

Home Assistant is used for:

* Dashboard interface
* Monitoring
* Optional remote control
* Weather data source
* Forecast-based automation assistance
* Diagnostics display
* OTA firmware updates through ESPHome

This architecture allows irriBRANT to continue operating even if Home Assistant is offline, unavailable, or rebooting.

---

# 🌱 Irrigation Program System

The controller is designed to support **3 independent irrigation programs**:

```text
Program A
Program B
Program C
```

Each program can include:

| Feature          | Description                                              |
| ---------------- | -------------------------------------------------------- |
| Enable / Disable | Allows each program to be turned on or off independently |
| Start Time       | Defines when the program starts                          |
| Days of Week     | Selects which days the program is allowed to run         |
| Included Zones   | Selects which active zones are part of the program       |
| Runtime per Zone | Defines how long each zone runs                          |
| Repeat Count     | Allows the same program to repeat multiple times         |
| Repeat Delay     | Defines the waiting time between repeated cycles         |

This allows the controller to support common irrigation strategies such as:

* Deep watering
* Cycle-and-soak
* Morning-only irrigation
* Separate lawn and garden programs
* Seasonal runtime adjustments
* Different watering schedules for different areas

---

# 💧 Zone System

irriBRANT supports **9 independent irrigation zones**.

Each zone is exposed as a controllable valve entity and can be used by:

* Local ESPHome logic
* Home Assistant dashboard cards
* Manual controls
* Scheduled programs
* Weather-aware automation
* Future flow monitoring logic

## Zone Features

Each zone supports:

* Manual open / close
* Program inclusion / exclusion
* Runtime configuration
* Active / inactive configuration
* Individual status feedback
* Individual PCB indicator LED
* Home Assistant entity exposure

The dashboard is being refined to show only the zones that are active in the controller configuration, keeping the interface cleaner and easier to use.

---

# 🆕 Major Hardware Improvements

The current hardware revision introduced several important usability, serviceability, and diagnostic improvements.

## RGB Status LED

A dedicated RGB status LED provides immediate visual feedback for:

* Boot status
* Wi-Fi connection
* ESPHome status
* Error diagnostics
* Irrigation activity
* Future maintenance modes

## Individual Zone LEDs

Each of the 9 irrigation outputs includes an individual yellow status LED.

This makes it possible to identify active zones directly on the PCB during:

* Installation
* Debugging
* Field testing
* Valve troubleshooting
* Firmware validation

## Local Push Button

A tactile push button was added for local interaction.

Planned and current uses include:

* Manual override
* Emergency stop
* Captive portal trigger
* Maintenance actions
* Future local test modes

## Improved Diagnostics

The PCB layout and firmware structure were refined to make troubleshooting easier during real-world testing.

Diagnostic features include:

* Wi-Fi status
* Signal strength
* Uptime
* Schedule status
* Rain lock status
* Irrigation running status
* Zone activity
* System history through Home Assistant

---

# 📸 Real Board Photos

<p align="center">
  <img src="Photos/Board V1.01/20260515_112237.jpg" width="30%">
  <img src="Photos/Board V1.01/20260515_112247.jpg" width="30%">
  <img src="Photos/Board V1.01/20260515_112303.jpg" width="30%">
  <img src="Photos/Board V1.01/20260515_112318.jpg" width="30%">
  <img src="Photos/Board V1.01/20260515_112337.jpg" width="30%">
  <img src="Photos/Board V1.01/20260515_112406.jpg" width="30%">
  <img src="Photos/Board V1.01/20260515_112430.jpg" width="30%">
</p>

---

# 🧩 Hardware Visuals

## PCB Layout

<p align="center">
  <img src="hardware/PCB v1.2/PCB v1.2 top.png" width="400" alt="PCB Top View">
  <img src="hardware/PCB v1.2/PCB v1.2 bottom.png" width="400" alt="PCB Bottom View">
</p>

---

## 3D PCB Renderings

<p align="center">
  <img src="hardware/PCB v1.2/PCB 3D v1.2 a.png" width="280">
  <img src="hardware/PCB v1.2/PCB 3D v1.2 b.png" width="280">
  <img src="hardware/PCB v1.2/PCB 3D v1.2 c.png" width="280">
</p>

---

# 📐 Schematic

The complete schematic for the irrigation controller can be found below.

<p align="center">
  <img src="hardware/PCB v1.2/Schematic_IrrigBrant_v1.2.png">
</p>

---

# 🖥️ Home Assistant Dashboard

The Home Assistant dashboard is being developed as the main user interface for configuration, monitoring, and manual operation.

## Dashboard Goals

The dashboard is designed to provide:

* Clean visual layout
* Manual zone control
* Program control
* Active-zone-only display
* System diagnostics
* Irrigation history
* Weather and rain lock status
* Program execution buttons
* Mobile-friendly control

## Dashboard Sections

Current and planned dashboard areas include:

| Section               | Purpose                                                 |
| --------------------- | ------------------------------------------------------- |
| Zone Control          | Manual operation of active zones                        |
| Program Control       | Run Program A, B, or C                                  |
| Program Configuration | Configure days, start time, zones, runtime, and repeats |
| Diagnostics           | Wi-Fi, uptime, schedule status, rain lock               |
| History               | Logbook and irrigation events                           |
| Weather Logic         | Rain, snow, and forecast-based lockout status           |

<p align="center">
  <img src="Photos/Dashboard/Dashboard sample 01.png">
  <img src="Photos/Dashboard/Dashboard sample 02.png">
</p>

---

# ⚙️ Technical Overview

The irriBRANT platform was engineered with reliability, serviceability, electrical isolation, and expandability as core principles.

---

## 1. Main Controller: Seeed Studio XIAO ESP32-C6

The controller is based on the **Seeed Studio XIAO ESP32-C6**.

The ESP32-C6 provides:

* Wi-Fi 6
* Bluetooth LE
* Zigbee-capable hardware
* Matter-ready hardware platform
* Low power consumption
* Compact footprint
* ESPHome compatibility

This makes the board a future-ready platform for smart irrigation and connected home automation.

---

## 2. I/O Expansion: MCP23017

The **MCP23017 I2C I/O expander** manages the irrigation output control lines while preserving ESP32 GPIOs for other functions.

Benefits include:

* Clean GPIO expansion
* Simplified PCB routing
* Easy support for 9 outputs
* Better firmware organization
* Room for future expansion

---

## 3. Power System

The board is designed to work with standard irrigation transformer power.

## Input

```text
24VAC irrigation transformer
```

## Power Conversion Chain

```text
24VAC Input
→ Bridge Rectifier
→ Filtering Stage
→ Buck Converter
→ 5V Rail
→ ESP32 3.3V Regulation
```

The power stage is designed to provide a stable DC supply for the ESP32 and logic circuitry while the 24VAC side remains available for valve switching.

---

## 4. Valve Switching: Optoisolated Triac Outputs

Each irrigation valve is controlled through an optoisolated AC switching stage.

## Main Components

### MOC3041 Optocouplers

The optocouplers provide:

* Galvanic isolation
* Zero-cross switching
* Reduced electrical noise
* Safer separation between logic and valve power
* Improved reliability for AC valve loads

### BT136S Triacs

The output stage uses BT136S surface-mount triacs for AC switching.

Benefits include:

* Solid-state switching
* Silent operation
* No relay contacts
* No mechanical wear
* Compact PCB footprint
* Suitable for low-current 24VAC irrigation solenoids

Depending on sourcing and design revision, the board may use BT136S-600D or BT136S-800D class devices.

---

## 5. Protection & Signal Integrity

## RC Snubber Network

Each output includes an RC snubber network to help suppress transients generated by inductive irrigation valves.

Typical network:

```text
47Ω resistor
10nF capacitor
```

## Fuse Protection

A replaceable blade fuse protects the board and transformer side from excessive current events.

The fuse helps protect:

* PCB traces
* Valve power path
* Irrigation transformer
* Output switching stage

---

# 🔌 Home Assistant Integration

irriBRANT was built to work naturally with Home Assistant through ESPHome.

## Supported Features

* Native ESPHome integration
* Individual valve entities
* Manual zone control
* Program start buttons
* System diagnostics
* OTA firmware updates
* Wi-Fi status monitoring
* Signal strength monitoring
* Uptime monitoring
* Rain lock status
* Irrigation history
* Weather-based automations
* Dashboard customization

## Home Assistant as Optional Layer

The project direction is to avoid depending on Home Assistant helpers, scripts, or automations for the core irrigation logic.

The ESP32 should remain responsible for the actual watering schedule and execution.

Home Assistant becomes the interface, not the brain.

---

# 🌦️ Weather-Aware Irrigation

The project is being designed to support weather-aware irrigation decisions.

## Current and Planned Weather Inputs

irriBRANT can be integrated with Home Assistant weather data sources such as:

* Current rain condition
* Rain intensity
* Forecasted rain
* Forecasted snow
* Temperature
* Wind
* Humidity
* Evapotranspiration-related sensors
* Smart Irrigation integrations

## Weather Logic Goals

The weather-aware logic is planned to support:

* Rain lock
* Snow lock
* Forecast-based skip
* Rain delay
* Seasonal adjustment
* Water-saving operation
* Optional evapotranspiration-based runtime adjustment

This allows the system to avoid unnecessary irrigation when precipitation is occurring or likely to occur soon.

---

# 🛠️ Firmware Structure

The ESPHome firmware is organized into modular packages to keep the project easier to maintain.

Expected package structure:

```text
irribrant_vX_X.yaml
packages/
  hardware.yaml
  irrigation.yaml
  programs.yaml
  scheduler.yaml
  diagnostics.yaml
```

## Package Responsibilities

| Package          | Responsibility                                   |
| ---------------- | ------------------------------------------------ |
| hardware.yaml    | ESP32, I2C, MCP23017, GPIOs, outputs, LEDs       |
| irrigation.yaml  | Zone control, valve entities, irrigation runtime |
| programs.yaml    | Program A / B / C configuration                  |
| scheduler.yaml   | Time-based execution and repeat logic            |
| diagnostics.yaml | Wi-Fi, uptime, system status, debug sensors      |

This structure keeps the firmware readable and makes future development easier.

---

# 🧪 Testing Notes

Current testing has validated:

* ESPHome firmware flashing
* ESP32 boot
* MCP23017 I2C communication
* Correct zone addressing
* Zone output control in firmware
* Home Assistant entity creation
* Basic dashboard control
* Status sensors
* Program control layout concepts

Ongoing validation includes:

* 24VAC switching behavior
* Long-term outdoor reliability
* Output stage behavior under real solenoid loads
* Enclosure thermal behavior
* Dashboard usability
* Weather lockout logic
* Full standalone scheduler behavior

---

# 📦 Hardware Summary

| Subsystem         | Component / Feature                  |
| ----------------- | ------------------------------------ |
| Main Controller   | Seeed Studio XIAO ESP32-C6           |
| I/O Expansion     | MCP23017                             |
| Outputs           | 9 AC valve outputs                   |
| Switching         | MOC3041 optocouplers + BT136S triacs |
| Input Power       | 24VAC irrigation transformer         |
| Logic Power       | Rectified and regulated DC rail      |
| Status            | RGB status LED                       |
| Zone Feedback     | 9 individual yellow zone LEDs        |
| Local Control     | Tactile push button                  |
| Protection        | Blade fuse                           |
| Noise Suppression | RC snubber per output                |
| Firmware          | ESPHome                              |
| Integration       | Home Assistant native ESPHome API    |

---

# 🧭 Roadmap

Planned future improvements include:

* Final standalone scheduler implementation
* Full Program A / B / C configuration
* Cycle-and-soak refinement
* Weather forecast integration
* Rain and snow forecast lockout
* Soil moisture sensor integration
* Flow sensor monitoring
* Leak detection
* Master valve / pump start support
* DIN rail enclosure version
* Outdoor enclosure version
* Expansion module support
* Local web interface
* Matter-native exploration
* Improved documentation
* Installation guide
* Troubleshooting guide
* YouTube build and demo series

---

# 🌎 Ecosystem Links

* [Home Assistant](https://www.home-assistant.io/)
* [ESPHome](https://esphome.io/)
* [Seeed Studio XIAO ESP32-C6](https://www.seeedstudio.com/Seeed-XIAO-ESP32C6-p-5884.html)

---

# ⚠️ Safety Notice

irriBRANT is an open-source DIY electronics project.

Although the irrigation side is based on low-voltage 24VAC systems, users should still take proper precautions when working with transformers, outdoor wiring, water, and electrical enclosures.

Use proper fusing, waterproof enclosures, strain relief, and installation practices according to local electrical requirements.

---

# 📄 License

This project is open-source and intended for educational, maker, and home automation applications.

---

<p align="center">
  Developed as part of the Brant Channel project series.
</p>

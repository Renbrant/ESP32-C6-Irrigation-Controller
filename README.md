# irriBRANT - Advanced 9-Zone Smart Irrigation Controller

<p align="center">
  <img src="docs/banner2.png" alt="irriBRANT Banner">
</p>

<p align="center">
  <strong>Professional-grade ESPHome irrigation controller with native Home Assistant integration</strong>
</p>

---

## Overview

**irriBRANT** is a professional-grade smart irrigation controller designed to work natively with [Home Assistant](https://www.home-assistant.io/) and powered by [ESPHome](https://esphome.io/).

The main goal of this project is to replace traditional irrigation timers with a modern automation-first solution capable of using:

- Real-time weather conditions
- Soil moisture sensors
- Home Assistant automations
- Smart schedules
- Remote monitoring and diagnostics

The result is a more efficient, flexible, and sustainable irrigation system.

---

# 🚀 Project Status: PRODUCTION PHASE (V1.01)

The project has officially entered the production stage.  
**Version V1.01** has already been fabricated and assembled for real-world validation and testing.

### Current Progress

- [x] Schematic Design
- [x] PCB Layout & Routing
- [x] Gerber Generation
- [x] PCB Fabrication
- [x] PCB Assembly
- [x] ESPHome Firmware Development
- [ ] Long-Term Field Testing
- [ ] Weather-Based Automation Logic
- [ ] Final Enclosure Design

---

# 🆕 Major Hardware Improvements (V1.01)

Version V1.01 introduced several important hardware and usability upgrades:

### RGB Status LED
A dedicated RGB LED provides immediate visual feedback for:

- Boot status
- Wi-Fi connection
- ESPHome state
- Error diagnostics
- Irrigation activity

### Individual Zone LEDs
Each of the 9 irrigation outputs now includes its own yellow status LED, making it easy to identify active valves directly on the PCB.

### Local Push Button
A tactile push button was added for:

- Manual override
- Emergency stop
- Triggering ESPHome captive portal
- Future maintenance features

### Improved Diagnostics
The board layout was refined to simplify troubleshooting and field servicing.

---

# 📸 Real Board Photos (V1.01)

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

## PCB Layout (Top & Bottom)

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

# 🖥️ Firmware & Dashboard

## Home Assistant Dashboard Samples

<p align="center">
  <img src="Photos/Dashboard/Dashboard sample 01.png">
  <img src="Photos/Dashboard/Dashboard sample 02.png">
</p>

---

# ⚙️ Technical Overview

The irriBRANT platform was engineered with reliability, electrical isolation, and serviceability as core principles.

---

## 1. Main Controller: Seeed Studio Xiao ESP32-C6

The controller is based on the **ESP32-C6**, providing:

- Wi-Fi 6
- Zigbee support
- Matter compatibility
- Low power consumption
- Excellent ESPHome support

This creates a future-proof smart irrigation platform fully compatible with modern smart home ecosystems.

---

## 2. I/O Expansion: MCP23017

The **MCP23017 I2C I/O Expander** manages the 9 irrigation outputs while keeping ESP32 GPIOs available for:

- RGB LED
- Push button
- Future sensors
- Expansion features

Benefits include:

- Cleaner PCB routing
- Simplified firmware
- Better scalability

---

## 3. Power System: XL1509 Buck Converter

The board was designed for standard **24VAC irrigation transformers**.

### Power Conversion Chain

1. 24VAC Input
2. Bridge Rectifier
3. Filtering Stage
4. XL1509 Buck Regulator
5. Stable 5V Rail
6. ESP32 3.3V Regulation

### Why XL1509?

The **XL1509-5.0** was selected because it:

- Handles high input voltage efficiently
- Generates less heat than linear regulators
- Improves overall system reliability
- Supports continuous operation outdoors

---

## 4. Valve Switching: Optoisolated Triac Drivers

The irrigation valves are controlled using isolated solid-state AC switching.

### Components Used

#### MOC3041 Optocouplers
Features:

- Galvanic isolation
- Zero-cross switching
- Reduced EMI
- Improved reliability

#### BT136S Triacs
Used as the main AC switching devices for the 24VAC solenoid valves.

Advantages:

- Silent operation
- No relay wear
- Long lifespan
- Reliable inductive load handling

---

## 5. Protection & Signal Integrity

### RC Snubber Network
Each output includes a snubber network:

- 47Ω resistor
- 10nF capacitor

This suppresses voltage spikes caused by inductive valve loads.

### Blade Fuse Protection
A replaceable automotive-style blade fuse protects:

- PCB traces
- Power stage
- Irrigation transformer

---

# 🔌 Home Assistant Integration

irriBRANT was built from the ground up for Home Assistant.

### Supported Features

- Native ESPHome integration
- Individual zone entities
- Automation support
- Remote diagnostics
- OTA firmware updates
- Weather-aware irrigation logic
- Future soil moisture automation

---

# 🌎 Ecosystem Links

- [Home Assistant](https://www.home-assistant.io/)
- [ESPHome](https://esphome.io/)
- [Seeed Studio Xiao ESP32-C6](https://www.seeedstudio.com/Seeed-XIAO-ESP32C6-p-5884.html)

---

# 📌 Future Plans

Planned future improvements include:

- Weather forecast integration
- Flow sensor monitoring
- Leak detection
- Soil moisture automation
- DIN rail enclosure version
- Expansion modules
- Matter-native support
- Local web interface

---

# 📄 License

This project is open-source and intended for educational, maker, and home automation applications.

---

<p align="center">
  Developed as part of the Brant Channel project series.
</p>

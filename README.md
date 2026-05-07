# irriBRANT - Advanced 9-Zone Smart Irrigation Controller

<p align="center">
  <img src="docs/banner2.png" alt="irriBRANT Banner">
</p>

**irriBRANT** is a professional-grade smart irrigation controller designed to work natively with [Home Assistant](https://www.home-assistant.io/) and powered by [ESPHome](https://esphome.io/). 

The primary goal of this project is to integrate garden irrigation into a modern home automation ecosystem. By replacing traditional "dumb timers" with this intelligent, sensor-driven node, the system leverages real-time weather data, soil moisture levels, and complex logic to optimize water usage, making it far more efficient and sustainable.

---

## 🚀 Project Status: PRODUCTION PHASE (V1.01)

The project has officially moved into the production stage. **Version V1.01** has been sent for fabrication and assembly, featuring several hardware refinements based on initial design reviews.

- [x] Full Schematic Design (v1.01)
- [x] PCB Routing & Gerber Generation
- [x] **Sent to Production:** Fabrication and assembly of the V1.01 prototypes are currently underway.
- [x] Firmware Development (ESPHome YAML)
- [ ] Field Testing & Validation

---

## 🆕 Major Hardware Updates (v1.01)

The transition to V1.01 focused on improving the user interface and local diagnostics. The following features were added:

* **RGB Status LED:** A dedicated multi-color LED provides immediate visual feedback on the system's state.
* **Individual Zone Indicators:** Each of the 9 outputs now includes a dedicated yellow indicator LED on the DC side. This allows for quick visual confirmation of which valves are being triggered by the logic.
* **Local Control Button:** A tactile button was integrated for physical interaction. It can be used for manual overrides, emergency stops, or to trigger the ESPHome Captive Portal for network configuration without software access.

---

## Hardware Visuals

### 2D Layout (Top & Bottom)
<p align="center">
  <img src="hardware/PCB v1.2/PCB v1.2 top.png" width="400" alt="PCB Top View">
  <img src="hardware/PCB v1.2/PCB v1.2 bottom.png" width="400" alt="PCB Bottom View">
</p>

### 3D Renderings
<p align="center">
  <img src="hardware/PCB v1.2/PCB 3D v1.2 a.png" width="280" alt="PCB 3D Render 1">
  <img src="hardware/PCB v1.2/PCB 3D v1.2 b.png" width="280" alt="PCB 3D Render 2">
  <img src="hardware/PCB v1.2/PCB 3D v1.2 c.png" width="280" alt="PCB 3D Render 3">
</p>

### Schematic
The detailed circuit design for version 1.01 can be found below.
<p align="center">
  <img src="hardware/PCB v1.2/Schematic_IrrigBrant_v1.2.png">
</p>

---

## Technical Overview & Component Selection

The irriBRANT was engineered with stability, safety, and signal integrity as priorities:

### 1. Logic & Connectivity: Seeed Studio Xiao ESP32-C6
The ESP32-C6 provides a modern connectivity suite, supporting **Wi-Fi 6, Zigbee, and Matter**, ensuring a reliable connection even in outdoor environments.

### 2. I/O Expansion: MCP23017
To manage 9 independent zones, we utilize the MCP23017 I/O expander via I2C. This allows for clean addressing of the valve drivers while keeping the ESP32 pins free for the status LED, button, and future sensors.

### 3. Power Management: XL1509 Buck Converter
Designed for **24VAC** irrigation transformers:
* **Rectification:** A bridge rectifier converts 24VAC to ~34VDC.
* **Regulation:** The **XL1509-5.0** Step-Down Buck Converter handles the voltage drop efficiently without the heat issues of linear regulators.

### 4. Actuation: Optoisolated Triacs
Uses solid-state switching for maximum durability:
* **MOC3041 Optocouplers:** Provide galvanic isolation and **Zero-Crossing** detection to minimize electrical noise.
* **BT136S Triacs:** Robust AC switches designed to handle the inductive loads of 24VAC solenoid coils.

### 5. Protection & Signal Integrity
* **RC Snubbers:** Every channel includes a snubber ($47\Omega + 10nF$) to suppress voltage spikes.
* **Fuse Protection:** A professional blade fuse holder on the 24VAC input protects the PCB and transformer.

---

## Ecosystem Links
* **[Home Assistant](https://www.home-assistant.io/):** The open-source home automation platform that puts local control and privacy first.
* **[ESPHome](https://esphome.io/):** A system to control your microcontrollers by simple yet powerful configuration files.

---
*Developed as part of the Brant Channel project series.*

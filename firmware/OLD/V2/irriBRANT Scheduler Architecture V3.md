# irriBRANT Scheduler Architecture v1

## Overview

The irriBRANT scheduling system will support:

* 3 independent irrigation programs
* Multi-zone scheduling
* Per-zone runtimes
* Repeat cycles
* Manual watering
* Future weather integration
* Future smart irrigation logic

The firmware remains hardware-focused only.

All scheduling logic lives in Home Assistant.

---

# System Architecture

## Firmware Layer (ESPHome)

Responsible for:

* Valve control
* Hardware IO
* RGB status LED
* Sensors
* Safety logic
* OTA
* Watchdog

Entities exposed:

```text
valve.zone_1
valve.zone_2
...
valve.zone_9
```

These entity IDs NEVER change.

---

# Home Assistant Layer

Responsible for:

* Scheduling
* Program execution
* Timers
* Runtime management
* Future weather logic
* Dashboard UI

---

# Dashboard Layer

Responsible for:

* User interaction
* Program configuration
* Zone naming
* Status visualization
* Mobile UI

---

# PROGRAM STRUCTURE

The system supports:

```text
Program 1
Program 2
Program 3
```

Each program contains:

| Feature          | Description               |
| ---------------- | ------------------------- |
| Enable           | Turns program ON/OFF      |
| Days             | Days of week              |
| Start Time       | Program start             |
| Zones            | Included zones            |
| Runtime per zone | Individual runtime        |
| Repeat Count     | Number of repetitions     |
| Repeat Delay     | Delay between repetitions |
| Zone Delay       | Delay between zones       |
| Manual Start     | Run immediately           |
| Stop Program     | Stop running program      |

---

# PROGRAM DATA MODEL

Example:

```yaml
program_1:

  enabled: true

  days:
    - mon
    - wed
    - fri

  start_time: "06:00"

  repeat_count: 2

  repeat_delay_minutes: 30

  zone_delay_seconds: 2

  zones:

    - zone: 1
      duration_minutes: 10

    - zone: 2
      duration_minutes: 15

    - zone: 4
      duration_minutes: 5
```

---

# EXECUTION FLOW

Example:

```text
6:00 AM
↓
Zone 1 ON
↓
10 min
↓
Zone 1 OFF
↓
2 sec delay
↓
Zone 2 ON
↓
15 min
↓
Zone 2 OFF
↓
2 sec delay
↓
Zone 4 ON
↓
5 min
↓
Repeat cycle delay 30 min
↓
Repeat program
```

---

# REQUIRED DASHBOARD SECTIONS

## 1. System Status

Displays:

* Controller online/offline
* Current running zone
* Active program
* WiFi status
* Weather status (future)
* Rain delay status

---

# 2. Zone Control

Each zone card contains:

* Zone name
* ON/OFF status
* Manual start
* Manual stop
* Runtime remaining
* Last run

---

# 3. Programs

Each program card contains:

* Enable/disable
* Days
* Start time
* Included zones
* Total duration
* Repeat count
* Repeat delay
* Run now button

---

# 4. Global Controls

Includes:

* Stop all zones
* Suspend watering
* Rain delay
* Manual mode
* System reboot
* OTA status

---

# IMPORTANT DESIGN RULES

## Rule 1

Only ONE zone active at a time.

This prevents:

* Water hammer
* Pressure drops
* Transformer overload
* Pump overload

---

# Rule 2

Zone transitions require delay.

Recommended:

```text
2 seconds
```

---

# Rule 3

Programs must survive Home Assistant restart.

State persistence required.

---

# Rule 4

Firmware NEVER contains scheduling logic.

Scheduling stays entirely in Home Assistant.

---

# FUTURE FEATURES

## Phase 2

* Rain sensor
* Flow sensor
* Master valve
* Leak detection
* Pressure monitoring

---

# Phase 3

* Remote ESP32 irrigation nodes
* Distributed zones
* LoRa integration

---

# Phase 4

* Smart weather-based irrigation
* ET calculations
* Soil moisture logic
* Forecast prediction
* AI irrigation optimization

---

# INITIAL DEVELOPMENT PRIORITY

## Priority 1

Stable scheduler engine

## Priority 2

Dashboard UX

## Priority 3

Program editing

## Priority 4

Runtime visualization

## Priority 5

Weather integration

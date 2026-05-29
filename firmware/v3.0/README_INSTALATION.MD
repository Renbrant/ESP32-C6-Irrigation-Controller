# irriBRANT PRO

Smart ESPHome irrigation controller with offline scheduling and Home Assistant integration.

---

# Overview

irriBRANT PRO is a fully local irrigation controller based on ESP32 + ESPHome.

The system is designed to operate even if Home Assistant becomes unavailable.

Home Assistant is used primarily for:

* Dashboard UI
* Monitoring
* Weather data
* Remote control
* Notifications

The ESP32 itself handles:

* Program storage
* Irrigation scheduling
* Zone execution
* Repeat logic
* Runtime control
* Offline operation

---

# Features

## Irrigation Features

* 9 irrigation zones
* Multiple irrigation programs
* Per-zone runtime
* Repeat cycles
* Weekly scheduling
* Manual zone control
* Auto-advance zones
* Rain-aware irrigation
* Rain delay support
* Offline capable

---

# Requirements

## Hardware

* ESP32
* Relay board or MOSFET outputs
* 24VAC irrigation transformer
* Irrigation solenoid valves

## Recommended

* Home Assistant
* HACS
* Mushroom Cards
* Stack-in-Card

---

# ESPHome Installation

## Install ESPHome

Recommended methods:

* Home Assistant Add-on
* Docker
* Python package

Official documentation:

https://esphome.io/

---

# Firmware Structure

The firmware uses ESPHome packages.

Your ESPHome directory should look like this:

```text
esphome/
└── irribrant/
    ├── irribrant_v3_2.yaml
    └── packages/
        ├── hardware.yaml
        ├── irrigation.yaml
        ├── scheduler.yaml
        ├── programs.yaml
        ├── diagnostics.yaml
        ├── weather.yaml
        └── next_activities.yaml
```

---

# Main Firmware File

The main firmware file is:

```text
irribrant_v3_2.yaml
```

This file loads all support modules using ESPHome packages.

Example:

```yaml
packages:
  hardware: !include packages/hardware.yaml
  irrigation: !include packages/irrigation.yaml
  scheduler: !include packages/scheduler.yaml
  programs: !include packages/programs.yaml
  diagnostics: !include packages/diagnostics.yaml
  weather: !include packages/weather.yaml
  next_activities: !include packages/next_activities.yaml
```

---

# Installing the Firmware

## 1. Create ESPHome Device

Create a new ESP32 device inside ESPHome.

Recommended board:

```yaml
esp32:
  board: esp32dev
```

---

## 2. Copy Firmware Files

Copy:

* `irribrant_v3_2.yaml`

into the main device folder.

Copy all remaining YAML files into:

```text
packages/
```

folder.

---

## 3. Flash the ESP32

### First Flash

1. Connect ESP32 using USB
2. Open ESPHome
3. Select `irribrant_v3_2.yaml`
4. Click Install
5. Choose "Plug into this computer"

---

## 4. OTA Updates

After the first successful USB flash, future updates can be installed wirelessly using OTA.

---

# Home Assistant Integration

The controller automatically exposes entities to Home Assistant through ESPHome.

Examples:

* Zone switches
* Program settings
* Runtime sensors
* Status sensors
* Rain status
* Scheduling information

---

# Dashboard Installation

## Required HACS Components

Install through HACS:

### Mushroom Cards

https://github.com/piitaya/lovelace-mushroom

### Stack-in-Card

https://github.com/custom-cards/stack-in-card

---

# Import Dashboard

1. Open Home Assistant
2. Go to Dashboards
3. Create dashboard
4. Edit dashboard
5. Paste YAML dashboard configuration

---

# Weather Integration

irriBRANT uses Home Assistant weather providers for:

* Rain probability
* Current rain intensity
* Smart irrigation blocking

---

# Recommended Weather Providers

* OpenWeatherMap
* PirateWeather
* AccuWeather

---

# Creating Rain Template Sensors

If your `configuration.yaml` contains:

```yaml
template: !include templates.yaml
```

Then you must add the following sensors inside:

```text
templates.yaml
```

---

# Add This to templates.yaml

```yaml
- sensor:

    - name: "irriBRANT Rain Probability 12h"
      unique_id: irribrant_rain_probability_12h
      unit_of_measurement: "%"
      state: >
        {{ state_attr('weather.forecast_home', 'forecast')[0].precipitation_probability | default(0) }}

    - name: "irriBRANT Current Rain Intensity"
      unique_id: irribrant_current_rain_intensity
      unit_of_measurement: "mm/h"
      state: >
        {{ states('sensor.openweathermap_rain') | float(0) }}
```

---

# Important

Replace:

```yaml
weather.forecast_home
```

with your actual weather entity.

Examples:

```yaml
weather.home
weather.openweathermap
weather.pirateweather
```

---

# Finding Your Weather Entity

Go to:

```text
Developer Tools → States
```

Search for:

```text
weather.
```

---

# Restart Home Assistant

After adding the templates:

1. Go to Developer Tools
2. Open YAML tab
3. Click Check Configuration
4. Restart Home Assistant

---

# Verify Template Sensors

After restart, verify these entities exist:

```text
sensor.irribrant_rain_probability_12h
sensor.irribrant_current_rain_intensity
```

---

# Recommended Rain Settings

| Setting                    | Recommended |
| -------------------------- | ----------- |
| Rain Probability Threshold | 60%         |
| Rain Intensity Threshold   | 0.1 mm/h    |
| Rain Delay Hours           | 12          |

---

# Recommended Dashboard Cards

## Zone Cards

Recommended card type:

* Mushroom Template Card

Supports:

* Dynamic sprinkler icons
* Active/inactive colors
* Toggle control

---

## System Status

Recommended card types:

* Entities Card
* Mushroom Cards
* Tile Cards

---

# Troubleshooting

---

## YAML Error

### "Implicit keys need to be on a single line"

Usually caused by indentation errors.

Verify spacing carefully.

Use spaces only.

Do not use tabs.

---

## Entity Not Found

Verify entity IDs inside Home Assistant.

---

## Rain Sensors Unavailable

Verify:

* Weather integration is working
* Correct entity IDs are used
* Forecast attribute exists

---

## ESPHome Compile Errors

Verify:

* Package paths
* YAML indentation
* ESP32 board type
* Included files exist

---

# Future Improvements

Potential future features:

* Flow monitoring
* Leak detection
* Freeze protection
* Soil moisture integration
* Automatic ET calculation
* Seasonal adjustment
* Smart irrigation optimization

---

# License

MIT License

---

# Credits

Built with:

* ESPHome
* Home Assistant
* ESP32
* Mushroom Cards
* Open-source community

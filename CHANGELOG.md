# Changelog

All notable changes to this project are documented here.

---

## [v1.2]

### Added
- MOV surge protection on 24VAC input
- NTC inrush current limiter (10D-11)

### Improved
- PCB layout isolation between AC and logic domains
- EMI performance with optimized routing
- Thermal handling for high load scenarios
- Support for all 9 zones operating simultaneously

### Changed
- AC input architecture updated:
  AC → MOV → NTC → Fuse → Rectifier

### Notes
This version transitions the design from prototype to near production-ready hardware.

---

## [v1.1]

### Initial Version
- Functional irrigation controller
- ESP32 + MCP23017 architecture
- Triac-based AC switching

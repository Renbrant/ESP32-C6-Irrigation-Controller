# Changelog

All notable changes to this project are documented here.

---

## [v4.3]

### Added
- Configurable Zone Transition Delay from -10s to +30s.
- Negative values overlap the next zone before closing the current zone to reduce water hammer.
- Positive values pause between zones.
- Transition logic applies between zones and between repeated cycles.
- Master valve timing remains controlled only by the existing v4 Master Valve open/close timing at the start and end of the full program run.

### Removed
- Removed per-program Cycle Repeat Delay / Zone Transition Delay controls in favor of one continuous queued cycle transition model.

---

## [v4.1]

### Added
- Independent signed Master Valve open and close offset settings.
- `Master Valve Open Offset` controls whether the Master Valve opens before, with, or after the irrigation zone.
- `Master Valve Close Offset` controls whether the Master Valve closes before, with, or after the final irrigation zone.

### Improved
- Safety shutdown paths continue to force all outputs off immediately without waiting for Master Valve close offsets.
- Default Master Valve behavior stays close to v4.0 by opening the Master Valve 2 seconds before the irrigation zone.

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

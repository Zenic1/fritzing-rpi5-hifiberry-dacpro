# Raspberry Pi 5 + HiFiBerry DAC+ Pro — Fritzing Project

This repository hosts a Fritzing project for a stacked HAT setup:
- Raspberry Pi 5 (using the Raspberry Pi 4B Fritzing part as a pinout-compatible proxy)
- HiFiBerry DAC+ Pro HAT (dual onboard oscillators, I2S over 40-pin header)
- Breadboard, Schematic, and PCB views
- PCB view sized to HAT dimensions with mounting holes, dual RCA jacks, optional 3.5 mm jack footprint, and a 2-pin AMP/MUTE header

Status
- v0.1: Project scaffolding and documentation added
- v0.2 (next commit): Add .fzz (self-contained Fritzing sketch with embedded parts)

Opening the project
- A .fzz will be added to the fritzing/ directory. Download it and open with Fritzing 0.9.10+.
- If you prefer raw .fz, we can also include that.

Notes
- Fritzing does not yet include an official Raspberry Pi 5 part. The Raspberry Pi 4B part is used as a drop-in proxy. The 40-pin header is pin-identical for our purposes.
- The HiFiBerry DAC+ Pro uses onboard oscillators; no MCLK is required from the Pi.
- The HAT ID EEPROM lines (ID_SD/ID_SC) are present but not required for manual setups.

Pin mapping (Raspberry Pi 40-pin header)
- Power and ground:
  - 5V: pins 2, 4
  - 3V3: pin 1
  - GND: pins 6, 9, 14, 20, 25, 30, 34, 39
- I2S (PCM):
  - BCLK / PCM_CLK: GPIO18 (pin 12)
  - LRCLK / PCM_FS: GPIO19 (pin 35)
  - DOUT / PCM_DOUT: GPIO21 (pin 40)
  - DIN  / PCM_DIN: GPIO20 (pin 38) — not used by DAC+ Pro
  - MCLK: not required (generated on DAC+ Pro)
- I2C (control):
  - SDA1: GPIO2 (pin 3)
  - SCL1: GPIO3 (pin 5)
- HAT EEPROM (ID):
  - ID_SD: GPIO0 (pin 27)
  - ID_SC: GPIO1 (pin 28)

Board elements in PCB view (target)
- 40-pin stacking header aligned to HAT spec
- Mounting holes: 2.5 mm at standard HAT coordinates (65 x 56.5 mm board outline)
- Dual RCA footprint for L/R output
- Optional 3.5 mm stereo jack footprint (line out)
- Optional 2-pin header for AMP/MUTE (label only, not connected by default)

Bill of Materials (BOM)
- Raspberry Pi 5 (use Pi 4B Fritzing part proxy)
- HiFiBerry DAC+ Pro HAT
- 40-pin stacking header
- 2x RCA phono jacks (panel or PCB footprint)
- Optional 3.5 mm stereo jack
- Optional 2-pin header (AMP/MUTE)

Software setup (reference)
- Enable I2S and the HiFiBerry overlay in /boot/firmware/config.txt (Raspberry Pi OS Bookworm):

  ```ini
  dtparam=audio=off
  dtoverlay=hifiberry-dacplus
  ```

- Reboot and verify the card appears (e.g., `aplay -l`).

License
- MIT License (see LICENSE)

Attribution
- Pinout references from Raspberry Pi documentation
- HiFiBerry DAC+ Pro electrical characteristics from vendor docs

Contributing
- Issues and PRs welcome. Please include screenshots from Fritzing for breadboard, schematic, and PCB views.
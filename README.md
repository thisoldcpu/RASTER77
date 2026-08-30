# RASTER77

**RASTER77** is a cycle-accurate Atari 2600 handheld built around the ESP32-S3.

The project aims to reproduce the original 6507, TIA, and RIOT timing closely enough for timing-sensitive software to behave correctly, while adding the conveniences expected from a modern dedicated handheld.

## Goals

* Cycle-accurate 6507 CPU emulation
* Accurate TIA video, audio, collision, and timing behavior
* RIOT RAM, timer, and I/O emulation
* Cartridge ROM and bankswitching support
* Original Atari-compatible controller support
* Low-latency RGB display output
* ROM library management
* Save states and snapshots
* Automatic suspend and resume
* Per-game bezel and title artwork
* Optional CRT-style display effects

Accuracy comes first. Modern features are intended to sit around the original console rather than alter its behavior.

## Hardware

Initial target hardware:

* **Adafruit Qualia ESP32-S3**
* **ESP32-S3 dual-core MCU**
* **TL040WVS03 480×480 IPS display**
* **RGB666 TTL display interface**
* **3.7V 3700mAh LiPo battery**
* Custom power, controls, audio, and controller I/O hardware

The display is continuously scanned using the ESP32-S3 RGB LCD peripheral and DMA.

The Atari image is presented in a centered **480×360** 4:3 viewport. The remaining 60-pixel areas above and below can be used for black borders, title artwork, cabinet-style bezel graphics, menus, or system information.

## Architecture

RASTER77 separates the emulated console from the modern handheld platform.

### Atari 2600

* 6507 CPU
* TIA
* RIOT
* Cartridge / mapper subsystem

### RASTER77 Platform

* RGB display and framebuffer management
* Audio output
* Physical controls and controller ports
* ROM storage and loading
* Snapshots and suspend states
* User interface
* Bezel artwork
* Optional display filtering

The ESP32-S3's dual-core architecture allows timing-critical console emulation to remain isolated from UI, storage, display composition, and other handheld services.

## Design Philosophy

RASTER77 is intended to feel like a dedicated Atari 2600 handheld, not a generic emulation frontend.

The original console remains the machine being emulated.

Everything else is the hardware built around it.

## Project Status

**Early development.**

Hardware architecture and emulator timing design are currently being defined before implementation begins.

## License

To be determined.

## Trademark Notice

Atari and Atari 2600 are trademarks of their respective owners.

RASTER77 is an independent project and is not affiliated with or endorsed by Atari.

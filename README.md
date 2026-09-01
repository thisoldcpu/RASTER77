# RASTER77

**RASTER77** is a dedicated Atari 2600 handheld project built around the ESP32-S3, with cycle accuracy as the primary design goal.

<img width="767" height="1024" alt="mockup_v01" src="https://github.com/user-attachments/assets/131c8de1-c5ce-4323-8cbb-acfdcb393a7b" />

<p align="center">
  <sub><em>Prototype concept v0.1 · Final hardware subject to change.</em></sub>
</p>

The project aims to reproduce the original 6507, TIA, and RIOT closely enough for timing-sensitive software to behave correctly, while adding the conveniences expected from a modern dedicated handheld.

Accuracy comes first. Modern features are intended to sit around the original console rather than alter its behavior.

## Goals

* Cycle-accurate 6507 CPU emulation
* Accurate TIA video, audio, collision, and timing behavior
* RIOT RAM, timer, and I/O emulation
* Cartridge ROM and bankswitching support
* Original Atari-compatible DE-9 controller support
* Built-in joystick, paddle, fire button, and console switches
* Bluetooth LE controller support
* Low-latency RGB display output
* ROM library management
* Save states and snapshots
* Automatic suspend and resume
* Per-game bezel and title artwork
* Optional CRT-style display effects

## Hardware

Initial target hardware:

* **ESP32-S3 dual-core MCU**
* **Adafruit Qualia ESP32-S3**
* **TL040WVS03 480×480 IPS display**
* **RGB666 TTL display interface**
* **3.7V 3700mAh LiPo battery**
* Original Atari-compatible DE-9 controller port
* Built-in analog joystick and paddle controls
* Custom power, controls, audio, and controller I/O hardware

The display is continuously scanned using the ESP32-S3 RGB LCD peripheral and DMA.

The Atari image is presented in a centered **480×360** 4:3 viewport. The remaining 60-pixel areas above and below can be used for black borders, title artwork, cabinet-style bezel graphics, menus, or system information.

## Architecture

RASTER77 keeps the emulated console isolated from the modern handheld platform.

### Core 1 - Atari 2600

* 6507 CPU
* TIA
* RIOT
* Cartridge / mapper subsystem
* Timing-critical emulation

### Core 0 - RASTER77 Platform

* RGB display and framebuffer management
* Audio output
* Physical and Bluetooth controller input
* ROM storage and loading
* Snapshots and suspend states
* User interface
* Bezel artwork
* Optional display filtering
* ESP-IDF system services

The ESP32-S3's dual-core architecture allows timing-critical console emulation to remain isolated from UI, storage, display composition, Bluetooth, and other handheld services.

## Design Philosophy

RASTER77 is intended to feel like a dedicated Atari 2600 handheld, not a generic emulation frontend.

The original console remains the machine being emulated.

Everything else is hardware built around it.

## Why RASTER77?

Most microcontroller emulator projects are designed to run many different 8-bit systems on common hardware.

RASTER77 takes the opposite approach.

The MCU, display pipeline, controls, audio system, controller interfaces, scheduler, and enclosure are all being designed specifically around the Atari 2600.

The goal is not simply to run Atari software on an ESP32-S3. The goal is to reproduce the behavior of the original machine closely enough that software depending on its timing and hardware peculiarities behaves as expected.

I have not found another project combining this dedicated single-system approach with cycle/microcycle-level 6507, TIA, and RIOT emulation, native real-time video and audio, original-controller I/O, BLE input, local ROM storage, and purpose-built handheld hardware on an MCU.

## Project Status

**Early hardware development. Emulator foundation running on real ESP32-S3 hardware.**

Currently working:

* ESP-IDF 6.0.1 build running on ESP32-S3 hardware
* Cycle/microcycle-driven 6507 core
* CPU bus-cycle timing validation
* TIA register, timing, and audio foundation
* RIOT RAM, timer, and I/O foundation
* RIOT timer compliance testing
* Cartridge bus and mapper subsystem
* F8 and F6 bankswitching with real ROMs
* SD-card ROM storage and catalog scanning
* I2S TIA audio output
* Bluetooth LE HID host
* Xbox Wireless Controller model 1914 pairing, bonding, reconnect, and input-report decoding
* Built-in diagnostic cartridge and startup compliance checks

Still under development:

* Complete TIA video path and scanline rendering
* Full TIA audio behavior and continuous cartridge-synchronized playback
* Additional cartridge and bankswitching schemes
* Controller integration with the emulated RIOT inputs
* RGB LCD output pipeline
* Physical handheld controls and DE-9 interface
* User interface, ROM browser, snapshots, and suspend/resume
* Final PCB and enclosure

The project is intentionally being developed foundation-first: emulator ICs, bus behavior, timing, and cartridge execution come before the display and user interface.

## License

RASTER77 firmware and emulator source code are licensed under the
Apache License 2.0.

RASTER77 is implemented independently and does not contain or require
Atari system firmware, BIOS ROMs, or commercial game ROMs.

Third-party components retain their respective licenses. See source
file SPDX headers and accompanying license notices for details.

## Trademark Notice

Atari and Atari 2600 are trademarks of their respective owners.

RASTER77 is an independent project and is not affiliated with or endorsed by Atari.

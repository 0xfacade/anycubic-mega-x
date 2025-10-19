# Configuration for Anycubic Mega X with BLTouch Probe and improved dual-drive extruder

This repository contains configuration files (Klipper & OrcaSlicer) for an Anycubic Mega X with the following modifications:
- BLTouch probe installed as described [here](https://github.com/knutwurst/Marlin-2-0-x-Anycubic-i3-MEGA-S/wiki/BLTouch-Installation-(english))
- This [dual-drive extruder](https://www.amazon.de/dp/B095HHRRJJ). In comparison to the stock extruder, this one uses gears on both sides of the filament to hold on tighter to the filament, and has a higher gear ratio of 1:3 for more power. This makes the machine a lot more reliable.

## Klipper Installation

This is a broad outline of how I personally set this up. There are many possible ways to get a running system.

### Host preparation

My host is a Debian VM on a proxmox server that sat next to my 3D printer. The printer is connected via USB to the server, and that port is passed through to the VM.

On the VM, I used [KIAUH](https://github.com/dw-0/kiauh) to install Klipper, Moonraker and Mainsail. See also the corresponding section in the [Klipper documentation](https://www.klipper3d.org/Installation.html#installing-via-kiauh).

### Flashing the printer

This is completely standard and follows the [Klipper installation instructions](https://www.amazon.de/dp/B095HHRRJJ).
The Mega X has a Trigorilla 1.1 board.

### Install configuration file

Visit the mainsail webpage on your host to edit the configuration file for the printer. Important bits to adapt to your liking:
- determine the serial connection on which the printer is running via `ls /dev/serial/by-id/*` and update the entry under `serial` with the correct path
- install [KAMPS](https://github.com/kyleisah/Klipper-Adaptive-Meshing-Purging) - the config file already makes references to KAMPS config. Make sure to follow the instructions in both "Requirements" and "Installation" 

## Printing

I use OrcaSlicer with the Generic Klipper printer config. Here are some important configuration changes:
- set "Machine start G-code" to `PRINT_START EXTRUDER_TEMP=[nozzle_temperature_initial_layer] BED_TEMP=[bed_temperature_initial_layer_single]`
- set "Machine end G-code" to `PRINT_END`

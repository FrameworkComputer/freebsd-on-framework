# FreeBSD on Framework

FreeBSD is not currently an officially supported Operating System on Framework
Computer systems. This repository documents the current state of how well
FreeBSD works on our systems and helps you set it up.

## Systems

| System       | Mainboard                 | Status                              |
|--------------| --------------------------|-------------------------------------|
| Framework 13 | Intel 11th Gen            | Working well                        |
| Framework 13 | Intel 12th Gen            | Working well                        |
| Framework 13 | Intel 13th Gen            | Working well                        |
| Framework 13 | Intel Core Ultra Series 1 | Working with DRM 6.6 (FreeBSD 15)   |
| Framework 13 | AMD 7040 Series           | Working with DRM 6.2 (FreeBSD 14.2) |
| Framework 16 | AMD 7040 Series           | Working with DRM 6.2 (FreeBSD 14.2) |

## Preparation

1. [Install latest FreeBSD from installer](installation-instructions.md)
2. Create your user, adding it to the `wheel` group
3. Reboot into installed system
4. Log into root
5. Install sudo: `pkg install sudo`
6. Run `visudo` and remove `#` from infront of the line with `wheel`
7. Log out and log into your user
8. `sudo pkg install git py311-ansible`
9. `git clone https://github.com/FrameworkComputer/freebsd-on-framework`
10. `cd freebsd-on-framework`
11. Run `sudo ls` and type your password to unlock passwordless sudo
12. Run your desired Playbook, e.g. `ansible-playbook kde-xorg.yml`

## Playbooks

- `kde-xorg.yml` KDE on Xorg

TODO: KDE on Wayland

## Hardware Support

### Generic

- [x] Fingerprint Reader ([Fixes contributed by Framework](fingerprint-reader.md))
- [ ] Ambient Light Sensor (I2C HID)
  - Work-in-progress by Framework
- [x] Display Brightness control
- [x] Built-in Speakers
- [x] Built-in Camera
- [x] Built-in Microphone
- [x] Headset Speaker
- [ ] Headset Microphone
  - [ ] AMD 13in/16in (Realtek ALC295)
  - [ ] Intel 11th Gen (Realtek ALC295)
  - [x] Intel 11th-13th Gen (Tempo 92HD95B)
  - [ ] Intel Core Ultra Series 1 (Realtek ALC285)

### Intel Mainboards

- [x] UEFI Framebuffer (SCFB)
- [x] Intel GPU driver (11th-13th Gen)
  - Working with `drm-61-kmod` on 12th Gen
- [ ] Intel GPU driver (Intel Core Ultra)
  - Needs at least 6.6, not in FreeBSD yet, see below for details
- [x] Intel AX210 WiFi
  - Only 802.22g support in FreeBSD, up to 54Mbit
- [ ] Intel AX210 Bluetooth
  - Not supported in FreeBSD kernel yet, see below
- [x] Suspend (S3) on 11th-13th Gen
  - Works with Intel GPU driver, not with SCFB
  - Wakes up only on power button, or lid, not keyboard press
- [ ] Suspend (S0ix) on Intel Core Ultra
  - Not supported yet by FreeBSD, see below
- [ ] Intel P-State power measurements
  - Work-in-progress by Framework

### AMD Mainboards

- [x] AMD GPU driver
  - Working with `drm-61-kmod`
- [ ] Suspend (S0ix)
  - Not supported yet by FreeBSD, see below
- [x] Framework 13 Touchpad
- [ ] Framework 16 Touchpad

### Expansion Cards

- [x] USB-C
- [x] USB-A
- [x] MicroSD
- [x] SD
- [x] SSD
- [x] Audio
- [x] Ethernet
  - Currently with `cdce` driver, soon better support with `ure` driver
- [x] HDMI
  - Works with Intel GPU driver, does not work with SCFB
- [x] DisplayPort
  - Works with Intel GPU driver, does not work with SCFB

### Framework 13 Intel Core Ultra Series 1

The graphics driver in FreeBSD 14.1 does not work on this Intel CPU generation.
At least DRM 6.6 is needed, which can be built with FreeBSD 15-CURRENT and [drm-kmod PR #283](https://github.com/freebsd/drm-kmod/pull/283).

## Interacting with the hardware

Please refer to [Hardware Interaction](hardware-interaction.md) for details.
The commands there are especially useful for Linux users coming to FreeBSD.

## Known issues

- WiFi Driver (iwlwifi) sometimes crashes on shutdown or resume from S3)
  - [Workaround](https://bugs.freebsd.org/bugzilla/show_bug.cgi?id=263632)
- iwlwifi limited to 802.11g speed
  - [Workaround](https://github.com/pgj/freebsd-wifibox) by using a Linux virtual machine
- AX210 Bluetooth not supported yet
  - https://reviews.freebsd.org/D44861
- RZ616 not supported yet
  - https://bugs.freebsd.org/bugzilla/show_bug.cgi?id=264300
- S0ix and s2idle not supported yet
    - https://reviews.freebsd.org/D17675
    - https://reviews.freebsd.org/D17676
- AMD IOMMU Driver WIP
  - https://reviews.freebsd.org/D47256

# FreeBSD on Framework

FreeBSD is not currently an officially supported Operating System on Framework
Computer systems. This repository documents the current state of how well
FreeBSD works on our systems and helps you set it up.

## Systems

| System                           | Status                        |
|----------------------------------|-------------------------------|
| Framework 13 Intel 11th Gen      | Not tested yet, probably ok   |
| Framework 13 Intel 12th Gen      | Working well                  |
| Framework 13 Intel 13th Gen      | Not tested yet, probably ok   |
| Framework 13 Intel Core Ultra S1 | Working with DRM 6.6          |
| Framework 13 AMD 7040            | Not tested yet                |
| Framework 16 AMD 7040            | Not tested yet                |

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

- `kde-xorg.yml`

## Hardware Support

- [x] UEFI Framebuffer (SCFB)
- [x] Intel GPU driver (11th-13th Gen)
  - Working with `drm-61-kmod` on 12th Gen
- [ ] Intel GPU driver (Intel Core Ultra)
  - TODO: Needs at least 6.7, not in FreeBSD yet
- [x] Intel AX210 WiFi
  - Only 802.22g support in FreeBSD, up to 54Mbit
- [ ] Intel AX210 Bluetooth
  - Not supported in FreeBSD kernel yet
  - [Experimental patches](https://reviews.freebsd.org/D44861)
- [x] Fingerprint Reader
  - Working. Fixes are being upstreamed. [See here](fingerprint-reader.md)
- [ ] Ambient Light Sensor (I2C HID)
  - Work-in-progress by Framework
- [x] Built-in Camera
- [x] Built-in Microphone
- [x] Suspend (S3) on 11th-13th Gen
  - Works with Intel GPU driver, not with SCFB
  - Wakes up only on power button, or lid, not keyboard press
- [ ] Suspend (S0ix) on Intel Core Ultra
  - Not supported yet by FreeBSD
- Expansion Cards
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
- [ ] Intel P-State power measurements
  - Work-in-progress by Framework

### Framework 13 Intel Core Ultra Series 1

The graphics driver in FreeBSD 14.1 does not work on this Intel CPU generation.
At least DRM 6.6 is needed, which can be built with FreeBSD 15-CURRENT and [drm-kmod PR 283](https://github.com/freebsd/drm-kmod/pull/283).


## Known issues

- WiFi Driver (iwlwifi) sometimes crashes on shutdown or resume from S3)
  - [Workaround](https://bugs.freebsd.org/bugzilla/show_bug.cgi?id=263632)

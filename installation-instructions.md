# Detailed Installation Instructions

## Download and burn ISO

For Framework 13 Intel Core Ultra Series 1 systems (released  Summer 2024)
please use the latest development snapshot: [FreeBSD 15-CURRENT](https://download.freebsd.org/snapshots/amd64/amd64/ISO-IMAGES/15.0/).

All other systems can use the latest stable release
[FreeBSD 14.1](https://download.freebsd.org/ftp/releases/ISO-IMAGES/14.1/FreeBSD-14.1-RELEASE-amd64-dvd1.iso).

Burn the ISO to a USB thumb drive using your favorite imager.
For example dd, [Rufus](https://rufus.ie/en/), or [balena etcher](https://etcher.balena.io/).

## Instructions

1. Download and burn ISO
1. Boot Installer
1. Select Install
1. Select Keymap
1. Set hostname
1. Select distribution
    - Defaults are okay
1. Set up Internet connection
1. Select partitioning
    - The default, ZFS is ok, confirm all default options
1. Choose a password
1. Is CMOS Timezone UTC?
  - Yes, unless the previous OS on this system was Windows
1. Select timezone, confirm date and time
1. Choose services
    1. `moused`
    1. `ntpd`
    1. ~~`ntpd_sync_on_start`~~
    1. ~~`powerd`~~
1. Choose system hardening options (default nothing is fine)
1. Add user
    - Keep defaults (press enter) for
        - `Uid`
        - `Login Group`
        - `Login class`
        - `Shell`
        - `Home directory`
        - `Home directory permissions`
        - `ZFS Encryption`
    - Other groups: `wheel video`
1. No final modifications
1. Reboot into installed system

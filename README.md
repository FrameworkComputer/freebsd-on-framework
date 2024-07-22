# FreeBSD on Framework

## Systems

| System                           | Status                        |
| Framework 13 Intel 11th Gen      | Not tested yet                |
| Framework 13 Intel 12th Gen      | Testing                       |
| Framework 13 Intel 13th Gen      | Not tested yet                |
| Framework 13 Intel Core Ultra S1 | Graphics driver not supported |
| Framework 13 AMD 7040            | Not tested yet                |
| Framework 16 AMD 7040            | Not tested yet                |

## Preparation

1. Install latest FreeBSD 15-Current from installer
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

Work-in-progress:

- `kde-wayland.yml`   
- `gnome-wayland.yml`   
- `gnome-xorg.yml`   
- `sway-wayland.yml`   
- `i3-xorg.yml`
- `i3-scfb.yml`

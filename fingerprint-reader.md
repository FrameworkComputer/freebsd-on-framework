# Fingerprint Reader

## Installing

Install the fprintd package:
```
sudo pkg install fprintd
```

## Configuring

Once you have installed fprintd, you can set up your Login Manager, lockscreen and so on, to use it.
The Arch Wiki has detailed instructions: https://wiki.archlinux.org/title/Fprint
Note that on FreeBSD the etc files are in `/usr/local/etc/`, not in `/etc`.

Add the following as the first line to:

- `/usr/local/etc/pam.d/kde`
- `/usr/local/etc/pam.d/sudo`

```
auth            sufficient      pam_fprintd.so
```

## Enrolling and testing

```
fprintd-enroll
fprintd-verify
```

## Upstreaming effort

The following is no longer needed as the FreeBSD port / package has been updated to the latest version and patches were upstreamed.

- freebsd-ports
  - [branch with all changes](https://github.com/FrameworkComputer/freebsd-ports/tree/fprint)
- libfprint
  - [branch with all changes](https://gitlab.freedesktop.org/JohnAZoidberg/libfprint/-/tree/freebsd-usb?ref_type=heads)
  - Merge requests
    - [Allow build on non-Linux systems (disable SPI)](https://gitlab.freedesktop.org/libfprint/libfprint/-/merge_requests/499)
- fprintd
  - [branch with all changes](https://gitlab.freedesktop.org/JohnAZoidberg/fprintd/-/tree/freebsd?ref_type=heads)
  - Merge Requests
    - [freebsd: Fix building on FreeBSD](https://gitlab.freedesktop.org/libfprint/fprintd/-/merge_requests/210)
    - [pam: Allow build with OpenPAM instead of linux-pam](https://gitlab.freedesktop.org/libfprint/fprintd/-/merge_requests/211)
    - [pam: Allow build with basu instead of libsystemd](https://gitlab.freedesktop.org/libfprint/fprintd/-/merge_requests/212)

### Manually building forks

```
git clone https://gitlab.freedesktop.org/JohnAZoidberg/libfprint
cd libfprint
git checkout freebsd-usb
meson -Dudev_rules=disabled -Dudev_hwdb=disabled build
ninja -C build

git clone https://gitlab.freedesktop.org/JohnAZoidberg/fprintd
cd fprintd
git checkout freebsd
meson -Dlibsystemd=basu -Dsystemd=false -Dopenpam=true -Dpam_modules_dir=/usr/local/lib build
ninja -C build
```

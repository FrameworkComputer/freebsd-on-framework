# Framework Computer Related Changes

- Framework Ethernet Expansion Card
  - Use Realtek URE Driver instead of generic USB CDCE: https://reviews.freebsd.org/D45088
- AX210 Bluetooth
  - https://reviews.freebsd.org/D44861
- RZ616
  - https://bugs.freebsd.org/bugzilla/show_bug.cgi?id=264300


## Building a custom kernel

```
> git clone https://github.com/freebsd/freebsd-src
> sudo chmod 775 /usr/obj
> make buildworld buildkernel config=GENERIC-NODEBUG -j(nproc)
> sudo make installworld installkernel config=GENERIC-NODEBUG
> sudo reboot
> sudo pkg update
> sudo pkg upgrade
```

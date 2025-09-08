# Nvidia

## NVIDIA 5070 External Graphics Card

1. Disable internal graphic card in bios

Notice that the optimus mode is not tested. For simplicity, we can just disable internal graphic card in bios


2. Install Nvidia drm driver:

```
pkg install nvidia-drm-kmod
```

3. Apply boot config on it:

The NVIDIA 5000-series GPUs require GPE firmware, which is not loaded by default in FreeBSD’s nvidia-drm driver.
To enable it, add the following line to your /boot/loader.conf:

```
hw.nvidia.registry.EnableGpuFirmware=1
```

Reference:

[FreeBSD Forums – Xorg won’t start with officially supported NVIDIA 5070 GPU (discussion)](https://forums.freebsd.org/threads/xorg-wont-start-with-officially-supported-nvidia-5070-gpu.97659/page-3)

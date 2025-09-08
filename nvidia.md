# Nvidia

## NVIDIA 5070 External Graphics Card

1. Disable internal graphic card in bios

Notice that the optimus mode is not tested. For simplicity, we can just disable internal graphic card in BIOS.

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

4. Load the kernel driver

```
# Either load manually (once)
sudo kldload nvidia-drm
# Or add to /etc/rc.conf (persistent)
sysrc kld_list+=nvidia-drm
```

5. Start Desktop Environment

For example i3

```
echo 'exec i3` > ~/.Xinitrc
startx
```

6. Start proccesses that use the GPU

```
glxgears
```

### nvidia-smi

nvidia-smi can show status of the GPU and also the processes running on it

```
> sudo mount -t procfs procfs  /proc
> nvidia-smi
Mon Sep  8 17:42:08 2025
+-----------------------------------------------------------------------------------------+
| NVIDIA-SMI 570.181                Driver Version: 570.181        CUDA Version: N/A      |
|-----------------------------------------+------------------------+----------------------+
| GPU  Name                 Persistence-M | Bus-Id          Disp.A | Volatile Uncorr. ECC |
| Fan  Temp   Perf          Pwr:Usage/Cap |           Memory-Usage | GPU-Util  Compute M. |
|                                         |                        |               MIG M. |
|=========================================+========================+======================|
|   0  NVIDIA GeForce RTX 5070 ...    Off |   00000000:C2:00.0  On |                  N/A |
| N/A   51C    P8             11W /  100W |     131MiB /   8151MiB |     12%      Default |
|                                         |                        |                  N/A |
+-----------------------------------------+------------------------+----------------------+

+-----------------------------------------------------------------------------------------+
| Processes:                                                                              |
|  GPU   GI   CI              PID   Type   Process name                        GPU Memory |
|        ID   ID                                                               Usage      |
|=========================================================================================|
|    0   N/A  N/A            4212      G   /usr/local/libexec/Xorg                 109MiB |
|    0   N/A  N/A            4239      G   glxgears                                  3MiB |
+-----------------------------------------------------------------------------------------+
```

### References

[FreeBSD Forums – Xorg won’t start with officially supported NVIDIA 5070 GPU (discussion)](https://forums.freebsd.org/threads/xorg-wont-start-with-officially-supported-nvidia-5070-gpu.97659/page-3)

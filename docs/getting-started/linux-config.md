# Linux Configuration

To allow non-root users to profile GPU kernels using CUPTI (which `gpufl` relies on) on Linux, you must relax the NVIDIA driver security restrictions. Without this, `gpufl` may fail to capture kernel activity.

## Driver Security Settings

1.  **Create a configuration file**:
    ```bash
    sudo nano /etc/modprobe.d/nvidia-profiler.conf
    ```

2.  **Add the following line**:
    ```bash
    options nvidia NVreg_RestrictProfilingToAdminUsers=0
    ```

3.  **Apply changes and reboot**:
    ```bash
    sudo update-initramfs -u
    sudo reboot
    ```

## Verification

After rebooting, you can verify the setting with:
```bash
cat /proc/driver/nvidia/params | grep RestrictProfilingToAdminUsers
```
It should output `RestrictProfilingToAdminUsers: 0`.

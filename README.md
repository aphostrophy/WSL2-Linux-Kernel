# What this is

WSL2 kernel version checkpoint for personal kernel development

# Build Instructions

Instructions for building an x86_64 WSL2 kernel with an Ubuntu distribution are
as follows:

1. Install the build dependencies:  
   `$ sudo apt install build-essential flex bison dwarves libssl-dev libelf-dev`
2. Build the kernel using the WSL2 kernel configuration:  
   `$ make KCONFIG_CONFIG=Microsoft/config-wsl -j $(nproc)`

# WSLCONFIG

1. `cp arch/x86/boot/bzImage <kernel_path_in_windows>`
2. `nano /mnt/Users/<your_username>/.wslconfig`

.wslconfig should at least contain as below

```
[wsl2]
kernel = <kernel_path_in_windows>
```

3. `wsl --shutdown` to reboot
4. `uname -a` should show this kernel version

# Install headers

1. `sudo make headers_install INSTALL_HDR_PATH=/usr`
2. `sudo mkdir -p /lib/modules/$(uname -r)`
3. `sudo ln -s <path to WSL2-Linux-Kernel> /lib/modules/$(uname -r)/build`

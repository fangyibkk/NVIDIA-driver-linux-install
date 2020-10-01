# NVIDIA-driver-linux-install
Way to install NVIDIA driver on Linux
# Disable Nouveau driver and X Server

# Dependencies
C basic build tool
```
dnf install gcc make pkgconfig
```
Kernel development tool
you need to see kernel headers match your kernel release `uname -r`
```
dnf install kernel-devel kernel-headers dkms acpid
```
NVidia `glvnd` library \
The name come from "GL Vendor-Neutral Dispatch library"
```
sudo dnf install libglvnd-glx libglvnd-opengl libglvnd-devel 
```


## Disable nouveau in module loader
```
echo blacklist nouveau > /etc/modprobe.d/nouveau.conf
```

## Disable nouveau in GRUB
```
GRUB_LINUX_COMMAND="... rhgb silent ... rb.driver.blacklist=nouveau"
```
Grub need a compile to generate the new config file
For BIOS, MBR
```
grub2-mkconfig -o /boot/grub2/grub.cfg
```
For EFI
```
grub2-mkconfig -o /boot/efi/EFI/grub.conf
```
## New initramfs
```
cd /boot
dracut --force
```

## Set run level 3
At run level 3, it has network and multiuser.
```
systemctl set-default multi-user.target
```
For other run level,
- 0 = poweroff
- 1 = single user
- 2 = single user + network
- 3 = multi user + network
- 4 is not common
- 5 = GUI screen

# Install NVIDIA Driver
## Go to the directory
```
# ./NVIDIA-Linux-x86_64-450.66.run
```
## Set run level 5
```
systemctl set-default graphical.target
```
## Reboot
```
reboot
```

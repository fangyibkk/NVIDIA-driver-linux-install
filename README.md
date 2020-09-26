# NVIDIA-driver-linux-install
Way to install NVIDIA driver on Linux
# Disable Nouveau driver and X Server

## Disable nouveau by blacklisting it
```
echo blacklist nouveau > /etc/modprobe.d/nouveau.conf
```

## Disable nouveau in GRUB
```
GRUB_LINUX_COMMAND="... rhgb silent ... rb.driver.blacklist=nouveau"
```
Grub need a compile to generate the new config file
```
grub2-mkconfig -o /boot/efi/EFI/grub.conf
```
## new initramfs
```
cd /boot
dracut --force
```

## Set run level 3
At run level 3, it has network and multiuser.
```
systemd set-default multi-user.target
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
systemd set-default graphic.target
```
## Reboot
```
reboot
```

#arch-linux #raspberry-pi #installation #arm

Different from the standard `archinstall` flow in [[Installation]], Arch Linux ARM ships as a pre-built rootfs image, not an installer ISO.

1. Download the Arch Linux ARM image for the Pi model from [archlinuxarm.org](https://archlinuxarm.org/platforms).
2. Partition the SD card (boot + root partitions) and extract the image onto it per the ARM install guide for that platform.
3. Boot the Pi, log in with the distro's documented default root credentials, and change the root password immediately.
4. Create a sudo user:
```
useradd -m -G wheel <username>
passwd <username>
```
Uncomment the `%wheel` line in `/etc/sudoers` via `visudo`.
5. Configure wireless with `netctl`:
```
cp /etc/netctl/examples/wireless-wpa /etc/netctl/<profile_name>
```
Edit the copied profile with the real `Interface`, `ESSID`, and `Key`, then:
```
netctl enable <profile_name>
```
6. Set a static IP if needed, by adding an `Address=` line to the same `netctl` profile.
7. Add a swapfile (the Pi's RAM is limited):
```
fallocate -l 1G /swapfile
chmod 600 /swapfile
mkswap /swapfile
swapon /swapfile
echo '/swapfile none swap defaults 0 0' >> /etc/fstab
```

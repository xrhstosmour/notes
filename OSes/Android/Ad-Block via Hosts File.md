#android #adb #ad-blocking #hosts-file #root

Requires a rooted device.

1. Download a hosts-based blocklist, e.g. [StevenBlack/hosts](https://github.com/StevenBlack/hosts).
2. Remount the system partition writable:
```
adb shell mount -o rw,remount /system
```
3. Push the blocklist over the existing hosts file:
```
adb push hosts /system/etc/hosts
```
4. Reboot the device:
```
adb reboot
```

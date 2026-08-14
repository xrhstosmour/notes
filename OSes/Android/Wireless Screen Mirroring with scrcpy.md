#android #scrcpy #screen-mirroring #adb

[scrcpy](https://github.com/Genymobile/scrcpy) mirrors and controls an Android device from a desktop. USB is simplest, but it also works wirelessly:

1. Install `scrcpy` (`choco install scrcpy` / `brew install scrcpy` / distro package).
2. Enable USB debugging on the device (Developer Options), connect via USB once.
3. Switch `adb` to TCP/IP mode:
```
adb tcpip 5555
```
4. Find the device's IP address (Settings → About phone → Status, or `adb shell ip addr show wlan0`), it'll look like `192.168.x.x`.
5. Connect over Wi-Fi and disconnect the cable:
```
adb connect <device_ip>:5555
```
6. Run `scrcpy` as usual, it now mirrors over Wi-Fi.

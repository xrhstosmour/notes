#linux #pipewire #bluetooth #audio

Getting better-quality audio out of a Bluetooth headset under [PipeWire](https://wiki.archlinux.org/title/PipeWire).

## Switch to PipeWire (if still on PulseAudio directly)

```
yay -Rcns pulseaudio-jack
yay -S pipewire-jack pipewire-alsa pipewire-pulse
systemctl --user enable pipewire pipewire-pulse
systemctl reboot
```

## Enable mSBC / SBC-XQ Codecs

Better headset call/audio quality than the default SBC codec:

```
mkdir -p ~/.config/pipewire/media-session.d/
sudo nano ~/.config/pipewire/media-session.d/bluez-monitor.conf
```

```json
properties = {
    bluez5.msbc-support = true
    bluez5.sbc-xq-support = true
}
```

```
systemctl --user restart pipewire.service
```

## Battery Level Reporting

```
sudo systemctl edit bluetooth.service
```

Add:

```ini
[Service]
ExecStart=
ExecStart=/usr/lib/bluetooth/bluetoothd -E none
```

```
sudo systemctl restart bluetooth.service
```

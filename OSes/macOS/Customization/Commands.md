#macos #commands #customization #configuration

Here are some beneficial commands for tailoring your macOS experience:
#### Finder

- Display path in Finder windows:
``` bash
defaults write com.apple.finder ShowPathbar -bool true
```

- Show status bar in Finder windows:
``` bash
defaults write com.apple.finder ShowStatusBar -bool true
```

- Show hidden files in Finder windows:
``` bash
defaults write com.apple.finder AppleShowAllFiles true
```

- Show files's extensions:
``` bash
defaults write NSGlobalDomain AppleShowAllExtensions -bool true;

defaults write -g AppleShowAllExtensions -bool true
```

- Show all hidden files:
``` bash
defaults write com.apple.Finder AppleShowAllFiles true
```

- Show hidden `/Volumes` and `~/Library` folders:
``` bash
chflags nohidden ~/Library;
sudo chflags nohidden /Volumes
```

- Show icons for external hard drives, servers, and removable media on the desktop:
``` bash
defaults write com.apple.finder ShowExternalHardDrivesOnDesktop -bool true;

defaults write com.apple.finder ShowMountedServersOnDesktop -bool true;

defaults write com.apple.finder ShowRemovableMediaOnDesktop -bool true
```

- Use list view in all Finder windows by default:
``` bash
defaults write com.apple.finder FXPreferredViewStyle -string "Nlsv"
```

- Stop .DS_Store creation at network shares and removable drives:
``` bash
defaults write com.apple.desktopservices DSDontWriteNetworkStores true;
defaults write com.apple.desktopservices DSDontWriteUSBStores -bool true
```

#### Dock

- Disable single application mode:
``` bash
defaults write com.apple.dock single-app -bool false
```

- Disable animation when opening applications:
``` bash
defaults write com.apple.dock launchanim -bool false
```

- Disable animation when opening applications:
``` bash
defaults write com.apple.dock launchanim -bool false
```

- Automatically hide and show the Dock:
``` bash
sudo defaults write /Library/Preferences/com.apple.dock autohide -bool true;

defaults write com.apple.dock autohide -bool true;

defaults write com.apple.dock autohide-delay -float 0
```

- Show indicator lights for open applications in the Dock:
``` bash
defaults write com.apple.dock show-process-indicators -bool true
```

- Change minimize/maximize window effect to Scale:
``` bash
defaults write com.apple.dock mineffect -string "scale"
```

#### Menu Bar

- Display the time in seconds and reveal host info in login window:
``` bash
sudo defaults write /Library/Preferences/com.apple.loginwindow AdminHostInfo HostName
```

#### Keyboard

- Enable full keyboard access for all controls:
``` bash
defaults write NSGlobalDomain AppleKeyboardUIMode -int 3
```

#### Trackpad

- Map bottom right corner to right-click:
``` bash
defaults write com.apple.driver.AppleBluetoothMultitouch.trackpad TrackpadCornerSecondaryClick -int 2;

defaults write com.apple.driver.AppleBluetoothMultitouch.trackpad TrackpadRightClick -bool true;

defaults -currentHost write NSGlobalDomain com.apple.trackpad.trackpadCornerClickBehavior -int 1;

defaults -currentHost write NSGlobalDomain com.apple.trackpad.enableSecondaryClick -bool true;

defaults write com.apple.AppleMultitouchTrackpad TrackpadCornerSecondaryClick -int 2;

defaults write com.apple.AppleMultitouchTrackpad TrackpadRightClick -bool true;
```

- Set preffered tracking speed:
``` bash
defaults write -g com.apple.mouse.scaling 0.5
```
#### Sound

- Disable sound on startup/boot:
``` bash
sudo nvram StartupMute=%01
```

- Increase sound quality for Bluetooth headphones/headsets:
``` bash
defaults write com.apple.BluetoothAudioAgent "Apple Bitpool Min (editable)" -int 40
```

- Reduce latency for Bluetooth headphones/headsets:
``` bash
sudo defaults write bluetoothaudiod "Enable AAC codec" -bool true
```

- Disable speech recognition:
``` bash
sudo defaults write "com.apple.speech.recognition.AppleSpeechRecognition.prefs" StartSpeakableItems -bool false
```

- Stop iTunes from responding to the keyboard media keys:
``` bash
launchctl unload -w /System/Library/LaunchAgents/com.apple.rcd.plist 2> /dev/null
```

#### Displays

- Save screenshots to the desktop:
``` bash
defaults write com.apple.screencapture location -string "${HOME}/Desktop"
```

- Save screenshots in lossless PNG format:
``` bash
defaults write com.apple.screencapture type -string "png"
```

#### Smart Typing

- Disable smart quotes when typing code:
``` bash
defaults write NSGlobalDomain NSAutomaticQuoteSubstitutionEnabled -bool false
```

- Disable smart dashes when typing code:
``` bash
defaults write NSGlobalDomain NSAutomaticDashSubstitutionEnabled -bool false
```

- Disable auto-correct:
``` bash
defaults write NSGlobalDomain NSAutomaticSpellingCorrectionEnabled -bool false
```

#### System Preferences

- Disable press & hold for accents:
``` bash
defaults write -g ApplePressAndHoldEnabled -bool false
```

- Turn off Bluetooth, if you don't have a mouse/keyboard/headphone connected:
``` bash
sudo defaults write /Library/Preferences/com.apple.Bluetooth ControllerPowerState -int 0
```

- Show scrollbars always:
``` bash
defaults write NSGlobalDomain AppleShowScrollBars -string "Always"
```

#### Activity Monitor

- Show all processes in Activity Monitor:
``` bash
defaults write com.apple.ActivityMonitor ShowCategory -int 0
```

- Show the main window when launching Activity Monitor:
``` bash
defaults write com.apple.ActivityMonitor OpenMainWindow -bool true
```

---

To enact these commands, please reboot the device.
For more configuration and customization, visit [here](https://wilsonmar.github.io/dotfiles/).

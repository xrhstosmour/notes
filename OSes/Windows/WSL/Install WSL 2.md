#wsl-2 #hyper-v #linux #distro

Follow these steps to install Windows Subsystem for Linux (WSL) version 2 on your Windows system.

## Preliminary Windows Security Settings

1. **Control Flow Guard (CFG) Settings**:
   - Navigate to *Windows Security* > *App & Browser Control* > *Exploit Protection Settings*.
   - Under *System Settings*, ensure *Control Flow Guard (CFG)* is set to *Use default (On)*.
   - Under *Program Settings*, add entries for the following:
     - `C:\Windows\System32\vmcompute.exe`
     - `C:\Windows\System32\vmwp.exe`
   - For both entries, set *Control Flow Guard* to *Override System Settings > On > Use Strict CFG*.

## Enable Required Features via PowerShell

Open PowerShell as Administrator and execute the following commands:

1. **Enable Virtual Machine Platform**:

``` powershell
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

2. **Enable Windows Subsystem for Linux**:

``` powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```

## Install WSL 2

1. **Download the Linux Kernel Update Package**:
   - Download from [Microsoft's official guide](https://learn.microsoft.com/en-us/windows/wsl/install-manual#step-4---download-the-linux-kernel-update-package).

## Configure WSL 2

Use PowerShell to set WSL 2 as the default version and to manage distributions:

1. **Set Default WSL Version to 2**:

``` powershell
wsl --set-default-version 2
```

2. **Install Your Preferred Linux Distribution**:

   - Unregister a previous version (if applicable):

   ``` powershell
   wsl --unregister <disto_name>
   ```

   - Install a new distribution:

   ``` powershell
   wsl --install -d <disto_name>
   ```

Replace `<disto_name>` with the actual name of the Linux distribution you wish to install (e.g., Ubuntu, Debian, etc.).

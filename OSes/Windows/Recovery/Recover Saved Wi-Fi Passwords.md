#windows #wifi #passwords #netsh

Windows stores saved Wi-Fi profile keys locally and can reveal them in cleartext via `netsh`, useful when you've forgotten a network's password but a machine you own is still connected to it.

Single profile:

``` bat
netsh wlan show profile name="<profile_name>" key=clear
```

Look for `Key Content` in the output. To dump every saved profile at once:

``` bat
for /f "tokens=2 delims=:" %%i in ('netsh wlan show profiles ^| findstr "All User Profile"') do (
    for /f "delims= " %%j in ("%%i") do netsh wlan show profile name="%%j" key=clear
)
```

Requires an elevated command prompt.

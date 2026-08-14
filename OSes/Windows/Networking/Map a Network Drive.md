#windows #networking #smb #network-drive

``` bat
net use <DriveLetter>: \\<ServerName>\<ShareName>
```

Add `/persistent:yes` to have it reconnect automatically after a reboot. Unmap with `net use <DriveLetter>: /delete`.

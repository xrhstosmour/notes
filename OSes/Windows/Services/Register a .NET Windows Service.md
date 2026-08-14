#windows #dotnet #windows-service #installutil

1. Build the Windows Service project (must implement `ServiceBase` and have an installer class).
2. Register it:
```
InstallUtil.exe "<path_to_service>.exe"
```
3. Start it from the Services app (`services.msc`), or:
```
net start <ServiceName>
```
4. To uninstall:
```
InstallUtil.exe /u "<path_to_service>.exe"
```

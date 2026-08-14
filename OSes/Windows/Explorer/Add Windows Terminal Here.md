#windows #registry #explorer #context-menu #windows-terminal

Adds a "Open in Windows Terminal" entry to the folder and folder-background right-click menu, calling `wt.exe` (must already be installed and on `PATH`).

``` reg
Windows Registry Editor Version 5.00

[HKEY_CLASSES_ROOT\Directory\shell\wt]
@="Open in Windows Terminal"
[HKEY_CLASSES_ROOT\Directory\shell\wt\command]
@="wt.exe -d \"%V\""

[HKEY_CLASSES_ROOT\Directory\Background\shell\wt]
@="Open in Windows Terminal"
[HKEY_CLASSES_ROOT\Directory\Background\shell\wt\command]
@="wt.exe -d \"%V\""
```

Save as a `.reg` file and import it. Remove by deleting the `wt` keys under both paths.

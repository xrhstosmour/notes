#windows #registry #explorer #context-menu

A well-known registry tweak (originally documented by Shawn Brink on tenforums.com) that restores the classic "Open command window here" entry to the right-click menu for folders, folder backgrounds, drives, and Library folders on modern Windows, where it's no longer shown by default.

Save as a `.reg` file and import it (double-click, or `regedit` → File → Import):

``` reg
Windows Registry Editor Version 5.00

[HKEY_CLASSES_ROOT\Directory\shell\cmd2]
@="Open command window here"
[HKEY_CLASSES_ROOT\Directory\shell\cmd2\command]
@="cmd.exe /s /k pushd \"%V\""

[HKEY_CLASSES_ROOT\Directory\Background\shell\cmd2]
@="Open command window here"
[HKEY_CLASSES_ROOT\Directory\Background\shell\cmd2\command]
@="cmd.exe /s /k pushd \"%V\""

[HKEY_CLASSES_ROOT\Drive\shell\cmd2]
@="Open command window here"
[HKEY_CLASSES_ROOT\Drive\shell\cmd2\command]
@="cmd.exe /s /k pushd \"%V\""
```

To remove it later, delete the `cmd2` keys under each of those three paths.

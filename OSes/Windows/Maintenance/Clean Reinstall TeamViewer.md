#windows #teamviewer #reinstall #troubleshooting

For when a normal uninstall leaves TeamViewer in a broken state and it needs a fully clean reinstall:

1. Kill running processes:
```
taskkill /f /im TeamViewer.exe
taskkill /f /im tv_w32.exe
taskkill /f /im tv_x64.exe
```
2. Uninstall via its MSI product code:
```
msiexec /x {<product_guid>} /qn
```
The product GUID is version-specific, don't reuse one from an old guide blindly, look it up for the installed version via `wmic product where "name like 'TeamViewer%%'" get IdentifyingNumber` or the uninstall entry in `HKLM\Software\Microsoft\Windows\CurrentVersion\Uninstall`.
3. Remove leftovers:
```
rmdir /s /q "%APPDATA%\TeamViewer"
rmdir /s /q "%PROGRAMFILES(X86)%\TeamViewer"
reg delete "HKLM\SOFTWARE\TeamViewer" /f
```
4. Reinstall from [teamviewer.com](https://www.teamviewer.com/).

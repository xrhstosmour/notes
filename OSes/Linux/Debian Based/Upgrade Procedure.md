#linux #setup #upgrade
1. Execute the [Update Procedure](obsidian://open?vault=Notes&file=OSes%2FLinux%2FDebian%2FUpdate%20Procedure).
2. ```sudo apt dist-upgrade -y```
3. Change the version name at the sources.list with the appropriate next version name:
	1. Find the distro version: ```lsb_release -a```
	2. Version hierarchy: stretch → buster → bullseye → bookworm.
	3. ```sudo sed -i 's/<previous_version_name>/<next_version_name>/g' /etc/apt/sources.list```
4. ```sudo apt full-upgrade```
5. ```sudo reboot```
6. Execute the [Update Procedure](obsidian://open?vault=Notes&file=OSes%2FLinux%2FDebian%2FUpdate%20Procedure).

- - -

## Troubleshooting
* In case you can't update to bullseye version, try changing the ```sources.list``` content to:
```
deb http://deb.debian.org/debian bullseye main
deb-src http://deb.debian.org/debian bullseye main

deb http://security.debian.org/debian-security bullseye-security main
deb-src http://security.debian.org/debian-security bullseye-security main

deb http://deb.debian.org/debian bullseye-updates main
deb-src http://deb.debian.org/debian bullseye-updates main

deb http://deb.debian.org/debian bullseye-backports main
deb-src http://deb.debian.org/debian bullseye-backports main
```

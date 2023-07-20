#linux #unattended-updates #security
1. ```sudo apt install unattended-upgrades```
2. ```sudo systemctl enable unattended-upgrades```
3. ```sudo nano /etc/apt/apt.conf.d/10periodic```
4. Change/add the following lines at the 10periodic file:
```
APT::Periodic::Update-Package-Lists "1";
APT::Periodic::Download-Upgradeable-Packages "1";
APT::Periodic::AutocleanInterval "7";
APT::Periodic::Unattended-Upgrade "1";
```

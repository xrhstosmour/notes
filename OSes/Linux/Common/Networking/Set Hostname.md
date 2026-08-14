#linux #networking #hostname

1. Set the hostname:
```
sudo hostnamectl set-hostname <new_hostname>
```
2. Add (or update) a matching entry in `/etc/hosts` so local tools resolving the hostname don't fail:
```
127.0.1.1   <new_hostname>
```
3. A new shell picks it up immediately, existing shells/services may need a restart (or a reboot) to see the change everywhere.

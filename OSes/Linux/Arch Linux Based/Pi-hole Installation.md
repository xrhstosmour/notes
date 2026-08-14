#arch-linux #pi-hole #dns #ad-blocking

Pi-hole's official installer (`curl -sSL https://install.pi-hole.net | bash`) targets Debian/Ubuntu/Fedora/CentOS, Arch isn't officially supported by it. Check the AUR (e.g. `pi-hole-ftl`) first, it may be simpler than the manual route below and could have changed since this was last verified.

Manual install (FTL + a web server Pi-hole doesn't manage itself):

1. Install `pi-hole-ftl` from the AUR.
2. Install and configure a web server for the admin UI, `nginx` + `php-fpm`:
```
pacman -S nginx php-fpm php-sqlite
```
3. Point `nginx` at the Pi-hole admin web root (wherever the AUR package installs it) and enable the PHP-FPM socket in the `nginx` server block.
4. Start services:
```
systemctl enable --now pihole-FTL nginx php-fpm
```
5. Set the admin password:
```
pihole -a -p
```
6. Point client devices' DNS at this machine's IP, or push it through [[Server and Peer Configuration]] for VPN clients.

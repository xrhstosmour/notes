#linux #security #ufw #firewall

1. Install: `sudo apt install ufw` (Debian/Ubuntu, other distros have an equivalent package).
2. Allow SSH **before** enabling, enabling first without an SSH rule locks out remote access: `sudo ufw allow <ssh_port>/tcp`
3. Allow any other needed ports, e.g. `sudo ufw allow 80/tcp` and `sudo ufw allow 443/tcp`.
4. Enable: `sudo ufw enable`
5. Check status: `sudo ufw status verbose`

For finer-grained control than UFW's rule syntax allows, see [[iptables Hardening Rules]].

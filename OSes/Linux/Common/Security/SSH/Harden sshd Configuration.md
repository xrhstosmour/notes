#linux #security #ssh #sshd #hardening

After key-based login works (see [[ED25519 keys]] and [[Transfer keys]]), harden `sshd` itself:

1. Edit `/etc/ssh/sshd_config`:
```
PermitRootLogin no
PasswordAuthentication no
Port <custom_port>
```
2. Restart the service: `sudo systemctl restart sshd`
3. Verify a key-based login works from a **new** terminal before closing the current session, restarting `sshd` with a bad config or closing the only working session first can lock you out of a remote machine.

#linux #security #iptables #firewall #sysctl

A generic hardening baseline: kernel network settings via `sysctl`, then an `iptables` rule set. Interface names (`ens13`, `ens14`, `wg0`) and subnets below are placeholders, replace with the real ones.

Note: newer distros (Debian 11+/Ubuntu 20.04+) route `iptables` through an `nftables` backend by default (`iptables-nft`), these commands still work through that compatibility layer, but check `iptables --version` if rules behave unexpectedly, a from-scratch `nftables` ruleset may be more future-proof on a very recent install.

## Kernel Hardening (`sysctl`)

``` bash
# /etc/sysctl.d/99-hardening.conf
net.ipv4.conf.all.rp_filter = 1
net.ipv4.conf.default.rp_filter = 1
net.ipv4.conf.all.log_martians = 1
net.ipv4.icmp_echo_ignore_broadcasts = 1
net.ipv4.conf.all.accept_redirects = 0
net.ipv4.conf.default.accept_redirects = 0
net.ipv4.conf.all.send_redirects = 0
net.ipv4.tcp_syncookies = 1
```

Apply with `sudo sysctl -p /etc/sysctl.d/99-hardening.conf`.

## Base Policy

``` bash
iptables -P INPUT DROP
iptables -P FORWARD DROP
iptables -P OUTPUT ACCEPT

# Loopback and established connections.
iptables -A INPUT -i lo -j ACCEPT
iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
```

## Allow Core Services

``` bash
# SSH.
iptables -A INPUT -p tcp --dport <ssh_port> -m state --state NEW -j ACCEPT

# HTTP/HTTPS.
iptables -A INPUT -p tcp --dport 80 -j ACCEPT
iptables -A INPUT -p tcp --dport 443 -j ACCEPT
```

## Attack Mitigation

``` bash
# Port-scan protection.
iptables -N port-scan
iptables -A port-scan -p tcp --tcp-flags SYN,ACK,FIN,RST RST -m limit --limit 1/s -j RETURN
iptables -A port-scan -j DROP

# SSH brute-force throttling.
iptables -A INPUT -p tcp --dport <ssh_port> -m state --state NEW -m recent --set
iptables -A INPUT -p tcp --dport <ssh_port> -m state --state NEW -m recent --update --seconds 60 --hitcount 4 -j DROP

# SYN-flood protection.
iptables -A INPUT -p tcp --syn -m limit --limit 1/s -j ACCEPT

# Drop bogus TCP flag combinations (XMAS, NULL scans).
iptables -A INPUT -p tcp --tcp-flags ALL NONE -j DROP
iptables -A INPUT -p tcp --tcp-flags ALL ALL -j DROP
```

## WireGuard NAT/Forwarding

See [[Server and Peer Configuration]] for the full WireGuard setup, the forwarding rules it needs:

``` bash
iptables -A FORWARD -i wg0 -j ACCEPT
iptables -A FORWARD -o wg0 -j ACCEPT
iptables -t nat -A POSTROUTING -s 10.100.100.0/24 -o <public_interface> -j MASQUERADE
```

## Persist and Verify

``` bash
sudo iptables-save > /etc/iptables/rules.v4
sudo iptables -L -v -n
```

#linux #wireguard #vpn #networking

## Generate Keys

Run on both the server and every peer:

``` bash
wg genkey | tee privatekey | wg pubkey > publickey
```

## Server (`/etc/wireguard/wg0.conf`)

``` ini
[Interface]
PrivateKey = <server_private_key>
Address = 10.100.100.1/24
ListenPort = 51820

[Peer]
PublicKey = <peer_public_key>
AllowedIPs = 10.100.100.2/32
```

Add one `[Peer]` block per client. Bring the interface up with `sudo wg-quick up wg0`, enable on boot with `sudo systemctl enable wg-quick@wg0`.

## Peer

``` ini
[Interface]
PrivateKey = <peer_private_key>
Address = 10.100.100.2/24
DNS = <dns_server_ip>

[Peer]
PublicKey = <server_public_key>
Endpoint = <server_public_ip>:51820
AllowedIPs = 0.0.0.0/0
PersistentKeepalive = 25
```

`AllowedIPs = 0.0.0.0/0` routes all peer traffic through the VPN, scope it down (e.g. to the server's LAN subnet) for split-tunnel instead of full-tunnel.

## NAT and Forwarding

The server needs IP forwarding and NAT for peers to reach the internet or each other through it, see the WireGuard section of [[iptables Hardening Rules]]. Also set `net.ipv4.ip_forward = 1` in `/etc/sysctl.d/99-hardening.conf`.

## DNS Ad-Blocking Through the Tunnel

Point the peer's `DNS` at a Pi-hole instance reachable over the VPN (see [[Pi-hole Installation]]) to get ad-blocking on every connected device without per-device configuration.

# Network details

Fill this file using the actual VirtualBox and Kali configuration.

| Field | Actual value |
|---|---|
| VirtualBox NAT Network name | `NatNetwork` |
| IPv4 network / prefix | `10.0.0.0/24` (observed from Kali route) |
| DHCP enabled | Enabled |
| Kali interface | `eth0` |
| Kali IPv4 / prefix | `10.0.0.2/24` |
| Default gateway | `10.0.0.1` |
| DNS resolver | Not recorded; hostname lookup succeeded |
| Date verified | 2026-10-30 |

## Commands used

```bash
ip -br addr
ip route
cat /etc/resolv.conf
```

## Observations

Observed from Kali:
- `eth0` is UP with IPv4 address `10.0.0.2/24`.
- Default route is via `10.0.0.1` (gateway reachability by ping has not been independently tested).
- Connected route is `10.0.0.0/24`.
- `ping -c 4 8.8.8.8`: 4 packets received, 0% packet loss.
- `ping -c 4 google.com`: hostname resolved and 4 packets received, 0% packet loss.

The VirtualBox NAT Network settings screenshot confirms the network name is `NatNetwork`, the IPv4 prefix is `10.0.0.0/24`, and DHCP is enabled. The DNS resolver configured inside Kali has not yet been recorded.

# WK1-PM1 — Cybersecurity Lab Setup

> **Status:** Lab setup completed and verified against the available host, VirtualBox, and Kali Linux evidence. Any values not available from the evidence are explicitly identified below.

## 1. Project details

| Field | Details |
|---|---|
| Student name | Abhishek Deepak |
| Batch / course | B084C |
| Assignment | WK1-PM1 — Lab Setup |
| Completion date | 30 October 2026 |
| GitHub profile | https://github.com/abhicodes-007 |

## 2. Host laptop specifications

| Component | Actual details |
|---|---|
| Laptop make / model | Acer Nitro AN515-57 |
| Host OS and version | Windows 11 Home Single Language, version 10.0.26200, build 26200 |
| Processor | 11th Gen Intel Core i5-11400H @ 2.70 GHz |
| CPU architecture | x64 (64-bit) |
| Physical memory (RAM) | 16 GB (16,931,676,160 bytes reported) |
| Storage | 256 GB Kingston NVMe SSD + 1 TB Seagate HDD |
| Available storage space | Not recorded |
| VirtualBox version | 7.2.14r174565 |

**Evidence:** `screenshots/01-host-system-specs.png`

## 3. Lab objective and network topology

The objective was to configure a virtual cybersecurity lab using Oracle VirtualBox as the hypervisor and Kali Linux as the guest machine.

- Network type: **NAT Network**
- NAT Network name: `NatNetwork`
- IPv4 subnet: **10.0.0.0/24**
- Kali Linux address: **10.0.0.2/24**
- Default gateway: **10.0.0.1**
- DHCP: **Enabled**
- Internet connectivity: **Verified**

Topology:

```text
Host laptop (Windows 11)
        |
Oracle VirtualBox 7.2.14
        |
NAT Network: NatNetwork
Subnet: 10.0.0.0/24
Gateway: 10.0.0.1
        |
Kali Linux VM
Interface: eth0
Address: 10.0.0.2/24 (DHCP)
```

**Evidence:** `screenshots/02-nat-network-settings.png`

## 4. Virtual machine configuration

| Setting | Actual value |
|---|---|
| VM name | `kali-linux-2026.3-virtualbox-amd64` |
| Guest OS | Kali GNU/Linux Rolling 2026.3 |
| Guest architecture | x86_64 |
| Allocated RAM | Approximately 2 GiB (1.9 GiB visible in guest) |
| Allocated CPU cores | 2 |
| Virtual disk | 80.09 GB VDI |
| Network adapter | Intel PRO/1000 MT Desktop (82540EM) |
| Attached network | NAT Network |
| NAT Network name | `NatNetwork` |

**Evidence:** `screenshots/03-kali-vm-summary.png` and `screenshots/04-kali-network-adapter.png`

## 5. Kali network configuration

The following values were verified using `nmcli`, `ip` commands, and the Kali terminal.

| Parameter | Verified value |
|---|---|
| Network interface | `eth0` |
| IPv4 method | Automatic (DHCP) |
| IPv4 address / prefix | `10.0.0.2/24` |
| Default gateway | `10.0.0.1` |
| DNS in NetworkManager connection profile | `10.0.0.1` |
| Connection profile | `Wired connection 1` |

Command used:

```bash
nmcli -f ipv4.method,ipv4.addresses,ipv4.gateway,ipv4.dns connection show "Wired connection 1"
```

Observed configuration:

```text
ipv4.method:     auto
ipv4.addresses:  10.0.0.2/24
ipv4.gateway:    10.0.0.1
ipv4.dns:        10.0.0.1
```

The generated `/etc/resolv.conf` output also displayed additional nameserver entries (`1.1.1.1`, `0.0.0.1`, and `1.1.1.2`). The NetworkManager connection profile itself reports `10.0.0.1` as its configured DNS value. Hostname resolution was tested successfully. The unusual `0.0.0.1` entry is recorded as observed and has not been independently validated.

**Evidence:** `screenshots/05-kali-ip-address.png` and the terminal verification captured on 30 October 2026.

## 6. Connectivity verification

| Test | Command | Result |
|---|---|---|
| Interface and address | `ip -br addr` | Passed — `eth0` is UP with `10.0.0.2/24` |
| Routing table | `ip route` | Passed — default route via `10.0.0.1` |
| Gateway reachability | `ping -c 4 10.0.0.1` | Three replies received; command was suspended before the fourth reply |
| Internet by IP | `ping -c 4 8.8.8.8` | Passed — 4/4 replies, 0% packet loss; average 18.497 ms |
| DNS / hostname resolution | `ping -c 4 google.com` | Passed — resolved to `142.251.221.174` |
| Internet by hostname | `ping -c 4 google.com` | Passed — 4/4 replies, 0% packet loss; average 19.573 ms |

**Conclusion:** Internet connectivity from Kali is working. The default gateway is configured correctly and responded to the three observed ICMP requests; a complete four-packet gateway test was not recorded.

Test date: **30 October 2026**

**Evidence:** `screenshots/06-connectivity-tests.png` and the later terminal verification.

## 7. Shared clipboard and drag-and-drop

| Feature | Configured mode | Functional test |
|---|---|---|
| Shared clipboard | Bidirectional | Passed — actual copy/paste tested |
| Drag and drop | Bidirectional | Passed — actual drag-and-drop tested |

Both features were configured as Bidirectional in the VirtualBox VM settings and were functionally tested between host and guest. The exact Guest Additions version was not recorded.

**Evidence:** `screenshots/07-clipboard-drag-drop-settings.png` and user-confirmed functional tests.

## 8. Shared folder

The host Downloads folder was shared with the Kali guest.

| Setting | Actual value |
|---|---|
| Host folder | `C:\Users\[redacted]\Downloads` |
| VirtualBox share name | `downloads` |
| Auto-mount | Enabled |
| Folder type | Machine Folder |
| Access | Full access (not read-only) |
| Guest mount point | `/media/sf_downloads` |
| Guest access test | Passed — `ls -la /media/sf_downloads` displayed host files |

The Windows account name is redacted in this public documentation.

**Evidence:** `screenshots/08-shared-folder-settings.png` and `screenshots/09-shared-folder-in-kali.png`

## 9. VM snapshot

| Field | Actual value |
|---|---|
| Snapshot name | `Week 1 Kali Setup` |
| Date created | 30 October 2026, 12:04 |
| Snapshot state | Snapshot exists; VirtualBox showed Current State (changed) afterward |

**Evidence:** `screenshots/10-vm-snapshot.png`

## 10. Problems encountered and solutions

| Problem / symptom | Investigation | Solution / action | Outcome |
|---|---|---|---|
| PowerShell could not find `VBoxManage` | Executable was not available through PATH | Ran `VBoxManage.exe` using its full installation path | VirtualBox version `7.2.14r174565` returned successfully |
| Example: shared-folder permission denied | Could indicate missing `vboxsf` group membership | Example only: add the guest user to `vboxsf`, then log out and back in | Not encountered on this VM; shared folder access was verified |

Additional notes: `troubleshooting/issues-and-solutions.md`.

## 11. Final verification checklist

- [x] VirtualBox installed and version recorded.
- [x] Kali Linux installed and boots.
- [x] NAT Network created with subnet `10.0.0.0/24`.
- [x] DHCP enabled on the NAT Network.
- [x] Kali receives `10.0.0.2/24` through DHCP.
- [x] Default gateway `10.0.0.1` configured and responds to observed ping requests.
- [x] Internet connectivity tested by IP address.
- [x] DNS resolution and internet connectivity tested by hostname.
- [x] Shared clipboard configured as Bidirectional and copy/paste tested.
- [x] Drag-and-drop configured as Bidirectional and tested.
- [x] Host Downloads folder mounted and accessible in Kali.
- [x] VM snapshot created.
- [x] Screenshot evidence added to the repository.
- [x] Unavailable details (such as host free disk space and Guest Additions version) are identified rather than guessed.
- [x] Host account name redacted from the documented shared-folder path.

## 12. Learning outcomes

- Installed and configured Kali Linux 2026.3 as a VirtualBox guest.
- Configured a VirtualBox NAT Network and verified DHCP addressing.
- Inspected interface configuration, routing, gateway, and DNS settings using Linux networking commands.
- Tested external IP connectivity and hostname resolution.
- Configured and tested bidirectional clipboard and drag-and-drop integration.
- Configured a persistent, auto-mounted shared folder and verified guest access.
- Created a VirtualBox snapshot to preserve the configured lab state.
- Documented configuration details, verification results, and evidence in GitHub.

## Safety and scope

This environment is intended for authorized cybersecurity learning and testing. Only assess systems and networks for which explicit permission has been granted. Before publishing evidence, redact credentials, tokens, personal usernames, serial numbers, public IP addresses, and other sensitive information.

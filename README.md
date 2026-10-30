# WK1-PM1 — Cybersecurity Lab Setup

 > **Documentation status:** Based on the host and Kali evidence supplied for this lab. A few technical details that were not visible in the evidence are explicitly marked as unverified.

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
| Host OS and version | Windows 11 Home Single Language, version 10.0.26200, build 26200 (latest System Information screenshot) |
| Processor | 11th Gen Intel Core i5-11400H @ 2.70 GHz |
| CPU architecture | x64 (64-bit) |
| Physical memory (RAM) | 16 GB (16,931,676,160 bytes reported) |
| Storage type / free space | 256 GB Kingston NVMe SSD + 1 TB HDD (free space not recorded) |
| VirtualBox version | 7.2.14r174565 |

**Evidence:** `screenshots/01-host-system-specs.png`

## 3. Lab objective and topology

Set up a virtual cybersecurity testing environment with Oracle VirtualBox as the hypervisor and Kali Linux as the attacking machine.

Expected network from the assignment:

- Network type: **NAT Network**
- IPv4 subnet: **10.0.0.0/24**
- Kali Linux address: **10.0.0.2/24**
- Internet access from Kali: required

Topology (document any differences in the actual implementation):

```text
Host laptop
    |
Oracle VirtualBox
    |
NAT Network: `NatNetwork`
Subnet: 10.0.0.0/24
    |
Kali Linux VM
IP: 10.0.0.2/24
```

**Evidence:** `screenshots/02-nat-network-settings.png`

## 4. Virtual machine configuration

| Setting | Actual value |
|---|---|
| VM name | `kali-linux-2026.3-virtualbox-amd64` |
| Kali version / image | Kali GNU/Linux Rolling 2026.3 |
| Guest architecture | x86_64 |
| Allocated RAM | Approximately 2 GiB (1.9 GiB visible in guest) |
| Allocated CPU cores | 2 |
| Virtual disk size and format | 80.09 GB VDI (VirtualBox summary) |
| Network adapter | Intel PRO/1000 MT Desktop (82540EM) |
| Attached to | NAT Network |
| NAT Network name | `NatNetwork` |
| Adapter model | Intel PRO/1000 MT Desktop (82540EM) |

**Evidence:** `screenshots/03-kali-vm-summary.png` and `screenshots/04-kali-network-adapter.png`

## 5. Kali network configuration

| Parameter | Observed value |
|---|---|
| Interface name | `eth0` |
| IPv4 address / prefix | `10.0.0.2/24` |
| Default gateway | `10.0.0.1` |
| DNS resolver | Not recorded; hostname resolution succeeded |
| Configuration method (static / DHCP) | Not yet confirmed |

Commands used to inspect the network:

```bash
ip -br addr
ip route
cat /etc/resolv.conf
```

Observed output:

```text
eth0 UP 10.0.0.2/24
 default via 10.0.0.1 dev eth0
 10.0.0.0/24 dev eth0 src 10.0.0.2
```

DNS resolver and static/DHCP method remain unverified.

**Evidence:** `screenshots/05-kali-ip-address.png`

## 6. Connectivity tests

Record actual results and date/time. A successful ping to an IP tests IP connectivity; hostname resolution should be tested separately.

| Test | Command | Actual result |
|---|---|---|
| Interface and address | `ip -br addr` | Passed — `eth0` has `10.0.0.2/24` |
| Routing table | `ip route` | Passed — default route via `10.0.0.1` |
| Gateway reachability | `ping -c 4 10.0.0.1` | Not separately tested yet |
| Internet by IP | `ping -c 4 8.8.8.8` | Passed — 4/4 replies, 0% loss; avg. 18.497 ms |
| DNS resolution | `ping -c 4 google.com` | Passed — hostname resolved to `142.251.221.174` |
| Internet by hostname | `ping -c 4 google.com` | Passed — 4/4 replies, 0% loss; avg. 19.573 ms |

Overall internet status: Working (IP connectivity and DNS/hostname connectivity passed).

Test date: 2026-10-30

**Evidence:** `screenshots/06-connectivity-tests.png`

## 7. Clipboard and drag-and-drop

| Feature | Configured mode | Tested result |
|---|---|---|
| Shared clipboard | Bidirectional (shown in VM settings) | Configured; functional transfer test not yet shown |
| Drag and drop | Bidirectional (shown in VM settings) | Configured; functional transfer test not yet shown |
| Guest Additions / integration tools version | Not yet recorded | Not yet tested |

For the assignment, configure clipboard and drag-and-drop in the VM settings. Record the direction selected (for example, Bidirectional) and test it rather than relying only on the setting being selected.

**Evidence:** `screenshots/07-clipboard-drag-drop-settings.png` (Bidirectional selected for both features; functional transfer still to be tested).

## 8. Shared folder

The assignment asks for the host Downloads folder to be shared with the Kali VM. The host path is documented with the Windows account name redacted for privacy.

| Setting | Actual value |
|---|---|
| Host folder path | `C:\\Users\\[redacted]\\Downloads` (username redacted for public documentation) |
| VirtualBox share name | `downloads` (guest mount `/media/sf_downloads`) |
| Auto-mount | Enabled (VirtualBox Shared Folders list shows Auto Mount: Yes) |
| Make permanent | Listed under Machine Folders (persistent VM folder entry) |
| Guest mount location | `/media/sf_downloads` |
| Read-only | No — access is shown as Full |
| Guest access test | Passed — `ls -la /media/sf_downloads` displayed host files |

**Evidence:** `screenshots/08-shared-folder-settings.png` and `screenshots/09-shared-folder-in-kali.png`. The host-side share is a Machine Folder, has Full access, and Auto Mount is enabled.

## 9. VM snapshot

| Field | Actual value |
|---|---|
| Snapshot name | `Week 1 Kali Setup` |
| Date created | 30 October 2026, 12:04 (shown in VirtualBox) |
| VM state | Snapshot tree shows `Current State (changed)` after the snapshot |
| Notes | Snapshot exists and is named `Week 1 Kali Setup` |

**Evidence:** `screenshots/10-vm-snapshot.png`

## 10. Problems encountered and solutions

Document only problems that actually occurred during your setup. Include symptoms, investigation, action, and outcome.

| Problem / symptom | Investigation | Solution applied | Verified outcome |
|---|---|---|---|
| No setup issue reported so far | — | — | — |
| [ FILL IN ] | [ FILL IN ] | [ FILL IN ] | [ FILL IN ] |
| [ FILL IN ] | [ FILL IN ] | [ FILL IN ] | [ FILL IN ] |

More detailed notes: `troubleshooting/issues-and-solutions.md`

## 11. Final verification checklist

- [x] VirtualBox installed; version recorded (7.2.14r174565)
- [x] Kali Linux installed and boots (2026.3)
- [x] NAT Network created with subnet `10.0.0.0/24` (`NatNetwork`, DHCP enabled)
- [x] Kali configured with `10.0.0.2/24`
- [x] Kali internet access tested (IP ping and hostname ping passed)
- [x] Clipboard sharing configured as Bidirectional (transfer test pending)
- [x] Drag-and-drop configured as Bidirectional (transfer test pending)
- [x] Shared folder accessible in Kali at `/media/sf_downloads`
- [x] VM snapshot created (`Week 1 Kali Setup`, 30 October 2026)
- [x] Screenshot evidence captured and cropped; evidence ZIP prepared for repository upload
- [ ] Remaining unverified fields documented or confirmed
- [ ] Sensitive information redacted before making repository public

## 12. Learning outcomes

Initial observations: configured Kali Linux 2026.3 in VirtualBox 7.2.14; identified its `10.0.0.2/24` address and `10.0.0.1` default gateway; verified outbound IP connectivity and hostname resolution. Additional learning notes will be added after completing shared folders, integration features, and snapshots.

## Safety and scope

This environment is for authorized cybersecurity learning and testing. Only assess systems and networks for which you have explicit permission. Before publishing evidence, redact public IP addresses, credentials, tokens, personal usernames, serial numbers, and other sensitive information.

# WK1-PM1 — Cybersecurity Lab Setup

> **Documentation status:** Fill-in template. Replace every `[ FILL IN ]` field with verified details from your own machine. Only mark a requirement complete after configuring and testing it. Do not upload someone else's screenshots or sample IP details.

## 1. Project details

| Field | Details |
|---|---|
| Student name | [ FILL IN ] |
| Batch / course | B084C |
| Assignment | WK1-PM1 — Lab Setup |
| Completion date | [ FILL IN ] |
| GitHub profile | https://github.com/abhicodes-007 |

## 2. Host laptop specifications

| Component | Actual details |
|---|---|
| Laptop make / model | Acer Nitro AN515-57 |
| Host OS and version | Conflicting evidence: PowerShell reported Windows 10 Home Single Language; System Information screenshot shows Windows 11 Home Single Language, build 26200. Confirmation required. |
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
NAT Network: Name not yet verified
Subnet: 10.0.0.0/24
    |
Kali Linux VM
IP: 10.0.0.2/24
```

**Evidence:** `screenshots/02-nat-network-settings.png`

## 4. Virtual machine configuration

| Setting | Actual value |
|---|---|
| VM name | [ FILL IN ] |
| Kali version / image | Kali GNU/Linux Rolling 2026.3 |
| Guest architecture | x86_64 |
| Allocated RAM | Approximately 2 GiB (1.9 GiB visible in guest) |
| Allocated CPU cores | 2 |
| Virtual disk size and format | Not yet recorded |
| Network adapter | Intel PRO/1000 MT Desktop (82540EM) |
| Attached to | NAT Network |
| NAT Network name | `NatNetwork` |
| Adapter model | Not yet verified |

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

The assignment asks for the host `/downloads` folder to be shared with the Kali VM. Record the exact host folder, VirtualBox share name, and guest mount path used.

| Setting | Actual value |
|---|---|
| Host folder path | Windows host folder; exact path not shown |
| VirtualBox share name | Appears to be `downloads` based on guest mount path `/media/sf_downloads` |
| Auto-mount | Guest mount is present at `/media/sf_downloads`; VirtualBox auto-mount checkbox not shown |
| Make permanent | Not yet verified |
| Guest mount location | `/media/sf_downloads` |
| Read-only | Not yet verified |
| Guest access test | Passed — `ls -la /media/sf_downloads` displayed host files |

**Evidence:** `screenshots/07-clipboard-drag-drop-settings.png` and `screenshots/09-shared-folder-in-kali.png`. The guest mount and file listing are confirmed; the host-side share configuration screenshot is still required.

## 9. VM snapshot

| Field | Actual value |
|---|---|
| Snapshot name | Not yet recorded |
| Date created | Not yet recorded |
| VM state | Not yet recorded |
| Notes | Snapshot creation not yet confirmed |

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
- [ ] NAT Network created with subnet `10.0.0.0/24`
- [x] Kali configured with `10.0.0.2/24`
- [x] Kali internet access tested (IP ping and hostname ping passed)
- [x] Clipboard sharing configured as Bidirectional (transfer test pending)
- [x] Drag-and-drop configured as Bidirectional (transfer test pending)
- [x] Shared folder accessible in Kali at `/media/sf_downloads`
- [ ] VM snapshot created
- [ ] Actual screenshots added to `screenshots/`
- [ ] All placeholders completed or marked not applicable
- [ ] Sensitive information redacted before making repository public

## 12. Learning outcomes

Initial observations: configured Kali Linux 2026.3 in VirtualBox 7.2.14; identified its `10.0.0.2/24` address and `10.0.0.1` default gateway; verified outbound IP connectivity and hostname resolution. Additional learning notes will be added after completing shared folders, integration features, and snapshots.

## Safety and scope

This environment is for authorized cybersecurity learning and testing. Only assess systems and networks for which you have explicit permission. Before publishing evidence, redact public IP addresses, credentials, tokens, personal usernames, serial numbers, and other sensitive information.

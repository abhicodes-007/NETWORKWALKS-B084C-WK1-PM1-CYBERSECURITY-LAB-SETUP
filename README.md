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
| Laptop make / model | [ FILL IN ] |
| Host OS and version | [ FILL IN ] |
| Processor | [ FILL IN ] |
| CPU architecture | [ FILL IN ] |
| Physical memory (RAM) | [ FILL IN ] |
| Storage type / free space | [ FILL IN ] |
| VirtualBox version | [ FILL IN ] |

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
NAT Network: [ FILL IN network name ]
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
| Kali version / image | [ FILL IN ] |
| Guest architecture | [ FILL IN ] |
| Allocated RAM | [ FILL IN ] |
| Allocated CPU cores | [ FILL IN ] |
| Virtual disk size and format | [ FILL IN ] |
| Network adapter | [ FILL IN ] |
| Attached to | NAT Network |
| NAT Network name | [ FILL IN ] |
| Adapter model | [ FILL IN ] |

**Evidence:** `screenshots/03-kali-vm-summary.png` and `screenshots/04-kali-network-adapter.png`

## 5. Kali network configuration

| Parameter | Observed value |
|---|---|
| Interface name | [ FILL IN ] |
| IPv4 address / prefix | [ FILL IN ] |
| Default gateway | [ FILL IN ] |
| DNS resolver | [ FILL IN ] |
| Configuration method (static / DHCP) | [ FILL IN ] |

Commands used to inspect the network:

```bash
ip -br addr
ip route
cat /etc/resolv.conf
```

Paste a short, sanitized output or describe the result here:

[ FILL IN ]

**Evidence:** `screenshots/05-kali-ip-address.png`

## 6. Connectivity tests

Record actual results and date/time. A successful ping to an IP tests IP connectivity; hostname resolution should be tested separately.

| Test | Command | Actual result |
|---|---|---|
| Interface and address | `ip -br addr` | [ FILL IN ] |
| Routing table | `ip route` | [ FILL IN ] |
| Gateway reachability | `ping -c 4 [ GATEWAY ]` | [ FILL IN ] |
| Internet by IP | `ping -c 4 1.1.1.1` | [ FILL IN ] |
| DNS resolution | `getent hosts example.com` | [ FILL IN ] |
| Internet by hostname | `ping -c 4 example.com` | [ FILL IN ] |

Overall internet status: [ FILL IN — Working / Not working / Partially working ]

Test date: [ FILL IN ]

**Evidence:** `screenshots/06-connectivity-tests.png`

## 7. Clipboard and drag-and-drop

| Feature | Configured mode | Tested result |
|---|---|---|
| Shared clipboard | [ FILL IN ] | [ FILL IN ] |
| Drag and drop | [ FILL IN ] | [ FILL IN ] |
| Guest Additions / integration tools version | [ FILL IN ] | [ FILL IN ] |

For the assignment, configure clipboard and drag-and-drop in the VM settings. Record the direction selected (for example, Bidirectional) and test it rather than relying only on the setting being selected.

**Evidence:** `screenshots/07-clipboard-drag-drop-settings.png`

## 8. Shared folder

The assignment asks for the host `/downloads` folder to be shared with the Kali VM. Record the exact host folder, VirtualBox share name, and guest mount path used.

| Setting | Actual value |
|---|---|
| Host folder path | [ FILL IN ] |
| VirtualBox share name | [ FILL IN ] |
| Auto-mount | [ FILL IN ] |
| Make permanent | [ FILL IN ] |
| Guest mount location | [ FILL IN ] |
| Read-only | [ FILL IN ] |
| Guest access test | [ FILL IN ] |

**Evidence:** `screenshots/08-shared-folder-settings.png` and `screenshots/09-shared-folder-in-kali.png`

## 9. VM snapshot

| Field | Actual value |
|---|---|
| Snapshot name | [ FILL IN ] |
| Date created | [ FILL IN ] |
| VM state | [ FILL IN ] |
| Notes | [ FILL IN ] |

**Evidence:** `screenshots/10-vm-snapshot.png`

## 10. Problems encountered and solutions

Document only problems that actually occurred during your setup. Include symptoms, investigation, action, and outcome.

| Problem / symptom | Investigation | Solution applied | Verified outcome |
|---|---|---|---|
| [ FILL IN ] | [ FILL IN ] | [ FILL IN ] | [ FILL IN ] |
| [ FILL IN ] | [ FILL IN ] | [ FILL IN ] | [ FILL IN ] |
| [ FILL IN ] | [ FILL IN ] | [ FILL IN ] | [ FILL IN ] |

More detailed notes: `troubleshooting/issues-and-solutions.md`

## 11. Final verification checklist

- [ ] VirtualBox installed; version recorded
- [ ] Kali Linux installed and boots
- [ ] NAT Network created with subnet `10.0.0.0/24`
- [ ] Kali configured with `10.0.0.2/24`
- [ ] Kali internet access tested
- [ ] Clipboard sharing configured and tested
- [ ] Drag-and-drop configured and tested
- [ ] Host `/downloads` folder shared and accessible in Kali
- [ ] VM snapshot created
- [ ] Actual screenshots added to `screenshots/`
- [ ] All placeholders completed or marked not applicable
- [ ] Sensitive information redacted before making repository public

## 12. Learning outcomes

[ FILL IN — In your own words, describe what you learned about VirtualBox, virtualization, NAT networking, IP addressing, Kali Linux, shared folders, and troubleshooting. ]

## Safety and scope

This environment is for authorized cybersecurity learning and testing. Only assess systems and networks for which you have explicit permission. Before publishing evidence, redact public IP addresses, credentials, tokens, personal usernames, serial numbers, and other sensitive information.

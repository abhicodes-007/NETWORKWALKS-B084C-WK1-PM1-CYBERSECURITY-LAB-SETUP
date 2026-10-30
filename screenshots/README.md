# Screenshot evidence checklist

Capture your own screenshots from the actual host and Kali VM. Use the suggested filenames so they match the main README. The user has confirmed that shared clipboard copy/paste and drag-and-drop both work.

- [x] `01-host-system-specs.png` — host model, OS, CPU architecture, RAM and storage information.
- [x] `02-nat-network-settings.png` — VirtualBox NAT Network settings showing the 10.0.0.0/24 network.
- [x] `03-kali-vm-summary.png` — Kali VM summary or General/System settings.
- [x] `04-kali-network-adapter.png` — Kali VM network adapter attached to the intended NAT Network.
- [x] `05-kali-ip-address.png` — Kali terminal showing `ip -br addr` and the configured 10.0.0.2/24 address.
- [x] `06-connectivity-tests.png` — terminal showing route, gateway/internet ping, and DNS test results.
- [x] `07-clipboard-drag-drop-settings.png` — VM settings showing clipboard and drag-and-drop modes. Both features were also functionally tested: copy/paste and drag-and-drop passed.
- [x] `08-shared-folder-settings.png` — VirtualBox Shared Folders settings showing the host downloads folder.
- [x] `09-shared-folder-in-kali.png` — Kali showing the mounted folder and successful access.
- [x] `10-vm-snapshot.png` — VirtualBox snapshot list showing the created snapshot.

## Screenshot hygiene

- Capture full, readable windows; avoid heavily cropped evidence.
- Do not use sample screenshots from the reference repository or video.
- Redact public IP addresses, host usernames, serial numbers, credentials, tokens, and private file paths.
- Keep evidence genuine; do not edit command output or fabricate successful tests.
- If a feature could not be configured or tested, explain that in the README instead of implying completion.

# Troubleshooting log

This log separates an issue actually encountered during this setup from an illustrative troubleshooting example. The illustrative example is included for learning/documentation practice and was **not reported as an issue that occurred** on this VM.

## Issue 1 — VBoxManage command not recognized in PowerShell

- **Date:** 30 October 2026
- **Environment:** Windows 11 host, Oracle VirtualBox 7.2.14
- **Observed symptom / exact error:** Running `VBoxManage --version` in PowerShell returned `VBoxManage : The term 'VBoxManage' is not recognized...`
- **Investigation:** PowerShell could not locate `VBoxManage.exe` through the system PATH. The VirtualBox installation itself was present.
- **Action taken:** Invoked the executable using its full installation path:
  ```powershell
  & "C:\Program Files\Oracle\VirtualBox\VBoxManage.exe" --version
  ```
- **Verification and result:** The command returned `7.2.14r174565`. This confirmed VirtualBox was installed and the executable worked. Adding VirtualBox to PATH is optional if the full path is used.
- **Screenshot / log:** PowerShell output supplied in the project conversation; no separate screenshot was provided.

## Issue 2 — Illustrative example: shared folder permission denied

- **Status:** Example scenario only — not reported as an issue encountered in this lab.
- **Environment:** Kali Linux guest using a VirtualBox shared folder.
- **Example symptom:** A non-root Kali user receives `Permission denied` when opening files under `/media/sf_downloads`.
- **Likely cause:** The guest user is not a member of the `vboxsf` group, which controls access to VirtualBox shared folders.
- **Example corrective action:**
  ```bash
  sudo usermod -aG vboxsf "$USER"
  ```
  Log out of the Kali desktop session and log back in (or reboot) so the new group membership takes effect.
- **Example verification:**
  ```bash
  id
  ls -la /media/sf_downloads
  ```
  Confirm that `vboxsf` appears in the user's groups and that the shared-folder contents can be listed.
- **Actual outcome in this lab:** The supplied screenshot already shows `ls -la /media/sf_downloads` listing files successfully. Therefore, this permission problem was not observed and the example fix was not applied.

## Additional notes

- Kali's `eth0` interface was observed UP at `10.0.0.2/24`.
- The default route was `10.0.0.1`.
- Pings to `8.8.8.8` and `google.com` succeeded with 0% packet loss in the supplied command output.
- The NAT Network is `NatNetwork`, uses `10.0.0.0/24`, and has DHCP enabled.
- Shared clipboard and drag-and-drop are configured as Bidirectional; a real transfer test has not been shown.
- The VM snapshot `Week 1 Kali Setup` is visible in VirtualBox's snapshot list.

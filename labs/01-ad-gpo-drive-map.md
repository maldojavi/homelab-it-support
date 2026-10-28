# Lab 01: Active Directory and Group Policy Drive Map

## What I built
- Windows Server 2022 domain controller (`lab.local`) running on Proxmox
- Organizational Unit `Staff` with test users
- Security group `Printer-Users`
- Shared folder `LabShare` on the server
- GPO `Map LabShare`: maps drive L: to the share, targeted to `Printer-Users` using item-level targeting

## Problems and fixes
1. **Server kept shutting down.** The evaluation license had expired. Fixed with `slmgr /rearm` and a restart.
2. **Printer sharing failed.** `Add-Printer -Shared` and `Set-Printer -Shared` both returned error `0x80070bce`. I tried a TCP/IP port, a local `FILE:` port, and the v4 and v3 drivers. The printer was created but would not share. Not resolved.
3. **Control Panel and Settings were blocked or crashing.** I found a `Restrict Control Panel` GPO linked at the domain level, so it applied to the Administrator too. I disabled the link. Lesson: scope restrictive GPOs to the right OU.

## Next
- Join a Windows Pro client VM to the domain and test the GPO with `gpupdate /force` and `gpresult /r`
- Retry printer sharing and find the root cause
- Set a static IP on the domain controller

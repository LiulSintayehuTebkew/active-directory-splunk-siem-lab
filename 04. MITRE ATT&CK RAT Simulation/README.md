# 04 — Attack Simulation

This folder covers the offensive side of the lab — running real attacks against the Windows environment and verifying that Splunk detected them. Two approaches were used: a brute-force attack from Kali Linux, and MITRE ATT&CK technique simulation using Atomic Red Team on the Windows 10 target.

---

## Attacks run

### Brute-force (Kali Linux → Windows 10 / AD)

Used Kali to run a credential brute-force attack against the domain.

**What Splunk caught:**
- `EventID 4625` — repeated failed logon attempts from 192.168.10.250
- `EventID 4624` — successful logon after correct credentials found
- Source IP, username, and timestamp all visible in Splunk

---

### Atomic Red Team — MITRE ATT&CK simulation

Atomic Red Team was installed on the Windows 10 machine and used to simulate specific ATT&CK techniques. Each test generates real telemetry that a SOC analyst would investigate.

| Technique | ATT&CK ID | Description | Detected |
|---|---|---|---|
| Create Local Account | T1136.001 | Created a new local user account via command line | Yes — EventID 4720 |
| Windows Command Shell | T1059.001 | Executed commands via cmd/PowerShell | Yes — Sysmon EventID 1 |

---

## Screenshots

| File | What it shows |
|---|---|
| `01-mitre-attack-reference.png` | MITRE ATT&CK Enterprise matrix used as reference |
| `02-mitre-attack=[T1136.001].png` | Atomic Red Team running T1136.001 — local account creation |
| `03-mitre-attack=[T1059.001].png` | Atomic Red Team running T1059.001 — command shell execution |

---

## What this demonstrates

- Ability to simulate realistic adversary behavior using a recognized framework
- Understanding of how attacks generate specific Windows/Sysmon event IDs
- Practical experience correlating attack activity to log telemetry in a SIEM
- Familiarity with MITRE ATT&CK and how it maps to real detection use cases

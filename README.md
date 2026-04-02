# active-directory-splunk-siem-lab

A home lab I built to simulate a real corporate environment — complete with Active Directory, a Splunk SIEM, and actual attack simulation using Kali Linux and Atomic Red Team.

The goal was simple: set up the infrastructure, throw attacks at it, and see if Splunk catches them. It did.

---

## What's in this lab

| Component | Role |
|---|---|
| Windows Server 2022 | Domain Controller (Active Directory) |
| Windows 10 | Target endpoint, joined to domain |
| Ubuntu Server | Splunk SIEM server |
| Kali Linux | Attacker machine |
| Sysmon | Endpoint telemetry on Windows machines |
| Splunk Universal Forwarder | Ships logs from endpoints to Splunk |
| Atomic Red Team | MITRE ATT&CK technique simulation |

---

## Network overview

![Network Diagram](01-network-configuration-and-diagram/network-topology.png)

- **Domain:** Aksumite
- **Network:** 192.168.106.0/24
- **Splunk Server:** 192.168.106.136
- **Active Directory / DC:** 192.168.106.133
- **Attacker (Kali):** 192.168.106.130
- **Windows 10 Target:** DHCP

---

## How it went

1. Gathered all four VMs in Vmware and configured them on the same NAT network
2. Installed Sysmon on Windows 10 and Windows Server 2022 for detailed endpoint logging
3. Set up Splunk on Ubuntu and configured Universal Forwarders on both Windows machines
4. Built out Active Directory — promoted Server 2022 to a DC, created the Aksumite forest, added HR and IT organizational units with users in each
5. Windows 10 joined the domain
6. Ran a brute-force attack from Kali — Splunk caught it with EventID 4625 (failed logons)
7. Installed a RAT and ran Atomic Red Team techniques mapped to MITRE ATT&CK
8. Analyzed all telemetry in Splunk — every attack generated the expected events

---

## Tools used

- Vmware
- Windows Server 2022, Windows 10, Ubuntu Server, Kali Linux
- Splunk Enterprise + Universal Forwarder
- Sysmon (SwiftOnSecurity config)
- Atomic Red Team
- MITRE ATT&CK Framework
- draw.io for diagram sketching

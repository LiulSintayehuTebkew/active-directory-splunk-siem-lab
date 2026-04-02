# 01 — Network Configuration and Diagram

This is the foundation everything else is built on. All four VMs sit on the same internal network so they can talk to each other — the attacker can reach the target, and the target ships logs to Splunk.

---

## Network layout

| Machine | OS | IP | Role |
|---|---|---|---|
| Splunk Server | Ubuntu Server | 192.168.106.136 | SIEM — receives all logs |
| Domain Controller | Windows Server 2022 | 192.168.106.137 | Active Directory, Splunk Forwarder, Sysmon |
| Target PC | Windows 10 | DHCP | Endpoint, domain member, Splunk Forwarder, Sysmon |
| Attacker | Kali Linux | 192.168.106.130 | Attack simulation |

---

## Diagram

![Network Diagram](./01-network-configuration-diagram.png)

---

## Notes

- All machines are on the 192.168.106.0/24 subnet
- The domain controller also acts as the DNS server for the domain
- Kali is on the same subnet to simulate an internal threat — lateral movement scenario
- The cloud icon in the diagram represents internet access through the NAT adapter

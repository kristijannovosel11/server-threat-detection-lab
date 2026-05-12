# Tool Version Inventory

This document records the operating systems, services and tools used in the virtual laboratory environment.

The purpose of this file is to support reproducibility by documenting which systems and tools were used during scenario execution, data collection and log analysis.

## Operating Systems

| Component | Role | Version |
|---|---|---|
| VM1 - Target Server | Monitored server, Suricata sensor, SSH and web service | Ubuntu Server 24.04.4 LTS |
| VM2 - Attacker Machine | Controlled security scenario traffic generation | Kali Linux |
| VM3 - Legitimate Client | Benign traffic generation | Ubuntu Desktop |

Exact operating system version strings should be verified directly on each virtual machine before final publication.

Recommended verification command:

```bash
cat /etc/os-release
```

## Services and Tools

| Tool / Service | Lab Role | Verification Command |
|---|---|---|
| Suricata | Network IDS / NIDS sensor | `suricata --version` |
| OpenSSH Server | SSH target service and authentication log source | `ssh -V` or `sshd -V` |
| Apache HTTP Server | Web service and HTTP access log source | `apache2 -v` |
| nmap | Controlled port scanning scenario | `nmap --version` |
| Python 3 | Log parsing, event correlation and metric calculation | `python3 --version` |
| tcpdump | Optional packet capture and traffic verification | `tcpdump --version` |
| Wireshark | Optional packet inspection and validation | `wireshark --version` |

## Version Verification Commands

The following commands should be executed on the relevant virtual machines and the final outputs should be documented before publishing the repository publicly:

```bash
# Target Server
cat /etc/os-release
suricata --version
ssh -V
apache2 -v
python3 --version

# Attacker Machine
cat /etc/os-release
nmap --version
python3 --version

# Optional tools
tcpdump --version
wireshark --version
```

## Notes

Only verified tool versions should be added to this file. Version values should not be guessed.

This file does not include credentials, private hostnames or raw command outputs that may expose sensitive local information.

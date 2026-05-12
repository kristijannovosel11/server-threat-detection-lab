# Lab Environment Configuration

This document summarizes the technical configuration of the virtual laboratory environment used for the threat detection evaluation.

The lab was designed as a controlled and isolated environment for generating, observing and analyzing both legitimate and malicious network traffic. The main goal is to compare three detection approaches:

1. network-based detection using Suricata,
2. system and application log analysis,
3. correlation of Suricata alerts with local server logs.

## Virtualization Platform

The laboratory environment was implemented using Oracle VirtualBox.

The lab consists of three virtual machines connected through an isolated internal network segment. The target server also uses NAT connectivity for package installation and system updates.

## Virtual Machines

| VM | Operating System | IP Address | Role | vCPU | RAM |
|---|---|---:|---|---:|---:|
| VM1 - Target Server | Ubuntu Server 24.04.4 LTS | 192.168.100.10 | Server system, Suricata sensor, SSH service, web service, log generation | 2 | 4 GB |
| VM2 - Attacker Machine | Kali Linux | 192.168.100.20 | Execution of controlled attack scenarios | 2 | 4 GB |
| VM3 - Legitimate Client | Ubuntu Desktop | 192.168.100.30 | Generation of benign user traffic | 1 | 1.5 GB |

## Network Configuration

The lab uses an isolated internal VirtualBox network segment for experimental traffic.

| Network Segment | Purpose |
|---|---|
| NAT | Internet access, package installation and system updates |
| Internal Network: labnet | Isolated experimental traffic between lab machines |

The internal lab network uses the following subnet:

`192.168.100.0/24`

## Target Server Network Interfaces

The target server uses two network interfaces.

| Interface | Mode | Purpose |
|---|---|---|
| NAT interface | NAT | Internet access and package updates |
| enp0s8 | Internal Network - labnet | Experimental SSH and HTTP traffic monitoring |

## Host Roles

### Target Server

The target server is the central monitored system in the lab. It runs the services used during the detection scenarios and generates local logs for later analysis.

Main functions:

- SSH service for authentication-based scenarios
- Apache web server for HTTP-based scenarios
- Suricata in passive IDS mode
- generation of system and application logs

Main IP address in the lab network:

`192.168.100.10`

### Attacker Machine

The attacker machine is used to generate controlled malicious traffic toward the target server. It is based on Kali Linux and is used for tools such as nmap, Hydra and HTTP request generation tools.

Main functions:

- port scanning
- SSH brute-force testing
- HTTP request generation
- suspicious endpoint access testing

Main IP address in the lab network:

`192.168.100.20`

### Legitimate Client

The legitimate client is used to generate benign traffic toward the same services. This allows comparison between normal and malicious activity during evaluation.

Main functions:

- normal SSH access, if needed
- normal HTTP browsing
- benign request generation

Main IP address in the lab network:

`192.168.100.30`

## Monitored Services

| Service | Target Port | Purpose |
|---|---:|---|
| SSH | 22/TCP | Authentication attempts and brute-force detection |
| HTTP | 80/TCP | Web request analysis and suspicious endpoint detection |

## Data Sources

| Source | Location | Purpose |
|---|---|---|
| Suricata EVE JSON | `/var/log/suricata/eve.json` | Network IDS alerts, flow data and event metadata |
| SSH authentication log | `/var/log/auth.log` | Failed and successful authentication events |
| Apache access log | `/var/log/apache2/access.log` | HTTP requests, requested paths, methods and status codes |

## Reproducibility Notes

Static IP addressing is used to make scenario execution, log parsing and event correlation more consistent.

The repository does not include real credentials, full raw logs or sensitive system-specific data. Only sanitized configuration notes, selected command outputs and anonymized data samples should be included.

# Network Configuration

This document describes the network configuration used in the virtual laboratory environment.

## Network Design

The laboratory environment uses an isolated internal VirtualBox network for experimental traffic and NAT connectivity for system preparation.

## Network Segments

| Segment | Type | Purpose |
|---|---|---|
| NAT | VirtualBox NAT | Internet access, package installation and updates |
| labnet | VirtualBox Internal Network | Isolated communication between lab machines |

## IP Addressing

| Host | IP Address | Role |
|---|---:|---|
| Target Server | 192.168.100.10 | monitored server |
| Attacker Machine | 192.168.100.20 | attack traffic source |
| Legitimate Client | 192.168.100.30 | benign traffic source |

## Target Services

| Service | Protocol | Port | Host |
|---|---|---:|---|
| SSH | TCP | 22 | Target Server |
| HTTP | TCP | 80 | Target Server |

## Main Traffic Flows

| Source | Destination | Purpose |
|---|---|---|
| Attacker Machine | Target Server | malicious scenario traffic |
| Legitimate Client | Target Server | benign traffic |
| Target Server | Local log files | system and application logging |
| Target Server | Suricata EVE JSON | IDS event output |

## Monitoring Point

Suricata monitors traffic on the target server interface connected to the internal lab network.

Monitored interface:

`enp0s8`

## Notes

The network is intentionally isolated to prevent test traffic from affecting external systems. All attack scenarios are executed only inside the controlled lab environment.

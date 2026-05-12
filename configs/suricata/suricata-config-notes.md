# Suricata Configuration Notes

This document summarizes the Suricata configuration used on the target server in the virtual laboratory environment.

## Role in the Lab

Suricata is used as a network-based intrusion detection system in passive IDS mode. Its purpose is to monitor traffic in the isolated laboratory network and generate structured security events for later analysis.

The Suricata output is compared with system and application logs in order to evaluate the difference between network-only detection, log-based detection and correlated detection.

## Deployment Location

| Parameter | Value |
|---|---|
| Host | VM1 - Target Server |
| Operating System | Ubuntu Server 24.04.4 LTS |
| Lab IP address | 192.168.100.10 |
| Monitored interface | enp0s8 |
| Mode | Passive IDS / NIDS |

## Monitored Interface

Suricata monitors the interface connected to the internal VirtualBox network segment.

Monitored interface:

```text
enp0s8
```

Internal network segment:

```text
labnet
```

## Main Output File

The primary Suricata output used for analysis is:

```text
/var/log/suricata/eve.json
```

This file is important because it stores Suricata events in structured JSON format, which makes it suitable for parsing and correlation with local logs.

## Relevant Event Types

The analysis primarily focuses on the following Suricata event types:

- alert
- flow
- http
- ssh
- dns

The exact available event types depend on the enabled Suricata configuration and active rules.

## Important Fields for Analysis

The following EVE JSON fields are relevant for parsing, comparison and correlation:

- timestamp
- event_type
- src_ip
- src_port
- dest_ip
- dest_port
- proto
- flow_id
- alert.signature
- alert.category
- alert.severity

## Detection Role

Suricata is used to detect network-visible indicators such as:

- port scanning behavior,
- repeated SSH connection patterns,
- suspicious HTTP request patterns,
- traffic toward uncommon or suspicious web paths.

## Correlation Role

Suricata events are correlated with local server logs using:

- timestamp proximity,
- source IP address,
- destination service or port,
- event type.

For example, SSH-related Suricata events can be compared with `/var/log/auth.log`, while HTTP-related Suricata events can be compared with `/var/log/apache2/access.log`.

## Limitations

Suricata observes traffic from the network perspective. This means it can detect communication patterns, but it cannot always determine the local outcome of an event.

For example, in an SSH brute-force scenario, Suricata can observe repeated SSH traffic, but system authentication logs are required to confirm whether login attempts failed or succeeded.

## Repository Safety Note

The full Suricata configuration file is not included directly in this repository at this stage. Only relevant configuration notes and sanitized excerpts should be included.

Raw logs and full configuration dumps should be reviewed and sanitized before being added publicly.

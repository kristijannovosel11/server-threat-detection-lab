# Detection Scenarios

This document describes the security scenarios used in the lab.

The SSH brute-force scenario has been executed and documented. The remaining scenarios are planned for later testing.

## Scenario 1: SSH Brute Force

Tool: Hydra  
Goal: Generate repeated failed SSH login attempts.

Observed results:

- SSH authentication logs recorded repeated failed login attempts from the attacker
- Suricata recorded the SSH network connections
- No matching Suricata alert was generated with the active ruleset
- PCAP traffic was captured for later analysis

Full scenario documentation:

`docs/ssh-bruteforce.md`

Status: Completed

## Scenario 2: Port Scanning

Tool: nmap  
Goal: Detect reconnaissance activity against the target server.

Expected visibility:

- Suricata: high
- System logs: low
- Correlation: useful for confirming target service exposure

Status: Planned

## Scenario 3: HTTP Request Abuse

Tool: curl, bash loop or other HTTP client  
Goal: Generate repeated or automated HTTP requests.

Expected visibility:

- Suricata: depends on active rules
- Web logs: records request paths, methods and response codes
- Correlation: useful for separating normal traffic from automated abuse

Status: Planned

## Scenario 4: Suspicious Endpoint Access

Tool: curl, browser or wordlist-based requests  
Goal: Attempt access to suspicious or non-existent web paths.

Example paths:

- /admin
- /login
- /backup
- /.env
- /config.php

Expected visibility:

- Suricata: depends on active rules
- Web logs: high
- Correlation: useful for confirming suspicious request behavior

Status: Planned

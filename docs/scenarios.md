# Detection Scenarios

This document describes the planned security scenarios used in the lab.

## Scenario 1: Port Scanning

Tool: nmap  
Goal: Detect reconnaissance activity against the target server.

Expected visibility:

- Suricata: high
- System logs: low
- Correlation: useful for confirming target service exposure

## Scenario 2: SSH Brute Force

Tool: hydra  
Goal: Generate repeated failed SSH login attempts.

Expected visibility:

- Suricata: detects repeated SSH connection patterns
- System logs: records failed authentication attempts
- Correlation: strongest approach because it connects network activity with authentication outcome

## Scenario 3: HTTP Request Abuse

Tool: curl, bash loop or other HTTP client  
Goal: Generate repeated or automated HTTP requests.

Expected visibility:

- Suricata: detects traffic patterns depending on rules
- Web logs: records request paths, methods and response codes
- Correlation: useful for separating benign traffic from automated abuse

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

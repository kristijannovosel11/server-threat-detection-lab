# SSH Configuration Notes

This document summarizes the SSH service configuration used in the virtual laboratory environment.

## Role in the Lab

SSH is used as the target service for authentication-based detection scenarios. It provides a controlled service against which repeated authentication attempts can be generated and later analyzed.

The SSH service is important because it produces system authentication logs that can be compared with Suricata network events.

## Deployment Location

| Parameter | Value |
|---|---|
| Host | VM1 - Target Server |
| Operating System | Ubuntu Server 24.04.4 LTS |
| Lab IP address | 192.168.100.10 |
| Service | OpenSSH Server |
| Port | 22/TCP |

## Relevant Log Source

SSH authentication events are analyzed from:

```text
/var/log/auth.log
```

This log source provides local server-side context that is not fully visible from network traffic alone.

## Relevant Log Events

The analysis focuses on authentication-related events such as:

- failed password attempts,
- invalid user attempts,
- accepted logins, if intentionally generated,
- authentication failures,
- closed SSH connections.

## Detection Role

SSH logs are used to determine whether SSH network activity resulted in actual authentication attempts on the target server.

This is especially important because encrypted SSH traffic limits what can be interpreted from the network layer alone. Suricata can observe communication patterns, while `/var/log/auth.log` provides the authentication outcome.

## Important Fields for Analysis

The following information is important when parsing SSH authentication logs:

- timestamp,
- service or process name,
- source IP address,
- username, if present,
- authentication result,
- event message.

## Correlation Role

SSH log events can be correlated with Suricata events using:

- timestamp proximity,
- source IP address,
- destination port 22/TCP,
- event type.

This allows comparison between network-level SSH activity and host-level authentication evidence.

## Repository Safety Note

Real usernames, passwords and credential lists are not included in this repository.

Any future log examples should be sanitized before publication. Sensitive values such as real usernames, passwords, hostnames and unrelated IP addresses should be removed or replaced with lab-safe placeholders.

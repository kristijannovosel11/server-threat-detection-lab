# Web Service Notes

This document summarizes the web service used on the target server in the virtual laboratory environment.

## Role in the Lab

The web service runs on the target server and provides HTTP traffic for the laboratory evaluation. Its records are used together with Suricata events during later analysis.

## Deployment Location

| Parameter | Value |
|---|---|
| Host | VM1 - Target Server |
| Operating System | Ubuntu Server 24.04.4 LTS |
| Lab IP address | 192.168.100.10 |
| Service | Apache HTTP Server |
| Port | 80/TCP |

## Main Record Source

The main web service record source used in the lab is the standard Apache access record file on Ubuntu systems.

## Relevant Fields

The analysis focuses on:

- client IP address,
- timestamp,
- HTTP method,
- requested path,
- HTTP response code,
- user agent, if available.

## Use in Correlation

Web service records are compared with Suricata events using time, client address, destination service and request information.

This supports comparison between network-level visibility and application-level server evidence.

## Notes

Only sanitized examples should be included in this repository. Full raw records should be reviewed before publication.

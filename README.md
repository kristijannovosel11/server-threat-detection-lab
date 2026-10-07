# server-threat-detection-lab
Virtual lab for evaluating network IDS, system logs and correlated threat detection.

This repository documents a virtual cybersecurity lab built for evaluating different approaches to detecting security threats in server network traffic.

## Project Goal

The goal of this project is to compare three detection approaches:

1. Network-based intrusion detection using Suricata
2. System and application log analysis
3. Correlation of IDS alerts with host and application logs

## Lab Environment

The lab is built using virtual machines in an isolated network environment.

Planned components:

- Ubuntu Server as the target server
- Kali Linux as the attacker machine
- Ubuntu client as the legitimate user
- Suricata as the network IDS
- SSH service for authentication-based scenarios
- Apache or Nginx web server for HTTP-based scenarios
- Python scripts for log parsing, event correlation and metric calculation

## Detection Scenarios

Planned scenarios:

- SSH brute-force attempts
- Port scanning
- HTTP request abuse
- Access to suspicious or non-existent endpoints

## Data Sources

The analysis is based on:

- Suricata EVE JSON logs
- System authentication logs
- Web server access logs
- Processed CSV/JSON datasets

## Evaluation Metrics

The project will use quantitative metrics such as:

- True Positive Rate
- False Positive Rate
- Precision
- False Negatives
- Detection coverage by data source

## Repository Status

This project is currently in progress as part of a master's thesis laboratory implementation.

Initial README for threat detection lab

## Completed Lab Scenario

### SSH Brute-Force Detection

I executed a controlled SSH brute-force test from Kali Linux against the Ubuntu target server.

The test included:

- 30 password attempts with Hydra
- SSH authentication log analysis
- Suricata SSH event analysis
- packet capture with tcpdump

The SSH logs clearly recorded the failed authentication attempts.

Suricata recorded the SSH traffic, but no matching alert was generated with the active ruleset.

Full documentation and evidence:

[SSH Brute-Force Scenario](docs/ssh-bruteforce.md)

# Lab Architecture

The laboratory environment is designed as an isolated virtual network used to generate, observe and analyze both legitimate and malicious traffic.

## Virtual Machines

| VM | Role | Operating System | Purpose |
|---|---|---|---|
| Target Server | Victim / monitored server | Ubuntu Server | Runs SSH, web server and Suricata |
| Attacker | Attack machine | Kali Linux | Generates malicious traffic |
| Legitimate Client | Benign user | Ubuntu Desktop/Server | Generates normal traffic |

## Detection Sources

The lab uses three main data sources:

1. Suricata alerts and network events
2. System authentication logs
3. Web server access logs

## Detection Logic

The experiment compares detection results from:

- Network IDS only
- Log analysis only
- Correlated detection using both IDS and logs

# Methodology

This document describes the planned evaluation methodology. Automated correlation and metric calculation have not been implemented yet.

This document describes the methodology used to evaluate security threat detection in a controlled virtual laboratory environment.

## Evaluation Goal

The goal of the experiment is to compare three detection approaches:

1. Network-based detection using Suricata
2. System and application log analysis
3. Correlated detection using both IDS alerts and local logs

The comparison is performed under the same laboratory conditions and against the same predefined security scenarios.

## Laboratory Approach

The lab is based on an isolated virtual network containing:

- a target Ubuntu Server
- a Kali Linux attacker machine
- a legitimate Ubuntu client

The attacker machine is used to generate controlled malicious traffic, while the legitimate client is used to generate benign traffic. The target server runs network and application services that produce logs used in the analysis.

## Data Sources

The experiment uses the following data sources:

| Source | File / Output | Purpose |
|---|---|---|
| Suricata | eve.json | Network IDS alerts and flow/event data |
| SSH logs | auth.log | Authentication attempts and login outcomes |
| Web server logs | access.log | HTTP requests, paths, methods and status codes |
| Scenario notes | manual timestamps | Ground truth for each executed scenario |

## Ground Truth

Each test scenario is manually planned and timestamped before execution. This allows comparison between expected malicious activity and the events detected by Suricata, system logs and correlated analysis.

Ground truth records include:

- scenario name
- attacker IP address
- target IP address
- target service
- start time
- end time
- expected detection source

## Correlation Logic

Events from different sources are correlated using:

- timestamp proximity
- source IP address
- destination service or port
- event type

A time window of approximately ±5 seconds is used as the initial correlation threshold. This value may be adjusted depending on timestamp precision and observed log behavior.

## Evaluation Metrics

The following metrics are used to evaluate detection performance:

- True Positives
- False Positives
- False Negatives
- True Positive Rate
- False Positive Rate
- Precision

The final comparison focuses on detection coverage, reliability and practical usefulness of each approach.

## Limitations

The experiment is performed in a controlled virtual environment. Results may differ in production environments due to higher traffic volume, encrypted traffic, different rule sets, different system configurations and more diverse user behavior.

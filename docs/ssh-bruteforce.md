# SSH Brute-Force Scenario

## Goal

I used this scenario to generate repeated failed SSH login attempts against the target server.

The goal was to compare what the SSH authentication logs record and what Suricata sees on the network.

## Lab Setup

- Attacker: Kali Linux - 192.168.100.20
- Target: Ubuntu Server - 192.168.100.10
- Service: OpenSSH on TCP port 22
- Network IDS: Suricata
- Attack tool: Hydra

The machines communicated through the isolated laboratory network.

## Test Procedure

First, I confirmed that TCP port 22 was open on the target server.

I created a test wordlist with 30 incorrect passwords.

I then executed Hydra against the `target` user:

```bash
hydra -l target -P ~/ssh_bruteforce_wordlist_final.txt -t 4 -V ssh://192.168.100.10
```

Hydra executed 30 password attempts and reported that no valid password was found.

During the test, I captured SSH traffic with tcpdump. The final PCAP contained 300 captured packets and no packets were dropped by the capture process.

## SSH Log Observation

The target server recorded repeated failed authentication events in `auth.log`.

The log contains entries such as:

```text
pam_unix(sshd:auth): authentication failure
Failed password for target from 192.168.100.20
```

The log also showed messages such as `maximum authentication attempts exceeded` and `Too many authentication failures`.

I did not assume that every Hydra attempt produced exactly one matching log line because SSH and PAM can record the authentication process using multiple event types.

A small sample is stored in:

`evidence/ssh-bruteforce/auth_sample.txt`

## Suricata Configuration

The target server used Suricata version `7.0.3`.

The active rule configuration used:

- rule file: `/var/lib/suricata/rules/suricata.rules`
- loaded rules: `49,582`
- failed rules: `0`

The Suricata startup log confirmed that one rule file was processed successfully.
`suricata-update list-enabled-sources` returned no separately enabled rule sources, so I do not assume a specific external ruleset provider.

## Suricata Observation

Suricata recorded SSH traffic from `192.168.100.20` to `192.168.100.10` on TCP port 22.

The EVE JSON output contains SSH events with:

- source IP: `192.168.100.20`
- destination IP: `192.168.100.10`
- destination port: `22`
- event type: `ssh`

For the final run, I checked new EVE JSON entries generated after the recorded pre-test position and filtered alert events containing the attacker IP address.

The alert count was calculated using the following command:

```bash
sudo tail -n +15600 /var/log/suricata/eve.json \
  | grep '"event_type":"alert"' \
  | grep '192.168.100.20' \
  | wc -l
```

Line `15599` was recorded as the last EVE JSON line before the final test, so the analysis started from line `15600`.
The number of matching Suricata alerts was:

```text
0
```

Suricata therefore had visibility of the SSH connections, but I found no matching alert for this test with the active ruleset.

## Evidence

The following files are stored in `evidence/ssh-bruteforce/`:

- `auth_sample.txt` - sample of SSH authentication events
- `suricata_ssh_sample.json` - sample of Suricata SSH events
- `suricata_alert_count.txt` - matching alert count for the final run
- `ssh_bruteforce_final.pcap` - captured SSH traffic

## What I learned

I could see repeated failed login attempts in the server's SSH logs.

Suricata recorded the SSH connections, but I found no matching alerts for this test.

I learned that seeing network traffic does not automatically mean that an IDS will flag the activity.

## Limitations

This was one controlled test with one attacker and one target.

I used a wordlist with 30 incorrect passwords.

The result depends on the active Suricata rules and configuration.

It does not show how Suricata would perform in other scenarios.

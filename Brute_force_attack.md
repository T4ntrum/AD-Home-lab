#  MITRE ATT&CK T1110.001 Brute Force: Password Guessing


Environment: AD Lab 

Tools used: CrackMapExec, Kali Linux

--- 

## Overview

Brute force attack simulation against an SMB service on a domain-joined Windows 10 machine using a wordlist. 

The goal was to improve detection capabilities in Splunk and generate telemetry. 

**Target:** TARGET-PC (192.168.10.100)  
**Attacker:** Agnes-Tachyon (192.168.10.250)  
**Protocol:** SMB (Port 445)  
**Domain:** derby.local  
**Account Targeted:** dscarlet  

--- 
# Mock writeup
## Attack Summary 
19 failed authentication attempts were made against the account user `derby.local\dscarlet` via SMB (port 445), with a successful logon occurring on the 20th attempt. All attempts originated from 192.168.10.250

## Splunk detection query

`index="endpoint" host="target-PC" EventCode=4625 OR 4624`

Event code 4624: An account was successfully logged on.


Event code 4625: An account failed to log on.

This query shows unsuccessful logons and successful logons on the host machine "target-PC".


### Findings
- 19 failed logon attempts from a source IP of 192.168.10.250
- 1 successful logon attempt from source IP 192.168.10.250
- Large amounts of attempts within a short time span indicate that this was done with an automated tool. 

### Recommendations 

- Add a password maximum attempts lockout (5 attempts)
- Enforce password complexity policy 
- Create a Splunk alert rules based on the event code 4625 to trigger for future events

### Example Splunk rule for alerts
```spl 
index="endpoint" host="target-PC" EventCode=4625
| bucket _time span=1m
| stats count by _time, Account_Name
| where count > 5
```
- Groups all the events into 1 minute time buckets
- See all events that happened within a 1 minute time window
- Counts how many failures occurred per minute, per account

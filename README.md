# A home lab environment built to simulate real-world Active Directory attacks and practice SOC detection and analysis skills using Splunk and Sysmon.

## Purpose
This lab was built to develop hands-on experience in:

- Simulating adversary techniques mapped to the MITRE ATT&CK framework
- Detecting attacks using Splunk queries and alert rules
- Analyzing Windows Event Logs and Sysmon telemetry
- Writing SOC-style incident reports and detection documentation

## Network Overview
- Domain: derby.local
- Network: 192.168.10.0/24
- Splunk Server: 192.168.10.10
- Active Directory: 192.168.10.7
- Attacker Machine: 192.168.10.250
- Target Machine: 192.168.10.100

## Lab Components
- Ubuntu server: Splunk server
- Active Directory server: Windows Server 2022
- Attacker Machine: Kali Linux
- Target Machine: Windows 10

## Tools
- Sysmon
- CrackMapExec
- Atomic Red Team

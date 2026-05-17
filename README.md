# Splunk SIEM Homelab

## Overview
Built a fully functional SIEM environment using Splunk Enterprise to monitor an Active Directory domain. Configured log ingestion, built security dashboards, and created automated alerting rules to detect suspicious activity.

## Environment
- Host OS: Windows 11
- Hypervisor: VirtualBox
- Splunk Server: Ubuntu Server 24.04 (Splunk Enterprise 10.2.3)
- Domain Controller: Windows Server (Active Directory)
- Network: pfSense firewall/router managing internal LAN

## What I Built
- Deployed Ubuntu Server VM and installed Splunk Enterprise
- Configured Splunk to receive logs on port 9997
- Installed Splunk Universal Forwarder on Active Directory Domain Controller
- Configured Windows Event Log collection (Security, System, Application)
- Built AD Security Monitor dashboard with event summary and account activity panels
- Created automated alert for multiple failed login detection (EventCode 4625)

## Key Event Codes Monitored
| EventCode | Description |
|-----------|-------------|
| 4624 | Successful logon |
| 4625 | Failed logon attempt |
| 4634 | Account logoff |
| 4720 | User account created |
| 4726 | User account deleted |
| 4738 | User account changed |
| 4740 | Account locked out |
| 4767 | Account unlocked |
| 4672 | Admin privileges assigned |

## Splunk Searches Used
Failed logins: index=main EventCode=4625

Account management: index=main (EventCode=4720 OR EventCode=4726 OR EventCode=4740 OR EventCode=4767 OR EventCode=4738)

Alert rule: index=main EventCode=4625 | stats count by Account_Name | where count > 3

## Skills Demonstrated
- SIEM deployment and configuration
- Windows Event Log analysis
- Active Directory security monitoring
- Splunk Search Processing Language (SPL)
- Network configuration (pfSense, static IP, multi-adapter VM networking)
- Linux server administration (Ubuntu, netplan, systemd)

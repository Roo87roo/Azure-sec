# Azure-sec#Azure-Based SOC and Honeynet Project (Monitoring Live Traffic)
![Cloud Honeynet / SOC](https://i.imgur.com/ZWxe03e.jpg)

## Introduction

I create a honeynet in Azure and use Log Analytics workspace to ingest log data from different resources. Microsoft Sentinel helps me to visualize the attack patterns, generate alerts, and create incidents based on the log data. I show how applying some security controls improves the security metrics of the environment over two days. The metrics are:
- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture pre-Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/aBDwnKb.jpg)

##Architecture with Security Controls Applied (hardened)
![Architecture Diagram](https://i.imgur.com/YQNa9Pp.jpg)

The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

I measured the “BEFORE” metrics when the resources were first deployed, with no protection from the internet. The Virtual Machines had their Network Security Groups and their built-in firewalls completely open, and all other resources used public endpoints instead of Private Endpoints.

I measured the “AFTER” metrics when the resources were secured by security controls. The Network Security Groups only allowed traffic from my admin workstation and blocked everything else, and all other resources had both built-in firewalls and Private Endpoint for protection.
## Attack Maps Before Hardening / Security Controls
![NSG Allowed Inbound Malicious Flows](https://github.com/Roo87roo/test/blob/main/nsg-malicious-allowed-in%20(before).jpg?raw=true)<br>
![Linux Syslog Auth Failures](https://github.com/Roo87roo/test/blob/main/Syslog-ssh-auth-fail%20(before).jpg?raw=true)<br>
![Windows RDP/SMB Auth Failures](https://github.com/Roo87roo/test/blob/main/Windows-RDP-AUTH-Fail%20(before).jpg?raw=true)<br>

## Metrics Before Hardening / Security Controls

The metrics in the table below were measured in our insecure environment for 24 hours: 
Start Time 2023-03-15 17:04:29 
Stop Time 2023-03-16 17:04:29

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 12180
| Syslog                   | 2345
| SecurityAlert            | 8
| SecurityIncident         | 73
| AzureNetworkAnalytics_CL | 576

## Attack Maps Before Hardening / Security Controls

```There was no malicious activity in the 24 hour period after hardening, so no map queries had any results.```

## Metrics After Hardening / Security Controls

The metrics in the table below were measured in our environment for 24 hours after applying security controls.:
Start Time 2023-03-18 15:37
Stop Time	2023-03-19 15:37

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 110
| Syslog                   | 47
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

This project shows how to build a mini honeynet in Microsoft Azure and use Log Analytics and Microsoft Sentinel to monitor and respond to security events. The project also compares the metrics of the environment before and after applying security controls and shows how they reduced the number of security events and incidents significantly.

A possible caveat is that more security events and alerts might have occurred in the 24-hour period after the security controls were applied if the resources within the network had more regular user activity.

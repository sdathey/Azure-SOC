# Azure - SOC - Honeynet - Project (Live Traffic)
![Cloud Honeynet / SOC](https://i.imgur.com/VGcjyU7.jpg)

## Introduction

This project is a honeynet in Azure made with a Fictional Company called Rayda Estate to entice attackers on the Internet. I will ingest log sources from various resources into a Log Analytics workspace, which is then used by Microsoft Sentinel to build attack maps, trigger alerts, and create incidents. I measured some security metrics in the insecure environment for 24 hours, applied some security controls to harden the environment, measured metrics for another 24 hours, the results shown below. The metrics shown are:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening And Implementing Of Security Controls
![Architecture Diagram](https://i.imgur.com/1yJ0IJU.jpg)

## Architecture After Hardening And Implementing Of Security Controls
![Architecture Diagram](https://i.imgur.com/c0cSnfw.jpg)

The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

For the "BEFORE" metrics, all resources were originally deployed, exposed to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls wide open, and all other resources are deployed with public endpoints visible to the Internet (No Private Endpoints).

For the "AFTER" metrics, Network Security Groups were hardened by blocking ALL traffic with the exception of my admin workstation, and all other resources were protected by their built-in firewalls as well as Private Endpoints.

## Attack Maps Before Hardening And Implementing Security Controls
![NSG Allowed Inbound Malicious Flows](https://i.imgur.com/OKmlgcm.jpg)<br>
![Linux Syslog Auth Failures](https://i.imgur.com/Ywmqqwd.jpg)<br>
![Windows RDP/SMB Auth Failures](https://i.imgur.com/h9r5oGY.jpg)<br>
![MSSQL Auth Failures](https://i.imgur.com/JimzOeB.jpg)

## Metrics Before Hardening And Implementing Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 6/12/2023 8:44:39 AM
Stop Time  6/13/2023 8:44:39 AM

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 148544
| Syslog                   | 576
| SecurityAlert            | 0 
| SecurityIncident         | 330
| AzureNetworkAnalytics_CL | 1478

The number of alerts were staggering!!! Over 150000 alerts were created in 24 hours. I believe the naming (Rayda Estate) made attackers thought it was a real domain.

## Tools And Technologies Used To Harden The environments
- Microsoft Cloud security Benchmark
-  Microsoft Defender For Cloud
- NIST SP 800-53 R4
- Azure CIS 1.4.0
- PCI DSS 4
- Network Security Group (NSG)
- Virtual Network (VNet)
- Private Endpoint (PE)
- Firewalls
- ACLs

## Attack Maps Before Hardening And Implementing Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening And Implementing Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 6/15/2023, 8:57:44 AM
Stop Time	 6/16/2023, 8:57:44 AM

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 4690
| Syslog                   | 13
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Results Of The Change In The Reduction Of The Attack Surface

| Metric                        | Change After Security Controls Application
|-------------------------------| ------------------------------------------
| SecurityEvents                | 96.84%
| Syslog                        | 97.74%
| SecurityAlert                 | N/A
| SecurityIncident              | 100.00%
| AzureNetworkAnalytics_CL      | 100.00%

## Conclusion

In this project, a mini honeynet was constructed in Microsoft Azure and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. It is noteworthy that the number of security events and incidents were drastically reduced after the security controls were applied, demonstrating their effectiveness.

It is also worth noting that if the resources within the network were heavily utilized by regular users, it is likely that more security events and alerts may have been generated within the 24-hour period following the implementation of the security controls.

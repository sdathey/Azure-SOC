# Azure - SOC - Honeynet - Project (Live Traffic)
![Cloud Honeynet / SOC](https://i.imgur.com/VGcjyU7.jpg)

## Introduction

In this project, Rayda Estate, a fictional company, has deployed an Azure-based honeynet to attract Internet attackers. Log sources from various resources are collected in a Log Analytics workspace, enabling Microsoft Sentinel to generate attack maps, alerts, and incidents. Initial security metrics were measured over a 24-hour period in the insecure environment. Subsequently, security controls were implemented to fortify the environment, and metrics were measured for an additional 24 hours. The following metrics are used:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

The architecture of the honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

## Architecture Before Hardening And Implementing Of Security Controls
![Architecture Diagram](https://i.imgur.com/1yJ0IJU.jpg)

Before implementing any security controls, all resources in the honeynet were initially deployed and exposed to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls set to allow all traffic, and other resources were deployed with public IP Addresses visible to the Internet, without any private endpoints.

## Architecture After Hardening And Implementing Of Security Controls
![Architecture Diagram](https://i.imgur.com/c0cSnfw.jpg)

After implementing security controls, notable changes were made to the network infrastructure. The Network Security Groups were strengthened by blocking ALL traffic, except for communication originating from my admin workstation. Additionally, all other resources were safeguarded by their built-in firewalls and secured through the utilization of Private Endpoints, ensuring a more robust and restricted access environment.


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

The implementation of security controls in the honeynet project on Microsoft Azure resulted in a significant reduction in security events and incidents. This indicates the effectiveness of the applied security measures. It is important to mention that if the network resources were heavily utilized by regular users, there might have been a higher number of security events and alerts during the 24-hour period following the implementation of the security controls.

Overall, the project highlights the importance of implementing robust security measures to enhance the security posture of network environments and to reduce its attack surface.

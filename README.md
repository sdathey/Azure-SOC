# Azure - SOC - Honeynet - Project (Real Time Cyber Attacks)
![Cloud Honeynet / SOC](https://i.imgur.com/VGcjyU7.jpg)

## Introduction

In this project, Rayda Estate, a fictional company, has deployed an Azure-based honeynet open to the Internet to attract  hackers. Log sources from various resources are collected in a Log Analytics workspace, enabling Microsoft Sentinel to generate attack maps, alerts, and incidents. Initial security metrics were measured over 24 hours in the insecure environment. Subsequently, security controls were implemented to fortify the environment, and metrics were measured for another 24 hours. 

The architecture of the honeynet in Azure consists of the following components:

- Azure Key Vault
- Microsoft Sentinel
- Azure Storage Account
- Virtual Network (VNet)
- Log Analytics Workspace
- Network Security Group (NSG)
- Virtual Machines (2 Windows, 1 Linux)





## Architecture Before Hardening And Implementing Security Controls
![Architecture Diagram](https://i.imgur.com/1yJ0IJU.jpg)

Before implementing any security controls, all resources in the honeynet were initially deployed and exposed to the Internet. The Virtual Machines had both their Network Security Groups and built-in firewalls set to allow all traffic. Other resources were deployed with public IP Addresses visible to the Internet, without any private endpoints.

## Architecture After Hardening And Implementing Security Controls
![Architecture Diagram](https://i.imgur.com/c0cSnfw.jpg)

After implementing security controls, notable changes were made to the network infrastructure. The Network Security Groups were strengthened by blocking ALL traffic, except for communication originating from my admin workstation. Additionally, all other resources were safeguarded by their built-in firewalls and secured by using Private Endpoints, ensuring a more robust and restricted access environment.


## Attack Maps Before Hardening And Implementing Security Controls
The following metrics were used to query these maps:

- Syslog (Linux Event Logs)
- SecurityEvent (Windows Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

![NSG Allowed Inbound Malicious Flows](https://i.imgur.com/0654REU.jpg)<br>
![Linux Syslog Auth Failures](https://i.imgur.com/1qidkTm.jpg)<br>
![Windows RDP/SMB Auth Failures](https://i.imgur.com/GNDKcAy.jpg)<br>
![MSSQL Auth Failures](https://i.imgur.com/w56RB4X.jpg)

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

The number of alerts was staggering!!! Over 150000 were created in 24 hours. I believe the naming (Rayda Estate) made attackers think it was a real domain.

## Tools And Technologies Used To Harden The environments
- Microsoft Cloud Security Benchmark
- Microsoft Defender For Cloud
- NIST SP 800-53 R4
- NIST SP 800-61 R2
- Azure CIS 1.4.0
- PCI DSS 4
- Network Security Group (NSG)
- Virtual Network (VNet)
- Private Endpoint (PE)
- Firewalls
- ACLs

## Attack Maps After Hardening And Implementing Security Controls

```All map queries returned no results due to no instances of malicious activity for the 24 hours after hardening.```

## Metrics After Hardening And Implementing Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we applied security controls:
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
Rate of Change after the environment was secured

| Metric                        | Change After Security Controls Application
|-------------------------------| ------------------------------------------
| SecurityEvents                | 96.84%
| Syslog                        | 97.74%
| SecurityAlert                 | N/A
| SecurityIncident              | 100.00%
| AzureNetworkAnalytics_CL      | 100.00%

## Conclusion

The Implementation of security controls in this Honeynet project in Microsoft Azure resulted in a significant reduction in security events and incidents. This indicates the effectiveness of the applied security measures. It is important to mention that if the network resources were heavily utilized by regular users, there might have been a higher number of security events and alerts during the 24 hours following the implementation of the security controls.

Overall, this project highlights the importance of implementing robust security measures to enhance the security posture of network environments and to reduce their attack surface.

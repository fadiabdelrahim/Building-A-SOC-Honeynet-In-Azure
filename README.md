# <p align="center"> Building A SOC + Honeynet In Azure (Live Traffic)

<p align="center"><img src="images/Cloud Honeynet + SOC.png"></p>

## Introduction
In this project, I set up a mini honeynet on Azure and directed log sources from various resources into a Log Analytics workspace. This workspace was then leveraged by Microsoft Sentinel to generate attack maps, trigger alerts, and create incidents. I initially recorded security metrics in the unsecured environment over a 24-hour period, implemented security controls to reinforce the environment, and then captured metrics for an additional 24 hours. The following metrics are highlighted:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious network flows detected in the honeynet)

## Architecture Before Hardening / Security Controls

<p align="center"><img src="images/Architecture Before Hardening _ Security Controls.png"></p>

## Architecture After Hardening / Security Controls

<p align="center"><img src="images/Architecture After Hardening _ Security Controls.png"></p>

The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

For the "BEFORE" metrics, all resources were initially deployed and exposed directly to the internet. The Virtual Machines had their Network Security Groups and built-in firewalls fully open, with all other resources accessible through public endpoints—meaning Private Endpoints were not utilized.

For the "AFTER" metrics, the Network Security Groups were significantly tightened, blocking ALL traffic except for access from my admin workstation. Additionally, all other resources were secured using their built-in firewalls and protected by Private Endpoints.

## Attack Maps Before Hardening / Security Controls

<p align="center"><img src="images/(Before)24hr-nsg-malicious-allowed-in - Microsoft Azure.png"></p>

<p align="center"><img src="images/(Before)24hr-linux-ssh-auth-fail - Microsoft Azure.png"></p>

<p align="center"><img src="images/(Before)24hr-windows-rdp-auth-fail - Microsoft Azure.png"></p>

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:

***Start Time:*** 2024-08-23 21:22:46</br>
***Stop Time:*** 2024-08-24 21:22:46

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 20564
| Syslog                   | 1179
| SecurityIncident         | 161
| AzureNetworkAnalytics_CL | 417

## Attack Maps After Hardening / Security Controls

All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:

***Start Time:*** 2024-08-28 02:37:36</br>
***Stop Time:***	2024-08-29 02:37:36

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 8327
| Syslog                   | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, a mini honeynet was set up in Microsoft Azure, and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was used to trigger alerts and create incidents based on the logs collected. Metrics were recorded both in the unsecured environment and after applying security measures. The results clearly showed a significant reduction in the number of security events and incidents after implementing these controls, highlighting their effectiveness.






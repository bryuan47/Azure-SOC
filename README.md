# Azure-SOC
# Building a SOC + Honeynet in Azure (Live Traffic)
![Untitled drawing (1)](https://github.com/user-attachments/assets/28ee4136-e23f-414b-9dc9-ade41f9f4a07)



## Introduction

In this project, I built a mini honeynet in Azure and ingested log sources from various resources into a Log Analytics workspace, which Microsoft Sentinel then uses to build attack maps, trigger alerts, and create incidents. I measured some security metrics in the insecure environment for 24 hours, applied some security controls to harden the environment, measured metrics for another 24 hours, and then show the results below. The metrics we will show are:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![Untitled drawing (2)](https://github.com/user-attachments/assets/c8af1acd-a5f1-4f42-ae87-000f3f3b63f1)


## Architecture After Hardening / Security Controls
![Untitled drawing (3)](https://github.com/user-attachments/assets/48199d91-f1e9-4583-bb70-81967e2478b1)


The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

For the "BEFORE" metrics, all resources were originally deployed, exposed to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls wide open, and all other resources are deployed with public endpoints visible to the Internet; aka, no use for Private Endpoints.

For the "AFTER" metrics, Network Security Groups were hardened by blocking ALL traffic with the exception of my admin workstation, and all other resources were protected by their built-in firewalls as well as Private Endpoint

## Attack Maps Before Hardening / Security Controls
![Linux Fails before](https://github.com/user-attachments/assets/3955d9b3-135b-4069-bbd6-6653f143bc34)<br>
![Windows Auth Fail 30days](https://github.com/user-attachments/assets/d39a5dbd-ee47-4f4f-8d58-2c712dada790)<br>
![Windows RDP before](https://github.com/user-attachments/assets/16d18907-e5bc-46d0-8475-df8ac843148c)<br>

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2025-05-19 21:21:53
Stop Time 2025-05-20T21:21:53

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 864
| Syslog                   | 1591
| SecurityAlert            | 23
| SecurityIncident         | 24
| AzureNetworkAnalytics_CL | 29

## Attack Maps Before Hardening / Security Controls

```All map queries returned no results due to no instances of malicious activity for the 24-hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2023-03-18 15:37
Stop Time	2023-03-19 15:37

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 457
| Syslog                   | 0
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, a mini honeynet was constructed in Microsoft Azure, and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. It is noteworthy that the number of security events and incidents was drastically reduced after the security controls were applied, demonstrating their effectiveness.

It is worth noting that if the resources within the network were heavily utilized by regular users, it is likely that more security events and alerts may have been generated within the 24 hours following the implementation of the security controls.

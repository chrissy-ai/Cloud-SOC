# Building a SOC + Honeynet in Azure (Live Traffic)
![image](https://github.com/chrissy-ai/Cloud-SOC/assets/106142143/54e0b22d-8da2-408c-85d5-a5c4c7ce31a4)



## Introduction

In this project, I build a mini honeynet in Azure and ingest log sources from various resources into a Log Analytics workspace, which is then used by Microsoft Sentinel to build attack maps, trigger alerts, and create incidents. I measured some security metrics in the insecure environment for 24 hours, apply some security controls to harden the environment, measure metrics for another 24 hours, then show the results below. The metrics we will show are:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![image](https://github.com/chrissy-ai/Cloud-SOC/assets/106142143/dc80e480-07bf-4205-b1b9-7902c5aaf08e)



## Architecture After Hardening / Security Controls

![image](https://github.com/chrissy-ai/Cloud-SOC/assets/106142143/0ef26916-9fa9-4db1-88ba-d433f90716a3)


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
![image](https://github.com/chrissy-ai/Cloud-SOC/assets/106142143/d11da6ce-8f71-4760-9146-ea6e55522452)
![image](https://github.com/chrissy-ai/Cloud-SOC/assets/106142143/9ddea35c-0ac3-44df-8a9d-6c40aef5b9cf)
![image](https://github.com/chrissy-ai/Cloud-SOC/assets/106142143/c5a57548-14fa-4612-bebc-06dde48557b0)
![image](https://github.com/chrissy-ai/Cloud-SOC/assets/106142143/64f868d9-2599-4964-aa04-d438304c18fc)





## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2024-02-15 21:04:29
Stop Time 2024-02-14 21:04:29

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 17032
| Syslog                   | 868
| SecurityAlert            | 10
| SecurityIncident         | 213
| AzureNetworkAnalytics_CL | 843

## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2023-03-18 15:37
Stop Time	2023-03-19 15:37

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 5302
| Syslog                   | 3
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, a mini honeynet was constructed in Microsoft Azure and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. It is noteworthy that the number of security events and incidents were drastically reduced after the security controls were applied, demonstrating their effectiveness.

It is worth noting that if the resources within the network were heavily utilized by regular users, it is likely that more security events and alerts may have been generated within the 24-hour period following the implementation of the security controls.

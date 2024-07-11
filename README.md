# Building a SOC + Honeynet in Azure (Live Traffic)
![Screenshot (19)](https://github.com/intTone13/Azure_SOC/assets/124211905/5f933cd4-5f83-41fd-b5bf-209c7bc7a194)



## Introduction

In this project, I build a mini honeynet in Azure and ingest log sources from various resources into a Log Analytics workspace, which is then used by Microsoft Sentinel to build attack maps, trigger alerts, and create incidents. I measured some security metrics in the insecure environment for 24 hours, apply some security controls to harden the environment, measure metrics for another 24 hours, then show the results below. The metrics we will show are:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![Screenshot (13)](https://github.com/intTone13/Azure_SOC/assets/124211905/d86cedf5-6ab6-4750-ae20-4392aed3f0a2)


## Architecture After Hardening / Security Controls
![Screenshot (17)](https://github.com/intTone13/Azure_SOC/assets/124211905/89803181-f7c1-4893-b7b5-2c0e8911941e)



The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (1 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

For the "BEFORE" metrics, all resources were originally deployed, exposed to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls wide open, and all other resources are deployed with public endpoints visible to the Internet; aka, no use for Private Endpoints.

For the "AFTER" metrics, Network Security Groups were hardened by blocking ALL traffic with the exception of my admin workstation, and all other resources were protected by their built-in firewalls as well as Private Endpoint

## Attack Maps Before Hardening / Security Controls
![Screenshot (5)](https://github.com/intTone13/Azure_SOC/assets/124211905/ce4d1602-05cb-41ee-a89a-b1d3e3138243)<br>
![Screenshot (6)](https://github.com/intTone13/Azure_SOC/assets/124211905/d1a3118b-86a6-4f9f-baa6-1ba97225c5fc)<br>
![Screenshot (7)](https://github.com/intTone13/Azure_SOC/assets/124211905/f2e17c07-5c11-4086-9efe-bf8d979f414c)<br>

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2024-07-04 10:40:06 PM
Stop Time 2024-07-05 10:40:06 PM

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 21319
| Syslog                   | 2193
| SecurityAlert            | 1
| SecurityIncident         | 144
| AzureNetworkAnalytics_CL | 1896

## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2024-07-06 09:27:22 PM
Stop Time	2024-07-07 09:27:22 PM

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 9148
| Syslog                   | 5
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

For this project, I set up a small honeynet in Microsoft Azure and connected it to a Log Analytics workspace. I used Microsoft Sentinel to trigger alerts and create incidents based on the logs. I measured the metrics in the insecure environment before adding security controls, and then again after applying the security measures. The results showed that the number of security events and incidents went down significantly after the security controls were in place, proving their effectiveness.

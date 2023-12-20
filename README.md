# Building a SOC + Honeynet in Azure (Live Traffic)
![image](https://github.com/WilliusThe3rd/Azure-SOC/assets/115587517/3fce0783-ccd9-4754-a09b-da76ff8562fb)


## Introduction

In this project, I build a mini honeynet in Azure and ingest log sources from various resources into a Log Analytics workspace, which is then used by Microsoft Sentinel to build attack maps, trigger alerts, and create incidents. I measured some security metrics in the insecure environment for 24 hours, apply some security controls to harden the environment, measure metrics for another 24 hours, then show the results below. The metrics we will show are:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![image](https://github.com/WilliusThe3rd/Azure-SOC/assets/115587517/d96989e1-9d30-4d0d-95da-e39b25b3c1da)


## Architecture After Hardening / Security Controls
![image](https://github.com/WilliusThe3rd/Azure-SOC/assets/115587517/baca6d46-3094-4cd3-84ea-8aa0a82aca69)


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
![image](https://github.com/WilliusThe3rd/Azure-SOC/assets/115587517/519844b3-5187-4ca8-830d-829034228ff3)
![image](https://github.com/WilliusThe3rd/Azure-SOC/assets/115587517/0a6f9921-fb8d-4293-9832-6cb8da7f8a81)
![image](https://github.com/WilliusThe3rd/Azure-SOC/assets/115587517/004b6ff8-df7a-47d2-8772-d85ed6ba6c79)

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:

Start Time 2023-12-18 12:09:09

Stop Time 2023-12-19 12:09:09

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 23992
| Syslog                   | 1752
| SecurityAlert            | 1
| SecurityIncident         | 54
| AzureNetworkAnalytics_CL | 62924

## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:

Start Time 2023-03-18 15:37

Stop Time	2023-03-19 15:37

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 5778
| Syslog                   | 147
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, a mini honeynet was constructed in Microsoft Azure and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. It is noteworthy that the number of security events and incidents were drastically reduced after the security controls were applied, demonstrating their effectiveness.

It is worth noting that if the resources within the network were heavily utilized by regular users, it is likely that more security events and alerts may have been generated within the 24-hour period following the implementation of the security controls.


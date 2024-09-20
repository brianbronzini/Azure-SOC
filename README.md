# Building a SOC + Honeynet in Azure (Live Traffic)
<img src="https://i.ibb.co/KqQb9m9/Azure-SOC-main.png" alt="Azure-SOC-main" border="0">

## Introduction

In this project, I built a mini honeynet in Azure and ingested log sources from various resources into a Log Analytics workspace. Microsoft Sentinel was then used to generate attack maps, trigger alerts, and create incidents. I measured security metrics in the initial insecure environment for 24 hours, applied security controls to harden the system, and then measured the metrics for another 24 hours. The key metrics analyzed are:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/aBDwnKb.jpg)

## Architecture After Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/YQNa9Pp.jpg)

The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

### Before Hardening:
All resources were exposed to the internet. The Virtual Machines had wide-open Network Security Groups and firewalls, and the remaining resources were deployed with public endpoints, without utilizing Private Endpoints.

### After Hardening
Network Security Groups were tightened to block all traffic except from my admin workstation. Other resources were secured using built-in firewalls and private endpoints.

## Attack Maps Before Hardening / Security Controls
<img src="https://i.ibb.co/fNWqQhW/nsg-malicious-allowed-in.png" alt="nsg-malicious-allowed-in" border="0"><br>
<img src="https://i.ibb.co/0cHZXV6/linux-auth-fail.png" alt="linux-auth-fail" border="0"><br>
<img src="https://i.ibb.co/3CTrzXm/windows-rdp-auth-fail.png" alt="windows-rdp-auth-fail" border="0"><br>

## Security Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2024-08-31 22:51
Stop Time 2024-09-02 22:51

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 12421
| Syslog                   | 2122
| SecurityAlert            | 4
| SecurityIncident         | 279
| AzureNetworkAnalytics_CL | 666

## Attack Maps After Hardening / Security Controls

```All map queries returned no results due to no instances of malicious activity for the 24-hour period after hardening.```

## Security Metrics After Hardening / Security Controls

The following table shows the metrics I measured in our environment for another 24 hours, but after I applied security controls:
Start Time 2024-09-18 00:47
Stop Time	2024-09-19 00:47

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 4931
| Syslog                   | 7
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, I constructed a mini honeynet in Azure and integrated its log sources into a Log Analytics workspace. Microsoft Sentinel was used to trigger alerts and create incidents. Security metrics were measured both in the insecure environment and after implementing security controls. The significant reduction in security events and incidents after hardening demonstrates the effectiveness of the controls.

It's worth noting that if the network resources were heavily utilized by regular users, there might have been more security events in the 24-hour period following the implementation of these controls.

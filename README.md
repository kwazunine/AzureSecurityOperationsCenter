# Building a Security Operations Center (SOC) & Honeynet in Microsoft Azure (Live Traffic)
![Cloud Honeynet / SOC](https://i.imgur.com/QBRoQwa.png?2)

## Introduction

In this project, a mini honeynet is setup in Microsoft Azure, collecting log sources from various resources into a Log Analytics workspace. This workspace is then utilized by Microsoft Sentinel to build attack maps, trigger alerts, and generate incidents. Security metrics were measured in the unsecured environment over a 24-hour period. After implementing security controls to harden the environment, the metrics were remeasured for another 24 hours. The results of these metrics are shown below. The metrics presented include:

- AzureNetworkAnalytics_CL (Malicious Flows allowed into the honeynet)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityEvent (Windows Event Logs)
- SecurityIncident (Incidents created by Sentinel)
- Syslog (Linux Event Logs)

## Architecture Before Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/nqdD7Ud.png)

## Architecture After Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/zTXMFPS.png)

The architecture of the mini honeynet in Azure consists of the following components:

- Azure Key Vault
- Azure Storage Account
- Log Analytics Workspace
- Microsoft Sentinel
- Network Security Group (NSG)
- Virtual Machines (2 Windows, 1 Linux)
- Virtual Network (VNet)

For the "BEFORE" security metrics, all Azure resources were originally deployed, and then exposed to the public internet. The Virtual Machines Network Security Groups and built-in firewalls were configured to be open to all types of traffic, and all other Azure resources were deployed with public endpoints visible to the public internet.

For the "AFTER" security metrics, Network Security Groups were reconfigured by blocking all traffic with the exception of my workstation IP address, and all the other Azure resources were protected by their built-in firewalls including utilizing Azure Private Endpoint.

## Attack Maps Before Hardening / Security Controls
![Linux Syslog Auth Failures](https://i.imgur.com/dlTid3u.png)<br>
![NSG Allowed Inbound Malicious Flows](https://i.imgur.com/RbCHCt5.png)<br>
![Windows RDP/SMB Auth Failures](https://i.imgur.com/KNPEk0Q.png)<br>

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in the insecure environment for 24 hours:<br>
Start Time 10/11/2024 12:23 PM ET<br>
Stop Time 10/12/2024 12:23 PM ET<br>

| Metric                   | Count
| ------------------------ | -----
| AzureNetworkAnalytics_CL | 4472
| SecurityAlert            | 5
| SecurityEvent            | 21058
| SecurityIncident         | 361
| Syslog                   | 8217

## Attack Maps After Hardening / Security Controls
```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table displays the metrics measured in the environment for another 24 hours after security controls were applied:<br>
Start Time 10/19/2024 4:51 PM ET<br>
Stop Time 10/20/2024 4:51 PM ET<br>

| Metric                   | Count
| ------------------------ | -----
| AzureNetworkAnalytics_CL | 0
| SecurityAlert            | 0
| SecurityEvent            | 9163
| SecurityIncident         | 0
| Syslog                   | 7

## Conclusion

In this project, a mini honeynet was built in Microsoft Azure and log sources were ingested into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the logs. Furthermore, security metrics were measured in the insecure environment before applying security controls, and then again after implementing security measures. Notably, the number of security events and incidents significantly decreased after implementing the security controls, highlighting their effectiveness.

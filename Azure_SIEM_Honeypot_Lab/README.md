# Azure Honeypot + SIEM Lab

[![View Report](https://img.shields.io/badge/PDF_Report-View-blue?logo=adobeacrobatreader&style=for-the-badge)](./Azure_Honeypot_SIEM_Lab_Report.pdf)

## Overview

This project documents the planning and deployment of a **Windows honeypot in Microsoft Azure**, with centralized log forwarding to **Microsoft Sentinel**. The goal was to simulate malicious login attempts and visualize them using **KQL**, **GeoIP enrichment**, and **Sentinel workbooks**.

---

## Lab Architecture

- Windows 10 Pro VM (`FIN-SQL-02`) acting as a honeypot
- Microsoft Sentinel + Log Analytics Workspace
- KQL to analyze failed login attempts (Event ID 4625)
- Watchlist-based GeoIP lookups
- Global heatmap + dashboard in Sentinel

[![Lab Diagram](./images/1_Azure_Honeypot_Lab_Diagram.jpg)](./images/1_Azure_Honeypot_Lab_Diagram.jpg)
_Figure 1: Azure Lab Diagram
Visual summary of the honeypot lab setup, showing key Azure components and data flow to Microsoft Sentinel._

---

## Setup Steps

### 1. Azure Environment Setup

Created a new **resource group**, virtual network, and set up the Azure dashboard.

[![Azure Dashboard](./images/2_Fresh_dashboard.png)](./images/2_Fresh_dashboard.png)  
_Figure 2: Azure Dashboard View
Clean Azure portal layout showing the environment before resources are deployed._


[![Resource Group](./images/3_Created_resource_group.png)](./images/3_Created_resource_group.png)  
_Figure 3: Resource Group Creation
Screenshot confirming successful creation of **RG_SOC_Lab** for organizing Azure lab resources._


[![Virtual Network](./images/4_Vnet_deployed.png)](./images/4_Vnet_deployed.png)
_Figure 4: Virtual Network Setup
Configuration view of the virtual network supporting the honeypot infrastructure._


---

### 2. Deploying the Honeypot VM

Created a Windows VM with a finance-sounding name `FIN-SQL-02` and allowed **all inbound traffic** via the NSG. Disabled the Windows firewall.

[![WindowsVM](./images/5_WindowsVM_created.png)](./images/5_WindowsVM_created.png) 
_Figure 5: Windows VM Created
Deployment interface showing the newly created Windows honeypot VM named **FIN-SQL-02**._


[![VM deployed](./images/6_VM_deployed.png)](./images/6_VM_deployed.png)
_Figure 6: VM Deployed Confirmation
Final screen confirming successful deployment of the Windows honeypot VM._


[![NSG Firewall](./images/6_NSG_firewall.png)](./images/6_NSG_firewall.png) 
_Figure 7: NSG Firewall Rule Opened
NSG rule configured to allow all inbound traffic, mimicking an exposed server for honeypot testing._


[![Remote In](./images/8_Remote_in_desktop.png)](./images/8_Remote_in_desktop.png)  
_Figure 8: Remote Desktop Connection to Honeypot
A remote desktop session opened to the honeypot VM for interactive access and configuration._

[![Firewall Off](./images/9_WindowsVM_firewall_off.png)](./images/9_WindowsVM_firewall_off.png)
_Figure 9: Windows Firewall Disabled
Windows Defender firewall is disabled on the honeypot VM to ensure logging visibility._

[![Ping test](./images/10_Pingtest_to_VM.png)](./images/10_Pingtest_to_VM.png)
_Figure 10: Ping Test to VM
Network connectivity tested by sending pings to the honeypot VM, verifying open access._

---

### 3. Simulating Attacks and Viewing Logs

Used RDP to intentionally fail logins. Event Viewer immediately showed Event ID **4625** for failed attempts. Logs showed real brute-force attempts almost immediately.

[![Failed Logins](./images/11_VM_login_test_fail.png)](./images/11_VM_login_test_fail.png)  
_Figure 11: Manual Failed Login Attempt
Failed RDP login attempt using incorrect credentials to simulate brute-force login behavior._

[![Login Fail Alerts](./images/12_VM_longin_test_fail_results.png)](./images/12_VM_longin_test_fail_results.png)
_Figure 12: Failed Login Result in Event Viewer
Event Viewer showing **Event ID 4625**—failed login attempt detected and logged._

---

### 4. Log Forwarding to Sentinel

Created a **Log Analytics Workspace**, connected **Microsoft Sentinel**, and installed the **Azure Monitor Agent**.

[![Log Analytics Workspace](./images/13_Workspace_created.png)](./images/13_Workspace_created.png)  
_Figure 13: Log Analytics Workspace Created
Log Analytics Workspace setup screen used for connecting Microsoft Sentinel._

[![Sentinel Workspace](./images/14_Log_analytics_WS_created.png)](./images/14_Log_analytics_WS_created.png)  
_Figure 14: Sentinel Workspace Connected
Microsoft Sentinel successfully linked to the Log Analytics Workspace._

[![Sentinel Landing](./images/16_Sentinel_landingpage.png)](./images/16_Sentinel_landingpage.png)
_Figure 15: Sentinel Landing Page
Microsoft Sentinel dashboard displaying available setup and monitoring features._

[![Launch Windows Security Events](./images/17_Windows_security_events.png)](./images/17_Windows_security_events.png)
_Figure 16: Launch Windows Security Events Collection
Configuration screen for forwarding Windows security events into Sentinel._

[![Connected Security Evnents](./images/18_Connected_security_events_to_monitor_agent.png)](./images/18_Connected_security_events_to_monitor_agent.png)
_Figure 17: Monitor Agent Security Events Connected
Data collection rule configuration screen showing security event connection to Azure Monitor Agent._

[![Monitor Agent](./images/19_Collection_rule_to_send_to_sentinel.png)](./images/19_Collection_rule_to_send_to_sentinel.png)
_Figure 18: Collection Rule to Forward Logs
Collection rule set to ingest logs into Microsoft Sentinel via Azure Monitor Agent._

[![Monitor Agent](./images/19_Monitor_agent_deployed.png)](./images/19_Monitor_agent_deployed.png)
_Figure 19: Monitor Agent Deployed to VM
Screenshot confirming successful deployment of the Azure Monitor Agent to the honeypot VM._

[![Logs collecting](./images/20_Logs_collecting.png)](./images/20_Logs_collecting.png)
_Figure 20: Logs Actively Collecting
Dashboard showing logs from the honeypot VM are being successfully collected and sent to Sentinel._


---

### 5. Enriching Logs with GeoIP

Uploaded `geoip-summarized.csv` as a **Watchlist** and used the `ipv4_lookup()` function in KQL to identify geographic sources of attacks.

[![Watchlist Upload](./images/24_Sentinel_watchlist_geodata.png)](./images/24_Sentinel_watchlist_geodata.png)
_Figure 21: Sentinel Watchlist Uploaded (GeoIP Data)
Screenshot of the uploaded GeoIP watchlist (**geoip-summarized.csv**) for IP geolocation enrichment._

[![GeoIP Upload](./images/26_GeoIP_data_upload_success.png)](./images/26_GeoIP_data_upload_success.png)  
_Figure 22: GeoIP Data Upload Confirmation
Success message confirming the GeoIP data file was processed and added to Sentinel._

---

### 6. Visualizing the Attacks

Created a **Sentinel Workbook** and global **heatmap** for login attempts.

[![Heatmap](./images/27_HeatMap_generated.png)](./images/27_HeatMap_generated.png) 
_Figure 23: Heatmap Generated from KQL Data
A Sentinel Workbook heatmap visualizing failed login sources by global location after initial deployment._

[![Heatmap](./images/27_HeatMap_after_24hrs.png)](./images/27_HeatMap_after_24hrs.png)  
_Figure 24: Heatmap Results After 24 Hours
Updated heatmap visualization showing a larger dataset of global login attempts after one full day.
_

JSON text for map configuration
```JSON map configuration
{
	"type": 3,
	"content": {
	"version": "KqlItem/1.0",
	"query": "let GeoIPDB_FULL = _GetWatchlist(\"geoip\");\nlet WindowsEvents = SecurityEvent;\nWindowsEvents | where EventID == 4625\n| order by TimeGenerated desc\n| evaluate ipv4_lookup(GeoIPDB_FULL, IpAddress, network)\n| summarize FailureCount = count() by IpAddress, latitude, longitude, cityname, countryname\n| project FailureCount, AttackerIp = IpAddress, latitude, longitude, city = cityname, country = countryname,\nfriendly_location = strcat(cityname, \" (\", countryname, \")\");",
	"size": 3,
	"timeContext": {
		"durationMs": 2592000000
	},
	"queryType": 0,
	"resourceType": "microsoft.operationalinsights/workspaces",
	"visualization": "map",
	"mapSettings": {
		"locInfo": "LatLong",
		"locInfoColumn": "countryname",
		"latitude": "latitude",
		"longitude": "longitude",
		"sizeSettings": "FailureCount",
		"sizeAggregation": "Sum",
		"opacity": 0.8,
		"labelSettings": "friendly_location",
		"legendMetric": "FailureCount",
		"legendAggregation": "Sum",
		"itemColorSettings": {
		"nodeColorField": "FailureCount",
		"colorAggregation": "Sum",
		"type": "heatmap",
		"heatmapPalette": "greenRed"
		}
	}
	},
	"name": "query - 0"
}
```

---

### 7. Target Username Analysis

Queried the top usernames targeted and location by attackers using KQL.

[![Username Query](./images/29_Query_top_username_attempts.png)](./images/29_Query_top_username_attempts.png)
_Figure 25: Query of Top Targeted Usernames
KQL results showing the most common usernames used by attackers (e.g., admin, user, test)._

```kql
SecurityEvent
| where EventID == 4625
| summarize FailedLoginCount = count() by TargetUserName
| top 20 by FailedLoginCount desc
```

[![GeoMap](./images/28_Query_top_country_attacks.png)](./images/28_Query_top_country_attacks.png)
_Figure 26: Query of Top Attacking Countries
KQL results visualized with geographic enrichment to highlight the top IP sources by country._

```kql
let GeoIPDB_FULL = _GetWatchlist("geoip");
SecurityEvent
| where EventID == 4625
| summarize FailedLoginCount = count() by IpAddress
| top 10 by FailedLoginCount desc
| evaluate ipv4_lookup(GeoIPDB_FULL, IpAddress, network)
| project IpAddress, cityname, countryname, latitude, longitude, FailedLoginCount
```

---

## Final Testing

- Confirmed successful log ingestion to Sentinel  
- Real-world attackers were actively probing within **minutes**  
- Visualizations and heatmaps provided valuable SOC insight  
- Honeypot operated safely in isolated test environment  

---

## Summary

This lab was a deep-dive into:
- Honeypot deployment
- Cloud-based threat visibility
- KQL-based log analysis
- SOC-level visualization using Microsoft Sentinel

It provided practical blue team experience and reaffirmed the importance of log centralization and global attack visibility.

[![View Report](https://img.shields.io/badge/PDF_Report-View-blue?logo=adobeacrobatreader&style=for-the-badge)](./Azure_Honeypot_SIEM_Lab_Report.pdf)

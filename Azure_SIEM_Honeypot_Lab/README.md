# Azure Honeypot SIEM Lab

[![View PDF Report](https://img.shields.io/badge/PDF_Report-View-blue?logo=adobeacrobatreader&style=for-the-badge)](./Azure_Honeypot_SIEM_Lab_Report.pdf)

---

## 🧭 Overview

This project documents the setup of a honeypot in Microsoft Azure, with real-time log forwarding to Microsoft Sentinel. It explores the detection of brute-force attacks using KQL, geo-IP enrichment, and heatmap visualization to identify attacker origins and behavior.

---

## ⚙️ Step 1: Azure Environment Setup

### Fresh Azure Dashboard  
[![Fresh Azure Dashboard](./images/2_Fresh_dashboard.png)](./images/2_Fresh_dashboard.png)

### Created Resource Group  
[![Resource Group Created](./images/3_Created_resource_group.png)](./images/3_Created_resource_group.png)

### VNet Created  
[![Virtual Network Created](./images/4_Vnet_deployed.png)](./images/4_Vnet_deployed.png)

---

## 🖥️ Step 2: Deploying the Honeypot VM

### Windows VM Deployed  
[![Windows VM Deployed](./images/5_WindowsVM_created.png)](./images/5_WindowsVM_created.png)

### NSG Firewall Rule Opened  
[![Inbound NSG Rule Changed](./images/7_NSG_inboundrules.png)](./images/7_NSG_inboundrules.png)

### Windows Firewall Disabled  
[![Firewall Disabled in Windows](./images/9_WindowsVM_firewall_off.png)](./images/9_WindowsVM_firewall_off.png)

### Remote Desktop into VM  
[![Remote Desktop Connection](./images/8_Remote_in_desktop.png)](./images/8_Remote_in_desktop.png)

---

## 🛡️ Step 3: Simulating Attacks and Observing Logs

### Simulated Login Failures  
[![Login Failure Test](./images/12_VM_login_test_fail_result.png)](./images/12_VM_login_test_fail_result.png)

### Logs Capturing Real-World Brute Force  
[![Event Viewer Showing 4625 Events](./images/23_eventID_4625_filtered.png)](./images/23_eventID_4625_filtered.png)

---

## 📊 Step 4: Log Forwarding to Microsoft Sentinel

### Log Analytics Workspace Created  
[![Log Analytics Workspace](./images/13_Workspace_created.png)](./images/13_Workspace_created.png)

### Microsoft Sentinel Added  
[![Sentinel Workspace Activated](./images/16_Sentinel_landingpage.png)](./images/16_Sentinel_landingpage.png)

### Azure Monitor Agent Deployed  
[![Agent Deployment Verified](./images/19_Monitor_agent_deployed.png)](./images/19_Monitor_agent_deployed.png)

### Security Event Data Visible  
[![Security Events Streamed](./images/17_Windows_security_events.png)](./images/17_Windows_security_events.png)

---

## 🌍 Step 5: Enriching Logs with GeoIP Data

### GeoIP CSV Uploaded as Watchlist  
[![GeoIP File Uploaded](./images/25_GeoIP_data_file_uploaded_successfully.png)](./images/25_GeoIP_data_file_uploaded_successfully.png)

### Enrichment Query Run with KQL  
[![KQL Query Result](./images/24_KQL_Queries_ran.png)](./images/24_KQL_Queries_ran.png)

---

## 🗺️ Step 6: Visualizing Attacks on Heatmap

### Heatmap Display of Attacker Origins  
[![Heatmap After 24 Hours](./images/27_HeatMap_after_24hrs.png)](./images/27_HeatMap_after_24hrs.png)

---

## 🧑‍💻 Step 7: Most Common Usernames Attacked

### Top 20 Targeted Usernames  
[![Top Username Query](./images/29_Query_top_username_attempts.png)](./images/29_Query_top_username_attempts.png)

---

## ✅ Summary

Setting up this honeypot gave me hands-on experience in log collection, analysis, and visualization using Microsoft Sentinel. The lab clearly demonstrated how fast a vulnerable VM can be discovered and targeted. It reinforced the importance of basic security practices like closing ports and firewall hardening—and the power of modern SIEM tools.

This project also helped sharpen my skills in:
- 🛠️ Azure Virtual Machines & Networking
- 🛡️ Microsoft Sentinel and Log Analytics
- 🔎 KQL (Kusto Query Language)
- 🌐 GeoIP enrichment & Watchlists
- 📈 Visual threat tracking with Workbooks

---

[![View PDF Report](https://img.shields.io/badge/PDF_Report-View-blue?logo=adobeacrobatreader&style=for-the-badge)](./Azure_Honeypot_SIEM_Lab_Report.pdf)

---


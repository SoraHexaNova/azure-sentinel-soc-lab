# Azure Honeypot & SIEM Threat Analysis

## 🎯 Project Overview
Deployed a cloud-based honeypot environment on Microsoft Azure to capture, ingest, and analyze real-world brute-force SSH attacks. This project demonstrates the capability to monitor security threats, parse raw log data, and visualize attack origins using Microsoft Sentinel and Kusto Query Language (KQL).

## 🛠️ Architecture
- **Infrastructure:** Azure Virtual Machine (Ubuntu OS) exposed to the public internet as a honeypot.
- **Log Management:** Azure Log Analytics Workspace for centralized log storage.
- **SIEM:** Microsoft Sentinel for threat detection and visualization.
- **Visualization:** Custom Azure Workbook Map plotting attack telemetry in real-time.

##Architecture diagram
- I put together this architecture diagram to show how all the pieces of the lab actually talk to each other. It maps out the full journey of an attack—starting from a random bot hitting the public-facing honeypot, to getting parsed in Log Analytics, and finally showing up as a live plot on the map.
<img width="1696" height="927" alt="architecture diagram" src="https://github.com/user-attachments/assets/1f90e8ad-0853-4a87-981e-f32279033603" />


## 🔑 Key Skills Used
- **Cloud Security:** Hardening and monitoring virtual machine telemetry.
- **Log Analysis:** Querying and parsing unstructured SSH syslog data.
- **Kusto Query Language (KQL):** Creating complex queries for geolocation mapping and threat aggregation.
- **Visualization:** Building interactive dashboards to present security insights.

## 📈 Visualizing Attacks
Below is the attack map generated from the honeypot data. The map aggregates "Failed password" and "Invalid user" attempts, geolocating attacker IPs to identify global attack patterns.

<img width="1486" height="520" alt="image" src="https://github.com/user-attachments/assets/0111f3f7-bf28-458e-9f1d-80c32358f3db" />



## 🛠️ Technical Challenges & Solutions

* **Resource Constraints & OS Selection:** * The lab tutorials I referenced utilized Windows-based honeypots. However, due to Azure Free Tier resource limitations on lightweight VMs, I pivoted to a Linux-based environment.
    * **Strategic Pivot:** I deployed an Ubuntu Pro instance. While this required deviating from the tutorial's Windows-based steps, it provided a valuable opportunity to learn the differences between **RDP** (Windows Remote Desktop Protocol) and **SSH** (Secure Shell) authentication telemetry.
* **Log Ingestion & Parsing:** * Moving to Ubuntu meant I could not rely on Windows Event Logs. I had to identify the relevant Linux auth logs, define new log ingestion rules in the Azure Monitor Agent, and utilize Regex in KQL to parse raw, unstructured SSH syslog data.
* **Data Integration:** Initial raw SSH logs required complex extraction using Regex in KQL to isolate attacker IP addresses from unstructured text.
* **UI/UX Debugging:** Encountered a persistent bug where the Map widget's UI dropdowns failed to populate and threw a `locInfo` validation error.
* **Code-Level Resolution:** Bypassed the broken UI by directly modifying the Workbook's JSON code in the **Advanced Editor**. Explicitly defined `mapSettings` to bind `LatLong` data and `FailureCount` metrics, ensuring the map successfully rendered geographic clusters.

## ⚠️ Security Disclaimer
This project was conducted in a controlled lab environment. The virtual machine was intentionally left vulnerable to capture attack data and should never be exposed to the internet in a production environment.

## TODO
- Implement automated alerts to trigger notifications upon high-volume brute-force attempts.
- Integrate Azure Network Watcher to analyze incoming traffic flow logs for deeper network threat intelligence.
- SOAR Automation Playbooks
- Threat Intelligence Feeds
- MITRE ATT&CK Mapping
- Automated Incident Response

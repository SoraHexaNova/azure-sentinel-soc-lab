# Azure Honeypot & SIEM Threat Analysis

## 🎯 Project Overview
Deployed a cloud-based honeypot environment on Microsoft Azure to capture, ingest, and analyze real-world brute-force SSH attacks. This project demonstrates the capability to monitor security threats, parse raw log data, and visualize attack origins using Microsoft Sentinel and Kusto Query Language (KQL).

## 🛠️ Architecture
- **Infrastructure:** Azure Virtual Machine (Ubuntu OS) exposed to the public internet as a honeypot.
- **Log Management:** Azure Log Analytics Workspace for centralized log storage.
- **SIEM:** Microsoft Sentinel for threat detection and visualization.
- **Visualization:** Custom Azure Workbook Map plotting attack telemetry in real-time.

## 🔑 Key Skills Used
- **Cloud Security:** Hardening and monitoring virtual machine telemetry.
- **Log Analysis:** Querying and parsing unstructured SSH syslog data.
- **Kusto Query Language (KQL):** Creating complex queries for geolocation mapping and threat aggregation.
- **Visualization:** Building interactive dashboards to present security insights.

## 📈 Visualizing Attacks
Below is the attack map generated from the honeypot data. The map aggregates "Failed password" and "Invalid user" attempts, geolocating attacker IPs to identify global attack patterns.

![Insert your map screenshot here]

## 🛠️ Technical Challenges & Solutions
* **Data Integration:** Initial raw SSH logs required complex extraction using Regex in KQL to isolate attacker IP addresses from unstructured text.
* **UI/UX Debugging:** Encountered a persistent bug where the Map widget's UI dropdowns failed to populate and threw a `locInfo` validation error.
* **Code-Level Resolution:** Bypassed the broken UI by directly modifying the Workbook's JSON code in the **Advanced Editor**. Explicitly defined `mapSettings` to bind `LatLong` data and `FailureCount` metrics, ensuring the map successfully rendered geographic clusters.

## ⚠️ Security Disclaimer
This project was conducted in a controlled lab environment. The virtual machine was intentionally left vulnerable to capture attack data and should never be exposed to the internet in a production environment.

## TODO
- Implement automated alerts to trigger notifications upon high-volume brute-force attempts.
- Integrate Azure Network Watcher to analyze incoming traffic flow logs for deeper network threat intelligence.

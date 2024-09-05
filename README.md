# SOC-Automation-Lab
## Overview
The SOC Automation Lab is a project that integrates various security tools to automate incident detection, alerting, and response workflows. The setup utilizes the following tools:

- **Wazuh**: SIEM and XDR capabilities for monitoring and alert generation.
- **TheHive**: Case management platform for tracking incidents and responses.
- **Shuffle**: SOAR (Security Orchestration, Automation, and Response) platform to automate workflows and manage alerts.

The project automates the detection of suspicious activity (e.g., Mimikatz alerts) and sends these alerts to TheHive, notifies SOC analysts via email, and performs automatic response actions.

## Components
1. **Virtual Machine**: Running a Windows 10 ISO image with Wazuh and TheHive installed.
2. **Wazuh**: Responsible for monitoring logs, detecting threats, and generating alerts.
3. **TheHive**: Case management tool where alerts are sent for investigation.
4. **Shuffle**: SOAR platform used to automate alert processing and response actions.

## Objectives
- Automate the detection of suspicious behavior such as Mimikatz activity.
- Automatically create cases in TheHive for SOC analysts to investigate.
- Notify analysts via email for each case created.
- Enable automatic responsive actions, such as blocking malicious IPs or investigating further using VirusTotal.

## Workflow
1. **Mimikatz Alert Sent to Shuffle**: Upon detection of a Mimikatz alert, Wazuh sends the alert to Shuffle.
2. **Shuffle Receives Alert**: Shuffle processes the alert, extracts the SHA256 hash from the file, and performs additional actions.
3. **Check Reputation with VirusTotal**: The SHA256 hash is checked against VirusTotal to assess reputation.
4. **Alert Creation in TheHive**: If deemed suspicious, details are sent to TheHive, creating an alert for investigation.
5. **Email Notification**: An email notification is automatically sent to the SOC analyst with details of the alert.
6. **Optional Response**: Analysts can confirm or take additional actions such as blocking IP addresses.

## Setup
### 1. TheHive and Wazuh Configuration
The setup includes configuring firewalls in Wazuh and setting up connections between Wazuh and TheHive.

*Note*: Ensure that appropriate firewall settings are in place since the Cloud IP (Digital Ocean) will be public. The setup requires watching a step-by-step video tutorial for configuring Wazuh alerts and rules.

### 2. Mimikatz and Wazuh Alerts
Instructions for setting up Mimikatz alerts in Wazuh involve creating detection rules. A link for downloading Mimikatz is provided, but changes may be needed in Windows or Chrome's downloading settings for security purposes.

### 3. Shuffle (SOAR) Setup
- Install and configure Shuffle for alert automation.
- Build a workflow to automate the steps outlined in the workflow section (e.g., sending alerts to TheHive, checking VirusTotal, sending email notifications).

## Example Scenario
### Alert:
- **Suspicious Process**: Rundll32.exe
- **Activity**: Outbound Connection
### Triage:
- Investigate surrounding events and logs.
- Identify if the connection is to a suspicious domain.
### Research:
- Confirm if the activity is part of a widespread campaign or targeted attack.

## Response Demo
1. Create a low-spec Ubuntu machine (1GB RAM, 25GB HDD) and allow inbound traffic.
2. Install Wazuh agent on Ubuntu to monitor SSH brute force activity.
3. Push all high-severity (Level 5) alerts to Shuffle.
4. Enrich IP information using VirusTotal.
5. Send alert details via email to the user, asking for confirmation to block the IP.
6. Create an alert in TheHive for SOC team to investigate.
7. Automatically block the IP if the user confirms it is malicious.

## Additional Tools
- **Public.sqrx.com**: Use this service to safely simulate the behavior of malicious websites or files without risking your environment.

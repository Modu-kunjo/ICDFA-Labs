# SOC Lab: Introduction to Wazuh for Threat Detection & Monitoring

![Platform](https://img.shields.io/badge/Platform-Wazuh-blue)
![Focus](https://img.shields.io/badge/Focus-SOC%20%7C%20SIEM-orange)
![Technique](https://img.shields.io/badge/Technique-File%20Integrity%20Monitoring-green)
![Environment](https://img.shields.io/badge/Environment-VirtualBox%20%7C%20Windows-lightgrey)

## Overview

This lab explores the deployment and use of Wazuh for centralized security monitoring, endpoint visibility, and File Integrity Monitoring (FIM).

The scenario simulates a Level 1 Security Operations Center (SOC) analyst investigating potentially unauthorized changes to sensitive files on a Windows endpoint.

The objective is to establish a Wazuh monitoring environment, connect a Windows agent, monitor a designated directory, and investigate the resulting security events.

**Course:** Security Operations Center (SOC)  
**Module:** SIEM & Endpoint Monitoring Fundamentals  
**Instructor:** Aminu Idris, AMCPN


## Objectives

- Deploy Wazuh on an Ubuntu Server virtual machine.
- Access the Wazuh Dashboard.
- Install and register a Windows endpoint agent.
- Configure File Integrity Monitoring for a dedicated test directory.
- Generate controlled file creation, modification, and deletion events.
- Investigate alerts and interpret their relevant fields.
- Document troubleshooting, evidence, and lessons learned.

## Lab Architecture

| Component | Role |
|---|---|
| Ubuntu Server VM | Hosts Wazuh Manager, Indexer, and Dashboard in the all-in-one lab deployment |
| Windows host | Runs the Wazuh Agent and generates test events |
| VirtualBox | Provides the Ubuntu virtual machine |
| Bridged networking | Allows the VM and Windows host to communicate over the network |

## Prerequisites

- VirtualBox and an Ubuntu Server installation.
- Administrative access to the Windows host.
- Internet access for downloading installation packages.
- Network connectivity between Ubuntu and Windows.
- Sufficient resources for the Wazuh components.
- A dedicated directory for safe FIM testing.

## Tools and Technologies

- Wazuh
- Ubuntu Server
- Windows
- VirtualBox
- Windows Services
- Command-line utilities
- Security event analysis
- File Integrity Monitoring (FIM)

## Implementation Workflow

### 1. Deploy Wazuh

Add the official Wazuh package signing key and download the installation script specified in the lab guide.

```bash
curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH \
  | sudo gpg --dearmor \
  -o /usr/share/keyrings/wazuh-archive-keyring.gpg

curl -sO https://packages.wazuh.com/4.12/wazuh-install.sh
sudo bash ./wazuh-install.sh -a -i
```

The `-a` option requests an all-in-one installation. Follow the installer prompts and consult the documentation for the selected Wazuh version.

Check the manager service:

```bash
sudo systemctl status wazuh-manager
```

### 2. Access the Dashboard

Determine the Ubuntu VM's IP address:

```bash
ip addr show
```

Open:

`https://<UBUNTU_VM_IP_ADDRESS>`

Use the credentials provided by the installer. A self-signed certificate may trigger a browser warning in a controlled lab. Do not bypass certificate warnings on untrusted systems.

### 3. Install and Register the Windows Agent

Install the Windows Agent MSI package from the official Wazuh repository.

On Ubuntu, launch the agent management utility:

```bash
sudo /var/ossec/bin/manage_agents
```

Use its interactive menu to add the endpoint and extract its registration key. Apply the key and manager address using the Windows agent management interface.

Verify the agent's actual status in the Wazuh Dashboard.

**Agent status:** `[Active]`

### 4. Configure File Integrity Monitoring

Create a dedicated test directory, such as:

`C:\Users\<YourWindowsUsername>\SensitiveFiles`

Edit the agent configuration file:

`C:\Program Files (x86)\ossec-agent\ossec.conf`

Add the monitored directory inside the existing `<syscheck>` section:

```xml
<directories realtime="yes">C:\Users\<YourWindowsUsername>\SensitiveFiles</directories>
```

Replace the placeholder with your actual path. Avoid adding a second conflicting `<syscheck>` section. Save the configuration and restart the Windows agent.

### 5. Generate Test Events

In the dedicated test directory:

1. Create `secret_plan.txt`.
2. Add text and save it.
3. Modify the file and save it again.
4. Delete the file.

These actions provide controlled test cases for FIM.

### 6. Investigate Alerts

Search the Wazuh Dashboard for relevant file integrity events. Where supported, filter by the `syscheck` rule group.

Inspect the available fields, including:

- Event timestamp.
- Agent name.
- File path.
- Event description and action.
- Rule ID and severity.
- File size and checksum details, where available.

Record the observed results rather than assuming every expected alert was generated.

## Results

| Validation | Status |
|---|---|
| Wazuh installation | `[Documented]` |
| Dashboard access | `[Documented]` |
| Windows agent registration | `[Documented]` |
| FIM configuration | `[Documented]` |
| File creation detection | `[Documented]` |
| File modification detection | `[Documented]` |
| File deletion detection | `[Documented]` |


## Troubleshooting Notes

If the agent does not connect, investigate:

- Whether the Wazuh manager and its required components are healthy.
- Whether the configured manager IP is correct.
- Whether the agent service is running.
- Whether network routing and the required firewall ports allow communication.
- Whether the agent registration and authentication configuration are correct.
- Whether the manager and agent logs contain relevant errors.

If FIM alerts do not appear, check:

- Whether the monitored path exists and is correctly configured.
- Whether the configuration was saved and the agent restarted.
- Whether the agent is connected and reporting events.
- Whether the dashboard time range and filters include the test events.
- Whether the relevant FIM configuration and event-processing components are functioning.


## Evidence and Documentation

Suggested evidence structure:

```text
wazuh-threat-detection-lab/
├── README.md
├── Lab-Report.md
└── evidence/
    ├── 01-wazuh-service-status.png
    ├── 02-dashboard-access.png
    ├── 03-agent-status.png
    ├── 04-fim-configuration.png
    ├── 05-file-created-alert.png
    ├── 06-file-modified-alert.png
    └── 07-file-deleted-alert.png
```

---

**Author:** `[Muhammad Modu Kunjo]`  
**Lab status:** `[Completed]`  
**Last updated:** `[2026-10-20]`

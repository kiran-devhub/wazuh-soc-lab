# Wazuh SOC Monitoring Lab

A hands-on Security Operations Center (SOC) home lab built with Wazuh, Ubuntu Linux endpoints, and Kali Linux.

The project demonstrates endpoint monitoring, security event detection, file integrity monitoring, process investigation, custom detection rules, alert investigation, and incident documentation.

---

## Project Overview

This lab simulates a small SOC environment where security events are generated on an endpoint, collected by the Wazuh agent, analyzed by the Wazuh manager, and investigated through the Wazuh dashboard.

The project focuses on practical SOC workflows rather than only installation and configuration.

---

## Lab Architecture

```text
                    Kali Linux
                       |
                       |
                SSH / Administration
                       |
                       v
              +-------------------+
              |   SOC-Endpoint    |
              | Ubuntu Server     |
              | 192.168.56.102    |
              | Wazuh Agent       |
              +---------+---------+
                        |
                        | Wazuh Agent
                        | Private Network
                        |
                        v
              +-------------------+
              |   Wazuh Server    |
              | Ubuntu Server     |
              | 192.168.56.10     |
              |                   |
              | Wazuh Manager     |
              | Wazuh Indexer     |
              | Wazuh Dashboard   |
              | Filebeat          |
              +-------------------+
```

---

## Technologies

- Wazuh 4.14.8
- Ubuntu Server 24.04.5 LTS
- Kali Linux
- VirtualBox
- Wazuh Agent
- Wazuh Manager
- Wazuh Indexer
- Wazuh Dashboard
- Filebeat
- Linux journald
- SSH
- Bash

---

## Lab Components

| Component | Role | IP Address |
|---|---|---|
| Wazuh Server | SIEM / Manager | 192.168.56.10 |
| SOC-Endpoint | Monitored endpoint | 192.168.56.102 |
| Kali Linux | Administration / testing | Host system |

---

## Completed SOC Activities

### 1. Wazuh Deployment

Deployed an all-in-one Wazuh server containing:

- Wazuh Manager
- Wazuh Indexer
- Wazuh Dashboard
- Filebeat

### 2. Endpoint Monitoring

Installed and enrolled the Wazuh agent on the Ubuntu endpoint.

The endpoint successfully connected to the Wazuh manager.

### 3. SSH Authentication Monitoring

Generated controlled failed and successful SSH authentication events.

Investigated authentication alerts and identified the source IP, username, and associated Wazuh rule.

### 4. File Integrity Monitoring

Tested the Wazuh File Integrity Monitoring capability using a controlled test file.

The test demonstrated:

```text
File Creation
     ↓
File Modification
     ↓
File Deletion
```

Wazuh detected the corresponding file system changes.

### 5. Process Investigation

Investigated running Linux processes and Wazuh processes using Linux process-management tools.

Examples included:

```bash
ps
pstree
/proc
readlink
```

The investigation identified legitimate Wazuh processes and their process relationships.

### 6. Syscollector Process Inventory

Used Wazuh IT Hygiene process inventory to investigate endpoint process information.

The endpoint reported process information including:

- Process name
- Process ID
- Parent process ID
- Command line
- Process start time

### 7. Custom Detection Rule

Created a custom Wazuh detection rule:

```xml
<rule id="100100" level="10">
  <match>SOC_LAB_TEST</match>
  <description>SOC Lab: Controlled test event detected on the endpoint.</description>
  <group>soc_lab,custom_detection,</group>
</rule>
```

### 8. Controlled Detection Test

Generated a controlled event on the endpoint:

```bash
logger -t soc-lab "SOC_LAB_TEST controlled detection event"
```

The event was collected from journald and generated Wazuh rule 100100.

The alert was successfully investigated in the Wazuh Threat Hunting dashboard.

---

## Custom Detection Workflow

The completed detection pipeline:

```text
SOC-Endpoint
     |
     v
Linux journald
     |
     v
Wazuh Agent
     |
     v
Wazuh Manager
     |
     v
Custom Rule 100100
     |
     v
Wazuh Alert
     |
     v
Threat Hunting Dashboard
     |
     v
SOC Investigation
```

---

## Detection Evidence

The custom detection generated:

- Agent: SOC-Endpoint
- Agent ID: 001
- Agent IP: 192.168.56.102
- Log source: journald
- Program: soc-lab
- Rule ID: 100100
- Rule level: 10
- Detection: SOC Lab: Controlled test event detected on the endpoint

---

## Incident Response

The custom detection was treated as an authorized laboratory event.

Investigation confirmed:

- The event originated from the controlled SOC lab.
- The event was intentionally generated.
- Wazuh successfully collected the event.
- The custom rule matched the event.
- The resulting alert was visible in the dashboard.
- No malicious activity occurred.

Detailed documentation is available in:

```text
reports/custom-detection-incident.md
```

---

## Project Structure

```text
wazuh-soc-lab/
│
├── README.md
│
├── configs/
│
├── docs/
│
├── reports/
│   └── custom-detection-incident.md
│
├── rules/
│   └── local_rules.xml
│
└── screenshots/
```

---

## Skills Demonstrated

- SIEM deployment
- Linux administration
- Wazuh configuration
- Endpoint monitoring
- Log analysis
- SSH authentication monitoring
- File Integrity Monitoring
- Process investigation
- Security event investigation
- Custom detection engineering
- Wazuh rule creation
- Alert validation
- Threat hunting
- Incident documentation
- SOC investigation workflow

---

## Future Improvements

Planned improvements for the lab include:

- Additional custom detection rules
- Authentication attack detection
- Threat hunting exercises
- Controlled incident simulation
- Incident response playbooks
- Dashboard screenshots and visualizations
- Additional endpoint telemetry
- GitHub documentation improvements
- SOC investigation case studies

---

## Disclaimer

This project is an authorized cybersecurity laboratory environment.

All testing was performed on systems owned or controlled for educational and defensive security purposes.

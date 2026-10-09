# Incident Report: Custom Wazuh Detection

## 1. Incident Summary

A controlled security event was generated on the SOC-Endpoint to validate a custom Wazuh detection rule.

The event contained the test identifier:

SOC_LAB_TEST

Wazuh successfully collected the event through journald and generated an alert using custom rule 100100.

## 2. Environment

- SIEM: Wazuh 4.14.8
- Manager: Wazuh-Server
- Endpoint: SOC-Endpoint
- Endpoint IP: 192.168.56.102
- Log source: journald
- Detection rule: 100100
- Rule level: 10

## 3. Detection

Custom rule:

```xml
<rule id="100100" level="10">
  <match>SOC_LAB_TEST</match>
  <description>SOC Lab: Controlled test event detected on the endpoint.</description>
  <group>soc_lab,custom_detection,</group>
</rule>
```

## 4. Event

The controlled event was generated with:

```bash
logger -t soc-lab "SOC_LAB_TEST controlled detection event"
```

The endpoint journal confirmed the event.

## 5. Alert Evidence

Wazuh generated the following alert:

- Rule ID: 100100
- Rule level: 10
- Agent: SOC-Endpoint
- Agent ID: 001
- Agent IP: 192.168.56.102
- Log location: journald
- Program: soc-lab
- Manager: Wazuh-Server
- Alert description: SOC Lab: Controlled test event detected on the endpoint.

The alert was successfully recorded in the Wazuh alert database and was visible in the Threat Hunting dashboard.

## 6. Investigation

The alert was investigated using the Wazuh Threat Hunting dashboard.

The event was located by searching for:

SOC_LAB_TEST

The search returned one matching event from SOC-Endpoint.

The alert details confirmed that the event originated from the SOC-Endpoint and was detected by custom rule 100100.

## 7. Response

This was an authorized and controlled laboratory test event.

No malicious activity occurred.

The event was generated intentionally to validate the custom detection rule and the Wazuh monitoring pipeline.

The investigation confirmed that the endpoint event was successfully collected, processed by Wazuh, matched against the custom rule, and converted into a security alert.

## 8. Conclusion

The custom Wazuh detection was successfully validated from event generation through alert creation and dashboard investigation.

The test demonstrated the following SOC detection workflow:

Endpoint
→ Log Collection
→ Wazuh Manager
→ Custom Detection Rule
→ Security Alert
→ Dashboard Investigation

The successful alert confirms that the custom detection capability is operational in the SOC lab.

# MITRE ATT&CK Mapping

This investigation was mapped to relevant MITRE ATT&CK techniques based on observed endpoint activity.

## T1204.002 — User Execution: Malicious File

**Observed behavior:**
The executable `ckjg.exe` was downloaded to the user's Downloads directory and subsequently executed.

**Evidence:**
`01-suspicious-executable.png`

**Relevance:**
The activity is consistent with a user executing a potentially malicious file obtained from an external source.

---

## T1547.001 — Registry Run Keys / Startup Folder

**Observed behavior:**
`ckjg.exe` created:

`C:\Users\sarah.miller\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup\DeleteApp.url`

**Evidence:**
`02-persistence.png`

**Relevance:**
The Windows Startup folder can be used to establish persistence across user logons.

---

## T1047 — Windows Management Instrumentation

**Observed behavior:**
The investigation identified execution of:

`wmic computersystem get domain`

**Relevance:**
The command uses Windows Management Instrumentation (WMI) to query information from the host.

---

## T1082 — System Information Discovery

**Observed behavior:**
The malware-associated activity included a system information query using:

`wmic computersystem get domain`

**Relevance:**
The command retrieves information about the Windows system's domain membership.

---

## Network / Command-and-Control Activity

**Observed behavior:**
`ckjg.exe` established an outbound TCP connection to:

`193.46.217.4:7777`

The executable also queried:

`hkfasfsafg.click`

which resolved to the same IP address.

**Evidence:**
`03-c2-connection.png`

**Analyst note:**
The available telemetry establishes suspicious external communication and correlation between the DNS query and network connection. The specific application-layer C2 protocol should not be assumed without additional evidence.

---

## Summary

| Observed Activity                   | ATT&CK Technique                               |
| ----------------------------------- | ---------------------------------------------- |
| User executes downloaded executable | T1204.002 — User Execution: Malicious File     |
| Startup folder file creation        | T1547.001 — Registry Run Keys / Startup Folder |
| WMI command execution               | T1047 — Windows Management Instrumentation     |
| Domain/system information query     | T1082 — System Information Discovery           |
| External network communication      | Investigated as potential C2 activity          |

## Analyst Takeaway

Mapping observed behavior to MITRE ATT&CK provides a standardized way to describe adversary techniques and helps analysts communicate findings consistently during incident response.

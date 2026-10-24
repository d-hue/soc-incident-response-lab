# SOC Incident Response Lab

## Overview

This project documents a hands-on Security Operations Center (SOC) investigation performed in a simulated Windows environment using Sysmon and Windows Event Viewer.

The investigation focused on identifying suspicious process execution, persistence mechanisms, DNS activity, network connections, and potential command-and-control (C2) communication.

## Investigation Scenario

A Windows workstation used by a simulated employee, Sarah Miller, was investigated after suspicious activity was identified.

The investigation revealed a potentially malicious executable named `ckjg.exe` that was downloaded to the user's Downloads directory and subsequently executed.

The investigation reconstructed the activity using Windows Sysmon telemetry.

## Tools & Technologies

- Windows Event Viewer
- Sysmon
- Windows Event Logs
- TryHackMe
- MITRE ATT&CK
- DNS analysis
- Network connection analysis
- Incident response methodology

## Key Findings

### 1. Suspicious Executable

The executable `ckjg.exe` was executed from:

`C:\Users\sarah.miller\Downloads\ckjg.exe`

### 2. Potential Persistence

The executable created:

`C:\Users\sarah.miller\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup\DeleteApp.url`

This activity was investigated as a potential persistence mechanism.

### 3. Suspicious DNS Activity

The executable queried:

`hkfasfsafg.click`

The domain resolved to:

`193.46.217.4`

### 4. Command-and-Control Communication

The executable established an outbound TCP connection to:

`193.46.217.4:7777`

### 5. Initial Download Source

Sysmon telemetry identified the originating download URL as:

`http://gettsveriff.com/bgj3/ckjg.exe`

## Investigation Timeline

| Time | Activity |
|---|---|
| 4:07:38 PM | `ckjg.exe` downloaded |
| 4:08:43 PM | `ckjg.exe` executed |
| 4:08:46 PM | `DeleteApp.url` created in Startup directory |
| 4:08:57 PM | DNS query for `hkfasfsafg.click` |
| 4:08:58 PM | Connection established to `193.46.217.4:7777` |

## Analyst Assessment

The investigation identified a sequence of activity consistent with a potentially malicious execution chain.

The activity included an executable downloaded from an external URL, execution from a user Downloads directory, creation of a file within the Windows Startup directory, DNS resolution to an external domain, and subsequent outbound communication to the resolved IP address.

The findings were correlated across multiple Sysmon event types to reconstruct the activity timeline.

## Skills Demonstrated

- Security event analysis
- Windows endpoint investigation
- Sysmon analysis
- Process investigation
- Persistence identification
- DNS investigation
- Network traffic analysis
- C2 identification
- Timeline reconstruction
- Incident documentation
- Security analyst reasoning

## Disclaimer

This project was completed in a controlled, simulated cybersecurity training environment for educational and portfolio purposes.

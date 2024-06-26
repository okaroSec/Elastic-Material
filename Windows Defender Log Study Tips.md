

---


Windows Defender, now known as Microsoft Defender Antivirus, plays a crucial role in protecting Windows systems from malware and other threats. Analyzing its logs is essential for cybersecurity professionals to monitor, detect, and respond to potential security incidents. In this guide, we’ll explore essential queries and filters to efficiently isolate and analyze specific events within Windows Defender logs.

## Key Queries and Filters

### Isolating Windows Defender Logs

To filter logs specific to Windows Defender, use the following query:

```bash
winlog.provider_name: "Microsoft-Windows-Windows Defender"
```

### Isolating Threats

To find all detected threats within the logs, use this query:

```bash
winlog.event_data.ThreatName: *
```

### Identifying Important Paths

To locate logs mentioning specific file paths, use:

```bash
winlog.event_data.Path: *
```

## Important Event IDs

Certain event IDs in Windows Defender logs are crucial for identifying significant activities. Here are key event IDs to monitor:

- **1117**: Action taken against malware or potentially unwanted software.
- **5000**: Real-time protection enabled.
- **5001**: Real-time protection disabled.
- **5004**: Real-time protection enabled (repeated for emphasis).
- **1116**: Malware detected.
- **1117**: Scheduled scan started (repeated for emphasis).
- **1118**: Scheduled scan completed.
- **1119**: Malware remediation success.
- **1121**: Malware remediation failure.
- **1123**: User-initiated scan.
- **1125**: Malware remediation pending.
- **2001**: Antivirus scanning for malicious software.

## Key Fields for Detailed Analysis

When analyzing Windows Defender logs, pay attention to the following fields for comprehensive insights:

- `winlog.event_data.DetectionUser`: User context in which the threat was detected.
- `winlog.event_data.ActionSuccess`: Success status of actions like removal or quarantine.
- `winlog.event_data.ThreatSeverity`: Severity level of the detected threat.
- `winlog.event_data.RemediationAction`: Action taken by Windows Defender (e.g., quarantine, remove).
- `winlog.event_data.MalwareExecutionState`: State of the malware (e.g., blocked, allowed).

## Queries for Specific Scenarios

### Disabling of Windows Defender

Identify events where real-time protection was disabled:

```bash
winlog.provider_name: "Microsoft-Windows-Windows Defender" and winlog.event_id: "5001"
```

### Finding All Detected Threats

To list all detected threats:

```bash
winlog.provider_name: "Microsoft-Windows-Windows Defender" and winlog.event_data.ThreatName: *
```

### Actions Taken on Threats

To find logs where actions taken against threats were successful:

```bash
winlog.provider_name: "Microsoft-Windows-Windows Defender" and winlog.event_data.ActionSuccess: "true"
```

The hostname where the attacker is coming from.


```bash
winlog.event_data.WorkstationName
```
## Reminders !

- **Event Details**: Always check the message field for detailed information about each event.
- **Timestamp Filtering**: Utilize time filters to narrow down logs to specific periods of interest, enhancing the relevance of your analysis.


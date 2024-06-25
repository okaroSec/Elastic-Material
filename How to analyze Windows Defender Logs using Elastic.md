
## Important Queries and Filters

#### Isolating Windows Defender Logs:

```bash
winlog.provider_name : "Microsoft-Windows-Windows Defender"
```

#### Isolating Threats:

```bash
winlog.event_data.ThreatName : *
```

#### Identifying Important Paths:

```bash
winlog.event_data.Path : *
```

###  Event IDs to Consider:

```bash
event.code
```

- **1117:** The antimalware platform has taken action against malware or potentially unwanted software.
- **5000:** Real-time protection has been enabled.
- **5001:** Real-time protection has been disabled.


### Key Fields to Include in Your Searches:

- **winlog.event_data.DetectionUser:** Identifies the user context in which the threat was detected.
- **winlog.event_data.ActionSuccess:** Indicates whether the action taken (like removal or quarantine) was successful.
- **winlog.event_data.ThreatSeverity:** Provides the severity level of the detected threat.
- **winlog.event_data.RemediationAction:** Describes the action taken by Windows Defender (e.g., quarantine, remove).
- **winlog.event_data.MalwareExecutionState:** Indicates the state of the malware (e.g., blocked, allowed).


### Queries for Specific Scenarios:

** Disabling of Windows Defender

```bash
`winlog.provider_name: "Microsoft-Windows-Windows Defender" and winlog.event_id: "5001"`
```

**To Find All Detected Threats

```bash
winlog.provider_name : "Microsoft-Windows-Windows Defender" and winlog.event_data.ThreatName : *
```

**To Find Actions Taken On Threats

```bash
winlog.provider_name : "Microsoft-Windows-Windows Defender" and winlog.event_data.ActionSuccess : "true"

```

**Extra Reminder To Self

- **Event Details:** Always check the `message` field for detailed information about each event.

- **Timestamp Filtering:** Use time filters to narrow down to specific periods of interest


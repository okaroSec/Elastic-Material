
---

# Sysmon (System Monitor) for Threat Detection

Sysmon, also known as Microsoft System Monitor, is a powerful Windows system service and device driver. It remains persistent across reboots to monitor and log system activity in the Windows event log. Sysmon provides comprehensive details about process creations, network connections, and file changes, making it an invaluable tool for advanced threat detection and forensic investigations.

## When to Use Sysmon for Threat Detection

1. **Trace Command Execution Paths and Process Interactions:** Gain a detailed view of how an attack unfolded by tracing command execution paths and interactions between processes.
    
2. **Identify Suspicious Activities:** Detect potential breaches or attempts to compromise the system by identifying suspicious activities.
    
3. **Root Cause Analysis:** Perform detailed root cause analysis using Sysmon’s detailed logging capabilities to understand the nature of the attack and improve security measures.
    

## Important Sysmon Event Types

1. **Event ID 1: Process Creation**
    
    - Tracks when a process starts, including the command line that initiated the process. This is critical for identifying malicious processes or commands used by attackers.
2. **Event ID 3: Network Connection**
    
    - Monitors attempts to connect to a remote host, which is pivotal in detecting data exfiltration attempts or command and control (C&C) communication.
3. **Event ID 7: Image Loaded**
    
    - Logs when a DLL is loaded into a process, useful for detecting the use of malicious payloads or code injection techniques.

## Key Queries

### Check for Suspicious Web Downloads via Command Line

To identify suspicious web downloads initiated from the command line:

```bash
winlog.provider_name: "Microsoft-Windows-Sysmon" and winlog.event_data.CommandLine: *http*
```

### Root Cause of Alerts

- `winlog.event_data.User`: Provides information about the user account associated with the event.
- `winlog.event_data.CommandLine`: Records the exact command line used to start a process. Analyzing this can help identify malicious scripts, executables, or commands. For example, to detect the use of `cmd.exe`:

```bash
winlog.provider_name: "Microsoft-Windows-Sysmon" and winlog.event_id: "1" and winlog.event_data.CommandLine: *cmd.exe*
```

- `winlog.event_data.Image`: Use this field to get specific information on the actions of a particular file. For example, to check if an unknown file has sent out DNS queries to command-and-control servers:

```bash
winlog.event_data.Image: *filename* and winlog.event_id: 22
```

Then, use the `winlog.event_data.QueryName` field to identify the DNS queries made by the file.

### Example Query

To monitor DNS queries from a specific file, use the following query:

```bash
winlog.event_data.Image: *filename* and winlog.event_id: 22
```

And to check for DNS queries specifically:

```bash
winlog.event_data.QueryName: *
```

win
**Sysmon** (System Monitor) is a Windows system service and device driver that, once installed on a system, remains across system reboots to monitor and log system activity to the Windows event log. It provides detailed information about process creations, network connections, and file changes, making it an invaluable tool for advanced threat detection and forensic investigations.


## When to use Sysmon for Threat Detection

- Trace command execution paths and process interactions, offering a detailed view of how an attack unfolded.  
     
- Identify suspicious activities that could indicate a breach or an attempt to compromise the system.  
     
- Utilize the detailed logging to perform root cause analysis and improve security measures.

## Important Sysmon Event Types

- **Event ID 1:** Process Creation - Tracks when a process is started, including the command line that initiated the process. This is critical for identifying malicious processes or commands used by attackers.  
     
- **Event ID 3:** Network Connection - Monitors attempts to connect to a remote host, which can be pivotal in detecting data exfiltration attempts or command and control (C&C) communication.  
     
- **Event ID 7:** Image Loaded - Logs when a DLL is loaded into a process, which is useful for detecting the use of malicious payloads or code injection techniques.


## Queries

### Check for any suspicious web downloads that came from the cmd line

```bash
winlog.provider_name: "Microsoft-Windows-Sysmon" and winlog.event_data.CommandLine: *http*
```


### Extra Root Cause of Alerts

- **winlog.event_data.User

This field gives information regarding the User account

- **winlog.event_data.CommandLine:**  

This field records the exact command line used to start a process. By analyzing this, we can understand what commands were executed, potentially identifying malicious scripts, executables, or commands.

```bash
`winlog.provider_name: "Microsoft-Windows-Sysmon" and winlog.event_id: "1" and winlog.event_data.CommandLine: *cmd.exe*`
```

 - **winlog.event_data.ParentCommandLine:**

    
    This field shows the command line of the parent process that initiated the current process. It's invaluable for tracing the origin of suspicious activities, helping to map out attack chains, or identifying root causes.  
     
    
- **winlog.event_data.ChildCommandLine:**
    
    While Sysmon does not directly log a `ChildCommandLine` field, the concept of tracking command lines of child processes is crucial in understanding how a process spawns additional processes. This is typically inferred by analyzing the `CommandLine` of processes created by a parent process of interest.
    
    - **Investigative Approach:**  
        After identifying a suspicious parent process via its `ParentCommandLine`, further investigation into the `CommandLine` of processes spawned by this parent can provide insights into the spread or actions of malware.



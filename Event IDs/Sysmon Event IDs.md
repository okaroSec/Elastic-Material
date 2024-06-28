### Important Sysmon Event IDs

1. **Event ID 1: Process Creation**
    
    - Tracks when a process is started, including the command line that initiated the process. This is critical for identifying malicious processes or commands used by attackers.
2. **Event ID 3: Network Connection**
    
    - Monitors attempts to connect to a remote host, which can be pivotal in detecting data exfiltration attempts or command and control (C&C) communication.
3. **Event ID 7: Image Loaded**
    
    - Logs when a DLL is loaded into a process, useful for detecting the use of malicious payloads or code injection techniques.
4. **Event ID 8: CreateRemoteThread**
    
    - Logs when a thread is created in a remote process, which is commonly used in process injection attacks.
5. **Event ID 10: Process Access**
    
    - Captures detailed information about access to processes, useful for detecting unauthorized or suspicious process interactions.
6. **Event ID 11: File Creation**
    
    - Tracks the creation of files, which can be useful for detecting the presence of malware or unauthorized file modifications. File Created
7. **Event ID 12: Registry Event (Object Create and Delete)**
    
    - Monitors creation and deletion of registry keys and values, useful for detecting persistence mechanisms used by malware.
8. **Event ID 13: Registry Event (Value Set)**
    
    - Tracks changes to registry values, which can indicate the modification of system or application settings.
9. **Event ID 14: Registry Event (Key and Value Rename)**
    
    - Monitors renaming of registry keys and values, which can be part of a malware's attempt to evade detection.
10. **Event ID 15: File Create Stream Hash**
    
    - Logs file creation with MD5 hashes of alternate data streams, useful for detecting hidden or obfuscated files.
11. **Event ID 17: Pipe Event (Pipe Created)**
    
    - Tracks the creation of named pipes, which can be used for inter-process communication by malware.
12. **Event ID 18: Pipe Event (Pipe Connected)**
    
    - Logs connections to named pipes, useful for detecting malware communication channels.
13. **Event ID 19: WMI Event (WmiEventFilter activity detected)**
    
    - Monitors WMI event filters, which can be used by malware for persistence or lateral movement.
14. **Event ID 20: WMI Event (WmiEventConsumer activity detected)**
    
    - Tracks WMI event consumers, which can execute actions based on WMI events, commonly used by malware.
15. **Event ID 21: WMI Event (WmiEventConsumerToFilter activity detected)**
    
    - Monitors the binding of WMI event filters to consumers, useful for detecting complex WMI-based attacks.
16. **Event ID 22: DNS Query**
    
    - Logs DNS queries, which can be used to detect communication with known malicious domains or unusual DNS activity.
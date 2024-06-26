
## Common Windows Logon Types and Their Security Implications

### Logon Type 2: Interactive

Occurs when a user logs on directly to a computer and enters credentials at the login prompt. This is a common scenario for users accessing their workstations.

### Logon Type 3: Network

Triggered when a user accesses a computer from the network, such as when connecting to shared folders or printers. This type doesn't necessarily indicate direct physical interaction with the computer.

### Logon Type 10: RemoteInteractive (RDP)

Similar to interactive logons but specifically for users logging on remotely using Remote Desktop or Terminal Services. Monitoring these events is crucial for detecting unauthorized remote access attempts.

**Example Query for Detecting Unauthorized RDP Access in ELK Kibana:

```bash
winlog.channel: "Security" and winlog.event_id: "4624" and winlog.event_data.LogonType: "10"
```

This query isolates remote desktop logins, which are crucial for identifying potential lateral movement or unauthorized remote access.

### Logon Type 11: CachedInteractive

Occurs when users log on using cached credentials on the local machine, typically when the domain controller is unavailable. Understanding access patterns here is important, especially when network connectivity to the domain controller is discontinuous or down.

### Logon Type 4: Batch

Indicates a logon triggered by a batch job or scheduled task. Monitoring these can help identify potentially malicious scheduled tasks.

### Logon Type 5: Service

Occurs when a service starts on the computer. It's essential to monitor these for services starting with unusual or high-privileged user accounts, which could indicate a service being exploited for privilege escalation.

**Example Query for Monitoring Services Starting with Potentially Compromised Accounts:

```bash
winlog.channel: "Security" and winlog.event_id: "4624" and winlog.event_data.LogonType: "5"

```

### Logon Type 7: Unlock

Logged when a user unlocks a previously locked workstation, which could be benign or indicate someone attempting to gain access to a workstation that isn't theirs.

### Logon Type 8: NetworkCleartext

A logon with this type should raise immediate red flags as it involves credentials sent over the network in cleartext, potentially exposing sensitive information to eavesdropping.

## Strategies to Mitigate Lateral Movement

The `winlog.event_data.IpAddress` field plays a pivotal role here, enabling defenders to track the source IP of suspicious activities. Furthermore, understanding the context of logoff events through `winlog.event_id: "23"` provides insights into the attacker's operational window, which is essential for gauging the breach's extent.

** Query for unusual Access Patterns:

```bash
winlog.channel: "Security" and winlog.event_id: "4624" and winlog.event_data.IpAddress:"<specific_ip_address>"

```

Remember **4624 means successful login

** Query for Assessing Session Durations through LogOff events. This is good can see when the attacker left a session

```bash
winlog.provider_name: "Microsoft-Windows-TerminalServices-LocalSessionManager" and winlog.event_id: "23"

```
This query focuses on RDP session disconnects, marking the conclusion of the attacker's known activity period.

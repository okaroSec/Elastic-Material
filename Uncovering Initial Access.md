
`winlog.channel` represents the different categories or "channels" under which logs are recorded. These channels include Security, Application, System, and many others, each serving a distinct purpose:

- **Security:** This channel records events related to security, such as login attempts (both successful and failed), policy changes, and other activities that have implications for system security.  
     
- **Application:** Events related to software applications running on the system are logged here. This can include errors, information messages, or warnings generated by applications.  
     
- **System:** This channel captures events that are related to the operating system's functionality, such as driver failures, hardware issues, and system errors.

By specifying `winlog.channel:"Security"`, we can focus on security-related events to identify unauthorized access attempts. However, exploring other channels may also be beneficial depending on the context of your investigation.

- **Application logs** can be used to identify unusual application behavior or errors that may indicate exploitation or misuse.  
     
- **System logs** might show unexpected restarts, driver failures, or other system-level anomalies that could be symptoms of a deeper security issue.

## Windows security event IDs

Security event logs provide a detailed record of all access attempts to your systems, both authorized and unauthorized. By analyzing these logs, you can uncover patterns indicating a breach or an attempted breach. 

Including these event IDs in your analysis can provide a more comprehensive view of potential security incidents, helping you detect initial access attempts and subsequent actions taken by attackers once inside the network.

- **Event ID 4624** (Successful logon)**:** To identify abnormal and potentially unauthorized insider activity, such as logging in from inactive or restricted accounts, logging in outside of regular working hours, logging in concurrently to multiple resources, etc.  
     
- **Event ID 4625** (Failed logon): To detect possible brute-force, dictionary, and other password-guessing attacks characterized by a sudden spike in failed logins.  
     
- **Event ID 4648**: Indicates a successful login using explicit credentials, which might suggest the use of stolen credentials or pass-the-hash attacks.  
     
- **Event ID 4672**: Special privileges assigned to a new logon. This can be a sign of privilege escalation or that a high-privileged account has been compromised.  
     
- **Event ID 4720**: Creation of a new user account, which could indicate unauthorized changes to system users and potential backdoor account creation by an attacker.


This query helps identify potential brute-force attacks by detecting an abnormally large number of failed logon attempts.

```bash
winlog.channel:"Security" and winlog.event_id:"4625"
```

This query helps to identify unexpected or unauthorized user account creation activities, offering early detection of potential insider threats or attacker persistence mechanisms.

```bash
winlog.channel:"Security" and winlog.event_id:"4720"
```

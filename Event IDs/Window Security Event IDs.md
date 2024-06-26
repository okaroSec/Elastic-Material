
## Windows security event IDs

Security event logs provide a detailed record of all access attempts to your systems, both authorized and unauthorized. By analyzing these logs, you can uncover patterns indicating a breach or an attempted breach. 

Including these event IDs in your analysis can provide a more comprehensive view of potential security incidents, helping you detect initial access attempts and subsequent actions taken by attackers once inside the network.

- **Event ID 4624** (Successful logon)**:** To identify abnormal and potentially unauthorized insider activity, such as logging in from inactive or restricted accounts, logging in outside of regular working hours, logging in concurrently to multiple resources, etc.  
     
- **Event ID 4625** (Failed logon): To detect possible brute-force, dictionary, and other password-guessing attacks characterized by a sudden spike in failed logins.  
     
- **Event ID 4648**: Indicates a successful login using explicit credentials, which might suggest the use of stolen credentials or pass-the-hash attacks.  
     
- **Event ID 4672**: Special privileges assigned to a new logon. This can be a sign of privilege escalation or that a high-privileged account has been compromised.  
     
- **Event ID 4720**: Creation of a new user account, which could indicate unauthorized changes to system users and potential backdoor account creation by an attacker.
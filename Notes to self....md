

Sometimes a query won't work correctly if the `provider_name` is not included.
- Keep a timeline of events this is the most important thing. For every important event make sure to keep track of the time
- `winlog.event_data.Contents` can include command statements.
- `winlog.event_data.QueryName` contains information regarding the domain name.
- `winlog.event_data.ParentImage : *cmd.exe*` is very useful for checking executed commands.
- Check the current directory `winlog.event_data.CurrentDirectory` to see where files may have been saved.
- Use `winlog.channel: "Security" and winlog.event_id: "4625"` to identify potential brute force attacks. If possible, check `winlog.event_data.WorkstationName` to see the hostname where the attacker launched their attack.
- To check for commands, use `winlog.provider_name: "Microsoft-Windows-Sysmon" and winlog.event_id: "1" and winlog.event_data.ParentImage: "C:\Windows\System32\cmd.exe"`.
- Look for the earliest possible data of the executable and check `winlog.event_data.Image` to see how this file was downloaded.

Event ID 15: FileCreateStreamHash

> This event logs when a named file stream is created, and it generates events that log the hash of the contents of the file to which the stream is assigned (the unnamed stream), as well as the contents of the named stream. Some malware variants drop their executables or configuration settings via browser downloads. This event captures that activity based on the browser attaching a Zone.Identifier "mark of the web" stream.

Query used for Sysmon event 15: `winlog.provider_name: "Microsoft-Windows-Sysmon" and winlog.event_id: "15"`

Find DNS information with `winlog.provider_name: "Microsoft-Windows-Sysmon" and winlog.event_id: "22"`.

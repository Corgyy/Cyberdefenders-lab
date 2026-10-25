### The user clicked a link inside the email, which spawned a browser. What is the full URL of the delivery page the victim was directed to?

index=* host="FB-WKS64" EventCode=1 parent_process_name=olk.exe 
| table _time, parent_process_name, process_name, CommandLine


### The lure page automatically downloaded a malicious script to the host. What is the full source URL it was originally downloaded from?

index=* host="FB-WKS64" EventCode=15 
| table _raw
| head 5

index=* host="FB-WKS64" EventCode=15 Contents="*ReferrerUrl=http://52.59.253.168/download_invitee.php*"
| table _time, TargetFilename, Contents, _raw
| sort _time

### Once executed, the dropped script orchestrated the next stage by spawning multiple child processes within seconds. List the two children of wscript.exe in chronological order.

index=* host=FB-WKS64 EventCode=1 parent_process_name=wscript.exe
| table _time, _raw, parent_process_name, process_name
| sort _time


### After extracting the second-stage archive, the user double-clicked the loader executable. What is the full file path of the first-stage loader?

index=* host=FB-WKS64 "*1Yqzl-L-1FGWm4iOwieRFv9zr0urEEGWR*"
| table _time, EventCode, process_name, TargetFilename, Image, _raw
| sort _time

==> FileServer.7z download via gg drive
path C:\\Users\\chriskarma\\Downloads\\


index=* host=FB-WKS64 EventCode=11 TargetFilename="C:\\Users\\chriskarma\\Downloads\\FileServer*"
| table _time, EventCode, Image, TargetFilename
| sort __time


### Among the loader's discovery commands, one queried a specific scheduled task by name, likely an OPSEC check to verify a prior footprint. What task name was queried?


index=* host=FB-WKS64 "*FileServer.exe*" EventCode=7
| table _time, EventCode Image, TargetFilename, _raw
| sort _time

index=* host=FB-WKS64 "FileServer.exe" process_name=schtasks.exe
| table _time, EventCode, Image, CommandLine, _raw

### The loader inspected the ACL on a single file, suggesting preparation for a hijack or overwrite. What is the full path of that file?

index=* host=FB-WKS64 "FileServer.exe" process_name=icacls.exe
| table _time, EventCode, Image, CommandLine, _raw

### AD enumeration was performed via a wrapper script that was iteratively re-staged in two different filesystem locations during the operation. List both full paths of adf.bat in the order they appeared.

index=* host=FB-WKS64 "adf.bat"
| table _time, EventCode, Image, CommandLine, _raw

### The wrapper script queried four distinct Active Directory object types using LDAP objectcategory filters. List the four objectcategory values in the order the assembly commands ran.

index=* host=FB-WKS64 parent_process_name=FileServer.exe process_name=cmd.exe "objectCategory"
| table _time, EventCode, Image, CommandLine, _raw
| sort _time


### After execution, the first-stage loader retrieved and ran a second-stage implant. What is the full file path where it was written to disk?

index=* host=FB-WKS64 EventCode=1 parent_process_name=FileServer.exe 
| table _time, EventCode, process_name, Image, CommandLine, _raw
| sort _time

### A Python reverse shell to the primary C2 reveals the operator's source template, the script ends by spawning a non-native shell binary that wouldn't even resolve on Windows. What is the path of the shell binary in the subprocess.call list?

index=* host=FB-WKS64 process_name=cmd.exe python
| table _time, EventCode, parent_process_name, process_name, Image, CommandLine, _raw
| sort _time

### A persistence installer was dropped to the victim's Downloads folder well before the user was induced to execute it. What is the UTC timestamp when this MSI file was first written to disk?

index=* host=FB-WKS64 TargetFilename="C:\\Users\\chriskarma\\Downloads\\*"
| table _time, EventCode, Image, TargetFilename
| sort _time

### The operator's first attempt to archive user data referenced source paths that don't exist on this host,  a clear sign of script-template reuse from a previous engagement. What username appears in those non-existent paths?

index=* host=FB-WKS64 EventCode=1 *Compress-Archive*
| table _time, EventCode, ParentCommandLine, CommandLine, _raw
| sort _time

### The operator's PowerShell pipeline transformed the staged archive's bytes into a transmission-safe encoding before POSTing them out over HTTPS. What's the encoding scheme used and the full destination URL?

index=* host=FB-WKS64 CommandLine="*sys_upd.zip*"
| table _time, ParentCommandLine, CommandLine, _raw
| sort _time
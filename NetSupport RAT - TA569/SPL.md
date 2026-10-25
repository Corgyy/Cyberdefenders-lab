
While reviewing the logs, you notice the employee downloaded a malicious attachment that started the attack. What is the name of the file used to deliver this initial malicious payload to the victim’s system?

index=* source="XmlWinEventLog:Microsoft-Windows-Sysmon/Operational" EventCode=15
| dedup TargetFilename
| table _time, User, Image, TargetFilename, Contents, _raw
| sort _time

Digging into the employee’s workstation, you find that the attack began when a specific file from the malicious attachment was executed. What is the name of the file that triggered the attack?

index=* source="XmlWinEventLog:Microsoft-Windows-Sysmon/Operational" EventCode=1 "*Invoice_2326.js*"
| table _time, User, parent_process_name, process_name, ParentCommandLine, CommandLine, _raw
| sort _time


While examining the PowerShell script’s actions, you discover it fetched and ran an executable file to deepen the attacker’s foothold. What is the name of this executable file?

index=* host="IT-WS01" source="XmlWinEventLog:Microsoft-Windows-Sysmon/Operational" User="CORP\\danderson" EventCode=11
| table _time, Image, TargetFilename
| sort _time



Analyzing network traffic, you spot suspicious outbound connections from the compromised system to a command-and-control (C2) server. What is the IP address used for the initial C2 communication by the attacker’s beacon?

index=* host="IT-WS01" User="CORP\\danderson" "*netsupport.exe*" EventCode=3
| table _time, Image, SourceIp, SourcePort, DestinationIp, DestinationPort, _raw
| sort _time

To ensure persistence, the attacker modified the system to run their malicious code on every boot. Which registry key did they add to achieve this?

index=* host="IT-WS01" User="CORP\\danderson" (EventCode=12 OR EventCode=13) "*netsupport*"
| dedup TargetObject
| table _time, EventCode, Image, TargetObject, _raw
| sort _time


You notice a rogue SSH server running on the compromised system, likely for remote access. Which uncommon TCP port is this rogue SSH server using?

index=* host="IT-WS01" User="CORP\\danderson" EventCode=1 "*ssh.exe*"
| table _time, Image, ParentCommandLine, CommandLine, _raw
| sort _time


During your investigation, you find a new user account created on the compromised system, likely to blend in with normal operations. What is the password for this account, which the attacker used to maintain persistence?

index=* host="IT-WS01" User="CORP\\danderson" EventCode=4720

index=* host="IT-WS01" WDAGUtilityAccount2 EventCode=1 
| table _time, CommandLine, _raw
| sort _time



While reviewing the Windows Credential Manager on the compromised workstation, you discover the attacker tried to update credentials for an account identified during their reconnaissance. What is the name of this account?

index=* host="IT-WS01" "netsupport.exe" EventCode=1
| table _time, ParentCommandLine, CommandLine, process_name, _raw


Checking the antivirus logs, you notice the attacker tampered with the software to avoid detection. Which directory did they add as an exclusion in the antivirus settings?

index=* host="IT-WS01" "netsupport.exe" EventCode=1 "MpPreference"
| table _time, ParentCommandLine, CommandLine, process_name, _raw


While reviewing event logs, you pinpoint the moment the attacker successfully extracted password hashes from the compromised machine. At what time did this hash dump occur?

index=* host=IT-WS01 source="XmlWinEventLog:Microsoft-Windows-Sysmon/Operational" "lsass.exe" EventCode=10
| table _time, host, EventCode, SourceImage, TargetImage, _raw
| sort _time

As you analyze the compromised system, you find a file where the attacker stored data for later exfiltration. What is the name of this file?

index=* host=DC01 EventCode=1 "*Compress-Archive*"
| table _time, Image, CommandLine, _raw
| sort _time
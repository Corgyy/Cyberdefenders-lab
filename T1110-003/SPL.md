
Who was the last logged-in user?
index="t1110-003" "winlog.event_id"=4624
| table _time, winlog.event_id, winlog.event_data.SubjectUserName, winlog.event_data.TargetUserName, _raw
| sort _time


What is the logon type of the failed logons?
index="t1110-003" "winlog.event_id"=4625 winlog.event_data.TargetUserName="Administrator"
| table _time, winlog.event_id, winlog.event_data.SubjectUserName, winlog.event_data.TargetUserName, winlog.event_data.LogonType, _raw
| sort _time


What is the protocol the attacker tried to bruteforce?
index="t1110-003" "winlog.provider_name"="Microsoft-Windows-TerminalServices-RemoteConnectionManager"
| table _time, winlog.event_id, host.ip{}, host.os.name, message, _raw
| sort _time



index="t1110-003" ("winlog.event_id"=4624 OR "winlog.event_id"=4625) winlog.event_data.TargetUserName="Administrator"
| table _time, winlog.event_id, winlog.event_data.SubjectUserName, winlog.event_data.TargetUserName, winlog.event_data.LogonType, _raw
| sort _time



How many users did the attacker succeed in getting their accounts?

index="t1110-003" "winlog.provider_name"="Microsoft-Windows-TerminalServices-RemoteConnectionManager" winlog.event_id=1149
| dedup message
| table _time, winlog.event_id, host.ip{}, host.os.name, winlog.computer_name, message, _raw
| sort _time



How long did the bruteforce last? MM:SS

index="t1110-003" "winlog.event_id"=4625 winlog.event_data.SubStatus=0xc000006a 
| dedup winlog.event_data.TargetUserName
| table _time, winlog.event_id, winlog.event_data.SubjectUserName, winlog.event_data.TargetUserName, _raw
| sort _time

index="t1110-003" "winlog.event_id"=4625 winlog.event_data.TargetUserName=yokehorde
| table _time, winlog.event_id, winlog.event_data.SubjectUserName, winlog.event_data.TargetUserName, _raw
| sort _time
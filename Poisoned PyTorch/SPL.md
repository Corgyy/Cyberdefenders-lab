
index=* host=PC01 CommandLine=*python*
| table _time, EventCode, parent_process_name, process_name, CommandLine, _raw
| sort _time

==> AI/ML project directory


index=* host=PC01 EventCode=1 "torch-inference-stack"
| table _time, Image, TargetFilename CommandLine, _raw
| sort _time

==> compromised library, powershell code execute to download malicious payload

index=* host=PC01 "12480" "torch-inference-stack"
| table _time, EventCode, Image, ParentCommandLine, CommandLine, _raw
| sort _time

==> confirm jedilsp 3.12.9 spawn powershell PID 12480


index=* host=PC01 EventCode=1 "torch-inference-stack" ParentCommandLine="*downloadstring*"
| table _time, Image, ParentCommandLine, CommandLine, _raw
| sort _time

==> malicious powershell command executed


index=* host=PC01 "*updlate.dll*"
| table _time, EventCode, Image, ParentCommandLine, CommandLine, _raw
| sort _time

==> spawn dll and run for persistence (modify registry and add schedule task) and read exposed credentials

index=* EventCode=4624 LogonType=10
| table _time, host, EventCode, LogonType, LogonProcessName _raw
| sort _time

==> an account successfully logs on to a local computer (successfully log on to DC01, FILE-SERVER-01, BACKUP-SERVER-0)

index=* EventCode=4720 
| table _time, host, EventCode, _raw
| sort _time

==> identify account created

index=* host=FILE-SERVER-01 EventCode=1 "*http*"
| table _time, EventCode, parent_process_name, process_name, CommandLine, _raw
| sort _time

==> download payload on FILE-SERVER-01


index=* EventCode=11 host=FILE-SERVER-01 "system recovery.exe"
| table _time, host, parent_process_name, process_name, Image, TargetFilename, _raw
| sort _time

==> discover ransome bianry file after exploring file creation event on server
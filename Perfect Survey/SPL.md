
## Reconnaissance
index=* source="access.log" 
| table _time, clientip, useragent, uri, status, _raw 
| sort _time


index=* source="access.log" useragent="*nmap*" status=200
| table _time, clientip, useragent, uri, status, _raw 
| sort _time


The scanner identified a vulnerable third-party plugin installed on the CMS. What is the name of this vulnerable plugin?

index=* source="access.log" useragent="*wpscan*" status=200
| dedup uri
| table _time, clientip, useragent, uri, status, _raw 
| sort _time


The attacker attempted to exploit the vulnerable plugin for remote code execution. At what exact timestamp did the scanning tool attempt the RCE exploit? (in 24-hour format)

index=* source="access.log" useragent="*sql*" status=200 uri="*xp_cmdshell*"
| table _time, clientip, useragent, uri, status, _raw
| sort _time



After cracking the extracted hash, the attacker gained valid server credentials. Which user's password was compromised for initial authentication?

index=* source="Security.json" "Event.System.EventID"=4624 Event.EventData.IpAddress=47.128.63.0
| table _time, Event.EventData.IpAddress, Event.EventData.TargetUserName,  Event.EventData.TargetDomainName, Event.EventData.LogonType,  Event.EventData.WorkstationName
| sort _time



A Kerberoasting attack was conducted after compromising the first user. Which user was targeted by this attack?
index=* source="Security.json" "Event.System.EventID"=4769
| table _time, Event.EventData.IpAddress, Event.EventData.TargetUserName,  Event.EventData.TargetDomainName
| sort _time


A new account was created in preparation for a domain privilege escalation. What is the name of this machine account?
index=* source="Security.json" "*alonso.x*" Event.System.EventID=4741
| table _time, Event.System.EventID, Event.EventData.SubjectUserName, Event.EventData.TargetUserName
| sort _time

The attacker requested a service ticket through the configured Resource-Based Constrained Delegation chain. Which account was targeted for the service ticket request via RBCD?

index=* source="Security.json" "*MADRID$*" Event.System.EventID=4769
| table _time, Event.System.EventID, Event.EventData.TargetUserName, Event.EventData.ServiceName,  Event.EventData.TicketEncryptionType
| sort _time

index=* source="Security.json" "*MADRID$*" (Event.System.EventID=4769 OR Event.System.EventID=4742 OR Event.System.EventID=4741)
| table _time, Event.System.EventID, Event.EventData.TargetUserName, Event.EventData.ServiceName,  Event.EventData.TicketEncryptionType
| sort _time

The attacker exploited Active Directory Certificate Services to obtain privileged account hashes. Which high-privilege account was targeted through AD CS escalation?

index=* source="Security.json" "*APP-BKUP01$*" (Event.System.EventID=4886 OR Event.System.EventID=4887)
| table _time, Event.System.EventID, Event.EventData.Requester, Event.EventData.Attributes
| sort _time
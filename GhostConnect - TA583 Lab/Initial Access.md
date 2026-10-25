
user on host FB-WKS64 (username=chriskarma) is using email launcher (OUTLOOK)
user click a link inside the email, which spawned a browser (EventCode=1)
process tree:
- olk.exe --> chrome.exe (CommandLine="C:\Program Files\Google\Chrome\Application\chrome.exe" --single-argument http://52.59.253.168/download_invitee.php)
Hash: 86CC1935559906D1EFE7F134FA355A94


the full source URL it was originally downloaded from (EventCode=15 File create stream hash)
- Note: When a file is downloaded through a browser, Windows tags it Mark-of-the-Web (MotW) - metadata stored in ADS named Zone.Identifier. Sysmon captured the creation of this ADS via EC=15, with the original source URL recoreded


==> trong Field Contents có Field ReferrerUrl và HostURL

[ZoneTransfer] ZoneId=3 ReferrerUrl=http://52.59.253.168/download_invitee.php HostUrl=http://52.59.253.168/E-INVITE.vbs
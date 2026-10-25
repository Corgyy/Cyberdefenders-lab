
Loader "FileServer.exe" create a file named "FileR.exe" (53B705A1FF29B71C0872EE7E969BFAF4) which is a malware in SilentConnect family https://www.virustotal.com/gui/file/8bab731ac2f7d015b81c2002f518fff06ea751a34a711907e80e98cf70b557db/detection

Then, the Loader retrieve additional payload from C2 server (http://34[.]228[.]194[.]206:80/f) and execute a metasploit revershell to connect to another C2 server (52[.]59[.]253[.]168:4444)
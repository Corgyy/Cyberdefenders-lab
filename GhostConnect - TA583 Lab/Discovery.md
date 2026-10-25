a loader named "FileServer.exe" which is extracted from FileServer.7z execute many discovery commands:
- schtasks.exe to verify a specific schedule task named "vulntask"
- icals.exe to check ACL of schtask.bat
- using cmd to write the command `AF.exe -f (objectcategory=computer/ person/organizationalUnit/ group) > groups.txt` to two "adf.bat" files located in different paths. C:\Windows\Temp\adf.bat and C:\Users\chriskarma\AppData\Roaming\adf.bat 

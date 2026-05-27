# PowerShell Deep Dive

## What is PowerShell?

PowerShell is:
- A command-line shell
- A scripting language
- A Windows automation framework

### Built on:
- .NET Framework / .NET

### Used for:
- System administration
- Threat hunting
- Log analysis
- Malware execution
- Lateral movement
- Automation

# PowerShell Command Reference

| Purpose                     | Main Command                          | Alias            | Example                                           |
|-----------------------------|---------------------------------------|------------------|---------------------------------------------------|
| Show current directory      | Get-Location                          | pwd              | Get-Location                                      |
| List files/folders          | Get-ChildItem                         | ls, dir          | Get-ChildItem C:\Users                            |
| Change directory            | Set-Location                          | cd               | cd Downloads                                      |
| Read file contents          | Get-Content                           | cat, type        | Get-Content test.txt                              |
| Search text inside file     | Select-String                         | sls              | Select-String -Path log.txt -Pattern "error"      |
| View running processes      | Get-Process                           | ps               | Get-Process                                       |
| Kill process                | Stop-Process                          | kill             | Stop-Process -Id 4444                             |
| View services               | Get-Service                           | —                | Get-Service                                       |
| Start service               | Start-Service                         | —                | Start-Service WinDefend                           |
| Stop service                | Stop-Service                          | —                | Stop-Service Spooler                              |
| View network connections    | Get-NetTCPConnection                  | —                | Get-NetTCPConnection                              |
| Find process by PID         | Get-Process -Id                       | —                | Get-Process -Id 1234                              |
| Read event logs             | Get-WinEvent                          | —                | Get-WinEvent -LogName Security                    |
| Read old event logs         | Get-EventLog                          | —                | Get-EventLog Security                             |
| View top CPU processes      | Get-Process \| Sort CPU -Descending   | —                | Get-Process \| Sort CPU -Descending               |
| Select specific fields      | Select-Object                         | select           | Get-Process \| Select Name,Id,CPU                 |
| Filter output               | Where-Object                          | where            | Get-Service \| Where {$_.Status -eq "Running"}    |
| Sort output                 | Sort-Object                           | sort             | Get-Process \| Sort CPU                           |
| Show first few results      | Select-Object -First                  | —                | Get-Process \| Select -First 5                    |
| Export CSV file             | Export-Csv                            | —                | Get-Process \| Export-Csv proc.csv                |
| Import CSV file             | Import-Csv                            | —                | Import-Csv proc.csv                               |
| Download file from internet | Invoke-WebRequest                     | iwr, wget, curl  | iwr http://site.com/file.exe -OutFile malware.exe |
| Execute expression          | Invoke-Expression                     | iex              | iex "Get-Process"                                 |
| Get command help            | Get-Help                              | help             | Get-Help Get-Process -Examples                    |
| Get command syntax          | Get-Command                           | gcm              | Get-Command *process*                             |
| View execution policy       | Get-ExecutionPolicy                   | —                | Get-ExecutionPolicy                               |
| Change execution policy     | Set-ExecutionPolicy                   | —                | Set-ExecutionPolicy Bypass                        |
| Create variable             | Variable assignment                   | —                | $name = "SOC"                                     |
| Print output                | Write-Host                            | —                | Write-Host "Hello"                                |
| View environment variables  | Get-ChildItem Env:                    | dir Env:         | Get-ChildItem Env:                                |
| View PowerShell version     | $PSVersionTable                       | —                | $PSVersionTable                                   |
| Clear terminal screen       | Clear-Host                            | cls, clear       | cls                                               |
| Create new file             | New-Item                              | ni               | New-Item test.txt                                 |
| Copy files                  | Copy-Item                             | copy, cp         | Copy-Item a.txt b.txt                             |
| Move files                  | Move-Item                             | mv, move         | Move-Item a.txt C:\Temp                           |
| Delete files                | Remove-Item                           | rm, del          | Remove-Item malware.exe                           |
| Show running jobs           | Get-Job                               | —                | Get-Job                                           |
| Run background job          | Start-Job                             | —                | Start-Job {Get-Process}                           |
| Test connectivity           | Test-Connection                       | ping             | Test-Connection google.com                        |
| DNS lookup                  | Resolve-DnsName                       | —                | Resolve-DnsName google.com                        |
| Show current user           | whoami                                | —                | whoami                                            |
| View local users            | Get-LocalUser                         | —                | Get-LocalUser                                     |
| View local groups           | Get-LocalGroup                        | —                | Get-LocalGroup                                    |
| View scheduled tasks        | Get-ScheduledTask                     | —                | Get-ScheduledTask                                 |
| View startup items          | Get-CimInstance Win32_StartupCommand  | —                | Get-CimInstance Win32_StartupCommand              |


---
# Most Important SOC Hunting Commands

| SOC Task                   | Command                                                                 |
|-----------------------------|-------------------------------------------------------------------------|
| Failed logins              | Get-WinEvent -FilterHashtable @{LogName='Security'; ID=4625}             |
| Successful logins           | Get-WinEvent -FilterHashtable @{LogName='Security'; ID=4624}             |
| Process creation logs       | Get-WinEvent -FilterHashtable @{LogName='Security'; ID=4688}             |
| Find PowerShell usage       | Get-WinEvent -LogName Security \| Select-String "powershell"             |
| Hunt encoded commands       | Select-String -Pattern "EncodedCommand"                                 |
| Top suspicious processes    | Get-Process \| Sort CPU -Descending \| Select -First 10                  |
| Find active connections     | Get-NetTCPConnection                                                    |
| Find process using connection | Get-Process -Id <PID>                                                 |
| Search IOC in logs          | Select-String -Path *.log -Pattern "malware.com"                        |
| Decode Base64 PowerShell    | [System.Text.Encoding]::Unicode.GetString([Convert]::FromBase64String("BASE64")) |


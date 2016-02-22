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

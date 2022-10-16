---
title: CfgMgr Distribution Priority
date: 2020-11-27T01:01:01Z
tags: ["CfgMgr", "DP", "Powershell"] 
---

Quick one.

We have some remote DPs that are rate limited during business hours, but if an App or Package is set to High, then it'll distribute regardless.

I wanted to see which apps and driver packages I had previously set to High priority for distribution and no longer need to be.  
However, MECM doesn't show this in any columns I could find. So I went to PowerShell.

Unfortuntely, the Get-CMApplications cmdlet doesn't include any properties for 'Priority' so, that was a bust.

Bring in WMI Explorer.  
I used this to dig through Namespaces in ROOT\SMS\site_CM1 to find what Classes had a Priority attribute. Tedious process, but looking for things like "Application" or "Package" made the process a bit quicker.

I fell upon SMS_PackageBaseclass, which just so happened to include all Applications, Packages, Programs, and Drivers. and the Distribution Priority of them all. Jackpot!

WMI Explorer also has a nice feature to create PowerShell code for you on the fly.  
So I grabbed the code, mixed it in with the ISE code that gets generated when you open ISE from Config Manager Console, and hey presto:  
```powershell
# Uncomment the line below if running in an environment where script signing is 
# required.
#Set-ExecutionPolicy -ExecutionPolicy Bypass -Scope Process

# Site configuration
$SiteCode = "CM1" # Site code 
$ProviderMachineName = "cm01.contoso.com" # SMS Provider machine name

########################################################################################
# Do not change anything below this line ###############################################
########################################################################################

# Import the ConfigurationManager.psd1 module 
if((Get-Module ConfigurationManager) -eq $null) {
    Import-Module "$($ENV:SMS_ADMIN_UI_PATH)\..\ConfigurationManager.psd1" @initParams 
}

# Connect to the site's drive if it is not already present
if((Get-PSDrive -Name $SiteCode -PSProvider CMSite -ErrorAction SilentlyContinue) -eq $null) {
    New-PSDrive -Name $SiteCode -PSProvider CMSite -Root $ProviderMachineName
}

# Set the current location to be the site code.
Set-Location "$($SiteCode):\"

$computer = $ProviderMachineName
$namespace = "ROOT\SMS\site_$SiteCode"
$classname = "SMS_PackageBaseclass"

Write-Output "====================================="
Write-Output "COMPUTER : $computer "
Write-Output "CLASS    : $classname "
Write-Output "====================================="

Get-WmiObject -Class $classname -ComputerName $computer -Namespace $namespace -filter "Priority <> 2" |
    Select-Object __CLASS, __PATH, Name, Description, ObjectPath, PackageID, Priority | Out-GridView
```

In the last line, where filtering for `Priority`, "2" equals "Medium" and is the default. So I wanted to find everything that is not "Medium".
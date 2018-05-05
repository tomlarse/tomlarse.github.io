---
layout: post
title: Script: Create live tiles that changes power scheme
date: 2013-04-07 23:09
author: tomlarse
comments: true
categories: [General, powershell, script, Scripts, Surface Pro, Uncategorized]
---
After i got my Surface Pro, I've more often than before found myself needing to change between power schemes. On my laptop, I'll usually set it to "Max performance" and just leave it there, but on the Surface it's necessary to conserve power a bit more.

I've thought about making a live tile to do this, so I wrote a PowerShell script that will create one live tile for each configured powerscheme on the machine and pins it to the start screen. The code is based on a <a href="http://gallery.technet.microsoft.com/scriptcenter/Create-a-ShutdownRestartLog-37c8111d" target="_blank">codesample</a> for creating shutdown tiles, and <a href="http://blogs.technet.com/b/heyscriptingguy/archive/2010/08/31/get-windows-power-plan-settings-on-your-computer-by-using-powershell.aspx" target="_blank">this</a> ScriptingGuy post. The script needs to be run as Administrator. Enjoy!

Download <a href="http://codesalot.files.wordpress.com/2013/04/create-powerschemetiles.zip">Create-PowerSchemeTiles.zip</a> or copy the sourcecode:

```

#requires -Version 3.0

#####################################################################################
# Create-PowerSchemeTiles.ps1
#
# Creates live tiles for all configured power schemes on the machine and pins them to
# the start screen.
#
#
# Usage:
# .Create-PowerSchemeTiles.ps1
#
# Written by Tom-Inge Larsen (&lt;a href=&quot;http://www.codesalot.com&quot;&gt;http://www.codesalot.com&lt;/a&gt;)
#
#####################################################################################

Function CreatePowerSchemeTile
{
    Param
    (
        [parameter(Mandatory=$true)][String[]]$SchemeGUID,
        [parameter(Mandatory=$true)][String[]]$SchemeName
    )
Write-Verbose &quot;Creating Windows shutdown tile to Start menu.&quot;

#create a new shortcut
$ShortcutPath = &quot;$env:ProgramData\Microsoft\Windows\Start Menu\Programs\&quot; + $SchemeName + &quot;.lnk&quot;
$Shortcut = $WshShell.CreateShortcut($ShortcutPath)
$Shortcut.TargetPath = &quot;$env:SystemRoot\System32\powercfg.exe&quot;
$arguments = &quot;-s &quot; + $SchemeGUID
$Shortcut.Arguments = $arguments
$Shortcut.Save()

#change the default icon of shortcut
$Lnk = $Desktop.ParseName($ShortcutPath)
$LnkPath = $Lnk.GetLink
$LnkPath.SetIconLocation(&quot;$env:SystemRoot\System32\ddores.dll&quot;,20)
$LnkPath.Save()

#pin application to windows Start menu
$Verbs = $Lnk.Verbs()
Foreach($Verb in $Verbs) {
    If($Verb.Name.Replace(&quot;&amp;&quot;,&quot;&quot;) -match &quot;Pin to Start&quot;) {
        $Verb.DoIt()
    }
}

If(Test-Path -Path $ShortcutPath) {
    Write-Host &quot;Create&quot; $SchemeName &quot;tile successfully.&quot; -ForegroundColor Green
    } Else {
    Write-Host &quot;Failed to create&quot; $SchemeName &quot;tile.&quot; -ForegroundColor Red
   }
}

$Shell = New-Object -ComObject Shell.Application
$Desktop = $Shell.NameSpace(0X0)
$WshShell = New-Object -comObject WScript.Shell
$plans = Get-WmiObject -Class win32_powerplan -Namespace root\cimv2\power
$regex = [regex]&quot;{(.*?)}$&quot;
foreach ($plan in $plans) {
    $planGuid = $regex.Match($plan.instanceID.Tostring()).groups[1].value
    $planName = $plan.ElementName.Tostring()
    Write-Debug $planGuid
    Write-Debug $planName
    CreatePowerSchemeTile -SchemeGUID $planGuid -SchemeName $planName
}
```

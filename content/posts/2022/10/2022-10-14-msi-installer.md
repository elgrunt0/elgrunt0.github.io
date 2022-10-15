---
title: "MSI Windows Installer"
date: 2022-10-14T21:42:58+01:00
draft: false
tags: ["applications", "installers"]
---

# MSI Files

These are generally easy as 3.14. If the vendor has adhered to MS standards then it should just be a case of running the MSI with:

`MSIEXEC /i setup.msi /qn`
|Parameter| Meaning |
|---------|---------------------------|
| MSIEXEC | is the install engine.    |
| /i      | means install.            |
| /qn     | means quiet, no dialogue. |

*Try: run "msiexec" in cmd to see the options.*

Things get a little more complicated when vendors start adding custom dialogues to the setup process, e.g. for serial numbers, or license server addresses, optional components, etc.

If the vendor has done it right, this should all be documented in their support pages. Often searching for "silent installation" or "unattended install" for the product will get you the info you need.

If they haven't documented it, then it is sometimes possible to glean that info straight from the MSI itself using tools like Orca.

Orca is part of the [Windows SDK:](https://docs.microsoft.com/en-us/windows/win32/msi/orca-exe)
(An alternative is [SuperOrca from Pantaray](http://www.pantaray.com/msi_super_orca.html))

Orca can be used to *see inside* an MSI file and can view or edit specific properties which can help prepare a silent install.

In this example, we have a product called BricsCAD. When installed silently with `msiexec /i bricscad.msi /qn` it automatically opens up release notes at the end of the install sequence - which defeats the purpose of silent installs.

The support website didn't document any way to suppress this action, so I decided to delve into the MSI with Orca and see if they left any properties to assist.

Once opened in Orca, we look for the Properties table and see what's there.

![](/MSI-image1.png)

Generally, the properties we care about are in CAPITALS.

We've got a few here which stand out immediately:
-   **ADDDESKTOPSHORTCUT**
-   **SHOWRELEASENOTES**

Bingo!

The default value for **SHOWRELEASENOTES** is **1**. So we can add this property to the install string to specify it as **0**.

If you recall from running '**msiexec**' in **cmd**, there is the option for **Setting Public Properties**

![](/MSI-image2.png)

So all we need to do is append the following to the silent install string: SHOWRELEASENOTES=0

`MSIEXEC /i bricscad.msi /qn SHOWRELEASENOTES=0`


# Transforms

Some applications can have a setup customiser which will generate a TRASNFORMS file (*.MST). This file contains extra settings or adjustments which can be applied to a MSI when run.

Even if not supplied, it is possible to create your own using (Super)Orca, but we will not be getting into that.

To use a TRANSFORMS file, all you have to do is put the MST file in the same directory as the MSI and run it with the command:

`MSIEXEC /i "setup.msi" TRANSFORMS="customsettings.mst" /qn`

# Logging

It can be very useful to get installation process logs, especially to find out why things go wrong before you push an application to production.

Windows Installer can provide some extremely verbose logging. Takes a bit of getting used to the logs, but hopefully can find out what went wrong.

To add logging to your setup, add the following to the command:

`MSIEXEC /i "setup.msi" /l*v C:\Windows\Temp\MyApplicationInstall.log`


# Resources
Articles

[Article: The Complete Guide to MSI Switches for Silent Software Installation (itninja.com)](https://www.itninja.com/blog/view/the-complete-guide-to-msi-switches-for-silent-software-installation)

[MS Learn](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/msiexec)
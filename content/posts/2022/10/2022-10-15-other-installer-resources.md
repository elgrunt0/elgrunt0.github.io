---
title: Other Installer Resources
date: 2022-10-15T12:50:12+01:00
draft: false
tags: ["Applications/Packaging", "Software", "Installs" ] 
---


## Setup Technologies
### MSI
See post: [MSI Installer]({{<ref 2022-10-14-msi-installer >}})

#### MSI Authoring Tools
[Wix Toolet](https://wixtoolset.org/) - Free - Hard to learn  
[Master Packager](https://www.masterpackager.com/)  - Freemium  
[MSI Installer Tool (advancedinstaller.com)](https://www.advancedinstaller.com/)  - Freemium

---
### InstallShield
See post: [InstallShield Setups]({{<ref 2022-10-14-installshield >}})

---
### Wise
Wise Setup files are a discontinued technology, but are still fairly prevalent.

Setup switches are very simple.  
ITNinja.com has an article on them here [Article: Wise Setup.exe Switches (itninja.com)](https://www.itninja.com/blog/view/wise-setup-exe-switches)

Usual silent install parameter:
`setup.exe /S`

---
### Nullsoft NSIS

Website: [NSIS Wiki (sourceforge.io)](https://nsis.sourceforge.io/Main_Page)
Nullsoft (Creators of Winamp) created their own opensoure and scriptable install system.

Once again, very simple setup switches. Usually just pass `/S` to install silently.

Review documentation on the website for more complex setups.

---
### Inno Setup

Website: [Inno Setup (jrsoftware.org)](https://jrsoftware.org/isinfo.php)

Another opensource setup system that is often used as a replacement for InstallShield.

Most common silent install parameters are:

`Setup.exe /VERYSILENT /NORESTART`

---
### InstallAnywhere

Website: [Installer and Uninstaller Command-Line Arguments (revenera.com)](https://docs.revenera.com/installanywhere2012/Content/helplibrary/ia_ref_command_line_install_uninstall.htm)

Most common silent install parameters are:
`Setup.exe -i silent`

---
## Other Software
### MSI / MST Editors
- [SuperOrca MSI Editor - Pantaray Research](http://www.pantaray.com/msi_super_orca.html)  
- [InstEd](http://www.instedit.com/)

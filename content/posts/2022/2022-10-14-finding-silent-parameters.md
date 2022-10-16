---
title: "Finding Silent Parameters"
date: 2022-10-14T21:10:43+01:00
draft: false
tags: ["Applications/Packaging", "Software", "Installs" ] 
---

If you don't know what the setup file's silent install switches are, there are a few ways to find out.

(Also, you will want the silent/unattended **uninstall** commands too.)


# RT\*M

Check the vendor documentation. Sometimes they'll provide the info needed to silently install their product. Even better if they actually provide step by step instructions on how to install via Config Manager! (But don't get your hopes up...)


# Just Bing it!

Ok, maybe not Bing, but whatever your favourite, privacy-aware search engine of choice is, you can try searching for `$Application silent install` (Where `$Application` is the name of the app you want to install silently) and perhaps someone has already done the hard work for you.

# Test

Firstly, you should get yourself a test VM. Hyper-V on your work laptop would suffice if you've got the RAM, but check with your IT Support what's allowed. Some SOC's frown upon sysadmins being able to actually do their job effectively.

With a VM, you can take snapshots of the VM and try software installs without messing up your own or other physical machine and have to rebuild every time.

Grab the install files and put in a temp directory on your test machine.

Run CMD/Terminal as administrator.

Run the setup file with `/?`

e.g. `Setup.exe /?`

Most of the time, it will give you a list or a popup of available commands that you can use to figure out how to run the setup silently.

# Test some more

If the setup doesn't give you any info on how to install silently, there is a tool called [Universal Silent Switch Finder (USSF)](https://github.com/alexandruavadanii/USSF) which can open the setup file and it will try to find out what type of setup it is and give you an idea of what the silent switches might be.  
NOTE: *You'll need to install AutoIT v3 and use Aut2Exe to compile `ussf.au3` into an EXE*

It's not 100% correct - but worth a try if you've hit a dead end.

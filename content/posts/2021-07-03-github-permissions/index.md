---
title: "Github Permissions"
date: 2021-07-03T15:06:08Z
url: /2021/07/03/github-permissions/
tags: [github]
---

# Error
When trying to `git clone` or `git push` I would get the following error:

> git@github.com: Permission denied (public key).
> fatal: Could not read from remote repository.  
> Please make sure you have the correct access rights
> and the repository exists.

To fix this, you need github to trust the machine.  
On your machine, run:  
```bash 
ssh-keygen
```

Keep it simple by just pressing Enter, Enter, Enter.  

```none
grunt@debian:~/dotfiles$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/home/grunt/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/grunt/.ssh/id_rsa.
Your public key has been saved in /home/grunt/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:w1Hjuasmd84nbfs897phkWO3dS0qlC8v9N9xClsr+rDU grunt@debian
The key's randomart image is:
+---[RSA 2048]----+
|          o      |
|         o o     |
|        . o      |
|   .   . . .     |
|  . .   S ..     |
|o. . . + o+      |
|o+ .o.+.o=E.     |
|X...o=.=o==..    |
|@B. oo=o*+oo     |
+----[SHA256]-----+
```


Keys will be stored in `~/.ssh`  
Run `cat ~/.ssh/id_rsa.pub` and copy the content.  

Open github and go to **Account Settings > SSH and GPG keys**  
Click **New SSH key**  
**Title**: machine name  
**Key**: _paste key here_  

Now try `git push` or `git clone` and it should work!
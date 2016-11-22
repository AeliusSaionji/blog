Lately, I've been learning the wonders of PowerShell and have taken to managing as much of my software as I can through [chocolatey](https://chocolatey.org/). The more comfortable I become with PowerShell, the more strongly I soured over the lack of a good way to have remote terminal access for Windows. RDP-ing into my desktop to run terminal commands just felt silly. Oh, I know about WinRM through PowerShell, and that OpenSSH's sshd _technically_ works, but neither of those solutions are actually functional, and they certainly aren't very good.

<!-- more -->

## The sub-optimal

► OpenSSH's sshd can be installed under Windows through cygwin, or through a various number of unmaintained standalone cygwin ports (all of which seem to have stopped working with Windows 8 and up, or merely do not work within a user/admin context). It also requires that you create a new user account specifically for it; it's all very messy and hack-ish. If you do manage to get it to work, what have you actually achieved? Remote access to an administrative account, under cygwin, in a non optimal terminal. That may be good enough for some, but not for me.

► PowerShell's WinRM is meant for an enterprise/corporate context. The configuration is obtuse and convoluted, as is the process to actually initiate a remote session. Although I did get it to work at one point, whenever I asked for help setting it up, the usual response from ##PowerShell@freenode was "oh, you're not on a domain? Good luck with that." Another sticking point with WinRM is that it requires a client-side administrative PowerShell terminal! SSH doesn't require superuser; I'm having a hard time rationalizing why WinRM does.

## The optimal

Luckily, I found the perfect sshd: [Bitvise SSH Server](https://www.bitvise.com/ssh-server). This has been around for a while, but for whatever reason it took me a few years to find it. Not open source, but it is free for personal use, and it is the only sane option (until perhaps Windows 10 gets native ssh).
This is sshd for Windows done right:

* Installs as a service, no extra users are created.
* Is 100% UAC compliant and UAC conscious. All settings comprehend the idea of privilege separation and work with it.
* Appears to be capable of literally anything you might do with SSH on Linux: virtual users, virtual paths, configurations for days.
* Well organized and coherent UI, complete with logging and statistics.

## Terminal elevation

OK, I've gushed over Bitvise enough. I have a clean solution for sshd on Windows, but that alone isn't enough. As everyone should, I have a regular user (Link) and a separate admin account (root). It's a bad idea to expose your root account over sshd, but since the Windows' sudo equivalent (UAC elevation dialog) is exclusive to the GUI, there is no simple way a regular user can remotely execute commands that require administrative access. I did discover it is possible to create a credential object in PowerShell, with which you may run processes as the admin user. The method is tedious to say the least, and as best I can tell, none of the processes are going to be connected to your terminal session. You will not see any output from any of the processes; it's a one-way lane.

Maybe I'm a bit daft, but just today it occurred to me that instead of disabling ssh access to root, I could simply restrict access to localhost. It's not quite sudo, it's more like su; even so, **this** is the answer I’ve been looking for! It's clean, it's easy, it's safe, and it's familiar. Simply "ssh root@127.0.0.1".
Now, I can truly administer Windows machines from a remote terminal.
I will update this post (or perhaps write a new one) with specific instructions for how to set this up. For now, here is a brief overview of what you need to do:

* Configure "Client address rules" for your root user in Bitvise. These rules are processed sequentially. You'll want to have one rule to disallow logins from any IP, and a second rule to allow logins from 127.0.0.1
* You need a terminal based ssh client to initiate the ssh connection, obviously.

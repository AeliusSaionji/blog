I use vim as my main editor, and on Windows I usually install GVim. Vim can make use of curl and git to update plugins, so I need to have those on Windows as well.

Typically, I’d install msys2 to provide my Windows install with ssh, curl, git, rsync, etc. However, now that Windows Subsystem for Linux (WSL/LXSS) exists, I figured I’d give that a spin.

<!-- more -->

The only problem is that GVim for Windows cannot easily make use of the git and curl Linux binaries tucked away in the WSL. So, I set off to see if I could just use Vim from WSL. I can! I no longer need to install msys2 or GVim.

I may not stick with this solution- the clipboard register doesn’t work, and the Windows cmd terminal might not be ideal. Time will tell.

<https://github.com/Link-Satonaka/LxVim>

## Update 2016/11/29

Well, I didn't really get along with WSL. I might return to it in the future, but for the time being I am using msys2. I have my binaries on `PATH` and the clipboard register works in vim; these things are well worth installing msys2 for. I've adapted my script to fit msys2's vim, and created a batch file with which I can associate file extensions. Enjoy!

<https://github.com/Link-Satonaka/msysVim>

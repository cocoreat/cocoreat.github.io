---
layout: post
title: Use SSH Agent in WSL2 with Git
category: thoughts
tags: [linux, wsl, ssh, git]
---

No, this is no April Fools' Day joke. Instead I'll show you how to correctly set-up the SSH-agent in the Windows-Subsystem for Linux (WSL). Like most of my posts, this is more a reminder to myself on how to do it.

## Generate SSH key

First of all, we'll need to generate a pair of SSH keys[^1]. So we run the following command in bash to create an SSH key-pair using the Ed25519-algorithm:

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```  

You will be prompted for a passphrase. Although setting a passphrase is recommended for most scenarios, there are some problems with it if you're using Git in WSL2 with SSH via Visual Studio Code, e.g. the GUI-buttons in the "Source Control"-Tab for syncing a repo will not work proberly. Therefore, the VS Code developers recommend either using the command line for pulling/pushing, removing the passphrase from the SSH key or use HTTPS for cloning[^2].
As this is my setup, I'll deliberately NOT set a passphrase. However, I'll recommend reading the following article on this topic: [Is it okay to use a SSH key with an empty passphrase?](https://serverfault.com/questions/142959/is-it-okay-to-use-a-ssh-key-with-an-empty-passphrase/142963#142963).

If you want to share the genrated SSH keys between WSL and Windows, I'll recommend the following article: [Sharing SSH keys between Windows and WSL 2](https://devblogs.microsoft.com/commandline/sharing-ssh-keys-between-windows-and-wsl-2/)

## Fix permissions

As also pointed out in the article about sharing SSH keys, the SSH-agent is very picky about local file and folder permissions. So make sure that they are set correctly[^3]:

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/config
chmod 600 ~/.ssh/id_ed25519.pub
chmod 600 /path/to/other/key/file
```

SSH config
----------

Next, we're editing our `~/.ssh/config`. We're adding the host that we want to connect to, as well as the preffered authentication mode and the path to our private key:

```text
# GitHub
Host github.com
  PreferredAuthentications publickey
  IdentityFile ~/.ssh/id_ed25519
```

We can now test if our SSH setup is working by manually starting the SSH-agent and testing the connection to GitHub:

```bash
eval $(ssh-agent -s)
ssh -T git@github.com
```

&nbsp;
## SSH-agent persistence

However, the session of the SSH-agent will not persist when opening a new terminal window or closing the last one. Therefore we will use a tool called `keychain`[^4][^5], which we probably need to install first:

```bash
sudo apt-get install keychain
```

Then let's open our `~/.bashrc` and add the following line to the end of the file:

```text
# Autostart SSH-Agent by using keychain
eval ``keychain --agents ssh id_ed25519``
```

If you now open the terminal the first time after a reboot, the SSH-agent will be started and the according SSH key will be added. If the SSH key is protected by a passphrase, you'll have to enter it only on first launch. The session of the SSH-agent will persist if you close the terminal or open an additional one.

## Footnotes

[^1]: [About SSH key generation](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent#about-ssh-key-generation)
[^2]: [Resolving hangs when doing a Git push or sync from WSL](https://code.visualstudio.com/docs/remote/troubleshooting#_resolving-hangs-when-doing-a-git-push-or-sync-from-wsl)
[^3]: [Local SSH file and folder permissions#](https://code.visualstudio.com/docs/remote/troubleshooting#_local-ssh-file-and-folder-permissions)
[^4]: [Using SSH-Agent the right way in Windows 10 WSL2](https://esc.sh/blog/ssh-agent-windows10-wsl2/)
[^5]: [Git extension in vscode in WSL window via SSH not working](https://stackoverflow.com/questions/69584056/git-extension-in-vscode-in-wsl-window-via-ssh-not-working)

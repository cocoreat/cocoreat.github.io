---
layout: post
title: Send WOL from Linux
category: thoughts
tags: [linux, wsl, ssh, git]
---

No, this is no April Fools' Day joke. Instead I'll show you how to correctly set-up the SSH-agent in the Windows-Subsystem for Linux. Like most of my posts, this is more a reminder to myself on how to do it.

I wanted to wake up one of my servers regularly by sending a Wake-On-Lan (WOL) Magic Packet from a Raspberry Pi running Ubuntu 20.04 LTS. I'm using the program "wakeonlan" to send a magic packet:

```bash
apt install wakeonlan
wakeonlan aa:11:bb:22:cc:33
```

In order to send the command on a regular basis, I've added it to the crontab configuration. First, open the crontab configuration:

```bash
crontab -e
```

Then add the command with the according schedule on the first five columns:

```text
# m h  dom mon dow   command
# minute(0-59) hour(0-23) day(1-31) month(1-12) weekday(0-6) command
0 0 * * * wakeonlan -i 192.168.1.255 aa:11:bb:22:cc:33
```

If you need more information on how to use crontab, check out this [guide](https://www.howtogeek.com/101288/how-to-schedule-tasks-on-linux-an-introduction-to-crontab-files/).

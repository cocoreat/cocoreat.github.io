---
layout: post
title: RoboRock S5 Custom Firmware Installation
category: projects
tags: [homelab, iot]
---

Update 2020-09-07
=================

FYI: The experimental patch, which I've included in the last build of the firmware image is still working.

--- 
&nbsp;

Update 2020-05-07
=================

My robot resetted itself to factory settings. That is a known bug when using custom firmwares. So this time when building the firmware image, I've enabled an experimental patch for it. These are my current settings:

![DustBuilder Settings](/assets/img/posts/2020-05-07/dustbuilder-settings.JPG)

Let's see if it helps. 

Oh, and if you are searching for voice packs, you'll find them here: [https://dustbuilder.xvm.mit.edu/pkg/voice/](https://dustbuilder.xvm.mit.edu/pkg/voice/)

And there is now another project on Github, where you can get pre-compiled firmware images: [https://github.com/zvldz/vacuum](https://github.com/zvldz/vacuum)

---
&nbsp;

Original Post 2020-03-21
=======================

I wanted to get a vacuum cleaner robot for some time now. Actually, I've already owned one more than a decade ago. But it was a silly one, which was just changing direction when it bumped into something. After some of the sensors broke (which unfortunately couldn't be fixed easily) I was putting the topic aside.

Nowadays smart vacuum cleaners have fancy laser sensors, which allow them to navigate quickly through a room. The downside is, that in order to use all features you've to connect your device to some cloud where all the information (e.g. the layout of your apartment) is stored.

Therefore I was buying a RoboRock S5 after checking that it allows the installation of custom firmwares to circumvent the cloud connection. In order to achieve this, I was basically following this [guide on selfhostedhome.com](https://selfhostedhome.com/cloud-free-smart-vacuum-valetudo-for-roborock-s5/) 

I'll quickly go through the necessary steps:

Extract security token
======================

Before anything else, we need to make sure that we can actually communicate with our robot. For this to work we need to extract a token, which the robot is using to communicate to its app. 

The easiest way to do this is to use an old version of the Mi Home app. I've been using version 5.4.54 and saved the APK-file for later use. Out of security concerns I don't want to recommand a webpage where you can download the APK, but you'll find a link on this [other guide on selfhostedhome.com](https://selfhostedhome.com/zoned-cleaning-with-the-xiaomi-roborock-s5-robotic-vacuum/).

Once you have the app, log in with your Mi-Account (or create one if you haven't already) and follow the instructions to connect your robot.

The advantage of using the old version of the app: You can access the app's log files on your phone. Just open your file browser and find the *SmartHome/logs/plug_DeviceManager* folder. After connecting to your robot successfully, search for the token string in the most recent log file. It will look something like this:
```json
SmartHome 328:[DEBUG]-03-21 15:18:38.177 processResult in result=
{"code":0,"message":"ok","result":{"list":[{"did":"261921897",
"token":"35774d584b45777143634964304c6c6a", ...
```

If there are no log files, then either you've the wrong version of the app, or you'll need to start a vacuum clean first.

Build custom firmware image
===========================

You can either go to the [DustCloud Github-Repo](https://github.com/dgiese/dustcloud), clone it and follow the build instructions to build the firmware image yourself, or you can trust the developer and let him build the image for you by using [DustBuilder](https://builder.dontvacuum.me/). I was using DustBuilder. 

Those were the settings that I've been using:

![DustBuilder Settings](/assets/img/posts/2020-03-21/dustbuilder-settings.JPG)

However, the options for DustBuilder can change frequently, so you should read the instructions on the website carefully. Just make sure to integrate the public key of your SSH-key-pair (or let the builder create a pair for you) and to select the correct vacuum model.

I also recommend to include [Valetudo RE](https://github.com/rand256/valetudo) in your firmware image. It'll provide you with a nice web interface for controlling your robot.

Once you submitted your build request, you can grab a cup of coffee. It can take a while until it is mailed to you.

Install custom firmware image
=============================

After getting your E-mails from DustBuilder, downloading the image and verifying its hash, you can finally install it.

For flashing the firmware image I was using the [RoboRock Control Center](https://github.com/LazyT/rrcc). The application is pretty self-explanatory: After starting the application the first time, you'll be prompted to connect to your robot. All you need is its IP and the token we've extracted earlier.

![RRCC Connection](/assets/img/posts/2020-03-21/rrcc-v088-01.JPG)

Once we've connected successfully, navigate to the firmware menu item and click on update. You'll hear the robot announcing the start and the end of the firmware update. The update can take quite long (up to 10 minutes). So just wait for it to finish. 

![RRCC Connection](/assets/img/posts/2020-03-21/rrcc-v088-02.JPG)

Once the custom firmware was installed successfully, you can access the Valetudo web interface by navigating to the robot's IP in a web browser.

That's it.

Related Readings
================

&raquo; [DustCloud](https://github.com/dgiese/dustcloud)  
&raquo; [DustBuilder](https://builder.dontvacuum.me/)  
&raquo; [DustBuilder (old URL)](https://dustbuilder.xvm.mit.edu/)  
&raquo; [Valetudo RE](https://github.com/rand256/valetudo)  
&raquo; [RoboRock Control Center](https://github.com/LazyT/rrcc)  
&raquo; [Firmware builder by zvldz](https://github.com/zvldz/vacuum)  
&raquo; [Voice packages](https://dustbuilder.xvm.mit.edu/pkg/voice/) 
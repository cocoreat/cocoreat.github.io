---
layout: post
title: Managed Service Accounts
date: 2020-03-04 12:00:00+0100
category: thoughts
tags: [active directory, service accounts]
---

{{ page.title }}
================

<p class="meta">Published: 04 Mar 2020</p>

I had to set up a service account in AD for one specific application, which was running on just one server. I've decided to write this process down, because if you're searching for "Managed Service Accounts" (MSA) your first results will most probably be about ["Group Managed Service Account (gMSA)"](https://docs.microsoft.com/en-us/windows-server/security/group-managed-service-accounts/group-managed-service-accounts-overview), which is basically an evolved form of service accounts (and too complex for my needs in this case).

So, let's start. In order to create a MSA in AD, I use the following Powershell-Cmdlet. Please notice the parameter *RestrictToSingleComputer*, which will make it an ordinary MSA.
```powershell
New-ADServiceAccount -Name MSA-Name -RestrictToSingleComputer -Enabled $true
```

To bind the newly created MSA to a computer, we'll run the following Cmdlet.
```powershell
Add-ADComputerServiceAccount -Identity Computer-Name -ServiceAccount MSA-Name
```

In order to use the MSA on the computer we've just specified, it needs to be installed there. This is done by running the following Cmdlet on the computer, where it should be installed.
```powershell
Install-ADServiceAccount -Identity MSA-Name
```

Now you can run a service on this computer in context of the MSA. Just open the service's properties and navigate to the *Log on* tab. The MSA needs to be entered in the following form: *domain\<MSA-Name>$*
The password fields need to be left empty. On clicking *Apply* or *OK* you'll get a warning, that the MSA got the permission to log on as a service. 

Related Readings
================
[New-ADServiceAccount](https://docs.microsoft.com/en-us/powershell/module/activedirectory/new-adserviceaccount)
[Add-ADComputerServiceAccount](https://docs.microsoft.com/en-us/powershell/module/activedirectory/add-adcomputerserviceaccount)
[Install-ADServiceAccount](https://docs.microsoft.com/en-us/powershell/module/activedirectory/Install-ADServiceAccount)
---
layout: post
title: Batch Create AD User Accounts
category: thoughts
tags: [active directory, powershell]
---

I had to create quite a lot of AD user accounts. To facilitate the task, I've used the PowerShell according to [instructions from the TechNet-Community](https://social.technet.microsoft.com/wiki/contents/articles/25111.creating-batch-users-in-active-directory-using-powershell.aspx).

I've created a CSV-file with six columns: Name, UserPrincipalName, SurName, FirstName, Displayname, Password

~~~csv
Name,UPN,SurN,FirstN,DN,Pass
cocoreat,cocoreat@domain.local,Repeat,CoffeeCode,CoffeeCodeRepeat,Password
~~~

Then I've used the the PowerShell-Cmdlet "New-ADUser" to iterate over the file and create the user accounts with their properties.

~~~powershell
$users = Import-Csv CreateUsers.csv
$users | ForEach-Object { New-ADUser -Path 'OU=PCs,DC=lab,DC=wu,DC=ac,DC=at' -Name 
$_.Name -Surname $_.SurN -GivenName $_.FirstN -UserPrincipalName $_.UPN -DisplayName 
$_.DN -AccountPassword (ConvertTo-SecureString -AsPlainText $_.Pass -Force) -Enabled 
$True}
~~~

Related Readings
----------------

&raquo; [Import-Csv](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/import-csv)
&raquo; [New-ADUser](https://docs.microsoft.com/en-us/powershell/module/addsadministration/new-aduser)  
&raquo; [ConvertTo-SecureString](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.security/convertto-securestring)

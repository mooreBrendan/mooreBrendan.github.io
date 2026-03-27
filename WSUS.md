# ~~WSUS~~

## Purpose
WSUS (Windows Server Update Service) is windows update service that allows you to control updates for your other windows servers.  This means you can download updates locally to one computer and then your other servers can just download updates off of that server, saving external bandwith and allowing faster downloads overall as intranet connections are typically faster than external connections.  You can also manage which updates to approve and when so that you can hold updates to see if others report issues with the update.


## Setup


## Installation


## Group Policy Setup
Computer Configuration/Policies/Administrative Templates/Windows Components/Windows Update
"Configure Automatic Updates", enable, 4-download & schedule install, day, time, install updates for other microsoft products, apply

"Specify intranet Microsoft update service location", enable, enter link as http://server:8530 (if you have certificates setup, use https://server:8531 instead) for both server and statistics server.  If you have an alternative server, you can use that as well.  apply

"Automatic Updates detection frequency", enable, interval 1 hour, apply

close the edit window

open powershell on the domain controller as an administrator, enter `gpupdate /force` to manually force an update of the group policies.  Do the same for any client servers.


## Configure HTTPS

## Verification

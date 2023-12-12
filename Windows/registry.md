#windows
### 2 main folders, all others are subfoldera
---
HKEY_LOCAL_MACHINE
	HKEY_CURRENT_CONFIG
HKEY_USER
	HKEY_CURRENT_USER
		S-1-5-18 -> this is the reference to a specific user


each registry folder can have his own ntfs permissions.

## modifying the registry settings:
- control panel
- mmc
- powershell
- regedit

## create a backup of the registry

file -> save ->

## user account database
only local on each machine
SAM database -> store for local user credentials


## First user on a machine is automatically the administrator of that machine.

## UAC
Since windows 8 , a user with admin permissions will always be prompted before he can actually perform a administrative action.
this is an extra security measure, so that a admin users not always has his admin privileges.

## services

A list with all the daemons which defines what has to be started during boot of os.
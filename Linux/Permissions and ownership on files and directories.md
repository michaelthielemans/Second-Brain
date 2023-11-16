#linux 

	u = user-owner = owner of the file
	g = group-owner =  group owner of the file
	o = other  = all other users

	rwx = read write execute
	x => only usefull on executable files
## setting permissions with symbolic notation
#### adding permissions
	chmod o+rwx filename
#### removing permissions
	chmod o-x filename
#### make permissions exactly
	chmod o=rx filename

## Permissions effects on directory

	r = only read the content of the folder =  lists names of files and subfolders
	x = cd into the folder + list extra metadata, but cannot show names of files inside the directory
	w = add files or directories in the directory
	write access without execute is useless because you have not the necessary permissions to store the extra needed metadata, so ...
	
> [!info] W needs X !!! 

## Special permissions - setuid - setgid - sticky bit

### setuid on files

Setuid , a script or application that is the owner of the file where the setuid is set, a user without any special permissions can modify the file.
A user can have write permissions on a file via a script or application.

> example -> /etc/shadow file
> the tool passwd is owner of the shadow file, a standard user has no permissions at all on that file, but with the setuid flag set a user can modify the shadow file via the passwd tool.

> [!info] setuid and setgid are like -> run as administrator

### Setgid on folders

> when the setgid flag is set on directories, all files and subfolders automatically will inherit the same group-owner as the parent directory.

>[!info] Force group-owner inheritance from parent folder

### sticky bit




| | user-owner | groupID | other|
|--|--|--|--|
|standard | rwx|rwx|rwx|
| setuid - setgid - stickybit |rw<u>s</u>|rw<u>s</u>|rw<u>t</u>|

| octal notation | setuid | setgid | sticky bit |
|--|--|--|--|
|setuid| 4777 | 
|setgid | 2777 | 
|sticky bit| 1777|




## Permission priority

> [!info] The user-owner priority always wins
If the permissions on a file is u=---, g=rwx, o=--- , then the user-owner has no access to the file even if he is a member of the group-owner group.

## Ownership on files and directories

Ownership can only be modified by user with root privileges
group ownership can be modified by root and user-owner of the file IF he is also a member of the new owning-group

	chown <newowner>:<newgroup> filename/dirname
	chgrp <newgroup filename/dirname

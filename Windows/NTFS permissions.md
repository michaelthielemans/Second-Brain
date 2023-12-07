#windows 
#### Can be applied on:
- NTFS partitions.
- registry
- MSSQL
- mailservers

>[!warning] NTFS permissions cannot be set on FAT volumes ( FILE Allocation Table)
### inheritance
Disable inheritance -> copy permissons or delete permissions


#### implicit groups
- authenticated users
system owned groups

#### explicit groups
all groups that are manageable by the adminf


### Permissions conflicts

- multiple allow permissions on from
	- => highest allow wins
- Allow and deny permissions
	- => deny wins
- permissions given through inheritance + conflicting permissons directly set on the object(folder, file,..)
	The directly set permissions wins!
## Deny permissions scenario -> examen vraag

>[!error] allow permissions = most permissive wins

>[!error] deny permissions = always overrules 'allow' settings

> allow -> full control
> deny -> read + execute
> directly set permissions(added permissions on a subfolder on top of inherited permissions) overrule inherited permissions.

in order to have 'execute' permissions you always need 'read'

### Powershell get permissions set permissions
```
get-acl 'foldername'
set-acl
```
### Copy versus move

|   |   |   |
|---|---|---|
|c: to another location on the c:|The copied file is a new file, created in a new target location and will inherit the permissions of the target folder.|Moving from one folder to another folder on the same drive, let’s you keep the permissions of the original location.|
|From the c: drive to another drive on the computer or on the network|The copied file is a new file, created in a new target location and will inherit the permissions of the target folder.|Moving from one drive to another drive is a “copy & delete” operation. Since you copy the file that you are moving first, you don’t keep the original file permissions , but inherit the permissions on the target folder.|




## Ownership

### The ownership permission on a file is:
gives you the ==ability to TAKE== ownership

### The ownership property on a file is :
defines ==WHO== is the owner

### Take ownership of files or folders” user RIGHT
independent of NTF permissions this settings is configured in the registry and overrules NTFS ownership.

this setting can be adjusted with a local group policy, regedit(HKEY_local_machine), powershell


## Sharing


## Auditing

enable auditing on a ntfs file. All actions on a folder or file will be audited and saved in the eventviewer -> windows logs -> security.

-> disabled by default.

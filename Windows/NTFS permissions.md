#windows 
#### Can be applied on:
- NTFS partitions
- registry
- printers
- MSSQL
- mailservers

>[!warning] NTFS permissions cannot be set on FAT volumes ( FILE Allocation Table)
### inheritance
Disable inheritance -> copy permissions or delete permissions
#### implicit group
- authenticated users
system owned groups

#### explicit groups
all groups that are manageable by the admin

## Inheritance and precedence

>inherited permissions = permissions coming from parent
>explicit permissions = set on folder or file

## Precedence from highest to lowest prio

1. explicit deny
2. explicit allow
3. inherited deny
4. inherited allow
### Permissions conflicts

- multiple allow permissions on from
	- => highest allow wins
- Allow and deny permissions
	- => deny always wins
- permissions given through inheritance + conflicting permissions directly set on the object(folder, file,..)
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

| location  | COPY  | MOVE  |
|---|---|---|
|On the same NTFS volume |The copied file is a new file, created in a new target location and will inherit the permissions of the target folder. = NEW PERMISSIONS |Moving from one folder to another folder on the same drive, let’s you keep the permissions of the original location. The file itself is not moved only the pointer link to the file is altered. = PERMISSIONS ON THE FILE WILL BE PRESERVED |
|To another NTFS volume |The copied file is a new file, created in a new target location and will inherit the permissions of the target folder. = RECEIVES NEW PERMISSIONS |Moving from one volume to another volume is a “copy & delete” operation. Since you copy the file that you are moving first, you don’t keep the original file permissions , but inherit the permissions on the target folder. = RECEIVES NEW PERMISSIONS |
## Ownership

The owner of a NTFS resource:
	- has full control on the resource
	- can change permissions on the resource
	- Transfer ownership to another user or group
	- 
### The ownership right on a device:
gives you the ==ability to TAKE== ownership of all NTFS objects on that device. This is a security POLICY setting and not a NTFS permission!!

### The ownership property on a file is :
defines ==WHO== is the owner

### Take ownership of files or folders” user RIGHT
independent of NTF permissions this settings is configured in the registry and overrules NTFS ownership.

this setting can be adjusted with a local group policy, regedit(HKEY_local_machine), powershell

### Ownership for administrators
if a user is a member of the administrator group, all files he creates will be owned by the administrators group, this means that other administrators also have owner privileges
## NTFS permission levels

### Full control
> - can take ownership
> - change permissions
> - has read, write, modify

### Modify
> - can modify the content
> - change the name of a file or folder
> - create new file or folder in a folder
> - delete content or folders/files


## Auditing

#### Policy auditing
Auditing can be enable with a policy -> at the end this will alter a setting in the registry
Different types of auditing can be enabled in the policy console.

### NTFS auditing
>[!warn] to enable NTFS auditing you first have to enable the policy setting ' audit object access'  ->> values. 'success' or 'failure'


Enable auditing on a ntfs file. => is a tab in the advanced security setting on a file or folder
- All actions on a folder or file will be audited and saved in the eventviewer -> windows logs -> security.

NTFS auditing is disabled by default.

all auditing events can be viewed in the 'eventviewer'

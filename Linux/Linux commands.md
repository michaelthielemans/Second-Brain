#linux
## System commands
##### CPU
>`arch`
>`lscpu
>`uptime`
#### memory
> `free -m`
#### peripherals
> `lspci`
> `lsusb`
#### Storage (hard disks)

formatting and partitioning
> `fdisk` -> mbr disks (older)
> `gdisk` -> gpt disks (newer)
> parted -> new
## User and group commands
#### show user info
```
last 
last b #failed logons
who 
w 
id 
groups
```

#### user and group configuration
```
useradd -u <userid>  #create user with default settings but with specific userID
useradd -D  #change the default settings
useradd -g <primaryGroupname> <username>
useradd -G <secondaryGroupname> <username>
useradd -M <username> #do not create a homedir
useradd -m <username> #create always a homedir
useradd -mk <skeletonpath> <username>
useradd -c <comment> <username>

usermod -aG <secondaryGroupname>

userdel -r <username> # will remove the homedir as wel

groupadd -g <groupID> <groupname>
groupadd -r <groupname> specify group ID lower than 500 or 1000
groupmod -n <newgroupname> <oldgroupname>
groupmod -g <newgroupid> <groupname>
groupdel

```

### Files info
>`stat <filename>`  -> show all information about a file
## [[Permissions and ownership on files and directories]]

>	chmod 755 <filename>
>	chmod ugo=rx
>	chown <username>:<groupname> filename
>	chgrp <groupname> filename

## Listing and finding

	find <path> -nogroup. #find all orphaned files

## Time and scheduling

```
datetimectl
crontab -l # list crontab settings
crontab -e  # edit the crontab of the current user
crontab -u <username> -e # edit crontab of other user

```
## Viewing text files
```
more (depricated)
less
head
tail
```

## Filtering and editing text
```
grep <pattern> filename
grep -c (linecount) -n (linenumbers) -v (invert) -i (not case sensitive) -w (whole words)
cut -d <delimiter> -f1,2,3 filename
wc -l (word count -> -l lines , -w words, -c chars)
sort -t <delimiter> -k2 -n -r (sort field 2, numeric, reverse)
```
## [[Logging]]

	journalctl /var/log/logfilename
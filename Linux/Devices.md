#linux
All devices can be found in
/dev/

## storage devices
/dev/hd -> IDE disks
/dev/sd -> sata, scsi, USB disks

/dev/sdb2
b2 means disk b with partition 2

## mounting storage devices
### removable storage
mount in /media/...

### non-removable storage
/mount in /mnt/....

### mounting and unmouting

permanent mounting -> /etc/fstab

mount all device that are specified in fstab:
```
mount -a
```

unmount a specific disk or partition:
```
umount /dev/sdb2

```
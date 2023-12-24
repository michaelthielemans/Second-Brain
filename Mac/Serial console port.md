#mac
## Check for serial terminal devices
> There are 2 different methods:

You notice that each serial device shows up twice in /dev, once as a tty.* and once as a cu.\* So, what's the difference? Well, TTY devices are for calling into UNIX systems, whereas CU (Call-Up) devices are for calling out from them (eg, modems). We want to call-out from our Mac, so /dev/cu.* is the correct device to use. 

The technical difference is that /dev/tty.* devices will wait (or listen) for DCD (data-carrier-detect), eg, someone calling in, before responding. /dev/cu.* devices do not assert DCD, so they will always connect (respond or succeed) immediately.

```
ls /dev/cu.*
```

```
ls /dev/tty.*
```
## check if the 'file' is already in use

```
lsof /dev/tty.*
or
lsof | grep usbserial

screen 18085 michaelthielemans 5u CHR 9,2 0t6160 731 /dev/tty.usbserial-1120
```

The PID is 18085 !!
### If the file is not in use

```
screen /dev/cu.usbserial 9600

-or-

screen /dev/tty.usb.......... 9600
```

### If the file is already in use
```
screen -x 18085
```
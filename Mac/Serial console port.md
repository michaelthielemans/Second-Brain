#mac
## check for serial terminal devices
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
screen /dev/tty.usb.......... 9600
```

### If the file is already in use
```
screen -x 18085
```
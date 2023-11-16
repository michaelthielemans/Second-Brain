#cisco
## boot sequence

1. start POST from ROM
2. load bootloader from rom and start the bootloader
3. Bootloader does initial memory configs
4. bootloader initializes the flash file system
5. bootloader loads and starts the IOS and hands over control to the os
6. IOS starts and initializes interfaces using the commands from the startup config
7. -> the startup config is the config.txt file on flash

## Files on Flash

IOS is located on the flash xxxxxxxxx.bin
## recovery from a system crash:

1. power on -> within 15s press and hold syst button until system led is steady green
2. `switch: set`
3. `switch: flash_init`
4. `switch: dir flash:`

## Switch LED
SYST: green = ok, amber = fault
RPS:
STAT: off=no connection on port | green=
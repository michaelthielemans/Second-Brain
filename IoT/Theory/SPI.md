#IoT
### Enable SPI on the raspberry / orange pi
sudo nano /boot/orangepiEnv.txt and add  
    overlays=spi-spidev1
    CTRL+X and save
    reboot
#### PINS
- MOSI: Master Out Slave In
- MISO: Master In Slave Out
- CLK: Clock
- CS: Chip Select

Is a Synchronous protocol:
- SPI is a “synchronous” data bus
- It uses separate lines for data and a “clock” that keeps both sides in perfect sync
- Full duplex

**Advantages of SPI:**
- It’s faster than asynchronous serial
- The receiving hardware can be a simple shift register


Multiple slaves with SPI:
- Each slave will need a separate SS (slave/chip select) line.
- To talk to a particular slave, you’ll make that slave’s SS line low and keep the rest of them high   (two slaves can’t be activated at the same time)
- We will use this method for the AD convertor and an LCD display
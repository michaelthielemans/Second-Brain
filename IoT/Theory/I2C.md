- It only requires 2 wires:
	- SCK: Serial Clock
	- SDA: Serial Data
- It is slow
- It is a synchronous protocol, It has a common clock (SCK from the master)
- Master/slave or controller/peripherals
- BI-directional communication
- For short distances
- Every device has a preset-ID, with addressing the controller can target a specific device
- The bus is Active LOW -> pull up resistors are used so Voltage = Vcc at rest

### Data sequence
8 bit (one Byte) is one sequence
 
1. Start bit (1 bit)
2. The first sequence that is 8 bit (1 Byte)
	1.  Contains the target device address (7 bit)
	2. plus the R/W bit. this defines if the master wants to read data from the device or write data to the device.
	3. If the device has a register, the controller need to send the 7 bit address completed with a write bit (0). The device now knows that the controller wants to send another address (the register address)
3. Acknowledge bit (1 bit)
4. The second sequence contains the internal register address (8bit)
	1. a internal register is needed for example when a device has multiple sensors and each register contains a value from a specific sensor.
5. Acknowledge bit (1 bit)
6. The actual data payload (8 bit), MSB first
7. Stop bit (1 bit)

##### Start transmission (start bit):
When the SDA line falls from High to LOW = start of transmission

##### Stop transmission (stop bit):
When the SDA line 

| first bit | 7bit addressing       | R/W bit                                 | ACK bit                                                      | 8bit data | stop bit |
| --------- | --------------------- | --------------------------------------- | ------------------------------------------------------------ | --------- | -------- |
| start     | address of the device | bit = 0 -> data is written to device    | The device itself should now make the sda low or high to ack |           |          |
|           |                       | bit = 1 -> data is read from the device | NACK -> SDA = high<br>ACK -> SDA = LOW                       |           |          |

One ore multiple data sequences are transferred until a stop bit is send/received.


## Serial connections
#### Pins:
- RX: receive
- TX: Transmit
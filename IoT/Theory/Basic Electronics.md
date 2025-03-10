#IoT
## Ohms law

Resistance in serie:
Rt = R1 + R2  + R3

Resistors in parallel:
Rt = 1 / (1/R1 + 1/R2 + 1/R3)

## LED basics

| Anode   | +   | longer leg  | anvil( semicondutor die) |
| ------- | --- | ----------- | ------------------------ |
| Kathode | -   | shorter leg | post                     |
#### Threshold voltages of leds
- Allowed current range: 5mA -> 20mA ( commonly = 10mA)
-  voltage: 
	- **Infrared**: Less than 1.9V
	- **Red**: 1.7 to 2.2V
	- **Orange**: 2.0 to 2.2V
	- **Yellow**: 2.1 to 2.4V
	- **Green**: 2 to 2.3V
	- **Blue**: 3.2 to 4.0V
	- **Ultraviolet**: 2.1 to 3.8V
	- **White**: 3.3 to 3.6V
#### Calculate the Led Resistor

The value of the resistor you have to place before the LED is:
(the total voltage minuis the voltage over the led ) devided be the allowed current through the led
R = (Utotal- Uled)/ I

## Types of Resistors and color codes

### Koolstof weerstanden
- goedkoper
- 4 banden kleurencode
- licht bruine kleur behuizing

#### Kleurencode:
1e band: waarde
2e band: waarde
3e band: multiplier
4e band: tolerance

### Metaal film weerstanden
- Nauwkeuriger
- 6 banden kleurencode
- licht blauwe kleur van de behuizing

#### Color code:
1e band: value
2e band : value
3e band: value
4e band: multiplier
5e band: tolerance
6e band: temp coefficient
## Transistors

#### NPN transistor
- Collector +
- Base -> should be more positive than the emitter 
- Emitter -

In cut-off state :
- There is no positive voltage on the base (not more positive that the emmiter)
- There is no current flowing from collector to emmiter.

In a conductive state:
- A voltage higher than 0.7 V is applied to the base, you need to overwin the threshold voltage
- A small current from base to the emitter will flow
- A large current between collector + and emitter can flow.

#### PNP transistor
Collector -
base : apply a negative voltage to get in a saturation state
emmiter: +

#### Cut-of phase:
no current from the base -> current from collector to emitter is blocked

#### Saturation phase
Little base current -> current from collector to emitter can flow
There is still a small resistance that is inherit to the transister. 

### Drempel spanning of threshold voltage:
Base <-> emmiter : silicium= 0.8 V , germanium = 0.3V
Collector <-> emmiter: 0.3 V ( it depends on how big the current is that flows through the transister)

## Stepper Motor
- The stepper motor has 4 coils.

Wave drive:  One coil at a time is enforced
Full step: two coils at a time are enforced.
## Pull up and pull down resistors

Remember!
- In the rest state the pull up will pull the pin to the Vcc.
- In the rest state the pull down will pull the pin to the GND.
#### Pull down resistor
- The resistor is placed between the input port and the GND
- When the contact is open the resistor will make sure that the tension on the input port will be kept low.
#### Pull up resistor
- The resistor is placed between the input port and the Vcc


**Why we need pull ups and pull downs**
Never leave a input "hanging in the air", it will start flipping between the + and - state
Or you connect it to the ground (LOW)
Or you connect it to the Vcc (high)

## LDR - Light Dependend Resistor

More light = lower resistance
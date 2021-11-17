# Cabin Area Network

This is a system for basic housekeeping tasks such as getting sensor data on temperature, humidity, other weather indicators, or sending alerts when local fauna such as bears or coyotes have entered the garden area. The network can also be used for signalling devices to turn on or off such as floodlights connected to solar charged batteries, well pumps, windows on greenhouses, or fans installed in outdoor composting toilets.

All devices on the network act independently without the use of a "Master" controller, which greatly simplifies signalling. Each device has an independent ID, which also doubles as its priority. The basic premise of the network is based on the Controller Area Network, or CAN bus, with elements borrowed from other robust systems.

Work in progress...

## Rationale 

While the basic operation of various CAN bus systems is well known, the actual details are often opaque and difficult or impossible to modify. Most CAN components are proprietary and communicate via various hardwired schemes. Reusing off-the-shelf components and other simple electronics should be sufficient to create an alternative which, although significantly limited compared to commercial and proprietary counterparts, is still capable of many ordinary tasks while remaining relatively robust. This system will also implement device self-addressing which can be modified without special equipment while in operation.

**IMPORTANT** **: This system is not intended to replace mission critical applications, such as in vehicles, where the risk to human life in the event of a failure is unacceptable.**

## Concept

Communication between devices is through a single pair of twisted wire designated "CAN High" and "CAN Low", ideally with a grounded shield, which is specially terminated on each end. Using twisted pairs is highly recommended. If twisted pair cable is not available, at least a conductive ground shielded wire pair is recommended. The wire pair is referred to as the "bus".

Devices communicate by sending and receiving messages based on address priority. The physical location of each device on the bus is irrelevant to its priority. Priority "arbitration" is built into the hardware of the transmit/receive buffer and requires no further processing on the device itself. The message with the lowest address (in binary) gets priority. The address is eight (8) bits long, which allows for 255 unique devices on the same bus. The builder of this system may add any number of addresses as necessary to fit their own purposes as long as the address length is consistent.

A baseline voltage of 2.5V is maintained on both CAN High and CAN Low by the connected device. The maximum current draw of the bus is limited by the transceiver/buffer to 150mA. This is to reduce power consumption and to prevent damage to components in the event of a dead short across the two wires of the bus or to ground. I.E. Rodent damage, accidental shovel strike of a buried line etc... 

### Messaging

Communication to and from the bus passes through the buffer. Physical device arrangement: Bus - Buffer - Device. The buffer transmits its own address before sending the device payload to the bus.

Messages start with a "0", which acts as an intent to send. The message length is up to the builder's preference. Since this is intended for simple tasks that aren't mission critical, there is only an address and data. In more durable systems, there should be a length value and checksum value added to messages.

This message has the highest priority and its data is 32 bits in length:

| I | Address	| Data					|
|---|-----------|-----------------------------------------|
| 0 | 0000 0000	| 0000 0000 0000 0000 0000 0000 0000 0000 |

The message "frame" is therefore 41 bits in total in this particular implementation. 

This message has a lower priority than the one above:

| I | Address	| Data					|
|---|-----------|-----------------------------------------|
| 0 | 0000 1100	| 0000 0000 0000 0000 0000 0000 0000 0000 |

This message has the lowest priority of all 255 possible addresses on the bus in this implementation:

| I | Address	| Data					|
|---|-----------|-----------------------------------------|
| 0 | 1111 1111	| 0000 0000 0000 0000 0000 0000 0000 0000 |

Message frame length should be kept consistent throughout the builder's preferred implementation. The address of each device should be unique on each bus, if it's meant to transmit any data, and can be set via an 8 position DIP switch or similar. Addresses can be modified after installation without having to reprogram the attached device. This allows for easily changing device priorities in the field at a later date.

### Devices

All devices receive all message data payloads on the bus at all times. 

The devices connected to their bus transceiver/buffer should be electrically isolated as much as possible. E.G. Only communicate via optocouplers to the buffer, regulated power supplies if they may share the same power source etc... Each connected device may be given a specific device name or destination as a portion of the 32 bit data payload. The device itself need not know their physical addresses on the bus, but it may be easier to debug if the bus address (set via the 8 DIP switches) is the same as the device destination name. 

One possible arrangement of the 32 bits of the device data payload:

| Destination	| Origin	| Word/Function	| Value		|
|-----------|-----------|-----------|---------------------------|
| 0000 0000	| 0000 0000	| 0000 0000	| 0000 0000	|


Many different devices may have the same origin or destination address, however for sensors, it is recommended that the origin be unique and the buffer address priority be higher as well. A device may be configured to ignore the rest of the 32 bits of the data payload if its name isn't in the destination. Or it may note the destination if the connected device is a logger or monitor of some sort. The word or function is also up to the system builder.

E.G. A possible message from a monitor or user console somewhere on the bus to an electric fan to turn on for 30 minutes:

| Destination	| Origin	| Word/Function	| Value		|
|-----------|-----------|-----------|---------------------------|
| 0100 0110	| 1000 1000	| 0000 0010	| 0001 1110	|

In this case, the destination, 0100 0110, is the device name of the fan and not the fan's bus address, both of which are entirely up to the builder of the system. The origin, 1000 1000, could be the name of the console. The device can be configured to only accept commands from a specific origin(s). The word or function name is similarly arbitrary and, in this example, is the fan on command of 0000 0010. The value is 30 in 8 bit binary as 0001 1110.

E.G. An elevated temperature alert in the chicken coop could indicate a fire or the presence of an intruder, such as a fox.

| Destination	| Origin	| Word/Function	| Value		|
|-----------|-----------|-----------|---------------------------|
| 1000 1000	| 0100 0110	| 0100 0000	| 0000 0011	|

The destination is the monitor or user console in the above example while the origin is another arbitrary address given to a temperature sensor. The word or function indicates here a possible temperature rise. The value indicates a 3 degree increase on the builder's preferred temperature scale in a short period of time.

Function names, and even the device name, may be created with simple logic gates and need not be stored on a microcontroller. Function execution may be carried out with transistors connected to MOSFETs.

### Signalling

The connected device sends a Request to Send (RTS) signal to its buffer indicating it's ready to transmit its payload of 32 bits. The buffer checks for traffic on the bus for 41 clock pulses, the length of a "frame" in this particular implementation, and sends intent to send (I, which is always "0"), followed by the eight digit address. With each clock pulse and digit transmission of the address, the buffer checks if the value it is sending is the same on the bus.

A value of one "1" is 2.5V on both CAN High and CAN Low, same as the baseline voltage. A value of zero "0" pushes CAN High up to 3.5V and CAN Low down to 1.5V. This [differential signalling](https://en.wikipedia.org/wiki/Differential_signalling) reduces the effect of noise and allows the buffer to detect if the transmitted digit is the same when it reads it back. Since the Intent to transmit is "0", if two or more buffers happen to transmit the same "0", there should be no contention and transmission can continue.

Since "0" is "louder" (3.5V/1.5V High/Low) than "1" (2.5V both), the buffer will stop transmitting if the "1" in its address causes it to lose arbitration to a "0" of another buffer at any point during its address transmission phase. The buffer will keep trying as long as its connected device indicates RTS and it hasn't detected a "0" on the bus for the last 41 clock pulses. Any number of devices up to the maximum address size may participate in this arbitration since very little current is drawn by the bus itself.

If the transmitting buffer "wins" arbitration, it will send a Clear to Send (CTS) signal back to the connected device which will send its 32 bit payload, digit-by-digit, with each clock pulse which the buffer will immediately push to the bus.

When a device is first connected to the bus or powered on, it will listen on the bus for an address with higher priority than its own. Once detected, it will "bump" or sync its clock pulse to the last verified (not noise) pulse to ensure it can communicate synchronously. Periodic clock syncs are recommended over time to ensure devices don't drift too far away from each other.

Arbitration at the hardware level in this manner can be accomplished with simple electronics such as transistors, op amps, and discreet logic without the use of a microcontroller. E.G. The RTS and CTS can be detected with a logical AND gate IC such as the CD4081.

### Wiring

Bus end termination when a grounded shield is available:

![CAN bus termination](https://raw.githubusercontent.com/cypnk/Cabin-Life/master/Cabin%20Area%20Network/Wiring/canbustermination.png)

The other end follows the same scheme, but it is not connected to any other "Earth" on its own, except the shield, to avoid ground loops. 

The wire pair is linked together with two 68ohm resistors connected in series and linked to ground via three separate capacitors in parallel. This method reduces signal reflections and attenuates noise from connected devices or any other sources nearby. If a wire pair with a grounded shield is not available, it should still be terminated with a resistor, however the capacitors should be skipped.

Example termination with a 120ohm resistor when no ground is available:

![CAN bus termination](https://raw.githubusercontent.com/cypnk/Cabin-Life/master/Cabin%20Area%20Network/Wiring/canbustermination_noground.png)

Wiring for a [common access port](https://github.com/cypnk/Cabin-Life/tree/master/Cabin%20Area%20Network/Common%20Port) to the bus.

![common access port](https://raw.githubusercontent.com/cypnk/Cabin-Life/master/Cabin%20Area%20Network/Common%20Port/portwiring.png)

An example of a port being used as a bus termination.

![common port termination](https://raw.githubusercontent.com/cypnk/Cabin-Life/master/Cabin%20Area%20Network/Common%20Port/portwiringtermination.png)

Using unshielded wires with a port is not recommended.

The test addressing system will use a counter such as the CD4017 for determining the length of transmitted bits. Operational amplifiers (op amps) such as the LM741, LM358 or LM324 are used to detect signals on high and low lines and reject noise. A simple logic gate such as the CD4081 may be used for further signalling. A handful of discreet transistors in common values will be used throughout.

Initial testing will use the 555 timer IC for clock pulse generation due to its ubiquitous availability. The final system will use a base data pulse frequency of 32.768KHz via a dedicated oscillator circuit. A crystal of this value can be easily scavenged from a large number of discarded devices such as TVs and clocks. The frequency is under the maximum operating limits of many older discreet components and simple transistors. This frequency also easily falls within the data sampling rates of many low-level microcontrollers, which themselves are likely running at much higher internal speeds.

If a single twisted pair is used, the highest possible speed for that pair is dependent on twist rate and shielding, if available. In that regard, discarded or unused [CAT5](https://en.wikipedia.org/wiki/Category_5_cable) cable is viable since the proliferation of [CAT6](https://en.wikipedia.org/wiki/Category_6_cable) and higher in new installations has made the older standard obsolete.

Possible scheme for speeds based on cable twist rates, matching the capabilities and the tolerances of simple components.

Shielded twisted pair (S/FTP):


| Wire Color	| Function			|
|---------------|-------------------------------|
| Blue		| 16MHz High			|
| White Blue	| 16MHz Low			|
| Green		| 8MHz High			|
| White Green	| 8MHz Low			|
| Orange	| 4MHz High			|
| White Orange	| 4MHz Low			|
| Brown		| 32.768KHz High		|
| White Brown	| 32.768KHz Low			|
| Shield/Drain	| Ground			|

Use of unshielded twisted pair (UTP) is not recommended, especially at higher frequencies. Note: a counter other than CD4017, such as CD4040 or CD4060, or their higher speed CMOS equivalents in the CD74HC... range should be used for frequencies above 4MHz. Op amps should also be changed for frequencies above 1MHz.

Alternative frequency schemes when using scavenged components from older electronics:

| Wire Color	| Function			|
|---------------|-------------------------------|
| Blue		| 16.384MHz High		|
| White Blue	| 16.384MHz Low		|
| Green		| 8.192MHz High			|
| White Green	| 8.192MHz Low			|
| Orange	| 4.096MHz High			|
| White Orange	| 4.096MHz Low			|
| Brown		| 32.768KHz High		|
| White Brown	| 32.768KHz Low			|
| Shield/Drain	| Ground			|

The frequency ranges in the alternate scheme were chosen to allow devices without onboard timing to use sync pulses as a clock for any additional processing. This method is best suited if the transmitting device only uses rudimentary logic and no microcontroller.

### TODO Transceiver/Buffer Circuit

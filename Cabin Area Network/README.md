# Cabin Area Network

This is a system for basic housekeeping tasks such as getting sensor data on temperature, humidity, other weather indicators, or sending alerts when local fauna such as bears or coyotes have entered the garden area. The network can be also used for signalling devices to turn on or off such as floodlights connected to solar charged batteries, well pumps, windows on greenhouses, or fans installed in outdoor composting toilets.

All devices on the network act independently without the use of a "Master" controller, which greatly simplifies signalling. Each device has an independent ID, which also doubles as its priority. The basic premise of the network is based on the Controller Area Network, or CAN bus, with elements borrowed from other robust systems.

Work in progress...

## Rationale 

While the basic operation of various CAN bus systems is well known, the actual details are often opaque and difficult or impossible to modify. Most CAN components are proprietary and communicate via various hardwired schemes. Reusing off-the-shelf components and other simple electronics should be sufficient to create an alternative which, although significantly limited compared to commercial and proprietary counterparts, is still capable of many ordinary tasks while remaining relatively robust. This system will also implement an addressing system which can be modified without special equipment while in operation.

**IMPORTANT** **: This system is not intended to replace mission critical applications, such as in vehicles, where the risk to human life in the event of a failure is unacceptable.**

## Concept

Communication between devices is through a single pair of twisted wire (bus), ideally with a grounded shield, which is specially terminated on each end. Using twisted pairs is highly recommended. If twisted pair cable is not available, at least a conductive ground shielded wire pair is recommended.

Bus end termination when a grounded shield is available. The other end follows the same scheme, but it is not connected to any other "Earth" on its own, except the shield, to avoid ground loops.
![CAN bus termination](https://raw.githubusercontent.com/cypnk/Cabin-Life/master/Cabin%20Area%20Network/canbustermination.png)

The wire pair is linked together with two 62ohm resistors connected in series and linked to ground via three separate capacitors in parallel. This method reduces signal reflections and attenuates noise from connected devices or any other sources nearby.

If a wire pair with a grounded shield is not available, at least one end should be terminated as above, however the capacitors should be skipped on the opposite end. 

The test addressing system will use a counter such as the CD4017 for determining the length of transmitted bits. Operational amplifiers (op amps) such as the LM741, LM358 or LM324 are used to detect signals on high and low lines and reject noise. A simple logic gate such as the CD4081 may be used for further signalling. A handful of discreet transistors in common values will be used throughout.

Initial testing will use the 555 timer IC for clock pulse generation due to its ubiquitous availability. The final system will use a base data pulse frequency of 32.768KHz via a dedicated oscillator circuit. A crystal of this value can be easily scavenged from a large number of discarded devices such as TVs and clocks. The frequency is under the maximum operating limits of many older discreet components and simple transistors. This frequency also easily falls within the data sampling rates of many low-level microcontrollers, which themselves are likely running at much higher internal speeds.

If a single twisted pair is used, the highest possible speed for that pair is dependent on twist rate and shielding, if available. In that regard, discarded or unused [CAT5](https://en.wikipedia.org/wiki/Category_5_cable) cable is viable since the proliferation of [CAT6](https://en.wikipedia.org/wiki/Category_6_cable) and higher in new installations has made the older standard obsolete.

Possible scheme for speeds based on cable twist rates, matching the capabilities and the tolerances of simple components.

Shielded twisted pair (S/FTP):


| Wire Color	| Function			|
|---------------|-------------------------------|
| Blue		| 10MHz High			|
| White Blue	| 10MHz Low			|
| Green		| 8MHz High			|
| White Green	| 8MHz Low			|
| Orange	| 4MHz High			|
| White Orange	| 4MHz Low			|
| Brown		| 32.768KHz High		|
| White Brown	| 32.768KHz Low			|
| Shield/Drain	| Ground			|

Use of unshielded twisted pair (UTP) is not recommended, especially at higher frequencies. Note: a counter other than CD4017, such as CD4040 or CD4060, should be used for frequencies above 4MHz. Op amps should also be changed for frequencies above 1MHz.

Alternative frequency schemes when using scavenged components from older electronics:

| Wire Color	| Function			|
|---------------|-------------------------------|
| Blue		| 11.0592MHz High		|
| White Blue	| 11.0592MHz Low		|
| Green		| 8.192MHz High			|
| White Green	| 8.192MHz Low			|
| Orange	| 4.096MHz High			|
| White Orange	| 4.096MHz Low			|
| Brown		| 32.768KHz High		|
| White Brown	| 32.768KHz Low			|
| Shield/Drain	| Ground			|

The frequency ranges in the alternate scheme were chosen to allow devices without onboard timing to use sync pulses as a clock for any additional processing. This method is best suited if the transmitting device only uses rudimentary logic and no microcontroller.

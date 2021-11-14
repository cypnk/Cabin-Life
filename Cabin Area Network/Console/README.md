# Console

A direct access interface for interacting with the Cabin Area Network. This may be built with a general purpose microcontroller with extensions to give basic functionality only relevant to its key purposes. Dedicated keys are added to reduce code overhead on parts with limited storage space and improve direct access to functions. 

## Keypad
The final functionality implemented is up to the builder, however this particular layout is meant to be built into a handheld device which can be operated with only one hand.

Work in progress...

![console keypad layout](https://raw.githubusercontent.com/cypnk/Cabin-Life/master/Cabin%20Area%20Network/Console/keyboard-layout.png)

These may change at a later date.

| Key	| Function		|
|-------|-----------------------|
| Status	| Get the console status or the selected device status |
| New		| Create a new bus payload or instruction |
| Print		| Show pending data payloads or instructions before being sent on the bus |
| Clear		| Delete entire line (after confirmation) or cancel current action |
| Back		| Backspace or delete one character back |
| OK		| Select or enter depending on the current screen |
| Action	| List available functions or actions on the selected device, if that feature is available |
| Bus		| Cycle through the available buses, if the console is connected to more than one |
| Items		| List all available devices and their statuses, if also sent, on the currently selected bus |
| Option	| Set optional parameter, E.G. Reorder instructions, delay etc... |

This switch arrangement should still be usable while wearing thin gloves, when placed in an enclosure. Taller stems will allow greater tactile feedback when little or no ambient light is available to see the keypad at the risk of slightly reduced operational life. If operation with thick gloves or mittens is desired, a wider key spacing and different switches are strongly recommended. The sides with the leads on each switch are oriented vertically.

![console key switches](https://raw.githubusercontent.com/cypnk/Cabin-Life/master/Cabin%20Area%20Network/Console/keypad-switches.png)

Switch orientation is up to the builder's preference, however consistency is critical across all switches. In the above example, the disconnected (normally off when not pressed) poles on each switch are facing each other.

Note: When reusing scavenged tactile switches of a similar style, check for continuity across poles 1 to 2 and 3 to 4 when the switch is off (not being pressed) and continuity across poles 2 to 4 and 1 to 3 when the switch is on (pressed). The disconnected (normally off when not pressed) pairs are bent in the same direction. Lack of continuity or intermittent continuity could indicate internal corrosion.

## Key Signals

Because the devices on a bus have their own definitions for words or functions and values, there should be some consistency when implementing commands to control them. This is one possible interpretation for bus transmission control handling and device commands to be translated internally.

| Label	| Signal value	|
|-------|---------------|
| 0	| 0011 0000	|
| 1	| 0011 0001	|
| 2	| 0011 0010	|
| 3	| 0011 0011	|
| 4	| 0011 0100	|
| 5	| 0011 0101	|
| 6	| 0011 0110	|
| 7	| 0011 0111	|
| 8	| 0011 1000	|
| 9	| 0011 1001	|
| BKS, \*| 0000 1000	|
| OK, #	| 0000 1101	|
| DEL	| 0111 1111	|
| STA	| 0000 0111	|
| NEW	| 0000 1010	|
| PRN	| 0000 1110	|
| LST	| 0000 0101	|
| BUS	| 0000 1100	|
| DIR	| 0001 0110	|
| OPT	| 0001 0010	|
| Up	| 0000 0001	|
| Left	| 0000 0010	|
| Right	| 0000 0011	|
| Down	| 0000 0100	|
| A	| 0100 0001	|
| B	| 0100 0010	|
| C	| 0100 0011	|
| D	| 0100 0100	|
| E	| 0100 0101	|
| F	| 0100 0101	|
| G	| 0100 0111	|
| H	| 0100 1000	|
| I	| 0100 1001	|
| J	| 0100 1010	|
| K	| 0100 1011	|
| L	| 0100 1100	|
| M	| 0100 1101	|
| N	| 0100 1110	|
| O	| 0100 1111	|
| P	| 0101 0000	|
| Q	| 0101 0001	|
| R	| 0101 0010	|
| S	| 0101 0011	|
| T	| 0101 0100	|
| U	| 0101 0101	|
| V	| 0101 0110	|
| W	| 0101 0111	|
| X	| 0101 1000	|
| Y	| 0101 1001	|
| Z	| 0101 1010	|

To select different values in one key, E.G. "2" as 2, A, B, or C, a timer may be implemented to cycle through the character labels and values if another key pressed is the same key ID within a very short period of time.

It may be more simple and practical to implement one set of binary values per key press. E.G. Label "A" as only uppercase with 0100 0001 instead of both uppercase and lowercase "a" with 0110 0001. And "\*", found on most off-the-shelf "phone style" keypads, only as 0000 1000 for backspace instead of both backspace and 0010 1010. Since other devices on the bus may only have primitive components to implement commands, this will also significantly reduce complexity.

Using the above example, a value may be interpreted based on the transmitted binary. E.G. A device on the network which understands "minutes" and "seconds" can take the highest 4 bits of the value portion of the [32 bit message payload](https://github.com/cypnk/Cabin-Life/tree/master/Cabin%20Area%20Network#devices) as either "M" or "S" and the lowest to mean the duration. So an interpreted value of 1101 0011 could mean 30 minutes and 0011 0011 could mean 30 seconds. A combined value of "30 minutes and 30 seconds" if they're received back to back, or 1111 0000 command for letter "O" and zero meaning "override previous" value. A value of 0000 0000 could be "OFF". There is some overlap in letters here such as "C" and "S" when only using the lower 4 bits, however this level of logic can be achieved without the use of a microcontroller on the device being addressed.

## Enclosure and Interface

The console may be built into a stationary location on a wall or built into a handheld case which can be plugged into an isolated port. The port interface may be yet another device on the network or simply the live twisted pair wire of the bus(es) and its ground. For mobile consoles, an interface based on the [Device Key](https://github.com/cypnk/Cabin-Life/tree/master/Cabin%20Area%20Network/Device%20Key) is possible.


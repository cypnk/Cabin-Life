# Console

A direct access interface for interacting with the Cabin Area Network. This may be built with a general purpose microcontroller with extensions to give basic functionality only relevant to its key purposes. Dedicated keys are added to reduce code overhead on parts with limited storage space and improve direct access to functions. 

## Keypad
The final functionality implemented is up to the builder, however this particular layout is meant to be built into a handheld device which can be operated with only one hand.

Work in progress...

![console keypad layout](https://raw.githubusercontent.com/cypnk/Cabin-Life/master/Cabin%20Area%20Network/Console/keyboard-layout.png)

These may change at a later date.

| Key	| Function		|
|-------|-----------------------|
| STA	| Get the console status or the selected device status |
| NEW	| Create a new bus payload or instruction |
| PRN	| Show pending data payloads or instructions before being sent on the bus |
| DEL	| Delete entire line (after confirmation) |
| BKS	| Delete one character back |
| OK	| Select or enter depending on the current screen |
| LST	| List available functions on the selected device, if that feature is available |
| BUS	| Cycle through the available buses, if the console is connected to more than one |
| DIR	| List all available devices and their statuses, if also sent, on the currently selected bus |
| OPT	| Set optional parameter, E.G. Reorder instructions, delay etc... |

This switch arrangement should still be usable while wearing thin gloves, when placed in an enclosure. Taller stems will allow greater tactile feedback when little or no ambient light is available to see the keypad at the risk of slightly reduced operational life. If operation with thick gloves or mittens is desired, a wider key spacing and different switches are strongly recommended. The sides with the leads on each switch are oriented vertically.

![console key switches](https://raw.githubusercontent.com/cypnk/Cabin-Life/master/Cabin%20Area%20Network/Console/keypad-switches.png)

Switch orientation is up to the builder's preference, howevever consistency is critical across all switches. In the above example, the disconnected (normally off when not pressed) poles on each switch are facing each other.

Note: When reusing scavenged tactile switches of a similar style, check for continuity across poles 1 to 2 and 3 to 4 when the switch is off (not being pressed) and continuity across poles 2 to 4 and 1 to 3 when the switch is on (pressed). The disconnected (normally off when not pressed) pairs are bent in the same direction. Lack of continuity or intermittent continuity could indicate internal corrosion.


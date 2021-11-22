# Common Port

A simple and durable connection interface for the network using minimal and commonly available parts.

## Rationale

While stationary devices can be hard wired into the network, it may be necessary to connect or disconnect devices or [consoles](https://github.com/cypnk/Cabin-Life/tree/master/Cabin%20Area%20Network/Console) periodically. Connections need to be robust enough for repeated use while protecting the wire bus itself from undesirable interference or accidental surges. The port entry may be embedded in a wall or placed in a sheltered outdoor enclosure where it may be subject to undesirable conditions.

The hardware is based on the 1/4 inch or 6.35mm [audio jack and port](https://en.wikipedia.org/wiki/Phone_connector_(audio)) in the stereo or 2-channel version. This format was chosen for its simplicity, availability, low cost, and because it gives the bare minimum number of contacts to interact with a 2-wire + ground network bus. While the design of this connector is very old, it has proven itself since its inception and was routinely used on [telephone switchboards](https://en.wikipedia.org/wiki/Telephone_switchboard) where repeated plugging and unplugging may occur hundreds of times a day for years. The format remains available due to its ubiquity in the audio industry. This application may not have the same degree of endurance, due to modern manufacturing and sourcing issues as well as potentially adverse environmental factors, however it will be robust enough for its intended purpose here.

## Concept

Surge voltages are directed to ground on both the CAN High and CAN Low lines and the connections are terminated with the shortest possible links to avoid signal reflection or degradation on the rest of the bus.

In the TRS or "tip, ring, sleeve" arrangement, the tip will be connected to CAN High and the ring to CAN Low. The sleeve is a low impedance connection to the ground or shield of the wire bus. If the port is located at the end of the bus, it will also contain the [bus termination](https://github.com/cypnk/Cabin-Life/tree/master/Cabin%20Area%20Network#wiring). 

When being plugged, the port ground connected to the bus is the first contact point of the plug and will be the likely location to experience static electricity.

The outdoor port enclosure may be connected directly to Earth to reduce the possibility of damage by static electricity to the bus, however the bus ground (sleeve) is separated from the enclosure ground to avoid potential ground loops and to reduce the likelihood of damage from lightning feedback nearby.

Work in progress...

## Wiring

Basic port wiring connections are via a zener barrier in a "star" configuration to prevent high voltage spikes on either line or the ground itself from reaching the bus from the device being connected or from the bus to the device. There are 100ohm resistors in series at the tip and ring inputs as the connecting device would switch its signals based on its own power supply, which may be higher than the typical CAN High signal pulse of 3.5V. The difference in voltage potential between CAN High and CAN Low is what matters. The 1N750 in this example has a breakdown voltage of 4.7V, however a 1N4733A or similar zener at a 5.1V breakdown may be used. The devices should be tolerant of at least twice this voltage.

![port wiring](https://github.com/cypnk/Cabin-Life/blob/master/Cabin%20Area%20Network/Common%20Port/portwiring.png)

The outputs here are soldered to the port socket as labeled.

Wiring scheme when the port on either end is the last on the bus. This method of termination may be a better alternative to simply leaving the bus cable hanging with a termination. The port is a known end to the bus.

![port wiring](https://github.com/cypnk/Cabin-Life/blob/master/Cabin%20Area%20Network/Common%20Port/portwiringtermination.png)

Note, one of the ports on either end of the bus should have its shield ground connected to Earth if the bus is terminated in this fashion, but not both.

The outdoor version of the port requires special consideration due to possible external surge events such as static electricity and lightning proximity. The contacts to the rest of the bus need to be protected while allowing signals to pass through with relatively little attenuation. On the transceiver side, this may be handled with coupling transformers or similar passive components or [optocouplers](https://en.wikipedia.org/wiki/Opto-isolator) and similar active components, however ports must be relatively more robust, size optimized, and still remain inexpensive.

The bus current should not exceed 200mA and the transceivers aren't meant to provide more than 150mA during normal operation. Therefore, the current entering or leaving the bus should not exceed 500mA at any time. Fuses should be added in series between the tip contact and CAN High line and the ring contact and CAN Low line of rest of the port circuit.

Fuses, while effective at stopping sustained high voltage, are less capable of handling fast transient high voltage events. In commercial equipment is generally handled via transient voltage suppression (TVS) diodes which may be scavenged from older equipment, however their thresholds may not be suitable for this application. As an alternative, a spark gap may be used for static events over shorter distances. Since such a gap must be isolated from its environment, allocating additional space to an already cramped location such as an outdoor enclosure will be infeasible. In this instance, normally open (N/O) reed switches may suffice to protect the circuit as they're already in sealed glass envelopes and require very little space.

Grounding the bus is more delicate as ground loops may introduce undesired operation of devices. The bus should only be grounded at one location. The port will need to handle this ground connection while also directing suppressed transients to Earth, where the port enclosure is also connected. "Earth", in this instance, refers to the physical conductor to the soil where the outdoor port is installed and "ground" refers to the signal cable's shield, which is terminated elsewhere.

During normal operation, there should be no sustained voltage on the bus shield, therefore any sustained excess voltage should be sent to the enclosure and then to Earth while still providing normal "0" reference to the device connected to the port avoiding ground loops. This dual role may be handled with a low value inductor and diode in series.

One possible arrangement for the outdoor port circuit using these concepts.

![protectedport](https://raw.githubusercontent.com/cypnk/Cabin-Life/master/Cabin%20Area%20Network/Common%20Port/protectedport.png)

For added security of the outdoor port, is a disconnecting switch set may be added with the aid of an outdoor-rated cabinet lock. Since the spark gaps are using ordinary normally open reed switches, 3 additional reed switches of the same type may be added to create a Break-Before-Make disconnector using a single magnet attached to the lever of the lock. When the port is "locked" the reed switches to the main bus lines should be opened and the switches closest to the external socket should be closed, therefore any attempted communication will be shorted to Earth, including any static or other high voltage events. When the port is "unlocked", the switches closest to the socket are opened and revert to their role as spark gaps, while the three bus switches are closed or "Enabled".

![protectedport](https://raw.githubusercontent.com/cypnk/Cabin-Life/master/Cabin%20Area%20Network/Common%20Port/lockingport.png)

If the magnet loses its strength at some point or if it is accidentally detached, in this configuration, the port should safely disable itself as both sets of reed switches will revert to being opened.

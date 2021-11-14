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

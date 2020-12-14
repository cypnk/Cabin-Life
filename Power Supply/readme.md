# Power Supply

This is a work in progress to create a simple, portable, power supply for various off-grid projects and solutions.

Whenever possible, generic parts will be used to reduce cost and increase availability as well as maximize scavenge and reuse potential.

Eventually, there will be several types optimized for various supply voltages, all with isolated power and ground.
- Type 1: Accept 6V - 28V and supply 1A @ 3.3V to 5V
- Type 2: Accept 10V - 52V and supply 2A @ 3.3V, 5V, and 12V
- Type 3: Accept 10V - 52V and supply 5A @ 3.3V, +5V, -5V, and 12V
- Type 4: Accept 10V - 52V and supply 8A @ +3.3V, -3.3V, +5V, -5V, +12V, and -12V

The first type is to test build feasibility and check if the concept is useful in a small footprint with commonly available components. The 28V upper limit is to is to accommodate a 24V solar power system with allowance for an increase during a battery charge cycle while also being compatible with a smaller cellular phone charging solar panel. The 52V upper limit in the rest of the power supplies is to match a 48V solar power system. The low amperage rating is to maximize runtime while ensuring the solar panel system isn't damaged in the absence of an inverter or other kind of current limiting circuit.

The power supply circuitry will be protected as much as possible from electrostatic discharge (ESD) and over-current situations.

Efficiencies have not yet been determined, but the goal is to approach at least ~80% without using any specialized, high-efficiency, components.

Components for the power supply may come from new stock or salvaged electronics made from around 1980 and after. 

**IMPORTANT** **: *The reuse of old-stock electrolytic capacitors, especially from the 1990s, is strongly discouraged for safety reasons. Ceramic capacitors should be inspected for cracks and large capacitance variations (a sign of internal shorting). All components should be thoroughly tested for faults before being reused***

**Electricity is dangerous and the author is not responsible for any damage to property, injuries, or worse, which may be caused by using any of the information presented here.**

In any area of the power supply where a microcontroller can be used, but not available or undesired for any reason, a configurable timing chip, such as the 555 or 556 IC, may be used with additional passive components to regulate the pulse-width-modulated (PWM) output and to limit the input voltage to levels the IC can tolerate. There is greater salvage and reuse potential with timing chips as opposed to microcontrollers which may be more precise, however microcontrollers require additional infastructure, some propietary, to program and configure initially. There is a tradeoff with both options.

Most of the efficiency losses are expected to happen in the high side constant voltage circuit.

A microcontroller may be used to provide a PWM signal to the low side current and voltage regulators for the multiple outputs. A microcontroller may also be useful to provide temperature sensing capability, connection status monitoring, fault condition monitoring, and for wireless status reporting and control. Timing chips may also be used if a microcontroller is not available or desirable.

The narrowest recommended wire diameter is 14AWG for both supply and loads when approaching the 8A limit.

A rough sketch of the high side supply circuit for the 10V - 52V types:
```
 [ High side ]                                                                                          [ Low side ]

 +10V-52V
     |                       { D G S }                                                   [1:1 Isolation]
     +-[ 8A Fuse ]-----+--+-[ P-MOSFET ]-+-----------+--+---+    +--GND                 GND--+    +----> [ Low GND ]
                       |  |      +                   |  |   *)||(*                GND        *)||(*
    GND--+--[ TVS ]----+  |      |  +---[ 100K R ]---+  |    )||(                  |          )||(
         +-[ 1M 1W R ]-+  |      |  |                   |    )||(                  +          )||(
         |                |      |  |                   |    )||(              { D G S }      )||(
         |  +-------------+      |  +------+--------+   |   +    +----------+-[ P-MOSFET ]-+-+    +-+--> [ Low V+ ]
         |  |                    |         |        |   |   |               |                       |
         |  +-[ Capacitor ]-+    |         +        |   |   +-[ (Big)Caps ]-+                       +---------+
         |  +---[ 100K R ]--+----+---[ Power BJT ]  |   |   |                                                 |
         |                             { C B E }    |   |   |  { D G S }            [ Low GND ]--[ Diode >| ]-+
         +-----------------------------------+      |   |   +-[ N-MOSFET ]--GND
         |                                          |   |   |      +
         +---------------------[ 50V Zener >| ]-----+   |   |      |
                                                        |   |      |
                               GND--+-[ (Medium)Caps ]--+   +----+ +
                                    |                   |      { A B }
                                    +-----+-[ 1M 1W R ]-+   [ Controller ]

                           A = Charge sense, B = Charge trigger (PWM)
```

The "controller" in this instance may be microcontroller or a hard-wired oscillator circuit with high voltage and static tolerant passive components to limit trigger frequency and duty cycle. The final P-MOSFET before the isolation transformer can be replaced with a schottky diode.

High side voltage limiting for the 6V - 28V type
```
 +6V-28V
     |                     { D G S }
     +--[ 5A Fuse ]--+--+-[ P-MOSFET ]-+-----------+--+--- [ Rest of circuit ]
                     |  |      +                   |
   GND--+--[ TVS ]---+  |      |  +----[ 50K R ]---+
        +-[ 1M 1W R ]+  |      |  |
        |               |      |  |
        |   +-----------+      |  +------+---------+
        |   |                  |         |         |
        |   +-[ Capacitor ]-+  |         +         |
        |   +---[ 50K R ]---+--+---[ Power BJT ]   |
        |                            { C B E }     |
        +----------------------------------+       |
        |                                          |
        +--------------------[ 25V Zener >| ]------+
```

The output of the high side supply is expected to vary between 20V - 24V depending on the original input voltage (6V - 52V). The low side regulators with input and output isolation will connect to the high side constant voltage supply.

If the circuit is directly connected to a solar panel or other outdoor supply, additional precautions must be taken to reduce the likelihood of damage from lightning. Damage from a direct strike to the solar panel is likely unavoidable, however some transient voltage spikes can be reduced if the input end is wired differently. The solar panel itself must also be adequately grounded for these to have any effect.

The circuit must be wired with its own Earth return separately from the common ground return. The Earth can be a copper spike or other good conductor driven into solid ground with the other end connected to the circuit with 10AWG - 14AWG wire. The Earth may also be a household ground connection, provided it is close to where the actual conductor makes contact with the Earth.

Alternate transient protection with independent Earth, separate from common ground
```
     V+
     | 
     +-[ Fuse ]--+-----+-[ Inductor ]-+-+-[ Rest of circuit ]
                 |                      |
EARTH---[ TVS ]--+     GND--[ 1M 1W R ]-+
```

High spike (one-time or very limited number of times) transient protection with gas discharge tube (spark gap)
```
     V+
     | 
     +-[ Fuse ]---+-----+-[ Inductor ]-+-[ Rest of circuit ]
                  |                    |
EARTH----[ GDT ]--+                    |
                    GND-+----+-[ TVS ]-+
                        |              |
                        +--[ 1M 1W R ]-+
```

High spike transient protection with independent Earth instead of common ground
```
     V+
     | 
     +-[ Fuse ]---+--+-[ Inductor ]-+------+-[ Rest of circuit ]
                  |  |                     |
EARTH--+-[ GDT ]--+  |                     |
       |             |   GND---[ 1M 1W R ]-+
       +-[ TVS ]-+---+
```


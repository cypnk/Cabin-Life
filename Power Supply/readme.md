# Power Supply

This is a work in progress to create a simple, portable, power supply for various off-grid projects and solutions.

Whenever possible, generic parts will be used to reduce cost and increase availability as well as maximize scavenge and reuse potential.

Eventually, there will be several types optimized for various supply voltages, all with isolated power and ground.
- Type 1: Accept 6V - 28V and supply 1A @ 3.3V to 5V
- Type 2: Accept 10V - 52V and supply 2A @ 3.3V, 5V, and 12V
- Type 3: Accept 10V - 52V and supply 5A @ 3.3V, +5V, -5V, and 12V
- Type 4: Accept 10V - 52V and supply 8A @ 3.3V, +5V, -5V, +12V, and -12V

The first type is to test build feasibility and check if the concept is useful in a small footprint with commonly available components. The 28V upper limit is to is to accommodate a 24V solar power system with allowance for an increase during a battery charge cycle while also being compatible with a smaller cellular phone charging solar panel. The 52V upper limit in the rest of the power supplies is to match a 48V solar power system. The low amperage rating is to maximize runtime while ensuring the solar panel system isn't damaged in the absence of an inverter or other kind of current limiting circuit.

The power supply circuitry will be protected as much as possible from electrostatic discharge (ESD) and over-current situations. Lightning protection is being considered.

Efficiencies have not yet been determined, but the goal is to approach at least ~80% without using any specialized, high-efficiency, components.

A rough sketch of the front high side supply circuit so far:
```
 +10V-52V
     |                     { D G S }
     +-[ 10A Fuse ]--+--+-[ P-MOSFET ]-+-----------+--+---+    +--GND
                     |  |      +                   |  |   *)||(*
    GND--+--[ TVS ]--+  |      |  +---[ 100K R ]---+  |    )||(
         |              |      |  |                   |    )||(               { D G S }
         |  +-----------+      |  +------+---------+  |   +    +----------+-[ P-MOSFET ]-+-----+---> [ Load ]
         |  |                  |         |         |  |   |               |       +      |     |
         |  +-[ Capacitor ]-+  |         +         |  |   +-[ (Big)Caps ]-+       |      |     |
         |  +---[ 100K R ]--+--+---[ Power BJT ]   |  |   |                       |      |     |
         |                           { C B E }     |  |   |  { D G S }            |      |     |
         +---------------------------------+       |  |   +-[ N-MOSFET ]--GND     |      |     |
         |                                         |  |   |      +                |      |     |
         +-----------------------[ Zener >| ]------+  |   |      | +-------------+       |     |
                                                      |   |      | | +-------------------+     |
                               GND--[ (Medium)Caps ]--+   +----+ + + +                         |
                                                      |      { A B C D }                       |
                                                      +---+-[ Controller ]-+-+--[ Capacitor ]--+
                                                                             |
                                                                            GND

                           A = Charge sense, B = Charge trigger, C = Discharge trigger, D = Load sense
```

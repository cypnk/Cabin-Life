# Power Supply

This is a work in progress to create a simple, portable, power supply for various off-grid projects and solutions.

Whenever possible, generic parts will be used to reduce cost and increase availability as well as maximize scavenge and reuse potential.

Eventually, there will be several types optimized for various supply voltages, all with isolated power and ground.
- Type 1: Accept 6V - 28V and supply 1A @ 3.3V to 5V
- Type 2: Accept 10V - 52V and supply 2A @ 3.3V, 5V, and 12V
- Type 3: Accept 10V - 52V and supply 5A @ 3.3V, +5V, -5V, and 12V
- Type 4: Accept 10V - 52V and supply 8A @ +3.3V, -3.3V, +5V, -5V, +12V, and -12V

The first type is to test build feasibility and check if the concept is useful in a small footprint with commonly available components. The 28V upper limit is to is to accommodate a 24V solar power system with allowance for an increase during a battery charge cycle while also being compatible with a smaller cellular phone charging solar panel. The 52V upper limit in the rest of the power supplies is to match a 48V solar power system. The low amperage rating is to maximize runtime while ensuring the solar panel system isn't damaged in the absence of an inverter or other kind of current limiting circuit.

The power supply circuitry will be protected as much as possible from electrostatic discharge (ESD) and over-current situations. Lightning protection is being considered.

Efficiencies have not yet been determined, but the goal is to approach at least ~80% without using any specialized, high-efficiency, components.

Components for the power supply may come from new stock or salvaged electronics made from around 1980 and after. 

**IMPORTANT** **: *The reuse of old-stock electrolytic capacitors, especially from the 1990s, is strongly discouraged for safety reasons. Ceramic capacitors should be inspected for cracks and large capacitance variations (a sign of internal shorting). All components should be thoroughly tested for faults before being reused***

**Electricity is dangerous and the author is not responsible for any damage to property, injuries, or worse, which may be caused by using any of the information presented here.**

In any area of the power supply where a microcontroller can be used, but not available or undesired for any reason, a configurable timing chip, such as the 555 or 556 IC, may be used with additional passive components to regulate the pulse-width-modulated (PWM) output and to limit the input voltage to levels the IC can tolerate. There is greater salvage and reuse potential with timing chips as opposed to microcontrollers which may be more precise, however microcontrollers require additional infastructure, some propietary, to program and configure initially. There is a tradeoff with both options.

A rough sketch of the high side constant voltage supply circuit so far:
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

Most of the efficiency losses are expected to happen here.

The "controller" in this instance may be microcontroller or a hard-wired oscillator circuit with high voltage and static tolerant passive components to limit trigger frequency.

The output of the high side supply is expected to vary between 20V - 24V depending on the original input voltage (6V - 52V). The low side regulators with input and output isolation will connect to the high side constant voltage supply.

A microcontroller may be used to provide a PWM signal to the low side current and voltage regulators for the multiple outputs. A microcontroller may also be useful to provide temperature sensing capability, connection status monitoring, fault condition monitoring, and for wireless status reporting and control. Timing chips may be used if a microcontroller is not available or desirable.




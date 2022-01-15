# Power Storage

A durable, fault-tolerant, rechargeable system based on the Zinc bromide (ZnBr₂) battery chemistry. The primary benefit of this battery type is the limited skill necessary to make them. The properties of the chemistry make it appropriate for locations where ready access isn't possible year round and so will receive little attention by necessity.

Other benefits include readily available and relatively cheap replacement parts and electrolyte raw ingredients. When stored in properly sealed containers, the raw ingredients for the electrolyte have an indefinite shelf-life. The electrolyte can be made in situ with simple household utensils. The battery can be fully discharged to 0% without permanent damage, unlike LiFePO₄ batteries, and can be left for months or years in the discharged state and is far less susceptible to temperature extremes. This type of battery should exceed several thousand charge cycles before needing electroylte replenishment.

Potential drawbacks are that the energy density per volume is far lower than LiFePO₄, which means larger cells for equivalent capacity. The battery may be difficult to move, depending on the type of container used, once assembled and must be checked for leaks before filling with the electrolyte since it's a liquid battery. Charging may produce H², similar to lead acid batteries, especially at higher currents. Potential Bromine gas release is possible, which may cause "pool smell". The battery must be periodically shorted to 0% charge to reduce electrode dendrite buildup.

Potential solutions to drawbacks include using end-sealed lengths of PVC pipe as containers, which are already leak resistant and allow easier movement once assembled. A gelling agent such as Sodium polyacrylate may be added to the electrolyte and the patent for this process has already expired. A venting system similar to when charging lead acid batteries can be used to take care of undesirable gases. Using a timing system, multiple batteries can be set to charge/discharge on different days or skip charging entirely using a controller connected to automotive or solid-state relays for each each battery. The logic for such a system may be hard-wired using simple TTL chips if a microcontroller is unavailable or undesirable.

### Electrolyte components:
* Zinc sulfate (ZnSO₄). Available as a dietary supplement or for other pharmaceutical use
* Sodium bromide (NaBr). Available as a disinfectant for swimming pools and hot tubs
* Distilled water

Premade Zinc bromide can be purchased, however it may not be readily available in all areas and may be costly.

### Test cell components:
* Heavy duty, reclosable, plastic storage bag
* 14-16AWG wire with outdoor rated insulator
* Zinc wire and/or zinc strips (negative electrode)
* Graphite foil sheets (positive electrode) without binders or inserts. Available as gaskets or seals for high-temperature applications
  * A carbon rod electrode can be substituted, if available 

### Final cell components:
* 4" (locales outside the U.S. may use equivalent sizes) PVC schedule-40, or SDR 35, or similar drainage pipes
* PVC cement (with primer or primer combination recommended)
* Threaded end caps and couplings
* Pressure fit end caps
* 12AWG wire with outdoor rated insulator
* Zinc flashing roll or similar Zinc strip at least 2.5" or 6.25cm to 6.5cm wide (or similar strip which can be coiled)
* Graphite foil sheets or carbon rod electrodes 
* Carbon foam (optional, but will increase charge/discharge efficiency by adding surface area to positive electrode)

As an alternative to pre-made carbon foam, a powder organic material, such as table sugar, can be heated with a finely mixed blowing agent until carbonized. The material should be left to cool before exposing it to ambient air. The resulting carbon material can then be formed into an electrode with a very high surface area. The greater the surface area of the electrodes, the greater the amps the battery is able to handle.

### Tools and utensils:
* Metal snips, also called tin snips or aviation snips
* Pliers
* Steel wool (to clean the Zinc in case of surface impurities, not needed if Zinc is clean)
* Glass measuring cup showing milliliter increments
* Digital scale with at least 800g limit and 0.1g resolution
* Wooden or plastic spoons
* Metal container or large tin with an inner glass container capable of holding 1L or a dedicated double-boiler
* Stove or heater
* Gloves

### Electrolyte chemistry: 
Batch production is recommended instead of large volumes to reduce cost and the impact of any errors during production. Small batches are also more more practical to use in mutiple test cell configurations.

* Dissolve 556g Sodium bromide (NaBr) in 500ml hot water
* Dissolve 575g Zinc sulfate (ZnSO₄) in 500ml hot water

The water should be hot, but not boiling.

The double boiler may be used to keep the temperature adequate while dissolving the chemicals separately. Once thoroughly dissolved, the two solutions can be mixed together in another glass container. This ensures the reaction is as thorough as possible. Note: This composition can be made slightly excess in Zinc sulfate.

After mixing thoroughly, the solution is then evaporated, which can be done in the stove under a low setting or in the double boiler under gentle heat. Sodium sulfate (Na₂SO₄) should precipitate out as a white salt in the container, leaving behind nearly pure Zinc bromide in the solution. Evaporation should be stopped when the volume of the solution has gone down to approximately ~200ml.

The Zinc bromide solution can then be poured through filter paper or through a paper towel to remove any residual Sodium sulfate crystals. The internal resistance of the cell rises as it is fully charged, making it inherently safe from overcharging, however this reduces charging efficiency. Some dissolved Sodium sulfate can be added back into the Zinc bromide solution as needed to improve charging efficiency. This final step is left up to the builder.

### Cell physical properties:
Typically, the positive carbon electrode is kept below the negative Zinc electrode due the charging behavior of this electrolyte chemistry.

During the charge cycle, Bromine will be produced in the electrolyte at the positive carbon electrode and Zinc in the solution will start depositing on the negative electrode forming Zinc dendrites. Closer proximity of the electrodes will lower resistance and increase efficiency at the cost of higher self-discharge. The self-discharge will accelerate if the negative Zinc electrode comes into contact with the Bromine, however this is unavoidable due to diffusion unless there's a physical separator between the electrodes which is permeable to ions.

The electrolyte will change color to appear more red and brown as the Bromine concentration rises while charging. The Bromine will settle in the cell and so both electrodes should be elevated off the bottom of the container to let it collect there while keeping fresh Zinc bromide in contact with the electrodes above. The cell should be considered fully charged when the Bromine level rises up to the negative Zinc electrode.

As the cell discharges, either through a connected load or through self-discharge over time, the solution should lose its red/brown color. The cell is fully discharged when the solution becomes clear. The charging circuit should measure the rising resistance in the cell as it is fully charged. The charging cutoff should be well before reaching maximum resistance to avoid damage to the power source such as solar panels or AC/DC inverter.

If bubbles appear at the electrodes during the charging cycle, the charging current is too high. To reduce the likelihood of hydrogen gas buildup, the charging current should be gradually increased up to a safe level in the test cell. The maximum output current and charge current is highly dependent on the electrode surface area and their proximity to each other. 

Typical cell voltage should be ~1.5V and at least 18 cells may need to be wired in series to produce a 24V bank with enough charging overhead. The capacity of the battery is directly proportional to the volume of electrolyte in each cell.

Bromine can be corrosive to most forms of plastic and the use of sewer-rated PVC is recommended for the final cell construction intended for permanent installation. Silicone may be used to seal around protrusions in the container to prevent contamination and to reduce electrolyte evaporation.

Assembly and final design in progress...



# Directional WiFi Antenna
For remote, point-to-point links, this antenna may be built from household wiring, roof flashing, and other scavenged sources of material. 

The antenna is tuned to both 2.4GHz and 5GHz and the estimated gain is ~5dB, depending on the selected materials and build quality. Housing the antenna in a waterproof enclosure, of a material transparent to radio signals, is strongly recommended if used outdoors. Based on the suggested build materials, the overall size of the antenna is 60mm wide, 80mm tall, and approximately 8mm deep, excluding the feed cable.

Overall antenna profile in front and side view:
![antenna profile](https://raw.githubusercontent.com/cypnk/Cabin-Life/master/Directional%20Wifi%20Antenna/antenna_profile.png)

## Materials
* Copper (recommended) or Zinc roof and gutter flashing material
* 14 AWG household wiring
* RG-316 or similar WiFi-suitable coaxial cable pigtail
* Insulating separator dowel material of 3mm to 10mm wide. Plastic, wood etc...

### Material alternatives 
* Brass or aluminum (aluminium) sheet can be substituted for the radiator elements and backplane
* Hot glue may be used as the insulating separator, however the segments must be held in position until the glue solidifies completely
* Coax cable may be improvised from 14 AWG insulated household wire, tubular desoldering braid as shielding, and heat shrink tubing for the outer sheath

## Tools
* Drill and drill bit matching the size of the selected coax cable, minus the outer sheath
* Soldering iron and acid free solder
* Tin snips (aviation snips) or similar metal cutting tool
* Wire stripper or blade to trim insulation and cut dowels
* Sandpaper or metal file (recommended)
* Masking tape (optional, recommended)

### Tool alternatives
* If a drill bit matching the size of the cable, without its sheath, is not available, a nail may be used to punch through. The hole is not necessary if the antenna is fed from the front instead of the back.
* Hot glue gun may be used instead of tape to hold the components in place during and after soldering.

## Build process

The selected sheet material is cut into four(4), equal sized, 20mm x 20mm squares for the radiator elements.
![element](https://raw.githubusercontent.com/cypnk/Cabin-Life/master/Directional%20Wifi%20Antenna/element.png)

The size of the radiator elements is critical and cutting the squares slightly larger than needed and filing or sanding down to the correct size may be necessary.

The backplane is cut as a single 60mm x 80mm rectangle.
![backplane](https://raw.githubusercontent.com/cypnk/Cabin-Life/master/Directional%20Wifi%20Antenna/backplane.png)

The radiator elements are separated 30mm on center. The squares may be temporarily taped to ensure they don't move during the soldering process.
![element separation](https://raw.githubusercontent.com/cypnk/Cabin-Life/master/Directional%20Wifi%20Antenna/element_separation.png)

The 14 AWG wire is bent to give 6mm "legs" to the center of the radiator squares, the width of the segment is 30mm, matching the center separation. The length of wire on the square itself is not critical, except it must be long enough to give enough structural support while soldering.
![element segment](https://raw.githubusercontent.com/cypnk/Cabin-Life/master/Directional%20Wifi%20Antenna/element_segment.png)

This creates a single driven element segment. 

Two of the segments are separated vertically 30mm apart at the center, just as their individual squares. The measurement for the separation can be made at middle joining wire. 
![segment pair](https://raw.githubusercontent.com/cypnk/Cabin-Life/master/Directional%20Wifi%20Antenna/segment_pair.png)

Another length of 30mm wire is cut and soldered at the middle. This completes the driven elements.
![driven elements](https://raw.githubusercontent.com/cypnk/Cabin-Life/master/Directional%20Wifi%20Antenna/driven_elements.png)

Flipped over to the smooth side, the driven elements are centered vertically and horizontally on the backplane.
![backplane center](https://raw.githubusercontent.com/cypnk/Cabin-Life/master/Directional%20Wifi%20Antenna/backplane_center.png)

The driven elements are spaced 6mm off the backplane surface.
![backplane separation](https://raw.githubusercontent.com/cypnk/Cabin-Life/master/Directional%20Wifi%20Antenna/backplane_separation.png)

**Note:** The following drill steps are to feed the antenna from the back. Drilling is not necessary if the antenna is fed from the front, however the coax cable braid should be soldered to the backplane via a bent piece of 14 AWG wire and the center conductor should be soldered at the same location to the driven element. The spacing to the backplane should be maintained regardless of front or back feed.

The backplane is drilled at the separation feed point center location. The drilled hole should allow the center core of the coaxial cable through, but not be too wide.
![backplane drilled](https://raw.githubusercontent.com/cypnk/Cabin-Life/master/Directional%20Wifi%20Antenna/backplane_drilled.png)  
![backplane drill position](https://raw.githubusercontent.com/cypnk/Cabin-Life/master/Directional%20Wifi%20Antenna/backplane_drill_position.png)

The selected coax cable should be stripped of the outer sheath to expose the braided shield, and the center conductor.
![coax cable](https://raw.githubusercontent.com/cypnk/Cabin-Life/master/Directional%20Wifi%20Antenna/coax_cable.png)

Both the center conductor and the braided shield should be trimmed to maintain the 6mm spacing of the driven elements off the backplane. 
![coax installed](https://raw.githubusercontent.com/cypnk/Cabin-Life/master/Directional%20Wifi%20Antenna/coax_installed.png)

Before soldering the braided coax, insert insulation dowels, cut at 6mm height, underneath the driven element squares (not under the wire, but the square itself). The braid is trimmed and soldered to the backplane and the center conductor to the driven element separation segment.
![insulators installed](https://raw.githubusercontent.com/cypnk/Cabin-Life/master/Directional%20Wifi%20Antenna/insulators_installed.png)

Once the braid and center conductor are soldered, the antenna is complete.
![antenna complete](https://raw.githubusercontent.com/cypnk/Cabin-Life/master/Directional%20Wifi%20Antenna/antenna_complete.png)

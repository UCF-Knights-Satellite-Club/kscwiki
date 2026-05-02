---
description: Hardware overview for the PSB Physics Ground Station.
---

# Hardware

## Station location

The ground station antennas are mounted on the roof of the UCF Physical Sciences Building. The station equipment rack is located in the PSB lab space.

Roof work requires at least one person in the lab and one person on the roof, with active communication between both groups.

## Antennas

The source notes identify three antenna-related systems:

* Yagi antenna for the 70 cm band.
* Dish antenna for the 13 cm band.
* Future 2 m antenna support was discussed in Fall 2025 notes.

The Yagi antenna and dish antenna should be co-aligned straight outward with the rotator.

## Cabling

Known cable runs and open details from the source notes:

* The Yagi antenna uses N-type coax.
* The rotator has two motor-control wires.
* The rotator may also require a separate power wire; this still needs confirmation.
* The dish antenna cable type still needs confirmation.
* The cable distance from the lab to the ground station is approximately 100 ft.

The Fall 2025 notes mention that coax attenuation may be a concern for the dish antenna frequency because of the long cable run.

## Radio equipment

The source documents identify two Icom radios:

* IC-R8600 software-defined radio.
* IC-9700 radio transceiver.

![IC-R8600 rear panel](../../../.gitbook/assets/physics-ground-station/images/system-overview/image1.jpg)

![IC-R8600 front panel](../../../.gitbook/assets/physics-ground-station/images/system-overview/image3.jpg)

## Power equipment

The rack includes Astron power distribution units. The source setup notes refer to Astron 1 and Astron 2 when powering radio equipment.

![Astron rack power units](../../../.gitbook/assets/physics-ground-station/images/system-overview/image4.jpg)

## Rack layout

The source rack-position file is preserved in the source documents folder. The extracted rack layout image is shown below for quick reference.

![Rack layout](../../../.gitbook/assets/physics-ground-station/images/system-overview/rack-image1.png)

## Open hardware questions

These items were listed as unresolved in the source notes:

* Confirm whether the rotator controller powers the rotator or whether there is a separate power cable.
* Confirm the specific rotator installed on the roof, including whether it is the 12 V or 18 V model.
* Confirm the dish antenna use case, cable type, and what equipment connects to it.
* Confirm cable specifications for the approximately 100 ft run.

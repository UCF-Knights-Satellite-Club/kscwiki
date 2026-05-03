---
description: Radio and software setup notes for the PSB Physics Ground Station.
---

# Radio and Software Notes

This page captures setup notes from the PSB ground station source documentation. Treat these notes as the current working procedure until they are verified during an operating session.

## IC-R8600

The IC-R8600 is documented as the station software-defined radio.

### Computer interface setup

1. Power on Astron 2 PDU.
2. Power on the radio.
3. Connect USB A from the computer to USB B on the radio I/Q OUT port.
4. Power on and set up the rotator controller.
5. Launch SDR Console v3.2.
6. Select the IC-R8600 radio.

![SDR Console radio selection](../../../.gitbook/assets/physics-ground-station/images/system-overview/image2.png)

## IC-9700

The IC-9700 is documented as the station radio transceiver.

### Computer interface setup

1. Power on Astron 1 PDU.
2. Power on the radio.
3. Complete the remaining radio-interface setup after the station team verifies the final IC-9700 connection procedure.

## Satellite tracking software

The source notes identify the following software:

* SDR Console v3.2 for SDR control.
* Orbitron for satellite tracking and rotator control.
* SpidAlfa 0.97 driver for Orbitron rotator support.
* FLRig for transceiver control.

The source notes indicate that Orbitron should be the main rotator-control program because the rotator documentation supports Orbitron through the SpidAlfa 0.97 driver. SDR Console's satellite interface can also use Orbitron rotor control in the background, allowing radio and rotor control through the SDR Console satellite interface.

## Network notes

Fall 2025 notes indicate:

* DHCP was turned off.
* Ethernet ran from the transceiver to the PC.
* The PC successfully pinged the radio.
* Future work may include connecting radios to the UCF Ethernet network for remote access.

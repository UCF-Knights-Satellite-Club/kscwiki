---
description: "Set up the radios and satellite tracking software."
---

# Radio and software

{% hint style="warning" %}
**These setup notes are incomplete.** There is no recorded test date.
{% endhint %}

## IC-R8600

This radio receives signals.

1. Turn on the power unit labeled Astron 2.
2. Turn on the radio.
3. Connect the cable’s USB-A end to the computer and its USB-B end to the radio port labeled **I/Q OUT**.
4. Turn on and set up the rotator controller.
5. Launch SDR Console v3.2 and select the IC-R8600.

## IC-9700

This radio can receive and transmit. Turn on Astron 1, then the radio. The steps for connecting it to the computer still need to be tested and written down.

## Tracking software

* SDR Console v3.2 — controls the receiver
* Orbitron — predicts satellite positions and controls antenna pointing
* SpidAlfa 0.97 — connects Orbitron to the rotator controller
* FLRig — controls the radio from the computer

The setup notes use Orbitron with SpidAlfa to move the antennas. SDR Console can also use Orbitron in the background.

Earlier Ethernet tests are in [Project notes](project-notes.md).

## SDR Console

![SDR Console radio selection](../../../.gitbook/assets/physics-ground-station/images/system-overview/image2.png)

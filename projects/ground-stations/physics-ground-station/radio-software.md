---
description: "Receiver, transceiver, and tracking setup."
---

# Radio and software

{% hint style="warning" %}
**Partial procedure.** Last tested: not recorded.
{% endhint %}

## IC-R8600

1. Power on Astron 2 PDU.
2. Power on the radio.
3. USB A on the computer to USB B on the radio I/Q OUT port.
4. Power on and set up the rotator controller.
5. Launch SDR Console v3.2 and select the IC-R8600.

## IC-9700

VHF/UHF all-mode transceiver. Power Astron 1, then the radio. Remaining interface steps still need a verified write-up.

## Tracking software

* SDR Console v3.2 — SDR control
* Orbitron — satellite tracking and rotator control
* SpidAlfa 0.97 — Orbitron rotator driver
* FLRig — transceiver control

The documented tracking path uses Orbitron with SpidAlfa. SDR Console can run Orbitron in the background.

Earlier Ethernet tests are in [Project notes](project-notes.md).

## SDR Console

![SDR Console radio selection](../../../.gitbook/assets/physics-ground-station/images/system-overview/image2.png)

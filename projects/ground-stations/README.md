---
icon: satellite-dish
---

# Ground Stations

<table data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td>Engineering Ground Station</td><td>Ongoing</td><td><a href="engineering-ground-station.md">engineering-ground-station.md</a></td></tr><tr><td>Physics Ground Station</td><td>Ongoing</td><td><a href="physics-ground-station/">physics-ground-station</a></td></tr></tbody></table>

## What is a ground station

A ground station is the Earth end of a radio link with a satellite. It receives information from orbit and, when authorized, sends signals back. Depending on the satellite, that information might be images, voice, or **telemetry**: measurements such as battery voltage and temperature that tell operators how the spacecraft is doing.

### Why timing and pointing matter

A satellite in low Earth orbit moves across the sky. A **pass** is the period when it is above the station's horizon; direct contact is limited to that window. The station needs to be ready at the right time and keep its directional antennas aimed at the moving satellite.

### How a receive pass works

1. **Predict the pass.** Tracking software uses orbital data to calculate when the satellite will appear and where to point.
2. **Aim the antennas.** A motorized mount, called a **rotator**, turns the antennas to follow the satellite across the sky.
3. **Receive the signal.** The antenna picks up radio waves. The receiver tunes to the satellite's frequency and produces audio or digital samples for the computer.
4. **Decode and save.** Software suited to the satellite's signal can turn the reception into usable information. The operator saves recordings or decoded data and logs the result.

[More about satellite communications — NASA](https://www.nasa.gov/smallsat-institute/sst-soa/ground-data-systems-and-mission-operations/)

### Getting started

Start by joining a receive-only session with an experienced operator. At Physics, follow [Run a receive pass](physics-ground-station/receive-pass.md).

Receiving and transmitting are separate activities. Amateur-radio transmissions require a licensed control operator and must stay within that operator's privileges. Follow the station's operating procedures. [Control operator duties](https://www.ecfr.gov/current/title-47/chapter-I/subchapter-D/part-97/subpart-B/section-97.105)

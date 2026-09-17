---
description: Details about the software components of T-Sat-2A.
---

# Software

#### Software Architecture

The T-Sat 2A software system supported image acquisition, altitude measurement, onboard data storage, wireless communication, and deployment control. The system consisted of flight software running on the onboard ESP32 and ground-station software used to monitor telemetry and initiate the separation sequence.

Software development began with independent module testing for the cameras, BMP388 altimeter, LoRa radio, SD card, and servo. These modules were later integrated into the flight software as the required electronics became available.

#### Flight Software

The onboard software controlled two cameras, the BMP388 altimeter, SD card, RFM95W LoRa radio, and deployment servo. Images and altitude data were stored locally on the SD card, providing a record of the mission even when wireless communication was interrupted.

The cameras and LoRa radio shared an SPI interface, requiring software coordination to prevent communication conflicts. The `spiBusy` flag restricted radio processing while the cameras accessed the SPI bus, while the `servoActive` flag managed communication during the deployment sequence.

Altitude telemetry was transmitted to the ground station approximately every 25 seconds and was also recorded locally. The software used a continuous main loop with an approximately three-second delay, selected during testing to provide more stable radio behavior.

#### Ground Station and Deployment Control

The ground station used an ESP32 and RFM95W LoRa radio to receive altitude telemetry and send deployment commands. When the operator pressed the deployment button, the ground station transmitted the `Detach` command and waited for the expected `Detached` acknowledgement.

A command cooldown was implemented to reduce the possibility of repeated deployment commands. However, the acknowledgement only confirmed that the software processed the command; it did not verify that the servo physically cut the fishing wire or that the parachute deployed. This distinction became important during the mission.


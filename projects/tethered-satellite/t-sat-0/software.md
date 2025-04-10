---
description: Details about the software used for T-Sat-0.
---

# Software

## Overview

T-Sat-0 utilizes 3 pieces of software. The [Flight Software](software.md#flight-software-tsat0-fsw), [Burnwire Receive Software](software.md#burnwire-receive-burnwire_recv), and [Burnwire Send Software](software.md#burnwire-send-burnwire_send). The main payload runs the Flight Software on a DOIT ESP32 DEVKIT V1. The Burnwire Receiver that attaches the payload to the balloon runs the Burnwire Recieve software on a Seeeduino XIAO. The Burnwire Transmitter runs the Burnwire Send software which also runs on a Seeeduino XIAO.

## Development Environment

All of the software is developed with the [Arduino IDE](https://www.arduino.cc/en/software/) and external libraries. Unless stated otherwise, all libraries can be found in the Arduino IDE Library Manager.

### Dependencies

* **Arduino ESP32 Core** ([installation instructions](https://docs.espressif.com/projects/arduino-esp32/en/latest/installing.html))
* **Seeeduino Arduino IDE Support** ([installation instructions](https://wiki.seeedstudio.com/Seeed_Arduino_Boards/))
* **Radiohead** by Mike McCauley (Arduino IDE Library Manager version is outdated, [download directly](http://www.airspayce.com/mikem/arduino/RadioHead/))
* **Adafruit MMA8451 Library** by Adafruit
* **Adafruit BMP3XX Library** by Adafruit
* **Adafruit GFX Library** by Adafruit
* **Adafruit SSD1306** by Adafruit
* **Arducam\_Mega** by Arducam
* **ESP32Servo** by Kevin Harrington

## Flight Software ([TSat0-FSW](https://github.com/UCF-Knights-Satellite-Club/Tethered-Sat-0/blob/main/software/TSat0-FSW/TSat0-FSW.ino))

The T-Sat-0 FSW is written in C++ using the ESP32 Arduino Core. This allows use of existing Arduino libraries and includes FreeRTOS. The FSW monitors altitude and accelerometer readings to determine when to deploy the parachute.

### Tasks

The Flight Software makes use of 3 main FreeRTOS tasks. All tasks run on one core since a single ESP32 core is more than enough and multi-core software is more complicated.

| Task Name      | Job Description                                                                    | Priority                                                                                                                       | Frequency         |
| -------------- | ---------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ | ----------------- |
| Check Altitude | Continuously monitor the altimeter and accelerometer and manage the state machine. | 2                                                                                                                              | 20 Hz             |
| Camera Capture | Capture pictures with the ArduCam and copy the image data to the SD card.          | [tskIDLE\_PRIORITY](https://www.freertos.org/Documentation/02-Kernel/02-Kernel-features/01-Tasks-and-co-routines/15-Idle-task) | Whenever possible |
| Log Data       | Write sensor data to the SD card.                                                  | 1                                                                                                                              | 10 Hz             |

The Check Altitude task must run at 20 Hz which means any functions need to return with minimal delay. Sensor data is pushed into a queue which the Log Data task then writes onto the SD card. This is to reduce contention between the SD card and ArduCam over the SPI bus to prevent delays.

### State Machine

The Flight Software utilizes a state machine to perform various tasks throughout the flight. The states can only move forwards and can only be reset by a reboot.

<table><thead><tr><th width="154">State Name</th><th width="151.5">Function</th><th>Description</th></tr></thead><tbody><tr><td>CALIBRATION</td><td>calibrationRun</td><td>Average several altimeter readings to determine starting altitude. Immediately moves to PREFLIGHT when done.</td></tr><tr><td>PREFLIGHT</td><td>preflightRun</td><td>Monitor altimeter and accelerometer to detect liftoff. Move to ASCENT once detected.</td></tr><tr><td>ASCENT</td><td>ascentRun</td><td>Monitor altimeter and accelerometer to detect Burnwire activation and free fall. Move to FREEFALL once detected.</td></tr><tr><td>FREEFALL</td><td>freefallRun</td><td>Monitor altitude during free fall and compare against preset deployment altitude.</td></tr><tr><td>LANDING</td><td>landingRun</td><td>Parachute deployed, (hopefully) gently return to the ground.</td></tr></tbody></table>

This system is designed to ensure that the parachute will always be deployed if the payload is in free fall and below the deployment altitude. This is done to be resilient against scenarios such as a premature separation.

### Image Capture

The ArduCam makes taking images extremely simple. JPEG encoded image data is copied from the camera over SPI and written directly to the SD card. Image transfer speed is limited by the SPI clock speed which is set to 1 MHz for stability. It takes 20-40 seconds to successfully transfer an image which necessitates the Camera Capture task to be run at the lowest priority to not inhibit other operations. Only data between the JPEG file header 0xFFD8 and the JPEG file footer 0xFFD9 is written to the SD card.

### SD Card

The SD card must be FAT32 formatted; exFAT will not work. We have had write issues due to the cards getting corrupted, a reformat usually fixes this.

Files will be written to a new folder each run named tsatlogX with X being incremented with each run. All sensor data is logged to data.csv and images written to picY.jpg with Y being incremented with each picture.

## Burnwire Receive ([burnwire\_recv](https://github.com/UCF-Knights-Satellite-Club/Tethered-Sat-0/blob/main/software/burnwire_recv/burnwire_recv.ino))

The Arduino program for T-sat 0 listens for a specific message from its ground station via (RH\_RF95) When it receives this message it activates a burn wire, which will cut and detach the T-sat from the ballon. It also sends a message back to ground confirming the burn process.

## Burnwire Send ([burnwire\_send](https://github.com/UCF-Knights-Satellite-Club/Tethered-Sat-0/blob/main/software/burnwire_send/burnwire_send.ino))

This Arduino program for T-sat 0 ground station, When a button is pressed, it sends the message ("BurnWire") to the T-sat using the RH\_RF95 LoRa radio module. it also turns on an LED indicating that the message is being sent, and waits for a reply from T-sat to confirm the burn process.&#x20;


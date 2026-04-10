---
description: >-
  Give an overview of how the code works and show the code (should have detailed
  comments in it already).
---

# Live Telemetry Code

## Telemetry

> Note: The code for these systems are documented quite well, so be sure to take a look at any comments in the code for additional information.

TSAT-2B has many on-board sensors, including pressure, temperature, and acceleration. From these, we can use pressure to derive altitude, and altitude + time to derive ascent velocity. Telemetry data is stored in all SI units.

Three systems work together to provide live telemetry on launch day:

* **Air**: This is the main board on TSAT-2B. It handles all communication with the satellite and collects all telemetry data.
* **Ground Pipe**: This is a receiver on the ground that allows a laptop to communicate with the Air controller.
* **Ground**: This is a Python program running on a laptop that displays and graphs received telemetry data.

All three systems are required for live telemetry, however if only on-board telemetry (and therefore post-landing data) is desired, then only `Air` is needed.

### Air

This is the main system that runs on TSAT-2B. While theoretically it can serve more purposes, its only purpose for this project is to collect sensor data and send it to the ground. Sensor data is collected and saved to the on-board SD card, and sent to the ground via the RFM69. While there is logic that allows `Air` to receive packets, for the purpose of this launch, it only sends `Telemetry` packets.

Once turned on, the system should initialize, showing a solid blue LED (via the built-in LED on the ESP32 dev board). If there is an error while initializing, the LED will begin blinking instead. See below for errors.

Every 500ms, a datapoint is collected through sensor data. This datapoint is saved to the SD card (appended to the CSV file), then converted into a telemetry packet. The telemetry packet is simply a C struct that is read as raw bytes and sent over the network. This is the easiest since it requires no (de)serialization for `Air` compared to other formats like JSON. This makes it very easy to compute and space efficient, but may be slightly riskier since it requires ensuring the structs have the correct alignment, and anything that communicates with it must use the same endianness. In the future, it may be useful to utilize more advanced protocols like CAN Bus if multiple systems are in use.

### Ground Pipe

This is a program that runs on an ESP32 on the ground. The ESP32 is hooked up to an RFM69 on the same frequency as `Air` (this can just be done on a breadboard). Any packets that are received on the ground are read as bytes and output to the UART bus as space-separated decimals. While this may seem weird, this offers an easy interface to transmit binary data without the pitfalls of non-packetized UART (such as having to create a protocol to delimit packets).

Example output:

```
0 0 0 1 209 200 189 109 139 172 215 86 145 19 61 103 86 127 37 248 79 172 192 30 195 108 7 43 115 141 176 217
```

`Ground` then reads this serial output, converts it to bytes, and decodes it using the Python `struct` module.

### Ground

This is the main ground program. This program has 2 main run modes.

* **Live**: This creates a serial connection to `Ground Pipe` from a device (`/dev/ttyUSBX` on Linux, `COMX` on Windows usually, replace X with a number). It will take any lines outputted by `Ground Pipe` and attempt to decode them using the Python struct module. Then, any telemetry packets are graphed live.
* **From File**: This opens a CSV file, specifically the CSV file recorded by on-board telemetry onto the SD card. The data is then graphed and displayed.

> Linux Note: If you get some type of 'Invalid Permission' error when trying to access the port, you might need to give yourself permissions. Ex: `sudo chmod a+rw /dev/ttyUSBX`

> Windows Note: You may need to download [Serial Drivers](https://meshtastic.org/docs/getting-started/serial-drivers/esp32/) in order for windows to correctly recognize the serial device.

We use plotly to graph data, mainly because matplotlib began to be very slow for this use case. In the plotly interface, there are 2 options at the top-left of the screen:

* **Autoscale 60s**: Displays the last 60s of data, scrolling when new data comes in.
* **Show Packet Loss**: Replaces the KSC logo with a packet loss graph, showing the percentage of packets lost within a timeframe. This will be 0 when loading from a file.

### Errors

If the `Air` system errors, it will begin to blink the blue LED. How many blinks occur depends on the type of error, as seen below:

* **1 Blink**: Radio is unable to initialize.
* **2 Blinks**: SD card is unable to initialize. Check that the SD card is formatted (Fat32) and inserted correctly. If this continues to happen, try reformatting the card anyways, since it may look correct but secretly not be (this is a real issue that happened).
* **3 Blinks**: Same as above, unsure if this can happen.

If the USB cable on the laptop disconnects the `Ground Pipe` system, the `Ground` system program will disconnect the socket. Unfortunately, there is no way to recover from this besides restarting the `Ground` software, losing all live telemetry data.



All information here is courtesy of Fred Reynolds (lead software engineer for T-Sat-2B).

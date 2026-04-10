---
description: Still need PCB design/diagram, and a wiring diagram.
---

# Electronics and PCB

Despite being in such a compact area, the live video and telemetry systems have largely separate electronics and are completely independent of each other.

For our live telemetry system, we had to design a PCB that would house all of the electronic components for that system. The following is a list of electronics used on the PCB.

1. ESP 32
   1. [https://a.co/d/1jCVLdx](https://a.co/d/1jCVLdx)
2. JST Connector
   1. [https://www.adafruit.com/product/1769](https://www.adafruit.com/product/1769)
3. 3.3V Buck Converter
   1. [https://www.adafruit.com/product/4711](https://www.adafruit.com/product/4711)
4. BMP388 (Temperature and Pressure Sensor)
   1. [https://www.adafruit.com/product/3966](https://www.adafruit.com/product/3966)
5. MMA 8451 (Accelerometer)
   1. [https://www.adafruit.com/product/2019](https://www.adafruit.com/product/2019)
6. RFM69HCW 915 MHz Transceiver
   1. [https://www.adafruit.com/product/3070](https://www.adafruit.com/product/3070)
7. Bump Switch
8. SD Card Breakout Board

We did not design a PCB for the live video system. Instead, this system had everything wired through the Raspberry Pi. The electronics for the live video system are listed below.

1. Raspberry Pi 0 2 W
   1. Bought on Digikey
2. ASUS USB-AC56 WiFi Adapter (2 were used)
   1. [ https://www.ebay.com/itm/336233816072](https://www.ebay.com/itm/336233816072)
3. TPS61023 5V Boost Converter&#x20;
   1. [https://www.adafruit.com/product/4654](https://www.adafruit.com/product/4654)
4. JST-PH 2-Pin Breakout
   1. [https://www.adafruit.com/product/1862](https://www.adafruit.com/product/1862)

The live video and live telemetry systems are independent, so they run their own software too. Live telemetry works using code created by Fred R, Adam S, and Tolu E. This code can be found in the "Live Telemetry Code" section of this project.&#x20;

Live video was run on a third-party software known as "OpenHD". Further details about OpenHD can be found in the "OpenHD" section of this project.


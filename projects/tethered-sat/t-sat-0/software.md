# Software

T-Sat-0 utilizes 3 pieces of software. The Flight Software, Burnwire Receive Software, and Burnwire Send Software. The main payload runs the Flight Software on an ESP32. The Burnwire Receiver that attaches the payload to the balloon runs the Burnwire Recieve software on a Seeeduino XIAO. The Burnwire Transmitter runs the Burnwire Send software which also runs on a Seeeduino XIAO.

## Flight Software ([TSat0-FSW](https://github.com/UCF-Knights-Satellite-Club/Tethered-Sat-0/blob/main/software/TSat0-FSW/TSat0-FSW.ino))

The T-Sat-0 Flight Software is written in C++ using the ESP32 Arduino Core. This allows use of existing Arduino libraries and includes FreeRTOS. Though not required, the easiest way to develop the Flight Software is with the Arduino IDE.

### Tasks

The Flight Software makes use of 3 main FreeRTOS tasks. All tasks run on one core since a single ESP32 core is more than enough and multi-core software is more complicated.

| Task Name      | Job Description                                                                    | Priority                                                                                                                       | Frequency         |
| -------------- | ---------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ | ----------------- |
| Check Altitude | Continuously monitor the altimeter and accelerometer and manage the state machine. | 2                                                                                                                              | 20 Hz             |
| Camera Capture | Capture pictures with the ArduCam and copy the image data to the SD card.          | [tskIDLE\_PRIORITY](https://www.freertos.org/Documentation/02-Kernel/02-Kernel-features/01-Tasks-and-co-routines/15-Idle-task) | Whenever possible |
| Log Data       | Write sensor data to the SD card.                                                  | 1                                                                                                                              | 10 Hz             |

The Check Altitude task pushes data into a queue which the Log Data task then writes onto the SD card. This is to reduce contention between the SD card and ArduCam over the SPI bus and ensure that the Check Altitude task can always run without delay.

### State Machine

The Flight Software utilizes a state machine to perform various tasks throughout the flight. The states can only move forwards and can only be reset by a reboot.

| State Name  | Description                                                                                                      |
| ----------- | ---------------------------------------------------------------------------------------------------------------- |
| CALIBRATION | Average several altimeter readings to determine starting altitude. Immediately moves to PREFLIGHT when done.     |
| PREFLIGHT   | Monitor altimeter and accelerometer to detect liftoff. Move to ASCENT once detected.                             |
| ASCENT      | Monitor altimeter and accelerometer to detect Burnwire activation and free fall. Move to FREEFALL once detected. |
| FREEFALL    | Monitor altitude during free fall and compare against preset deployment altitude.                                |
| LANDING     | Parachute deployed, (hopefully) gently return to the ground.                                                     |

This system is designed to ensure that the parachute will always be deployed if the payload is in free fall and below the deployment altitude. This is done to be resilient against scenarios such as a premature separation.

### Image Capture

The ArduCam makes taking images extremely simple. JPEG encoded image data is copied from the camera over SPI and written directly to the SD card. Image transfer speed is limited by the SPI clock speed which is set to 1 MHz for stability. It takes 20-40 seconds to successfully transfer an image which necessitates the Camera Capture task to be run at the lowest priority to not inhibit other operations. Only data between the JPEG file header 0xFFD8 and the JPEG file footer 0xFFD9 is written to the SD card.

## Burnwire Receive ([burnwire\_recv](https://github.com/UCF-Knights-Satellite-Club/Tethered-Sat-0/blob/main/software/burnwire_recv/burnwire_recv.ino))

The Arduino program for T-sat 0 listens for a specific message from its ground station via (RH\_RF95) When it receives this message it activates a burn wire, which will cut and detach the T-sat from the ballon. It also sends a message back to ground confirming the burn process.

## Burnwire Send ([burnwire\_send](https://github.com/UCF-Knights-Satellite-Club/Tethered-Sat-0/blob/main/software/burnwire_send/burnwire_send.ino))

This Arduino program for T-sat 0 ground station, When a button is pressed, it sends the message ("BurnWire") to the T-sat using the RH\_RF95 LoRa radio module. it also turns on an LED indicating that the message is being sent, and waits for a reply from T-sat to confirm the burn process.&#x20;


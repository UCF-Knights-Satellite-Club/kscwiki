---
description: Documentation of the changes between the TSat-0 and TSat-1 flight software.
---

# Software

Since TSat-1 used the same electronics as TSat-0, most of the software stayed the same. The main differences were removal of accelerometer based triggers and improvements to the picture writing code.

## Accelerometer Triggers

The accelerometer-based triggers for TSat-0 caused premature parachute deployment. Improved data filtering or processing was considered but the barometric altimeter data was very reliable so we decided to move forwards using only altimeter data.

## Picture Transfers

One of the biggest problems with TSat-0 was the slow picture rates. Since the Arducam and SD card use SPI, we are somewhat limited in the speed which we can transfer data. We also had a high rate of corrupted pictures where all JPEG data after a certain point was missing.

### Buffer Size

The code works by reading blocks of data from the cameras using the `readBuff` function provided by Arducam. This function can only read 254 bytes at a time which is then written to the SD card. The ESP32 SD card library is much more efficient with larger writes so we increased the buffer size to 4096 bytes and filled it with multiple calls to `readBuff`.

This appeared to speed up file writes fairly significantly. At the time we also thought it somewhat improved the situation with corrupted files but that may have just been due to faster transfers providing less time for whatever was causing the corruption to occur.

### Image Corruption

This was the most important fix. What's the point of having a camera if all the images are corrupted?

We confirmed that all image data was being transferred from the Arducam to the ESP32 by checking for the JPEG magic bytes `0xFFD8` and `0xFFD9` which signify the start and end of a JPEG file. The ESP32 was always finding the ending bytes but on corrupted images they were missing indicating the bug was with writing data to the SD card. After more investigation, we found that calls to `write` from the ESP32 Arduino Core would sometimes fail and return 0 bytes written. The code did not previously check for the return value and assumed that all bytes got written.

The really strange thing is that once `write` would fail and return 0, all subsequent calls would also fail and return 0. The only way we could find to get `write` to work was to close and reopen the file. The new code checks for that 0 return value and automatically closes and opens the file. This drastically reduced the frequency of corrupted images.

### SPI Clock Speed

We previously slowed down the clock speed because it helped with the corruption problems. This worked, but meant that it could take 30 seconds to write a single \~500 KB JPEG file. This meant that our first flight which lasted a little longer than 3 minutes only recorded 16 photos. The system should be capable of much more than that.

Once we found the main corruption issue, we experimented with increasing the SPI clock speed. We originally had it reduced to around 1 MHz and were able to increase it to 16 MHz before the SD card started crashing. This increased the speed for copying images off the cameras as well as the SD writing speed so had a very significant effect. Over the \~4 minute flight we recorded over 80 photos.

## I2C Clock Speed

We occasionally noticed some issues with our I2C devices. Devices would fail to initialize with errors such as these.

```
E (9) i2c.master: I2C hardware NACK detected
E (10) i2c.master: I2C transaction unexpected nack detected
E (10) i2c.master: s_i2c_synchronous_transaction(924): I2C transaction failed
E (15) i2c.master: i2c_master_transmit_receive(1220): I2C transaction failed
```

The I2C bus speed defaults to 100 kHz when using the ESP32 Arduino Core. Using a logic analyzer we saw invalid packets and a lot of NACK packets in these error states. We tried decreasing the clock speed to 50 kHz which permanently resolved this issue.

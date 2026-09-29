# **🚀 ESP32-S3 n16r8 Retro-Go Handheld Console – Hardware & Pinout Guide**

This repository contains the exact pin mapping, hardware wiring tables, microSD card layout, and firmware flashing steps for building a DIY portable retro gaming console using the **ESP32-S3 n16r8** dev board, **ILI9341 Display**, **MAX98357A I2S Audio Amplifier**, and **Retro-Go** firmware.

📥 **Download Firmware & Flasher:** [Download from Google Drive](https://drive.google.com/file/d/1HBvIWh_ksgA0kvTYS_lbayI8zbT-Zi2u/view?usp=sharing)

📺 Watch the Full Project Video on YouTube: https://youtu.be/DYWG1luQNXs

##

## **📌 ESP32-S3 Pinout & Wiring Table**

###

### **1\. Display (ILI9341 SPI) Connections**

| **Screen Pin**  | **ESP32-S3 GPIO Pin** | **Description / Wiring Ucu**                            |
| --------------- | --------------------- | ------------------------------------------------------- |
| **VCC**         | **3.3V**              | Display Power Supply                                    |
| ---             | ---                   | ---                                                     |
| **GND**         | **GND**               | Common Ground                                           |
| ---             | ---                   | ---                                                     |
| **MOSI / SDA**  | **GPIO 12**           | SPI Data Line                                           |
| ---             | ---                   | ---                                                     |
| **SCK / SCLK**  | **GPIO 48**           | SPI Clock Line                                          |
| ---             | ---                   | ---                                                     |
| **DC / RS**     | **GPIO 47**           | Data / Command Selector                                 |
| ---             | ---                   | ---                                                     |
| **RST / RESET** | **GPIO 3**            | Display Reset Pin                                       |
| ---             | ---                   | ---                                                     |
| **LED / BL**    | **GPIO 39**           | Display Backlight                                       |
| ---             | ---                   | ---                                                     |
| **CS**          | **GND**               | Defined as GPIO_NUM_NC in code; connect directly to GND |
| ---             | ---                   | ---                                                     |

###

### **2\. Integrated MicroSD Card Connections**

| **SD Card Pin**  | **ESP32-S3 GPIO Pin** | **Description**     |
| ---------------- | --------------------- | ------------------- |
| **SD_CS**        | **GPIO 10**           | MicroSD Chip Select |
| ---              | ---                   | ---                 |
| **SD_MOSI**      | **GPIO 11**           | MicroSD Data Input  |
| ---              | ---                   | ---                 |
| **SD_SCK / CLK** | **GPIO 13**           | MicroSD Clock Line  |
| ---              | ---                   | ---                 |
| **SD_MISO**      | **GPIO 9**            | MicroSD Data Output |
| ---              | ---                   | ---                 |

###

### **3\. Audio (I2S DAC - MAX98357A) Connections**

| **Audio Module Pin** | **ESP32-S3 GPIO Pin** | **Description**                 |
| -------------------- | --------------------- | ------------------------------- |
| **BCK / BCLK**       | **GPIO 41**           | Bit Clock                       |
| ---                  | ---                   | ---                             |
| **LRCK / WS**        | **GPIO 42**           | Word Select (Left/Right Clock)  |
| ---                  | ---                   | ---                             |
| **DIN / DATA**       | **GPIO 40**           | Data Input                      |
| ---                  | ---                   | ---                             |
| **AMP ENABLE**       | **GPIO 18**           | Amplifier Enable / Shutdown Pin |
| ---                  | ---                   | ---                             |

###

### **4\. Directional Buttons (D-Pad - Digital / Direct Wiring)**

**How to Wire:** Connect Leg 1 of each button to its assigned GPIO pin. Connect Leg 2 directly to **GND**. No external resistors required.

| **Button Name** | **Function**      | **ESP32-S3 GPIO Pin** | **Other Leg** |
| --------------- | ----------------- | --------------------- | ------------- |
| **UP**          | Direction (Up)    | **GPIO 1**            | **GND**       |
| ---             | ---               | ---                   | ---           |
| **DOWN**        | Direction (Down)  | **GPIO 2**            | **GND**       |
| ---             | ---               | ---                   | ---           |
| **LEFT**        | Direction (Left)  | **GPIO 6**            | **GND**       |
| ---             | ---               | ---                   | ---           |
| **RIGHT**       | Direction (Right) | **GPIO 7**            | **GND**       |
| ---             | ---               | ---                   | ---           |

###

### **5\. Action & Menu Buttons (Digital / Direct Wiring)**

**How to Wire:** Connect Leg 1 of each button to its assigned GPIO pin. Connect Leg 2 directly to **GND**. No external resistors required.

| **Button Name** | **Function**       | **ESP32-S3 GPIO Pin** | **Other Leg** |
| --------------- | ------------------ | --------------------- | ------------- |
| **A BUTTON**    | Confirm / Action A | **GPIO 15**           | **GND**       |
| ---             | ---                | ---                   | ---           |
| **B BUTTON**    | Back / Action B    | **GPIO 5**            | **GND**       |
| ---             | ---                | ---                   | ---           |
| **SELECT**      | Select             | **GPIO 16**           | **GND**       |
| ---             | ---                | ---                   | ---           |
| **START**       | Start              | **GPIO 17**           | **GND**       |
| ---             | ---                | ---                   | ---           |
| **MENU**        | Retro-Go Menu      | **GPIO 8**            | **GND**       |
| ---             | ---                | ---                   | ---           |

##

## **💾 MicroSD Card Directory Structure & Game Formats**

Format your MicroSD card to **FAT32** and organize your game ROMs using the following directory layout:

Plaintext

MicroSD Card (FAT32)

└── roms/

├── gb/ <-- Game Boy ROMs (.gb)

├── gbc/ <-- Game Boy Color ROMs (.gbc)

├── gba/ <-- Game Boy Advance ROMs (.gba)

├── nes/ <-- Nintendo (NES / Famicom) ROMs (.nes)

├── sms/ <-- Sega Master System ROMs (.sms)

├── gg/ <-- Sega Game Gear ROMs (.gg)

├── col/ <-- ColecoVision ROMs (.col)

├── pce/ <-- PC Engine / TurboGrafx-16 (.pce)

├── lynx/ <-- Atari Lynx ROMs (.lnx)

├── wsc/ <-- WonderSwan Color (.wsc)

└── prboom/ <-- Doom game file (DOOM.WAD)

## 

## **⚡ How to Flash Firmware (.img) Using ESP-Flasher**

You do not need to install complex build tools (like ESP-IDF or PlatformIO) to flash this console. The flasher application (**ESP-Flasher**) is included directly inside the project ZIP file.

1. **Extract the ZIP File:** Extract the downloaded ZIP file on your computer. You will see the retro-go and ESP-Flasher folders.
2. **Connect the Board:** Connect your ESP32-S3 development board to your PC using a USB cable.
3. **Run ESP-Flasher:** Open the ESP-Flasher folder and execute ESP-Flasher.exe.
4. **Select Port & Firmware File:**
   - **COM Port:** Select the COM port corresponding to your connected ESP32-S3 board.
   - **Firmware:** Browse to the retro-go folder and select the **retro-go_1.46-dirty_esp32-s3-devkit.img** file.
5. **Flash the Image:** Click the **Flash!** button and wait for the pro

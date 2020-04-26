# Xiaomi_LYWSD03MMC_for_HA
Collecting data via Bluetooth from the Xiaomi LYWSD03MMC Temperature Display using ESP32 running Micropython

## Introduction
I have developed this project to integrate the Xiaomi LYWSD03MMC LCD temperature and Humidity display with Home Assistant.


<p align="center">
  <img width="460" src="resources/Xiaomi_LYWSD03MMC.png">
</p>

The display outputs Temperature, Humidity and Battery level using Bluetooth Low Energy (BLE). This means we need some sort of hub to collect the data and render it in a way that Home Assistant understands. I initially chose to use a Raspberry Pi W for this job as it has built-in support for BLE, but this repository uses a much cheaper ESP32. 

MQTT is an efficient way for remote devices to communicate with Home Assistant, so I added suport for this.
## Building The Solution

Download Micropython with BLE support from https://micropython.org/resources/firmware/esp32spiram-idf4-20191220-v1.12.bin

Install esptool using the instructions here https://github.com/espressif/esptool

Connect your ESP32 board to your serial port by the usb port on the board or an external serial to usb convertor.

If you are putting MicroPython on your board for the first time then you should first erase the entire flash using:

```esptool.py --chip esp32 --port /dev/ttyUSB0 erase_flash```

From then on program the firmware starting at address 0x1000:

```esptool.py --chip esp32 --port /dev/ttyUSB0 --baud 460800 write_flash -z 0x1000 esp32spiram-idf4-20191220-v1.12.bin```

Note - if you are using windows the port will be the com port that you ESP32 is connected to e.g.
```esptool.py --chip esp32 --port com3 erase_flash```

Using a terminal emulator program, such as putty, connect to the ESP32 board at 115200 BAUD.
You should see a screen like this.

<p align="center">
  <img width="800" src="resources/Micropython Prompt.png">
</p>

Now close the terminal emulator and install ampy using the instructions from Adafruit here https://learn.adafruit.com/micropython-basics-load-files-and-run-code/install-ampy

Now you need to download the files:
* ble.py
* mqtt.py
* main.py

Now run  ```ampy -p com3 put ble.py```
and ```ampy-p com3 put mqtt.py```

Don't upload main.py yet.



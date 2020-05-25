# ESP32_stuff
Learning how to ESP32

# Micropython:  
### Installing epstool.py etc  
1. Used anaconda, created new env esp32 `conda create --name esp32`  
2. switch into it `conda activate esp32`  
3. install esptool `conda install -c conda-forge esptool`  
4. esptool.py is now in my path :)  

### Erasing Flash
0. Source: https://docs.micropython.org/en/latest/esp32/tutorial/intro.html  
0. Firmwares: https://micropython.org/download/esp32/  
1. Plugin device, came up as ttyUSB0 for me  
2. Enter bootloader mode, hold boot, press en (restart apparently)  
3. Run flash:
```
(esp32) bung@cubert:~$ esptool.py --port /dev/ttyUSB0 erase_flash
esptool.py v2.8
Serial port /dev/ttyUSB0
Connecting........_____....._
Detecting chip type... ESP32
Chip is ESP32D0WDQ6 (revision 1)
Features: WiFi, BT, Dual Core, 240MHz, VRef calibration in efuse, Coding Scheme None
Crystal is 40MHz
MAC: 24:62:ab:dd:95:2c
Uploading stub...
Running stub...
Stub running...
Erasing flash (this may take a while)...
Chip erase completed successfully in 13.6s
Hard resetting via RTS pin...
```  
4. Installing the new bootloader. The choice of bootloader was not obvious, I went with the SPIRAM which alledgidly adds a lot of RAM (16MB), dispite is being a lot slower access (again alledgidly). 
```
(esp32) bung@cubert:~$ esptool.py --chip esp32 --port /dev/ttyUSB0 write_flash -z 0x1000 Downloads/esp32spiram-idf3-20191220-v1.12.bin 
esptool.py v2.8
Serial port /dev/ttyUSB0
Connecting........___
Chip is ESP32D0WDQ6 (revision 1)
Features: WiFi, BT, Dual Core, 240MHz, VRef calibration in efuse, Coding Scheme None
Crystal is 40MHz
MAC: 24:62:ab:dd:95:2c
Uploading stub...
Running stub...
Stub running...
Configuring flash size...
Auto-detected Flash size: 4MB
Compressed 1327936 bytes to 816930...
Wrote 1327936 bytes (816930 compressed) at 0x00001000 in 72.1 seconds (effective 147.3 kbit/s)...
Hash of data verified.

Leaving...
Hard resetting via RTS pin...
```  

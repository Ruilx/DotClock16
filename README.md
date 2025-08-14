# Dot Clock 16

A simple LED 16*64 dot clock has RTC date & time, temperature, and sync with network time automatically.

## Hardware

* MCU: ESP32-DOWDQ6 with 2.4GHz Wi-Fi & Bluetooth
* FLASH: 25Q32 4MB
* UART: CH340C
* DISPLAY: 16*64 Red LED with 16pin connector
* RTC: DS1307 or DS3231
* TEMPERATURE: DS18B20
* EEPROM: 24C32 4KB

## Software

* ESP-IDF
* PlatformIO
* Arduino
* LVGL

## Component definition

1. ESP32-DOWDQ6 Connector
   `2.54 * 2 (gap 7) * 13`

| PIN | FUNCTION                               | PIN | FUNCTION                                    |
| --: | :------------------------------------- | --: | :------------------------------------------ |
|   1 | `GPIO_13` `HSPI_MOSI`              |  26 | `GND`                                     |
|   2 | `GPIO_15`                            |  25 | `GPIO_12` `HSPI_MISO`                   |
|   3 | `GPIO_2` **DOWNLOAD**          |  24 | `GPIO_14` `HSPI_SCK`                    |
|   4 | `GPIO_0` **BOOTLOADER**       |  23 | `GPIO_27`                                 |
|   5 | `GPIO_4`                             |  22 | `GPIO_26` `I2C1_SDA`                    |
|   6 | `GPIO_16` `UART2_RX`               |  21 | `GPIO_25` `I2C1 SCL`                    |
|   7 | `GPIO_17` `UART2_TX`               |  20 | `GPIO_33`                                 |
|   8 | `GPIO_5`                             |  19 | `GPIO_32`                                 |
|   9 | `GPIO_18` `VSPI_SCK` `I2C0_SCL`  |  18 | `GPIO_35` `VDET_2` **ONLY_INPUT** |
|  10 | `GPIO_23` `VSPI_MOSI`              |  17 | `GPIO_34` `VDET_1` **ONLY_INPUT** |
|  11 | `GPIO_19` `VSPI_MISO` `I2C0_SDA` |  16 | `EN`                                      |
|  12 | `GPIO_22`                            |  15 | `VN` `GPIO_39` **ONLY_INPUT**     |
|  13 | `3V3`                                |  14 | `VP` `GPIO_36` **ONLY_INPUT**     |

2. DS1307 & 24C32 & DS18B20 Connector
   `2.54 * 1 * 7`

| PIN | FUNCTION       | Connection   |
| --: | :------------- | ------------ |
|   1 | `DS1307_SQW` | `GPIO_34`  |
|   2 | `DS18B20_DS` | `GPIO_5`   |
|   3 | `I2C_SCL`    | `I2C1_SCL` |
|   4 | `I2C_SDA`    | `I2C1_SDA` |
|   5 | `3V3`        |              |
|   6 | `GND`        |              |
|   7 | `BAT`        |              |

3. DS3231 Connector (optional)
   `2.54 * 1 * 6`

| PIN | FUNCTION       | Connection   |
| --: | :------------- | ------------ |
|   1 | `DS3231_32K` |              |
|   2 | `DS3231_SQW` | `GPIO_34`  |
|   3 | `I2C_SCL`    | `I2C1_SCL` |
|   4 | `I2C_SDA`    | `I2C1_SDA` |
|   5 | `3V3`        |              |
|   6 | `GND`        |              |

4. 16*64 F3.75 Red LED Board Connector
   `2.54 * 2 * 8`

| PIN | FUNCTION   | Connection    | PIN | FUNCTION | Connection   |
| --- | ---------- | ------------- | --- | -------- | ------------ |
| 1   | `GND`    |               | 16  | `A`    | `GPIO_16`  |
| 2   | `GND`    |               | 15  | `B`    | `GPIO_17`  |
| 3   | `GND`    |               | 14  | `C`    | `GPIO_32`  |
| 4   | `EN`     | `GPIO_4`    | 13  | `D`    | `GPIO_33`  |
| 5   | `RED_DS` | `HSPI_MOSI` | 12  | `(NC)` |              |
| 6   | `(NC)`   |               | 11  | `(NC)` |              |
| 7   | `GND`    |               | 10  | `LT`   | `GPIO_27`  |
| 8   | `GND`    |               | 9   | `SCK`  | `HSPI_SCK` |

`POWER SUPPLY`

| PIN | FUNCTION |
| --: | :------- |
|   1 | `+5V`  |
|   2 | `GND`  |

5. SPI LCD connector (optional)
   `2.54 * 1 * 8`

| PIN | FUNCTION | Connection    |
| --: | :------- | ------------- |
|   1 | `GND`  |               |
|   2 | `3V3`  |               |
|   3 | `SCK`  | `VSPI_SCK`  |
|   4 | `MOSI` | `VSPI_MOSI` |
|   5 | `RES`  | `GPIO_12`   |
|   6 | `DC`   | `GPIO_27`   |
|   7 | `CS`   | `GPIO_14`   |
|   8 | `BLK`  | `GPIO_13`   |

6. SPI SD card connector (optional)
   `2.54 * 1 * 6`

| PIN | FUNCTION    | Connection    |
| --: | :---------- | ------------- |
|   1 | `GND`     |               |
|   2 | `3V3`     |               |
|   3 | `SD_MISO` | `VSPI_MISO` |
|   4 | `SD_MOSI` | `VSPI_MOSI` |
|   5 | `SD_SCK`  | `VSPI_SCK`  |
|   6 | `SD_CS`   | `GPIO_22`   |

7. External IIC Connection header
   `2.54 * 1 * 4`

| PIN | FUNCTION | Connection   |
| --: | :------- | ------------ |
|   1 | `GND`  |              |
|   2 | `3V3`  |              |
|   3 | `SCK`  | `I2C1_SCK` |
|   4 | `SDA`  | `I2C1_SDA` |

8. MAX7219 LED Matrix Connector (optional)
   **Not compatible with 16*64 LED**
   `2.54 * 1 * 5`

| PIN | FUNCTION | Connection   |
| --: | :------- | ------------ |
|   1 | `VCC`  |              |
|   2 | `GND`  |              |
|   3 | `DIN`  | `HSPI_SCK` |
|   4 | `CS`   | `GPIO_4`   |
|   5 | `CLK`  | `HSPI_CLK` |

9. WS2812 Connector (header)

| PIN | FUNCTION | Connection  |
| --: | -------- | ----------- |
|   1 | `GND`  |             |
|   2 | `VCC`  |             |
|   3 | `DATA` | `GPIO_15` |

## Components

1. 1 * ESP32-DOWDQ6 Connector
2. 1 * 16*64 F3.75 Red LED Board Connector
3. 1 * DS1307 & 24C32 & DS18B20 Connector
4. 1 * DS3231 Connector (Not used)
5. 1 * SD Card Connector (Not used)
6. 1 * External IIC Connection header (Not used)
7. 1 * MAX7219 LED Matrix Connector (not used)
8. 1 * Type-C USB Power Supply Connector
9. 1 * LDO 5V to 3.3V Voltage Level Converter
10. 3.3 to 5v IO voltage level converter (using mosFET)
11. 1 * Reset button

```

```

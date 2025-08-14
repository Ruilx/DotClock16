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
| 1   | `GND`    |               | 16  | `A`    | `GPIO_16` |
| 2   | `GND`    |               | 15  | `B`    | `GPIO_17` |
| 3   | `GND`    |               | 14  | `C`    | `GPIO_32` |
| 4   | `EN`     | `GPIO_4`    | 13  | `D`    | `GPIO_33` |
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
|   5 | `RES`  | `GPIO_12` |
|   6 | `DC`   | `GPIO_27` |
|   7 | `CS`   | `GPIO_14` |
|   8 | `BLK`  | `GPIO_13` |

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

|  PIN | FUNCTION | Connection |
| ---: | -------- | ---------- |
|    1 | `GND`    |            |
|    2 | `VCC`    |            |
|    3 | `DATA`   | `GPIO_15`  |



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
10. 3.3 to 5v converter
11. 1 * Reset button

## Connection diagrams

1. ESP32-DOWDQ6 HSPI -> F3.75 Red LED Board

* A pin: GPIO 32
* B pin: GPIO 33
* C pin: GPIO 34
* D pin: GPIO 35
* LT pin: GPIO 27

2. ESP32-DOWDQ6 HSPI -> MAX7219 LED Matrix

* CS pin: GPIO ?

3. ESP32-DOWDQ6 VSPI -> SD Card

* CS pin: GPIO 5

4. ESP32-DOWDQ6 VSPI -> SPI NAND Flash

* CS pin: GPIO 2

5. ESP32-DOWDQ6 VSPI -> SPI LCD

* CS pin: GPIO 15
* DC pin: GPIO 4
* RST pin: GPIO ?
* BLK pin: GPIO 22

6. ESP32-DOWDQ6 I2C1 -> DS1307 & 24C32

* SQW pin: GPIO ?

7. ESP32-DOWDQ6 I2C1 -> DS3231

* SQW pin: GPIO ?

8. DS18B20

* DS pin: GPIO ?

## Connection diagrams

## Connection diagrams

1. ESP32-DOWDQ6 HSPI -> F3.75 Red LED Board (主功能，优先保证)

* A pin: GPIO 32
* B pin: GPIO 33
* C pin: GPIO 25
* D pin: GPIO 26
* LT pin: GPIO 27
* EN pin: GPIO 4
* SCK: GPIO 14
* MOSI: GPIO 13
* MISO: GPIO 19

2. ESP32-DOWDQ6 I2C1 -> DS1307 & 24C32（或DS3231）

* SCL: GPIO 16
* SDA: GPIO 17
* SQW: 预留焊盘或直连ESP32某GPIO（如需外部中断，可用，否则可不连）

3. DS18B20 temperature sensor

* DATA: GPIO 5
  说明：

- 主功能（ESP32、DS1307/DS3231、DS18B20、LED点阵屏）优先保证直连，确保驱动能力和可靠性。
- SQW等辅助信号根据实际需求决定是否连接，推荐连接到GPIO27或GPIO33。
- 避免使用GPIO0、2、12、15、34~39等有特殊功能或仅输入的引脚作为关键输出或中断。
- 可选模块仅预留接口，实际使用时再考虑扩展芯片或GPIO分配，避免资源浪费。

---

可选/扩展功能（仅预留焊盘或说明，不分配GPIO）：
4. SPI LCD/SD卡/NAND Flash/MAX7219等模块

* 推荐仅预留接口焊盘，实际使用时可通过74HC595扩展片选/控制信号（如CS、DC、RST、BLK等），如有剩余GPIO可灵活分配。
* LCD的BLK可直接接电源，RST可用上电复位电路或与EN共用，无需单独GPIO。
* 可选模块与主功能不同时使用时，部分GPIO可复用。

说明：

- 主功能（ESP32、DS1307/DS3231、DS18B20、LED点阵屏）优先保证直连，确保驱动能力和可靠性。
- SQW等辅助信号根据实际需求决定是否连接。
- 可选模块仅预留接口，实际使用时再考虑扩展芯片或GPIO分配，避免资源浪费。| 功能模块    | 信号/接口 | ESP32 GPIO分配建议 |
  | ----------- | --------- | ------------------ |
  | LED点阵屏   | HSPI SCK  | GPIO 14            |
  |             | HSPI MOSI | GPIO 13            |
  |             | HSPI MISO | GPIO 19            |
  |             | A/B/C/D   | GPIO 32/33/25/26   |
  |             | LT        | GPIO 27            |
  |             | EN        | GPIO 4             |
  | RTC/EEPROM  | I2C SCL   | GPIO 25            |
  |             | I2C SDA   | GPIO 26            |
  | DS18B20温度 | DATA      | GPIO 2             |

### 2. 扩展功能GPIO分配（建议用74HC芯片扩展）

| 功能模块       | 信号/接口     | 建议扩展方式    |
| -------------- | ------------- | --------------- |
| SPI SD卡       | CS            | 74HC138扩展     |
| SPI NAND Flash | CS            | 74HC138扩展     |
| SPI LCD        | CS/DC/RST/BLK | 74HC138/595扩展 |
| MAX7219矩阵    | CS            | 74HC138扩展     |
| 其他控制信号   |               | 74HC595扩展     |

### 3. 扩展芯片选型说明

- 推荐使用74HC138（3-8译码器）扩展SPI设备的片选信号（CS），节省GPIO。
- 推荐使用74HC595（串行转并行）扩展LCD等模块的控制信号（如DC、RST、BLK），或LED屏行选等。
- 74HC系列速度和兼容性适合ESP32，74LC系列虽速度更快，但在本项目中用不到如此高的速度，且价格和供货不如74HC普遍。

### 4. 复用与扩展建议

- SPI/I2C总线可复用，片选/控制信号建议用扩展芯片分配。
- 必须功能（RTC、温度、LED屏）优先保证直连，其他模块通过扩展芯片预留接口。
- 设计时注意电流驱动能力，LED屏等大电流部分加缓冲/驱动芯片。

如需具体原理图或PCB设计建议，可进一步说明需求。

```

```

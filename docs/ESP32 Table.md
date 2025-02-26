---
title: ESP32 Table
---

| ESP Info                                      | Answer                                                                                                     |
| --------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| Model                                         | ESP32-S3-WROOM-1-N4                                                                                        |
| Product Page URL                              | [ESP32-S3-WROOM-1](https://www.espressif.com/en/products/modules/page#ESP32-S3)                                 |
| ESP32-S3-WROOM-1-N4 Datasheet URL             | [link](https://www.espressif.com/sites/default/files/documentation/esp32-s3-wroom-1_wroom-1u_datasheet_en.pdf) |
| ESP32 S3 Datasheet URL                        | [link](https://www.espressif.com/sites/default/files/documentation/esp32-s3_datasheet_en.pdf)               |
| ESP32 S3 Technical Reference Manual URL       | [link](https://www.espressif.com/sites/default/files/documentation/esp32-s3_technical_reference_manual_en.pdf) |
| Vendor link                                   | [link](https://www.digikey.com/en/products/detail/espressif-systems/ESP32-S3-WROOM-1-N4/16162639)           |
| Code Examples                                 | [ESP-IDF GitHub Repository](https://github.com/espressif/esp-idf)                                           |
| External Resources URL(s)                     | [YouTube Tutorials](https://youtu.be/ebsXSCKsHeQ?feature=shared)              |
| Unit cost                                     | $2.95 |
| Absolute Maximum Current for entire IC        | 1500 mA |
| Supply Voltage Range                          | 3.0 V to 3.6 |
| Maximum GPIO current (per pin)                | Not explicitly stated but typically around 40mA max |
| Supports External Interrupts?                 | Yes                                                                                                        |
| Required Programming Hardware, Cost, URL      | USB3131-30-0230-A Micro-USB Port; pricing available via [vendor link](https://www.digikey.com/en/products/detail/gct/USB3131-30-0230-A/9859642). |

| Module         | # Available | Needed | Associated Pins                                                                                                                                                                                                                         |
|----------------|-------------|--------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UART           | 2           | 2      | UART0: TXD0 (GPIO43), RXD0 (GPIO44); UART1: Configurable                                                                                                                                                                               |
| External SPI   | 4           | ?      | SPI2 (HSPI): SCK (GPIO36), MISO (GPIO37), MOSI (GPIO35), CS0 (GPIO34); SPI3 (VSPI): SCK (GPIO18), MISO (GPIO17), MOSI (GPIO8), CS0 (GPIO11); SPI0 and SPI1 are used internally for flash and PSRAM                                     |
| I2C            | 2           | ?      | I2C0: SCL (GPIO1), SDA (GPIO0); I2C1: SCL (GPIO3), SDA (GPIO2)                                                                                                                                                                         |
| GPIO           | 45          | ?      | GPIO0 to GPIO44; Note: Some GPIOs have specific functions or are used internally. Refer to the [ESP32-S3 datasheet](https://www.espressif.com/sites/default/files/documentation/esp32-s3_datasheet_en.pdf) for detailed information. |
| ADC            | 20          | ?      | ADC1: Channels on GPIO1 to GPIO10; ADC2: Channels on GPIO11 to GPIO20                                                                                                                                                                  |
| LED PWM        | 16          | ?      | Configurable on any GPIO                                                                                                                                                                                                               |
| Motor PWM      | 16          | ?      | Configurable on any GPIO                                                                                                                                                                                                               |
| USB Programmer | 1           | 1      | USB D+ (GPIO19), USB D- (GPIO20)                                                                                                                                                                                                       |
---
title: Component Selection
tags:
- Wi-Fi
- Embedded Systems
---

# Subsystem Documentation: Wi-Fi-Enabled Data Collection and Transmission

## **Introduction**
As part of our embedded systems design project, my subsystem is responsible for collecting data from all sensors in the system, transmitting it via a Wi-Fi network created by the ESP32 microcontroller, and updating this data in real-time on a GitHub-hosted webpage. This document outlines the selection of components for my subsystem, focusing on efficient power regulation, reliable wireless communication, and seamless integration with sensors.

---

## **Major Component Selections**

### **Microcontroller Selection**
The ESP32 microcontroller is the core of this subsystem, providing Wi-Fi connectivity and the processing power needed to gather and transmit sensor data.

| **Option**               | **Pros**                                                                 | **Cons**                                                       | **Unit Cost & Link**                                                                 |
|---------------------------|-------------------------------------------------------------------------|----------------------------------------------------------------|-------------------------------------------------------------------------------------|
| **ESP32-S3-WROOM-1-N4 (Final Choice)**  | Built-in Wi-Fi/Bluetooth, supports multiple serial protocols, low power modes, 4MB Flash | 3.3V logic may require level shifters for some peripherals      | [$2.95 DigiKey](https://www.digikey.com/en/products/detail/espressif-systems/ESP32-S3-WROOM-1-N4/16162639) |
| ESP8266                  | Low cost, simple to use                                                 | Limited GPIO pins, no dual-core processor                      | [$1.60 DigiKey](https://www.digikey.com/en/products/detail/espressif-systems/ESP8266EX/8028401) |
| Raspberry Pi Pico W      | Dual-core processor, Wi-Fi support                                      | Higher power consumption, larger physical size                 | [$6.00 DigiKey](https://www.digikey.com/en/products/detail/raspberry-pi/SC0918/16627943) |

**Final Selection: ESP32-S3-WROOM-1-N4**  
*Rationale:* The ESP32-S3-WROOM-1-N4 was selected due to its robust Wi-Fi capabilities, dual-core processor for multitasking, and excellent library support for embedded data transmission tasks.

---

### **Power Regulation**
To ensure stable operation of the ESP32 and sensors, a voltage regulator is required to step down the input voltage to 3.3V.

| **Option**           | **Pros**                                                  | **Cons**                                   | **Unit Cost & Link**                                                                 |
|-----------------------|----------------------------------------------------------|-------------------------------------------|-------------------------------------------------------------------------------------|
| **AP63203WU_7 (Final Choice)**    | High efficiency, compact size, low quiescent current  | Slightly higher cost than linear regulators | [$1.38 DigiKey](https://www.digikey.com/en/products/detail/diodes-incorporated/AP63203WU-7/9858426) |
| AMS1117-3.3           | Simple design                                            | Low efficiency                            | [$0.68 DigiKey](https://www.digikey.com/en/products/detail/umw/AMS1117-3-3/17635254) |
| LM2596                | High efficiency                                          | Larger physical size                      | [$6.70 DigiKey](https://www.digikey.com/en/products/detail/texas-instruments/LM2596S-ADJ-NOPB/363705) |

**Final Selection: AP63203WU_7**  
*Rationale:* The AP63203WU_7 was selected due to its high efficiency, low power loss, compact size, and suitability for surface mount applications, making it ideal for the power requirements of the ESP32 and associated components.

---

### **Power Input**
The subsystem requires a reliable power source capable of providing sufficient current for the ESP32 and sensors.

**Final Selection: DC Barrel Jack Adapter**  
*Rationale:* A DC barrel jack adapter was selected for its simplicity and ability to provide stable power from a wall adapter or external supply. This ensures consistent operation during extended use.

---

## **Additional Components to Enhance Subsystem**
To improve functionality and robustness, the following additional components are recommended:

1. **Capacitors (Decoupling):**
   - Add 10µF and 0.1µF capacitors near the ESP32 and voltage regulator to reduce noise and stabilize voltage.
   
2. **Heat Sink (Optional):**
   - Improve thermal performance of the voltage regulator during extended operation.

3. **LED Indicators:**
   - Include LEDs for power status and Wi-Fi activity to aid debugging.

---

## **Responsibilities**

1. **Data Collection:** Collect sensor data using UART (serial communication).
2. **Wi-Fi Communication:** Use the ESP32's built-in Wi-Fi module to create a local network and transmit sensor data.
3. **Power Management:** Regulate input voltage using the AP63203WU_7 regulator to ensure a stable 3.3V supply.
4. **Data Transmission:** Continuously update sensor readings on a GitHub-hosted webpage in real time.
5. **Integration:** Ensure seamless compatibility between sensors and the microcontroller through proper pin allocation and power management.

---

## **Pin Allocation**

### ESP32 Peripheral Pin Assignments:
| Peripheral      | Pin Assignment |
|------------------|----------------|
| UART TX          | GPIO1          |
| UART RX          | GPIO3          |
| Micro USB D-     | GPIO19         |
| Micro USB D+     | GPIO20         |
| Power Input      | VIN via DC Barrel Jack |

---

## **Conclusion**

The selected components ensure efficient integration of all sensors with the ESP32 microcontroller while meeting project specifications for real-time data collection and transmission to a GitHub-hosted webpage. By selecting the **AP63203WU_7** regulator, the subsystem benefits from improved power efficiency, and by limiting communication to **UART only**, the design is simplified for reliable data transfer.


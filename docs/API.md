# API Messaging Compliance  
**Author:** Kushagra Dashora  

This document outlines the message structure used by the Internet Communication Subsystem for receiving broadcast sensor data from the Sensor Suite. Messages are parsed over UART and published to the MQTT dashboard.

---

## 🔗 Subsystem Connection

This subsystem receives broadcasted sensor readings from **Ian Anderson’s Sensor Suite** and interacts with:

- **Solar Array** – Alex Comeaux  
- **HMI Interface** – Aarshon George  
- **MQTT Server / GitHub Dashboard** – Cloud endpoint  

---

## 📡 Broadcast Sensor Data

This message type broadcasts all sensor data.  
All numeric fields use **big-endian** format.

### 🧾 Message Format

|             | byte 1     | byte 2       | byte 3-4         |
|-------------|------------|--------------|------------------|
| **Variable Name** | `msg_type` | `sensor_num` | `sensor_val`     |
| **Variable Type** | `uint8_t`  | `uint8_t`    | `uint16_t`       |
| **Min Value**     | `0x31`     | `0x31`       | Varies by sensor |
| **Max Value**     | `0x31`     | `0x34`       | Varies by sensor |
| **Example**       | `0x31`     | `0x33`       | `0x0025` = 37    |

- **Purpose**: Broadcast real-time sensor values to all subsystems
- **Receiver Behavior**: Extract and log/display based on sensor number

---

### 📊 Sensor Number Reference Table

| Sensor         | Number | Hex Code | Data Min | Data Max |
|----------------|--------|----------|----------|----------|
| Wind Speed     | 1      | `0x31`   | 0        | 100      |
| Temperature    | 2      | `0x32`   | -40      | 85       |
| Humidity       | 3      | `0x33`   | 20       | 80       |
| Air Pressure   | 4      | `0x34`   | 10       | 1300     |

- Values are interpreted based on `sensor_num`
- Sensor values are sent as **2-byte unsigned integers**

---

## 🧠 Message Handling Logic (ESP32 UART)

### Message Receiver

1. **Monitor UART** for incoming messages from Sensor Suite.
2. **Parse incoming 4-byte messages**:
   - Validate message type: `0x31`
   - Identify sensor via `sensor_num`
   - Extract `sensor_val` as `uint16_t` (big endian)
3. **Forward decoded values** to:
   - Web dashboard via MQTT
   - Optional logging/local display

4. **Ignore**:
   - Invalid `msg_type`
   - Messages shorter than 4 bytes
   - Loopback data

---

## 🧭 Team Member IDs

Each subsystem is assigned a unique address for UART-based communication.

| Name     | Subsystem | Address |
|----------|-----------|---------|
| Aarshon  | HMI       | `0x61`  |
| Alex     | Motor     | `0x63`  |
| Ian      | Sensor    | `0x69`  |
| KD       | Websocket | `0x6B`  |
| Broadcast|           | '0x58'  |

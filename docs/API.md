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

## 📥 Received Messages

### Broadcast Sensor Data  
Receives real-time sensor values from the Sensor subsystem (Ian). Used to display values on a web dashboard via MQTT.

| Variable Name | byte 1   | byte 2         | byte 3-4                 |
|---------------|----------|----------------|--------------------------|
| msg_type      | `0x31`   | `0x31`–`0x34`   | `sensor_val` (uint16_t, big endian) |

#### Sensor Reference Table

| Sensor         | Number | Data Min | Data Max |
|----------------|--------|----------|----------|
| Wind Speed     | 1      | 0        | 100      |
| Temperature    | 2      | -40      | 85       |
| Humidity       | 3      | 20       | 80       |
| Air Pressure   | 4      | 10       | 1300     |

**Example**:  
`[0x31, 0x33, 0x00, 0x25]` → Humidity sensor sending value **37**

---

## 📤 Outgoing Messages

### Subsystem Error Code  
Sends a code representing WebSocket subsystem’s functionality.

| Byte 1 (msg_type) | Byte 2 (err_code) |
|-------------------|-------------------|
| `0x34`            | `0x01`–`0x03`      |

#### Error Code Table

| Code | Meaning              |
|------|----------------------|
| 1    | Full functionality   |
| 2    | Partial functionality|
| 3    | No functionality     |

**Example**:  
`[0x34, 0x01]` → System fully functional

---

### Subsystem Error Message  
Sends a descriptive error message to the HMI (Aarshon).

| Byte 1 (msg_type) | Byte 2–58 (err_msg)         |
|-------------------|-----------------------------|
| `0x35`            | char array (1–57 characters)|

**Example**:  
`[0x35, "MQTT server unreachable"]`

---

## 🧭 Message Structure Summary

| Byte Index | Description        | Example        |
|------------|--------------------|----------------|
| `[0]`      | Start Byte 1       | `'A'`          |
| `[1]`      | Start Byte 2       | `'Z'`          |
| `[2]`      | Sender ID          | `'k'`          |
| `[3]`      | Receiver ID        | `'a'`, `'i'`, `'c'` |
| `[4]`      | msg_type (1–5)     | `0x31`         |
| `[5–n]`    | Data / Payload     | Varies         |
| `[n+1]`    | End Byte 1         | `'Y'`          |
| `[n+2]`    | End Byte 2         | `'B'`          |

---

## 🧑‍🤝‍🧑 Team Member IDs

| Name     | Subsystem | Char Address |
|----------|-----------|--------------|
| Aarshon  | HMI       | `'a'`        |
| Alex     | Actuator  | `'c'`        |
| Ian      | Sensor    | `'i'`        |
| KD       | WebSocket | `'k'`        |

---
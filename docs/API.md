# **API Messaging Compliance Verification for Internet Communication Subsystem**

This document outlines the message types relevant to the Internet Communication Subsystem, including detailed tables for each message type, compliance verification, and implementation details.

---

## **Messages Sent or Received**

### **Messages Sent**
1. **Message Type 3: Alignment Frequency**  
   - Sent to: Alex  
   - Purpose: Set the solar panel alignment frequency.

### **Messages Received**
1. **Message Type 1: Sensor Data Transmission**  
   - Sent by: Ian (broadcast to all subsystems)  
   - Purpose: Receive environmental data (temperature and humidity) for display on the web interface.
   
2. **Message Type 4: Alignment Frequency Confirmation**  
   - Sent by: Alex  
   - Purpose: Confirm receipt of alignment frequency update.

---

## **Message Type Tables**

### **Message Type 1: Sensor Data Transmission**

Message type for receiving environmental data, including temperature and humidity, broadcasted to all subsystems.

| Byte(s) | Variable Name | Data Type   | Description               | Min Value | Max Value | Example Value |
|---------|---------------|-------------|---------------------------|-----------|-----------|---------------|
| 1       | `message_type`| `uint8_t`   | Message identifier        | 0         | 255       | 0x01          |
| 2-3     | `temperature` | `int16_t`   | Environmental temperature | -40       | +125      | +70           |
| 4-5     | `humidity`    | `uint16_t`  | Environmental humidity    | 0         | 100       | +30           |

- **Purpose**: Display real-time environmental data on the web interface.
- **Example Message**: `[0x01] [+70] [+30]`

---

### **Message Type 3: Alignment Frequency**

Message type for sending a command to set the solar panel alignment frequency.

| Byte(s) | Variable Name        | Data Type   | Description                       | Min Value | Max Value | Example Value |
|---------|----------------------|-------------|-----------------------------------|-----------|-----------|---------------|
| 1       | `message_type`       | `uint8_t`   | Message identifier                | 0         | 255       | 0x03          |
| 2-3     | `alignment_frequency`| `uint16_t`  | Panel alignment frequency (secs)  | 1         | 65535     | 300           |

- **Purpose**: Optimize solar panel performance by adjusting alignment intervals.
- **Example Message**: `[0x03][300]`

---

### **Message Type 4: Alignment Frequency Confirmation**

Message type for confirming receipt of an alignment frequency update.

| Byte(s) | Variable Name      | Data Type   | Description                 | Min Value    | Max Value    | Example Value |
|---------|--------------------|-------------|-----------------------------|--------------|--------------|---------------|
| 1       | `message_type`     | `uint8_t`   | Message identifier          | 0            | 255          | 0x04          |
| 2       | `confirmation_code`| `uint8_t`   | Confirmation status (e.g., success or error code)    | 0            | 255          | 200           |

- **Purpose**: Ensure successful communication between subsystems.
- **Example Message**: `[0x04][200]`

---

## **Handling Code Implementation**

### Message Receiver
The message receiver will:
1. Handle all incoming messages over the UART network.
2. Process messages intended for Kushagra:
   - For "Sensor Data Transmission," extract temperature and humidity data and forward it to the web interface.
   - For "Alignment Frequency Confirmation," log the confirmation status.
3. Trash messages sent by Kushagra that loop back to the subsystem.
4. Ignore malformed messages or those exceeding buffer size.

### Message Sender
The message sender will:
1. Format all outgoing messages with proper prefix, suffix, sender, receiver, and data fields.
2. Send example messages with time-varying data for testing purposes.
3. Prioritize forwarding received messages over sending new ones.
4. Limit sending rate using timers or interrupts.

---

## Example Messages

### Example Message Formats

#### Sensor Data Transmission
Byte Sequence:
[0x01] [+70] [+30]
Explanation:
Byte 1 (message_type): Sensor Data Transmission (0x01)
Byte 2-3 (temperature): Environmental temperature (+70°F)
Byte 4-5 (humidity): Environmental humidity (+30%)


#### Alignment Frequency
Byte Sequence:
[0x03]
Explanation:
Byte 1 (message_type): Alignment Frequency Command (0x03)
Byte 2-3 (alignment_frequency): Update interval (300 seconds)


#### Alignment Frequency Confirmation
Byte Sequence:
[0x04]
Explanation:
Byte 1 (message_type): Alignment Frequency Confirmation (0x04)
Byte 2 (confirmation_code): Success Code (200)


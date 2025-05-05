# Aim
To understand and implement IoT communication protocols (CoAP, MQTT) and integrate them with ThingSpeak for real-time data monitoring.

# Networking Protocols for IoT: CoAP and MQTT

## Materials Needed
1. Computer with internet access
2. Raspberry Pi or ESP32/ESP8266 microcontroller
3. MQTT Broker (e.g., Mosquitto)
4. ThingSpeak account
5. Python programming environment
6. CoAP client/server libraries
7. Network connectivity

## Overview of Protocols

### CoAP (Constrained Application Protocol)
- **Purpose:** Lightweight protocol for constrained devices
- **Transport:** Operates over UDP
- **Features:**
  * RESTful architecture
  * Built-in resource discovery
  * Asynchronous communication
  * Low overhead
  * URI support
  * Multicast support

### MQTT (Message Queuing Telemetry Transport)
- **Purpose:** Lightweight messaging protocol for IoT
- **Transport:** Operates over TCP
- **Features:**
  * Publish/Subscribe model
  * Quality of Service (QoS) levels
  * Persistent sessions
  * Retained messages
  * Topic-based filtering
  * Bi-directional communication

### ThingSpeak Cloud Platform
- **Purpose:** Cloud-based platform for IoT data collection and visualization
- **Features:**
  * Real-time data monitoring
  * MATLAB analytics
  * REST API and MQTT support
  * Device management
  * Data visualization tools

## Protocol Comparison

| Feature             | MQTT         | CoAP         |
|---------------------|--------------|--------------|
| Transport Protocol  | TCP          | UDP          |
| Communication Model | Publish/Subscribe | Request/Response |
| Overhead            | Low          | Very Low     |
| QoS Options         | 0, 1, 2      | Confirmable/Non-confirmable |
| Security            | TLS/SSL      | DTLS         |
| Bandwidth Usage     | Low          | Very Low     |
| Architecture        | Centralized  | Decentralized |
| Resource Discovery  | No           | Yes          |
| Use Cases           | Reliable messaging | Resource-constrained devices |

## Implementation Steps

### MQTT Setup
1. Install Mosquitto MQTT Broker.
2. Configure the broker and create topics.
3. Use a Python script to publish and subscribe to messages.

### CoAP Setup
1. Install a CoAP library (e.g., aiocoap for Python).
2. Set up a CoAP server and client.
3. Implement resource discovery and data exchange.

### ThingSpeak Integration
1. Create a ThingSpeak account and set up a new channel.
2. Obtain the API key for the channel.
3. Use Python to send data to ThingSpeak via MQTT or REST API.

## Example Python Code for MQTT
```python
import paho.mqtt.client as mqtt

# Define MQTT settings
broker = "test.mosquitto.org"
port = 1883
topic = "IoT/Example"

# Callback for connection
def on_connect(client, userdata, flags, rc):
    print("Connected with result code ", rc)
    client.subscribe(topic)

# Callback for receiving messages
def on_message(client, userdata, msg):
    print(f"Message received: {msg.payload.decode()}")

# Initialize MQTT client
client = mqtt.Client()
client.on_connect = on_connect
client.on_message = on_message

# Connect to broker and publish a message
client.connect(broker, port, 60)
client.loop_start()
client.publish(topic, "Hello from MQTT!")
client.loop_stop()
```

## Conclusion
This experiment demonstrates the use of CoAP and MQTT protocols for IoT applications, along with cloud integration using ThingSpeak. Each protocol has unique strengths:
- **CoAP:** Ideal for resource-constrained devices
- **MQTT:** Suitable for reliable messaging and telemetry

The choice of protocol depends on the specific requirements of the IoT application.

# Aim
To set up MQTT communication using Mosquitto and Node-RED, enabling real-time data exchange and visualization for IoT applications.

# MQTT and Node-RED Integration


## Setup Instructions

### 1. Install Node-RED
   Use the following command to install Node-RED globally:
   ```bash
   npm install -g --unsafe-perm node-red
   ```
   This will set up Node-RED on your system.

### 2. Install Mosquitto MQTT Broker
   Download Mosquitto from [https://mosquitto.org/download/](https://mosquitto.org/download/).

   After installation:
   - Navigate to `C:\Program Files\mosquitto`.
   - Open Command Prompt in the Mosquitto folder:
     ```bash
     cd "C:\Program Files\mosquitto"
     ```

### 3. Using Mosquitto

   - **Subscribe to a Topic**
     Use the `mosquitto_sub` command to subscribe to a topic:
     ```bash
     mosquitto_sub -t "<topic_name>"
     ```
     Example:
     ```bash
     mosquitto_sub -t "IoT/Topic1"
     ```

   - **Publish a Message**
     Use the `mosquitto_pub` command to publish a message:
     ```bash
     mosquitto_pub -t "<topic_name>" -m "<message>"
     ```
     Example:
     ```bash
     mosquitto_pub -t "IoT/Topic1" -m "Hello IoT!"
     ```

### 4. Configure Node-RED

   - Open Node-RED in your browser: `http://127.0.0.1:1880/`
   ![Node-RED Interface](https://github.com/dev-abby110/IOT_Practicals/blob/main/img/Screenshot%202025-05-05%20120230.png)

   - **Set Up MQTT in Node-RED**
     - Drag and drop the Debug node and the MQTT In node onto the workspace.
     - Double-click the MQTT In node to configure it:
       - Click **Add** to create a new server.
       - Set the server IP to `127.0.0.1` and port to `1883`.
       - Enter the topic name `<topic_name>`.
       - Click **Done**.
     - Deploy the Node-RED flow by clicking **Deploy**.

   - **Test Message Reception**
     Publish a message using Mosquitto to verify reception in Node-RED:
     ```bash
     mosquitto_pub -t "IoT/Topic1" -m "Test Message"
     ```

   - **Send a Message Using Node-RED**
     - Drag and drop the MQTT Out node onto the workspace.
     - Configure it with the same server and topic as the MQTT In node.
     - Add an Inject node to send a message.
     - Deploy the flow and test the message transmission.

![Node-RED Flow](https://github.com/abdullah-master/IOT_Lab/blob/main/img/node-red-abd.png)

## Conclusion
This experiment demonstrates the integration of MQTT and Node-RED for IoT applications. It highlights the simplicity and efficiency of MQTT for real-time data exchange and the versatility of Node-RED for creating interactive IoT workflows.



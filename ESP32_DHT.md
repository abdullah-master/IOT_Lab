# Aim
To monitor temperature and humidity using an ESP32 microcontroller and a DHT sensor, and log the data to ThingSpeak for real-time analysis.

# ESP32 DHT Temperature and Humidity Monitoring System

## Overview
This project focuses on building an IoT-based system to monitor temperature and humidity using an ESP32 microcontroller paired with a DHT11 or DHT22 sensor. The collected data is sent to ThingSpeak for real-time monitoring and analysis.

## Goals
- Configure an ESP32 with a DHT11/DHT22 sensor
- Establish WiFi connectivity
- Gather temperature and humidity readings
- Transmit data to the ThingSpeak cloud
- Enable real-time environmental monitoring

## Required Components
1. ESP32 Development Board
2. DHT11 or DHT22 Sensor
3. Breadboard
4. Jumper Wires
5. USB Cable for Programming
6. 10kΩ Resistor (Pull-up)

## Circuit Setup
![ESP32 DHT Connection](https://github.com/user-attachments/assets/ae1ea700-4eaf-49d1-b4ad-9b96f21ba586)

### Wiring Details
- Connect the VCC pin of the DHT sensor to the 3.3V pin of the ESP32
- Connect the GND pin of the DHT sensor to the GND pin of the ESP32
- Connect the DATA pin of the DHT sensor to GPIO 4 of the ESP32
- Use a 10kΩ pull-up resistor between the VCC and DATA pins

## Software Requirements
1. Arduino IDE
2. Libraries Needed:
   - WiFi.h
   - HTTPClient.h
   - DHT.h

## Steps to Follow
1. **Install Arduino IDE**
   - Download and install the Arduino IDE
   - Add ESP32 board support via the Board Manager

2. **Add Required Libraries**
   - Install the DHT sensor library using the Library Manager
   - Add the ESP32 board package

3. **ThingSpeak Configuration**
   - Sign up for a ThingSpeak account
   - Create a new channel
   - Save your API Key

4. **Code Setup**
   - Update WiFi credentials
   - Insert the ThingSpeak API key
   - Select the appropriate DHT sensor type (DHT11 or DHT22)

## Code Walkthrough

### Including Libraries and Setting Up Pins
```c
#include <WiFi.h>
#include <HTTPClient.h>
#include "DHT.h"

#define DHTPIN 4       // GPIO pin for the DHT sensor
#define DHTTYPE DHT11  // Change to DHT22 if using DHT22
DHT dht(DHTPIN, DHTTYPE);

// Wi-Fi credentials
const char* ssid = "YOUR_WIFI_SSID";
const char* password = "YOUR_WIFI_PASSWORD";

// ThingSpeak settings
const char* server = "http://api.thingspeak.com/update";
String apiKey = "YOUR_THINGSPEAK_API_KEY";

void setup() {
    Serial.begin(115200);
    dht.begin();

    WiFi.begin(ssid, password);
    Serial.print("Connecting to WiFi");

    while (WiFi.status() != WL_CONNECTED) {
        delay(500);
        Serial.print(".");
    }
    Serial.println(" Connected!");
}

void loop() {
    if (WiFi.status() == WL_CONNECTED) {
        float temp = dht.readTemperature();
        float hum = dht.readHumidity();

        if (isnan(temp) || isnan(hum)) {
            Serial.println("Failed to read from DHT sensor!");
            return;
        }

        Serial.print("Temperature: ");
        Serial.print(temp);
        Serial.print(" °C, Humidity: ");
        Serial.print(hum);
        Serial.println(" %");

        HTTPClient http;
        String url = server + "?api_key=" + apiKey + "&field1=" + String(temp) + "&field2=" + String(hum);
        
        http.begin(url);
        int httpResponseCode = http.GET();
        
        if (httpResponseCode > 0) {
            Serial.println("Data sent to ThingSpeak successfully");
        } else {
            Serial.print("Error sending data: ");
            Serial.println(httpResponseCode);
        }
        
        http.end();
    } else {
        Serial.println("WiFi Disconnected");
    }

    delay(15000);  // Send data every 15 seconds
}




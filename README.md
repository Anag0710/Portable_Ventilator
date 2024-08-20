# Portable Ventilator and Health Monitoring System

This repository contains the source code for the **Portable Ventilator and Health Monitoring System**. This project is designed to create an affordable and accessible ventilator system with integrated health monitoring features. It aims to provide a cost-effective solution for emergency ventilation and real-time monitoring of vital health parameters such as heart rate, SpO2 levels, temperature, and humidity.

## 🛠 Features

### 1. **Portable Ventilator System**
- **Servo Motor Control**: Adjusts the breathing cycle of the ventilator based on the user's input from a potentiometer, simulating different breathing patterns.
- **LCD Display**: Provides real-time feedback on the breathing cycle, speed, and angle of the ventilator mechanism.
- **Emergency Mode**: Automatically adjusts the ventilator parameters based on predefined settings in response to critical conditions.

### 2. **Health Monitoring System**
- **Pulse Oximeter Integration**: Utilizes the MAX30100 sensor to monitor and display heart rate (BPM) and oxygen saturation (SpO2) levels on an OLED screen.
- **Temperature and Humidity Sensing**: Uses a DHT11 sensor to measure and display environmental temperature and humidity, crucial for maintaining optimal conditions for patients.

## 🚀 Getting Started

### Prerequisites
- **Arduino IDE**: Ensure you have the latest version installed.
- **ESP8266 Module**: For Wi-Fi communication and processing.
- **MAX30100 Pulse Oximeter**: For heart rate and SpO2 measurement.
- **DHT11 Sensor**: For temperature and humidity sensing.
- **Servo Motor**: To control the ventilator's movement.
- **16x2 LCD Display**: For displaying ventilator status.
- **128x64 OLED Display**: For displaying health metrics.
- **Potentiometer**: For adjusting ventilator settings.
## 📄 Code Overview

### 1. **Pulse Oximeter and Display Code**
- This code initializes the MAX30100 Pulse Oximeter and processes heart rate and SpO2 data.
- The data is displayed on an OLED screen, and an alert is shown when a heartbeat is detected.

### 2. **Portable Ventilator Code**
- Controls a servo motor to simulate different breathing cycles based on the potentiometer input.
- The system displays the current cycle and speed on a 16x2 LCD screen.

### 3. **Temperature and Humidity Monitoring Code**
- Uses a DHT11 sensor to read environmental temperature and humidity.
- Data is displayed on an OLED screen for easy monitoring.

## 🖥️ Applications

The Portable Ventilator and Health Monitoring System addresses several critical needs:

- **Emergency Medical Situations**: Provides a quick and reliable ventilator system that can be used in ambulances, field hospitals, or homes during medical emergencies.
- **Real-Time Health Monitoring**: Continuously monitors vital health metrics, enabling early detection of potential issues and ensuring the patient’s safety.
- **Portable and Affordable**: The system is designed to be easily transportable and cost-effective, making it accessible to a broader population.

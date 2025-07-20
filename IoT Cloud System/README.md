# MQTT Cloud-based IoT Systems using Raspberry Pi (Oracle VirtualBox) & Sense HAT Emulator  

## Purpose:
This project guides how to build an Internet of Things (IoT) system using 
Raspberry Pi (running in Oracle VirtualBox), the Sense HAT emulator, and the MQTT 
protocol to publish and subscribe to real-time sensor data with topics via a 
cloud-based MQTT broker. The instructions are specific for Task 2 and 3.

## Requirements:

### 1. Raspberry Pi OS (running in VirtualBox)
   - Download from: [https://www.raspberrypi.com/software/](https://www.raspberrypi.com/software/)
   - Select the Raspberry Pi Desktop for PC and Mac (.iso file).

### 2. VirtualBox
   - Create a new virtual machine with the following specifications to run 
     Raspberry Pi in a virtual environment:
     - Type: Linux
     - Version: Debian (64-bit)
     - RAM: minimum 2 GB with 20 GB storage.
   - Mount the downloaded .iso file as a virtual CD to install Raspberry Pi OS 
     inside VirtualBox.

### 3. Python
   - Python 3.9.2 comes preinstalled with Raspberry Pi OS.
   - To check the version, open the terminal and run:
     ```bash
     python3 --version
     ```
   - To update to the latest version, run:
     ```bash
     sudo apt update
     sudo apt-get install python3
     sudo apt-get install python3-pip
     ```

### 4. Sense HAT Emulator (sense_emu)
   - The Sense HAT Emulator GUI is preinstalled on Raspberry Pi OS.
   - To run it from the desktop, click: `Menu > Programming > Sense HAT Emulator`.
   - Ensure this code is used: 
     ```python
     from sense_emu import SenseHat
     ``` 
     for all tasks to import the emulator.

### 5. MQTT Client (paho-mqtt)
   - Install the MQTT client library for Python:
     ```bash
     sudo apt install python3-pip
     pip3 install paho-mqtt
     ```

### 6. Internet Connection
   - To connect to a public MQTT broker, verify there is an active internet 
     connection by pinging google.com.



## Task 2: Publishing Sensor Data to EMQX Broker

1. From the Raspbian Desktop, open Terminal and run the following code:
     ```bash
     python3 /home/raspberry/Desktop/raspberry/DNCT702_A2_Practical_Assessment/Task3/Task2.py
     ```

**Note:**
MQTT topics specified in the code are:
- Temperature: `temperature/topic`
- Humidity: `humidity/topic`
- Barometric Pressure: `pressure/topic`
- Magnetometer: `magnetometer/topic`

The MQTT broker details are:
- Broker: `broker.emqx.io`
- Port: `1883`
- Keep alive Interval: `60`

2. The following expected output shows the real-time sensor values being published 
   to the respective topics at a sample rate of 1 second with QoS 1 to the EMQX 
   broker:

   Publishing the topics............
   Published Temperature: 24.98°C with QoS 1
   Published Humidity: 45.2% with QoS 1
   Published Pressure: 1013.0 hPa with QoS 1
   Published Magnetometer: 0.0° with QoS 1



## Task 3: Subscribing to Topics & Accessing Sensor Data from EMQX Broker

1. Ensure `Task2.py` has been saved in the same folder as `Task3.py`.
2. From the Raspbian Desktop, click `Menu > Programming > Sense HAT Emulator`.
3. From the Raspbian Desktop, click `Menu > Programming > Thonny`.
4. Load `Task3.py` in Thonny and press run.

The following joystick instructions will be printed in the shell area:

    ==================================================
    Use the Joystick to Subscribe to a Topic:
    Joystick UP → temperature/topic
    Joystick DOWN → pressure/topic
    Joystick LEFT → humidity/topic
    Joystick RIGHT → magnetometer/topic
    Joystick MIDDLE → Unsubscribe from all topics
    ==================================================

5. In Sense HAT Emulator, press the joystick to subscribe/unsubscribe to the desired 
   topic for sensor readings.
6. Open the corresponding CSV files saved in the same location as the `Task2.py` and 
   `Task3.py` files to verify sensor readings.
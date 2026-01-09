---
title: "Overhead Fan Automation Using ESP32 and a Node-RED Dashboard via MQTT"
date: 2026-01-09
---
I built an overhead light/fan controller IoT device using a Raspberry Pi 5, a handmade ESP-32 board, and a spare fan remote which connects a Node-RED flow through MQTT and is controlled by a Node-RED Dashboard.

### Why MQTT?
I wanted to implement MQTT into a project because I needed to understand how it worked, and how to apply it for future projects for my Senior Design project, and personal projects. I had heard that MQTT had been used to connect Industrial IoT devices at my internship and figured it would be a perfect oportunity to learn how a protocol that's actually used in industrial applications works.

### Raspberry Pi 5 MQTT Broker and Node-RED
I began this project by first intalling the MOSQUITTO broker service onto the RPi, which allowed the device to act as an MQTT broker able to send and recieve data to and from different endpoints and devices. I then attempted to develop a controller tool using Python and Flask, but proved to be too time and labor intensive. I then decided to switch to using Node-RED, which had MQTT support baked in on the inital install. I decided to include the dashboard-2 library as it made creating a simple UI to control the overhead fan with much easier. To integrate MQTT into the device, I had to publish to specific "topics" I had programmed within the ESP32; one for each button on the fan remote.

<p align = "center">
  <img src = "https://t33j4y1104.github.io/blog/Photos/NRFlow.png" alt="Node-RED Dashboard">
</p>

<p align = "center">
  <img src = "https://t33j4y1104.github.io/blog/Photos/NRDashboard.png" alt="Node-RED Dashboard">
</p>

Each button shown on the dashboard, when pressed, sends a different message to the MQTT broker running on the Pi, then the broker sends the the signal to the ESP-32 where it will be processed and determine which action to signal on the attached remote.

#### Alarmclock functionality

As an added piece of functionality, I added the ability to control the light at specific times of the day. By creating a second flow, with a new block that reads the time of day if the time matches what I specified, the light turns on, acting as a silent alarmclock

<p align = "center">
  <img src = "https://t33j4y1104.github.io/blog/Photos/AlarmFlow.png" alt="Node-RED flow used in manual control">
</p>


### ESP-32 program

The program running on the ESP is fairly simple. I programmed the device using the Arduino IDE because it had included libraries for wifi (WiFi.h) and MQTT (PubSubClient.h). From there I specified my network information, and created a loop which runs constantly until connected to the specified network. Once connected, the ESP begins to listen for messages from the Broker. Once a message is recieved, the title of the message is compared to specified values called Topics. If the message matches the topic, the ESP sets a pin high.

### ESP-32 Custom Circuit
When initally designing the circuit, I had to choose between using Relay Modules and using NPN BJTs to acctivate the remote to control the overhead light and fan. I ultimately decided to use BJTs as they were smaller in size
and I had them on hand. The final design follows the following diagram.

<p align = "center">
  <img src= "https://t33j4y1104.github.io/blog/Photos/CircuitDiagram.png" alt="Circuit Diagram">
</p>

The remote I used was an extra 3 speed ceiling fan remote from an old fan.

<p align="center">
  <img src="https://t33j4y1104.github.io/blog/Photos/MerwryRemote.png" alt="Remote Picture">
</p>

To power both the remote and the ESP32 board, I used an Adafruit bq25185 USB/ DC/ Solar Charger, which was able to supply sufficicent power to both boards via USB.  

<p align="center">
  <img src="https://t33j4y1104.github.io/blog/Photos/SolarCharger.png" alt="Solar Charger">
</p>



### Final Result:

<p align="center">
  <img src="https://t33j4y1104.github.io/blog/Photos/FinalBoard.jpeg" alt="Final Board">
</p>

The Final Result was better than I had hoped. I am able to control my light from anywhere in the house thanks to the Node-RED Dashboard and have an automatic alarmclock which turns my light on rather than using a normal audio alarm.


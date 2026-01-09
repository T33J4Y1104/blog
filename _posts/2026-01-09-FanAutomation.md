---
title: "Overhead Fan Automation Using ESP32 and a Node-RED Dashboard via MQTT"
date: 2026-01-09
---
I built an overhead light/fan controller IoT device using a Raspberry Pi 5, a handmade ESP-32 board, and a spare fan remote which connects a Node-RED flow through MQTT and is controlled by a Node-RED Dashboard.

### Why MQTT?
I wanted to implement MQTT into a project because I needed to understand how it worked, and how to apply it for future projects for my Senior Design project, and personal projects. I had heard that MQTT had been used to connect Industrial IoT devices at my internship and figured it would be a perfect oportunity to learn how a protocol that's actually used in industrial applications works.

### Raspberry Pi 5 MQTT Broker and Node-RED
I began this project by first intalling the MOSQUITTO broker service onto the RPi, which allowed the device to act as an MQTT broker able to send and recieve data to and from different endpoints and devices. I then attempted to develop a controller tool using Python and Flask, but proved to be too time and labor intensive. I then decided to switch to using Node-RED, which had MQTT support baked in on the inital install. I decided to include the dashboard-2 library as it made creating a simple UI to control the overhead fan with much easier. To integrate MQTT into the device, I had to publish to specific "topics" I had programmed within the ESP32; one for each button on the fan remote.

### ESP-32 Custom Circuit
When initally designing the circuit, I had to choose between using Relay Modules and using NPN BJTs to acctivate the remote to control the overhead light and fan. I ultimately decided to use BJTs as they were smaller in size
and I had them on hand. To power both the remote and the ESP32 board, I used an Adafruit bq25185 USB/ DC/ Solar Charger, was able to supply sufficicent power to both boards. 


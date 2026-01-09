---
title: "Overhead Fan Automation Using ESP32 and Node-RED"
date: 2026-01-09
---

Using a Raspberry Pi 5, a handmade ESP-32 board, and a spare fan remote, I created an IoT device which connects an ESP-32 WROOM32 board to a Node-RED flow through MQTT.

###Raspberry Pi 5 stack
Running on the RPi 5 is the MQTT broker process MOSQUITTO  which allows the RPi to act as the Broker device publishing or recieving data from endpoints. Running within a Docker conatiner is Node-RED which allows a user to
create workflows seemlessly with other protocols.

###ESP-32 

---
title: "Build a OpenHAB OS and MQTT server"
# author: 
tags:
  - Docker
  - MQTT
  - Smarthome
  - IoT
  - Linux
  - Mosquitto
date: '2022-11-06'
ShowToc: true
draft: true
---
A template for quickly generating content.
<!--more-->

---

## Required knowledge
- Docer
- Linux

## 1 Docker compose

> Use one command to run MULTIPLE Docker Container

- docker-compose YAML
- DOCKERFILE diffrent?
- VSMqtt

```bash
docker compose up -d
```

## 2 MQTT Brief
#### What and Why
[EXTEND READING](https://www.openhab.org/addons/bindings/mqtt.generic/?#mqtt-things-and-channels-binding)
MQTT has a Server called MQTT Broker, it receive all message and save as a "**Topic**" in a certain address which look like "**device123/brightness/set**". 
If some Client want this data, they need to "**Subscribe**" this topic.

![](Pasted%20image%2020221106234920.png)
#### Command topic & State topic
>Just like Set and Get in Object-orient language

Assume there is an MQTT capable light bulb. It has a unique id amongst all light bulbs, say "device123". The manufacturer decided to accept new brightness values on "device123/brightness/set". We call that a **command topic**.
we want to retrieve the current brightness value of a light bulbs. The manufacturer specified that this value can be found on "device123/brightness". We call that a **state topic**.
This binding can not provide any auto-discovery means.
[EXTEND READING](https://www.openhab.org/addons/bindings/mqtt.generic/?#mqtt-things-and-channels-binding)

## References
- [MQTT Brief by OpenHAB](https://www.openhab.org/addons/bindings/mqtt.generic/?#mqtt-things-and-channels-binding)
- 
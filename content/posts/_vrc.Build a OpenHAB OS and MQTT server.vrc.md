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
[READ MORE]()
MQTT has a Server called MQTT Broker, it receive all message and save as a "**Topic**" in a certain address which look like "**device123/brightness/set**". 
If some Client want this data, they need to "**Subscribe**" this topic.

![](Pasted%20image%2020221106234920.png)

## References
- [MQTT Brief by OpenHAB](https://www.openhab.org/addons/bindings/mqtt.generic/?#mqtt-things-and-channels-binding)
- 
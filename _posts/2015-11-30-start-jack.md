---
layout: post
title: Script to Start Jack
categories: [Linux, Applications]
tags: [linux, applications]
fullview: true
---

## What is...

Jack is a low-latency audio server for multi-processor machines.

## Starting after installation...

Below is my script to start the Jack server.

```shell
#!/bin/bash

# Set performance
sudo cpupower frequency-set -g performance

dbus-launch jack_control start
sudo schedtool -R -p 20 `pidof jackdbus`
jack_control eps realtime true
jack_control ds alsa
jack_control dps device hw:Track
jack_control dps rate 48000
jack_control dps nperiods 3
jack_control dps period 64
sleep 10
qjackctl &
```
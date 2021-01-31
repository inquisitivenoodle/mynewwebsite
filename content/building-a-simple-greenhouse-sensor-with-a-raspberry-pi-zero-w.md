+++
author = "inquisitve noodle"
categories = []
date = 2021-01-31T15:18:00Z
description = "n this post I will going through the steps to build a simple greenhouse sensor with a Raspberry Pi Zero W"
draft = true
image = ""
title = "Building a simple greenhouse sensor with a Raspberry Pi Zero W"
type = "post"

+++
In this post I will going through the steps of building a simple greenhouse sensor with with:

* A Raspberry Pi Zero W
* [DHT22 AM2302 Digital Temperature and Humidity Measure Sensor Module](https://learn.adafruit.com/dht/overview)
* [LTR-559 Light & Proximity Sensor](https://shop.pimoroni.com/products/ltr-559-light-proximity-sensor-breakout)

## Preparing the Raspberry Pi Zero W

I have covered the build of the Raspberry Pi Zero W in [this post](https://inquisitivenoodle.com/installing-raspberry-pi-os-headless-on-a-raspberry-pi-zero-w/).

## Connecting the DHT22 temperature and humidity sensor

As I will be using a headless connection (no monitor, mouse or keyboard) I added an empty ssh file to the directory. To do this I created an empty a new file called **ssh** and saved it into the root directory of the USB drive.

## Connecting the LTR-559 light sensor
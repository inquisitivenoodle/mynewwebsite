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

## Connecting the LTR-559 light sensor

The breakout board fits straight onto bottom left 5 pins on your Raspberry Pi's GPIO header (pins 1, 3, 5, 7, 9).

## Connecting the DHT22 temperature and humidity sensor

My Raspberry Pi Zero W had the 40-pin header already attached.  The pin mapping can be seen [here](https://pi4j.com/1.2/pins/model-zerow-rev1.html).

As the light sensor will be using the first set of pins.  I connected the sensor to the following pins:

* Power to Pin 17 (3v3)
* Data to Pin 16 (GPIO4)
* Ground to Pin 20 (Ground)

Then I ran the following commands to get the python libraries installed

    sudo apt-get install python3-dev python3-pip
    sudo python3 -m pip install --upgrade pip setuptools wheel
    sudo pip3 install Adafruit_DHT
+++
author = "inquisitve noodle"
categories = []
date = 2021-01-31T15:18:00Z
description = "n this post I will going through the steps to build a simple greenhouse monitoring system for light, temperature and humidity with a Raspberry Pi Zero W"
draft = true
image = ""
title = "Building a simple greenhouse monitoring system with a Raspberry Pi Zero W - Part 1"
type = "post"

+++
In this post I will going through the first steps of building a simple greenhouse sensor with with:

* A Raspberry Pi Zero W
* [DHT22 AM2302 Digital Temperature and Humidity Measure Sensor Module](https://learn.adafruit.com/dht/overview)
* [LTR-559 Light & Proximity Sensor](https://shop.pimoroni.com/products/ltr-559-light-proximity-sensor-breakout)

## Preparing the Raspberry Pi Zero W

I have covered the build of the Raspberry Pi Zero W in [this post](https://inquisitivenoodle.com/installing-raspberry-pi-os-headless-on-a-raspberry-pi-zero-w/).

## Connecting the LTR-559 light sensor

The breakout board fits straight onto bottom left 5 pins on your Raspberry Pi's GPIO header (pins 1, 3, 5, 7, 9).

## Connecting the DHT22 temperature and humidity sensor

My Raspberry Pi Zero W had the 40-pin header already attached.  The pin mapping can be seen [here](https://pinout.xyz/).

As the light sensor will be using the first set of pins.  I connected the sensor to the following pins:

* Power to Pin 2 (5V)
* Data to Pin 7 (GPIO4) - the pin number the script below uses is the GPIO number
* Ground to Pin 6 (Ground)

![Raspberry Pi Zero W with a DHT22 sensor](/images/raspberry-pi-zero-w-dht22.png "Raspberry Pi Zero W with a DHT22 sensor")

Then I ran the following commands to get the python libraries installed:

    sudo apt-get install python3-dev python3-pip
    sudo python3 -m pip install --upgrade pip setuptools wheel
    sudo pip3 install Adafruit_DHT

I created the following script, called _dht22.py_:

    import Adafruit_DHT
    import time
    
    DHT_SENSOR = Adafruit_DHT.DHT22
    DHT_PIN = 4
    
    while True:
        humidity, temperature = Adafruit_DHT.read_retry(DHT_SENSOR, DHT_PIN)
    
        if humidity is not None and temperature is not None:
            print("Temperature={0:0.1f}*C  Humidity={1:0.1f}%".format(temperature, humidity))
        else:
            print("Failed to retrieve data from humidity sensor")
        time.sleep(3);

The sensor only measures every 2 seconds, so rather than have the script execute continuously, it sleeps for 3 seconds between measurements.

![python script for a dht22 sensor](/images/script.png "python script for a dht22 sensor")

In the next post, I will be passing the temperature and humidity values to a mosquitto MQTT broker.
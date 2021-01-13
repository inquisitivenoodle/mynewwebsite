+++
author = "🍜 inquisitive noodle"
categories = ["raspberry pi", "home automation"]
date = 2020-11-22T18:51:00Z
description = "In this post, I detail out the steps for moving an installation from a microSD card to running off an external SSD drive. In this setup, I am connecting to the Raspberry Pi 4 remotely without the use of a dedicated monitor, keyboard or mouse. The external hard drive in this instance is an old laptop SSD drive with a simple USB 3.0 to SATA converter cable. "
image = "/images/post/post-2.jpg"
title = "Installing Home Assistant HassOS onto an external hard drive connected to a Raspberry Pi 4"
type = "post"

+++
If you haven't installed Raspberry Pi OS yet, please refer to this [post]().

## Updating the Raspberry Pi 4 firmware

To clarify, the hard drive is not connected to start with. I booted up to the Raspberry Pi 4, and logged onto the Raspberry Pi Desktop from within [VNC Viewer](https://www.realvnc.com/en/connect/download/viewer/). Then, I opened up a Terminal window by click the fourth icon in on the top left bar that looks like a black window with a blue title bar.

[![terminal icon in upper left navigation bar](https://github.com/inquisitivenoodle/mywebsite/raw/master/site/content/post/img/terminal-icon.png "terminal icon in the upper left navigation bar.")](https://github.com/inquisitivenoodle/mywebsite/blob/master/site/content/post/img/terminal-icon.png)

Once in _Terminal,_ I executed the following command and confirmed Y when asked to proceed.

    sudo rpi-update

This updated the Raspberry PI firmware. Then I rebooted the Pi and reconnected back into the Raspberry Pi desktop.

Once the Raspberry Pi had rebooted, I logged in and opened up a new _Terminal_ session and executed the following code to install the latest bootloader.

    sudo rpi-eeprom-update -d -a

Then, once again, I rebooted the Raspberry Pi.

## Enable USB boot mode on the Raspberry Pi

This time, after the reboot, I connected via [Putty](https://www.chiark.greenend.org.uk/\~sgtatham/putty/) to the Raspberry Pi 4, using the hostname _raspberrypi.local_ and after logging in, I ran:

    sudo raspi-config

I choose _6 Advanced Options_ then _A6 Boot Order_ then _B1 USB Boot._ Then I quit out raspi-config and rebooted the Raspberry Pi. After it came back up, I then powered it off.

## Installing Home Assistant HassOS on the external hard drive

I downloaded HassOS 5.5 64-bit for the Raspberry Pi 4, _hassos_rpi4_5.5.img.gz_, from the official [repo](https://github.com/home-assistant/operating-system/releases/tag/5.5).

[![hassos rpi4 5.5 repo file](https://github.com/inquisitivenoodle/mywebsite/raw/master/site/content/post/img/hassos-repo.png "hassos rpi4 5.5 repo file")](https://github.com/inquisitivenoodle/mywebsite/blob/master/site/content/post/img/hassos-repo.png)

From there I used [BalenaEtcher](https://www.balena.io/etcher/) on my Windows PC to flash this to my SSD external hard drive, which was a 320GB FAT32. The program gives a warning for the SSD being larger than expected for a USB drive. I accepted the warning and then continued with imaging the drive. I ejected the drive properly.

Next I plugged the SSD into the Raspberry Pi 4 and removed the microSD card and rebooted the machine. It took a while to boot up and I had to powercycle it once. After this I navigated to HassOS through a browser on [http://homeassistant:8123](http://homeassistant:8123) on my Windows PC, where I was prompted to create an account.

N.B. Some SSD enclosures, such as Sabrent, have been reported as having issues. Here I used a [USB 3.0 to SATA cable](https://www.amazon.co.uk/gp/product/B01N2JIQR7) adapter.
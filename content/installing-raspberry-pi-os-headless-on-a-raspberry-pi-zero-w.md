+++
author = "inquisitive noodle"
categories = ["Raspberry Pi"]
date = 2021-01-31T13:31:00Z
description = ""
draft = true
image = ""
title = "Installing Raspberry PI OS headless on a Raspberry Pi Zero W"
type = "post"

+++
In this post I will going through the steps of installing Raspberry Pi OS headless onto Raspberry Pi Zero W with no monitor, keyboard or mouse.

## Downloading the Raspberry Pi OS software

Firstly, I downloaded Raspberry Pi Imager software through Software Manager on Linux Mint.  If you are using Windows, you can download [BalenaEtcher](https://www.balena.io/etcher/) imaging software as an alternative.

I selected the most recent 32-bit Raspberry Pi OS image.

## Enabling SSH

As I will be using a headless connection (no monitor, mouse or keyboard) I added an empty ssh file to the directory. To do this I created an empty a new file called **ssh** and saved it into the root directory of the USB drive.

## Configuring wifi

Again I created a new empty file called **wpa_supplicant.conf** and then saved the following contents, replacing NETWORK-NAME and NETWORK-PASSWORD with my SSID and wifi password inside the quotes:

      country=UK
      ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
      update_config=1
    
      network={
          ssid="NETWORK-NAME"
          psk="NETWORK-PASSWORD"
      }
    

## Initial configuration via Putty

I inserted the microSD card into the Raspberry Pi 4 and then connected the power. Once the Pi had booted, I ran [Putty](https://www.chiark.greenend.org.uk/\~sgtatham/putty/), an SSH client, and connected to it on the _raspberrypi.local_ address.

![putty configuration screen](/images/putty-login.PNG "putty configuration screen")

I accepted the warning and then entered the login credentials to the default installation - username: _pi_, password: _raspberry_. At the terminal prompt then I ran:

    sudo raspi-config

This launched the raspi-config menu, and I chose _3 Interface Options_.

In the next menu, then I chose _P3 VNC_ and then I accepted turning the option on. I exited out of raspi-config back to the terminal. You can use the Tab key to jump from the menus to the "Select" and "Back" options and Enter to choose one once it's highlighted.

![VNC option in the raspi-config interfacing options](/images/vnc-option.PNG "VNC option in the raspi-config interfacing options")

Next up in _raspi-config_ I choose _2 DisplayOptions_ and then _D1 Resolution_, and then the _1280x720 16:9_ option.

Then I selected _Finish_ and then _Reboot_ to restart the Raspberry Pi.

I downloaded [VNC viewer](https://www.realvnc.com/en/connect/download/viewer/), launched it and connected to the Raspberry Pi 4 on the _raspberrypi.local_ address, using the same credentials as before - username: _pi_, password: _raspberry_.

![logging into raspberry pi via VNC](/images/vnc-login.PNG "logging into raspberry pi via VNC")

This allowed me to login to the desktop using the same credentials again. If you get a black background with a "_desktop cannot be displayed at this time"_ error message after authenticating on VNC, try changing the resolution to a lower one in the previous step.

![raspberry pi desktop login screen](/images/desktop-login.png "raspberry pi desktop login screen")

Following a successful login, the os then prompted me through a series of steps to secure the pi - such as changing the admin password.

## Connecting the Raspberry Pi to wifi

As part of the intial configuration dialogues, I was prompted to _Select a wireless network._ I chose the network name (SSID) and entered the password. The pi automatically connected to the network and this was reflected in the toolbar on the top right hand side, second notification icon in.

![wireless notification icon in upper right navigation bar](/images/wireless-icon.PNG "wireless notification icon in upper right navigation bar")

If you aren't going through the initial configuration the wireless network can be connected in the following ways:

1. If you can connect to the Raspberry Pi desktop, you can click on the wireless icon and choose your network from the list the Pi can see.
2. If you can't connect to the Raspberry Pi desktop, you can set the wireless credentials in the _raspi-config_ by choosing _1 System Options_ and then _S1 Wireless LAN._ Enter the network name as the SSID and the wireless password as the passphrase and then OK and exit out of the setup.

## Updating the Raspberry Pi

The last step in the initial setup is to update the raspberry pi through a dialogue box entitled _Update Software_. This will go back to the operating system servers and update and install any packages that may have been released since the version of the OS you downloaded was created.

You can achieve the same result by navigating to the _Terminal_ icon, the fourth one in on the top left bar that looks like a black window with a blue title bar.

![terminal icon in the upper left navigation bar](/images/terminal-icon.PNG "terminal icon in the upper left navigation bar")

Once _Terminal_ has opened, you can run the following commands:

    sudo apt-get update
    sudo apt-get upgrade

At the terminal prompt of "_Do you want to continue? \[Y/n\]",_ type "y" (no quotes) and the terminal will then start to install all the updated packages. Once terminal returns you to a prompt the update has completed and you can close the application.
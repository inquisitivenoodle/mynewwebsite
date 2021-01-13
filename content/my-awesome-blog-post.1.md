+++
author = "🍜 inquisitive noodle"
categories = ["raspberry pi"]
date = 2020-11-21T14:16:00Z
description = "Installing Raspberry Pi OS headless onto Raspberry Pi 4 with no monitor, keyboard or mouse"
image = "/images/post/post-3.jpg"
title = "Installing Raspberry Pi OS headless onto Raspberry Pi 4"
type = "post"

+++
## Downloading the Raspberry Pi OS software

Firstly, I downloaded [BalenaEtcher](https://www.balena.io/etcher/) imaging software for Windows. Then I downloaded the latest [Raspberry PI OS for Desktop](https://www.raspberrypi.org/software/operating-systems/) v5.4.

I inserted the microSD card into the a USB card reader and then ran the Raspbian PI Imager to install the OS onto the microSD card.

## Enabling SSH

As I will be using a headless connection (no monitor, mouse or keyboard) I added an empty ssh file to the directory. To do this I ran Notepad, created a new file and when I hit "Save As...", I set the "Save as type" to "All Files" and called the file **ssh** and saved it to the the root of the USB drive.

## Initial configuration via Putty

I inserted the microSD card into the Raspberry Pi 4 and connected it via ethernet and then booted the device. Once the Pi had booted, I ran [Putty](https://www.chiark.greenend.org.uk/\~sgtatham/putty/), an SSH client, and connected to it on the _raspberrypi.local_ address.

[![An image of the putty configuration screen](https://github.com/inquisitivenoodle/mywebsite/raw/master/site/content/post/img/putty-login.png "putty configuration screen")](https://github.com/inquisitivenoodle/mywebsite/blob/master/site/content/post/img/putty-login.png)

I accepted the warning and then entered the login credentials to the default installation - username: _pi_, password: _raspberry_. At the terminal prompt then I ran:

    sudo raspi-config

This launched the raspi-config menu, and I chose _5 Interfacing Options_.

[![raspi config interfacing menu option](https://github.com/inquisitivenoodle/mywebsite/raw/master/site/content/post/img/interfacing-option.png "interfacing option in the raspi-config menu")](https://github.com/inquisitivenoodle/mywebsite/blob/master/site/content/post/img/interfacing-option.png)

In the next menu, then I chose _P3 VNC_ and then I accepted turning the option on. I exited out of raspi-config back to the terminal. You can use the Tab key to jump from the menus to the "Select" and "Back" options and Enter to choose one once it's highlighted.

[![raspi config VNC menu options](https://github.com/inquisitivenoodle/mywebsite/raw/master/site/content/post/img/vnc-option.png "VNC option in the raspi-config interfacing options")](https://github.com/inquisitivenoodle/mywebsite/blob/master/site/content/post/img/vnc-option.png)

## Connecting into Raspberry PI desktop via VNC

Next up in _raspi-config_ I choose _3 Boot Options_ and then _B1 Desktop / CLI_, then _B3 Desktop_.

[![desktop boot options in raspi-config](https://github.com/inquisitivenoodle/mywebsite/raw/master/site/content/post/img/desktop-boot-option.png "desktop boot option in the raspi-config boot options")](https://github.com/inquisitivenoodle/mywebsite/blob/master/site/content/post/img/desktop-boot-option.png)

Also, because no monitor will be attached. I set the screen resolution by going through _7 Advanced Options > A5 Resolution_ and then selected the _1920x1080_ option.

[![screen resolution options in raspi-config](https://github.com/inquisitivenoodle/mywebsite/raw/master/site/content/post/img/screen-resolution-option.png "screen resolution entries in raspi-config")](https://github.com/inquisitivenoodle/mywebsite/blob/master/site/content/post/img/screen-resolution-option.png)

Then I selected _Finish_ and then _Reboot_ to restart the Raspberry Pi.

I downloaded [VNC viewer](https://www.realvnc.com/en/connect/download/viewer/), launched it and connected to the Raspberry Pi 4 on the _raspberrypi.local_ address, using the same credentials as before - username: _pi_, password: _raspberry_.

[![VNC login dialogue box](https://github.com/inquisitivenoodle/mywebsite/raw/master/site/content/post/img/vnc-login.png "logging into raspberry pi via VNC")](https://github.com/inquisitivenoodle/mywebsite/blob/master/site/content/post/img/vnc-login.png)

This allowed me to login to the desktop using the same credentials again. If you get a black background with a "_desktop cannot be displayed at this time"_ error message after authenticating on VNC, try changing the resolution to a lower one in the previous step.

[![raspberry pi desktop login screen](https://github.com/inquisitivenoodle/mywebsite/raw/master/site/content/post/img/desktop-login.png "raspberry pi desktop login screen")](https://github.com/inquisitivenoodle/mywebsite/blob/master/site/content/post/img/desktop-login.png)

Following a successful login, the os then prompted me through a series of steps to secure the pi - such as changing the admin password.

## Connecting the Raspberry Pi to wifi

As part of the intial configuration dialogues, I was prompted to _Select a wireless network._ I chose the network name (SSID) and entered the password. The pi automatically connected to the network and this was reflected in the toolbar on the top right hand side, second notification icon in.

[![wireless notification icon in upper right navigation bar](https://github.com/inquisitivenoodle/mywebsite/raw/master/site/content/post/img/wireless-icon.png "wireless notification icon in upper right navigation bar")](https://github.com/inquisitivenoodle/mywebsite/blob/master/site/content/post/img/wireless-icon.png)

If you aren't going through the initial configuration the wireless network can be connected in the following ways:

1. If you can connect to the Raspberry Pi desktop, you can click on the wireless icon and choose your network from the list the Pi can see.
2. If you can't connect to the Raspberry Pi desktop, you can set the wireless credentials in the _raspi-config_ by choosing _1 System Options_ and then _S1 Wireless LAN._ Enter the network name as the SSID and the wireless password as the passphrase and then OK and exit out of the setup.

## Updating the Raspberry Pi

The last step in the initial setup is to update the raspberry pi through a dialogue box entitled _Update Software_. This will go back to the operating system servers and update and install any packages that may have been released since the version of the OS you downloaded was created.

You can achieve the same result by navigating to the _Terminal_ icon, the fourth one in on the top left bar that looks like a black window with a blue title bar.

[![terminal icon in the upper left navigation bar](https://github.com/inquisitivenoodle/mywebsite/raw/master/site/content/post/img/terminal-icon.png "terminal icon in the upper left navigation bar")](https://github.com/inquisitivenoodle/mywebsite/blob/master/site/content/post/img/terminal-icon.png)

Once _Terminal_ has opened, you can run the following commands:

    sudo apt-get update
    sudo apt-get upgrade

At the terminal prompt of "_Do you want to continue? \[Y/n\]",_ type "y" (no quotes) and the terminal will then start to install all the updated packages. Once terminal returns you to a prompt the update has completed and you can close the application.
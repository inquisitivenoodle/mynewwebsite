+++
author = "🍜 Inquisitive Noodle"
categories = ["Linux Mint"]
date = 2021-01-13T20:22:00Z
description = "Installing Google Drive installed as a network online account in Linux Mint"
image = ""
title = "Installing Google Drive on Linux Mint"
type = "post"

+++
By default with a clean install of Linux Mint 20.01, the user is not prompted to configure their online accounts such as Google Drive, One Drive, Dropbox etc.

## Installing Online Accounts

In _Terminal_, run the following code:

    sudo apt install gnome-online-accounts
    XDG_CURRENT_DESKTOP=GNOME gnome-control-centre

The you can enter the details for your Google Drive, Dropbox, One Drive etc in the dialogue box that launches.
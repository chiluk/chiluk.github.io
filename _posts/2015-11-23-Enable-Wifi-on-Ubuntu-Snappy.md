---
layout: post
title: Enable Wifi on Ubuntu Snappy
date: 2015-11-23
author: chiluk
tags:
- linux
- snappy
- ubuntu
- raspberrypi
---

I recently spent more time than was necessary trying to figure out the "snappy" way of enabling wifi on my Raspberry Pi 2.  After reading through the documentation, I was expecting to find an elegant snap or framework.  Instead, in recent images all that's required is to add to the following to /etc/interfaces.d/wlan0.

	allow-hotplug wlan0
	iface wlan0 inet dhcp
	  wpa_ssid <SSID>
	  wpa_psk <passphrase>


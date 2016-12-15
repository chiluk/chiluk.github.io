---
layout: post
title: Fix Intel Nuc Boot Ordering
date: 2016-12-15
author: chiluk
tags:
- linux
- Intel
- nuc
- bios
- automation
---

I've been having a hell of a time getting my nucs to respect the drive boot order naming.  Basically I have an external USB disk attached, and for whatever reason the bios insists on making the external usb disk sda.  Normally this wouldn't be a problem since linux is usually configured to mount by UUID.  However, my nucs are commissioned in my maas cluster for use as ceph-osd nodes.  Yeah, I know not the most performant, but this is purely for development purposes.  Specifying the disk volume is accomplished via bios name i.e. sdb.  So when my root disk comes up as sdb, I get a big fat failure when ceph also tries to use sdb.

The Solution:
1. Remove the usb disk.
1. Commission the node.  You may have to remove the existing storage devices via the maas interface.
1. Install the node.
1. Shutdown the node.
1. Start the node.
1. Shutdown the node. *(Not sure if this second reboot cycle is necessary)
1. Attach the usb disk.
1. Cross fingers, and pray for pitty from the BIOS/EFI developers at Intel.
1. Start the node, and verify that the usb disk now shows up as sdb.
1. Release the node in maas.
1. Re-commission the node in maas.
1. Check that maas has the disks ordered correctly.
1. Redeploy the node in maas.

As best I can tell the Intel firmware has some logic in it that checks for successful boots, and attempts to rid itself of bad devices.  This typically affects me when my nuc is released, reset, or powered off in the midst of booting.  So the goal here is to get a few successful boots without the usb disk in the hopes of clearing that bit of the firmware's memory about the usb disk.
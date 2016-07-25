---
layout: post
title: Add Steam bigpicture to MythTV Menus
date: 2016-07-23
author: chiluk
tags:
- linux
- mythtv
- steam
- ubuntu
---

So I tried to find a good how-to for integrating steam big picture into my mythbuntu based mythtv installation. It turns out the change is fairly trivial.  All you have to do is add a button entry to /usr/share/mythtv/themes/defaultmenu/mainmenu.xml like the below diff. 

	--- mainmenu.xml.orig	2016-07-24 23:56:30.918935677 -0500
	+++ mainmenu.xml	2016-07-25 01:03:48.061586983 -0500
	@@ -16,6 +16,13 @@
	     </button>
	 
	     <button>
	+        <type>GAME</type>
	+        <text>Steam Games</text>
	+        <description>Launch Steam Big Picture Mode</description>
	+        <action>EXEC steam -bigpicture</action>
	+    </button>
	+
	+    <button>
		 <type>MENU_INFO_CENTER</type>
		 <text>Information Center</text>
		 <description>Information and Communications</description>

However when exiting steam, you have to select to exit steam instead of the other options.  This way mythtv regains focus again.  There is probably a way to accomplish this, but I haven't yet spent the time to figure it out.

Enjoy!

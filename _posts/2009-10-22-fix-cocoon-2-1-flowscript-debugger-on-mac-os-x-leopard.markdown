---
layout: post
title: Fix Cocoon 2.1 flowscript debugger on Mac OS X Leopard
tags: []
typo_id: 332
---
This is a tip which will no doubt have a very limited audience!

If you are using <a href="http://cocoon.apache.org/2.1/">Cocoon 2.1</a> on Mac OS X 10.5 or 10.6, the <a href="http://cocoon.apache.org/2.1/userdocs/flow/">flowscript</a> debugger doesn't work. This is because it isn't compatible with the Apple look & feel. You need to change the system default look & feel to get it working.

<!-- read more -->
You can do this by editing the file which configures the default look & feel - `/System/Library/Frameworks/JavaVM.framework/Versions/1.6/Home/lib/swing.properties`.

The contents of this file, by default, are:

	swing.defaultlaf=apple.laf.AquaLookAndFeel

You need to comment this out, and use Sun's metal look & feel instead:

	#swing.defaultlaf=apple.laf.AquaLookAndFeel
	swing.defaultlaf=javax.swing.plaf.metal.MetalLookAndFeel

Now the flowscript debugger will work properly.

---
layout: post
title: Fixed version of Logitech Control Center 2.12
tags:
- OSX
- Apple
typo_id: 299
---
I have just installed LCC 2.12 and it doesn't work. Version 2.11 worked fairly well but was a bit buggy
when switching scroll wheel settings when focus moved between apps.

I have tracked down the problem to the fact that some files are missing in the install, read on for more
info and a fix.

*Updated 2007-01-07:* 'a' pointed out that you need to make sure the ownership of the kext is correct,
so I've added another step.

*Updated 2007-01-11:* I've just noticed that Logitech have pulled version 2.12 from their site. You can only download version 2.11 at  the moment.

*Updated 2007-01-12:* Version 2.12 is back on Logitech's site. Unfortunately, it is still broken.

*Updated 2007-01-23:* [Logitech have fixed the bug]({{ site.baseurl }}{% post_url 2007-01-22-logitech-mx-revolution-drivers-fixed %}.
I've removed the download as it's not needed any more.

<!-- read more -->

The problem is that the Info.plist and PkgInfo files are missing from the Logitech kernel extension LogitechUSBHIDevices.kext.
Without those files, Mac OS X doesn't recognise it as a kernel extension and refuses to load it.

I've reinstalled LCC 2.11, extracted the files from that kext, and edited Info.plist so it refers to version 2.12 instead of 2.11.
The fixed version works.

To fix your version, do the following:
1. Understand that you do this at entirely your own risk! It seems to be working fine for me, but I cannot take responsibility
   for anything which might happen if you follow these instructions. I'm only supplying these details as a public service.
2. Install LCC 2.12 if you haven't already done so
3. Navigate to /System/Library/Extensions in Finder and delete LogitechUSBHIDevices.kext
4. Download and extract my <del>fixed version of the kext (151kb)</del>
5. Copy the extracted LogitechUSBHIDevices.kext to /System/Library/Extensions
6. *added 2007-01-07 (thanks to 'a', see comments):* make sure that the ownership of the files in the kext is correct. Open a
   Terminal prompt and execute `sudo chown -R root:wheel /System/Library/Extensions/LogitechUSBHIDevices.kext`
7. Restart

The only difference between the original Logitech 2.12 version of the kext and my version is that
my version includes the PkgInfo and Info.plist files.

Technically, you could probably avoid the need to restart by doing this:
1. Start Terminal
2. `sudo kextunload /System/Library/Extensions/LogitechUSBHIDevices.kext`
3. remove that old version and replace it with the one you downloaded as above
4. `sudo kextload /System/Library/Extensions/LogitechUSBHIDevices.kext`

I'll leave the file available until Logitech release a fixed version.

If you'd rather just revert to version 2.11 until they fix it, you can download that version from Logitech.

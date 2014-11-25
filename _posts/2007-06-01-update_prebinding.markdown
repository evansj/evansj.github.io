---
layout: post
title: update_prebinding
tags:
- Apple
typo_id: 310
---
My MacBook has been getting slower and slower lately, so today I
started to investigate what the cause might be. I'd noticed a while
ago that a message had started appearing in `system.log`:

    update_prebinding: error: dependent dylib is not prebound
    update_prebinding: error 256 running update_prebinding_core

You can run `update_prebinding` from the shell but you don't get
any extra insight into the problem because the error message is
exactly the same.


<!-- read more -->
There is a `-debug` option which looks promising, but that too
isn't as helpful as it could be -- it tells you the last library
it successfully prebound, then fails:

    [snip loads of other lines...]
    dyld: re-prebound: 0x90bee000 /usr/lib/libgcc_s.1.dylib
    update_prebinding: error: dependent dylib is not prebound
    update_prebinding: error 256 running update_prebinding_core

If only it told us the name of the library which was causing the
problem! As it happens, you can work it out, because it turns out
that update_prebinding just works its way though a list of files
in `/var/db/dyld/update-prebinding-paths.txt`. In my copy of that
file, the library on the line after `libgcc_s.1.dylib` is
`/Applications/Utilities/Java/Java Web Start.app/Contents/Resources/Java/libmacjavaws.jnilib`.
I commented that line out (by preceding it with a # character)
but the problem still wasn't solved, so I edited the file again
and commented out all of the Java 1.3.1 libraries. Now
`update_prebinding` runs to completion.

I have no idea whether I've actually fixed anything, but the
MacBook at least now feels quicker. I counted the number of
bounces of the dock icon were required to start Safari last week
and got at least 11, and today it started before it had even
bounced once. Yes, I know that's a completely bogus test. :-)

I still have another problem, which is that Disk Utility has
detected an error on my hard drive which it can't fix. Not even
by booting from the OS X DVD and running Disk Utility from there.
I'm going to refresh my hard drive backup and reinstall everything
at some point in the next few days to hopefully fix this.

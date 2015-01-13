---
layout: post
title: Geektool script to show the ping time to your home machine
tags:
- Apple
typo_id: 103
---
Here's a [Geektool](http://projects.tynsoe.org/en/geektool/) command to show the "network distance" to a particular machine on your desktop all the time.  I have the distance to my home server in the top left corner of my screen all the time.

Go to the Geektool preference pane and add a new entry.  Mine is called "ping home"

Set the entry type to "Shell"

Paste the following into the Command textbox:

    HOST=home
    PING=`ping -q -c 1 $HOST`
    if [[ $? -eq 0 ]] ; then
        TIME=`echo $PING |tail -1 | cut -d/ -f 5`
        echo -n ${TIME}ms away from $HOST
        exit 0
    else
        echo -n $HOST could not be reached
        exit 2
    fi

Change the value of HOST on the first line to the hostname of the server you want to ping.
(Hint for writing your own scripts: use Option-Return to insert a newline).

Switch to the "Colors and font" tab and choose something nice.  I use Gill Sans, in white because my desktop backgrounds are usually dark.  No frame, no shadow on the window.

Switch to the "Text" tab, turn on drop shadow, select left alignment of text.

On the "Icon" tab, check "Show icon", use the default success and failure icons, and pick the left, centered icon alignment.

Drag the window on your desktop to the top left and you're done.

If the network is working, you'll get something like this:

<img src="http://evansweb.info/files/Picture%201-1.png" height="24" width="300" border="1" hspace="4" vspace="4" alt="Picture 1-1" style="background: #000" />

If not, you'll get this:

<img src="http://evansweb.info/files/Picture%202-1.png" height="24" width="300" border="1" hspace="4" vspace="4" alt="Picture 2-1" style="background: #000" />

Update: [JAW Software](http://www.jaw.it/) is hosting a [more Tiger-friendly version of Geektool](http://www.jaw.it/pages/en/x_misc.html).  The changes will hopefully make it to the official version soon.

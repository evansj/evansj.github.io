---
layout: post
title: 'OBC part 2: Changing the backlight colour'
tags:
- BMW Repairs
- Cars
- From my old site
typo_id: 65
---
Now you have your OBC in bits (see part 1), how do you go about changing the stock orange backlight to something a bit more modern?
<!-- read more -->
There are two components to the obc backlighting -- the LCD backlight, and the keypad backlight.

At the end of part 1 of the diassembly instructions, you removed the LCD display itself (and I hope you put it somewhere safe, if you break it it's game over). If you look at the connector where the LCD used to go you will see that there is an orange diffuser clipped into place. This is the reason the display lights up orange.

<img src="/files/20030224212230292_1.jpg" height="275" width="400" border="1" hspace="4" vspace="4" alt=" Images Articles 20030224212230292 1" />


The diffuser is clipped at each end to a metal box in the middle of the LCD connector. It can be unclipped by carefully slipping a knife inbetween the filter and the connector at the centre of one of the long edges, and lifting it up in the middle. This will bend the diffuser, unclipping the ends. The connector will now look something like this.

<img src="/files/20030224212230292_2.jpg" height="190" width="400" border="1" hspace="4" vspace="4" alt=" Images Articles 20030224212230292 2" />

...note the clips on each end of the diffuser, they clip into the metal light box

<img src="/files/20030224212230292_3.jpg" height="215" width="299" border="1" hspace="4" vspace="4" alt=" Images Articles 20030224212230292 3" />


The lightbox itself is made of metal to withstand the constant heat from the two bulbs. It has two metal tabs to cover the bulbs to prevent the display from having two bright spots where the bulbs are.

I can think of a few ways to change the colour of the display. First you could try leaving the orange filter out, and using coloured bulbs. Second, you could make a small circuit board to fit in the light box, holding LEDs of the appropriate colour. It would be a good idea to paint the component side of the circuit board white before soldering in the LEDs. Third, you could make your own replacement filter with coloured gels.

My preference would be to use a circuit board populated with LEDs, but blue LEDs (which I think would look best) are still amazingly expensive. Like about &pound;3.50 each.

What about converting the display to an inverse (black on orange) display? Well, it would be easy, if the polarising filter had not been glued to the front of the LCD! If by some fluke yours does happen to be detached, you can invert your display by flipping the filter over. Whatever you do don't try to peel off the filter, you will only break it (the filter and the LCD).

How about the backlight for the keyboard? Well if anything you have an even harder job on your hands with this one. The light guide is in two parts, a part on the front side of the circuit board, and a part behind into which the bulb shines. The front light guide is fine, but the rear one has been tinted in the factory to produce the orange colour. You can clearly see it in the following photo.

<img src="/files/20030224212230292_4.jpg" height="375" width="400" border="1" hspace="4" vspace="4" alt=" Images Articles 20030224212230292 4" />


The only solution I can think of to this problem is to dispense with the rear light guide completely, and use LEDs for instead. You will need 6 very small LEDs to illuminate the front light guide, probably surface mount compoents are the only ones small enough. The problem is that the light guide finishes extremely close to the sides of the case, in fact the 6 extremities of the light guide can be seen through cutouts in the side of the case.

In the light (pun intended!) of all these problems I decided to leave it all orange for now.

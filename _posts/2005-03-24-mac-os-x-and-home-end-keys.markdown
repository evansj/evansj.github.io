---
layout: post
title: Mac OS X and Home / End keys
tags:
- Apple
typo_id: 16
---
The default key bindings for the home and end keys in Mac OS X are different to any other operating system I've ever used.  By default, they seem to be bound to the viewport, rather than the line of text you are editing.  In a multi-line document, the Home key scrolls up to the top of the document, and the End key scrolls down to the bottom.  In each case the caret stays where it was.

As a programmer I find this behaviour to be just plain wrong&mdash; I want Home and End to move to the start and end of the current line.

I have found a way to "fix" this problem by editing the default keybindings file, <kbd>~/Library/KeyBindings/DefaultKeyBinding.dict</kbd>.  Create the directory and / or the file if they're not already there, and make it look like this:

<pre>
{
        /* Remap Home / End to be correct :-) */
        "\UF729"  = "moveToBeginningOfLine:";                   /* Home         */
        "\UF72B"  = "moveToEndOfLine:";                         /* End          */
        "$\UF729" = "moveToBeginningOfLineAndModifySelection:"; /* Shift + Home */
        "$\UF72B" = "moveToEndOfLineAndModifySelection:";       /* Shift + End  */
}
</pre>

If there are already entries in DefaultKeyBinding.dict, just add the 4 new mappings above to the main section of your file.

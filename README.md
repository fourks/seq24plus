#seq24plus README


##Installation

How to install? 

    read INSTALL.

##Usage

How to use seq24?
    
    Documentation on using seq24 is in the SEQ24 file.

##License

Information on modifying, copying?

    This software is free, and released under the GPL.
    This is available in the COPYING file.

##Authors

Who wrote this?

    Read AUTHORS.

Why did they write this?

    Again, Read SEQ24

What to do with a fresh repository checkout?

    Apply "autoreconf" to get a configure script, then read INSTALL.

----
#DEV NOTES

If you add new .cpp or .h files, you'll need to modify Makefile.am, and then run ./configure to generate Makefile.in and Makefile




----
#TODO list:

in no particular order

## [DONE] songmode start/stop

*In song mode, be able to start and stop using 'space' and 'tab' keys regardless of which window is active.*

This already works in the version I have (0.9.2) - need to get this version onto Wallace

----

## STOP marker

Have a 'stop' marker in the song window (check whether this can be achieved by deleting the trailing empty bars).
This should be detected automatically by scanning the pattern
First job is to print the pattern length to console when perfroll is opened
    
#### Strategy

Iterate through each active sequence and calculate the time it ends. Do this at every update. This shouldn't be hard to do, because the updates are already drawn onto the perfroll, and this info can only be changed if a perfroll window is open. 

1. Find out how the song data is laid out. This should be done when perfroll is constructed.
- use printfs to show where the bits of the song are being laid out.     
- figure out how the bars of each song relate to midi time - thus we should know when to stop
- implement a stop at this point

Long term, it'd be better to calculate the stop time without the perfroll window being open, so we aren't dependent on that...
    
#### Code Analysis
`perfroll.cpp` is the file that lays out the performance roll. It has a `perform` object called `m_mainperf`. This gets each sequence that has data, and gets a list of tick data. The maximum value of the `tick_off' parameter (see line 350 in perfroll.cpp) is the end of the sequence. So if I find the tick value when the system is playing, I can trigger a stop!
    
`perform.cpp` is the class that holds the midi data. It has an array of pointers to `sequence` objects

`sequence.cpp` is the class that holds each sequence (I think)

----

## Song editor scroll

*Allow the song editor to scroll across when playing*

Subtasks

1.Look at how the horizontal scroll bar works
2. Detect when the play marker hits the edge of the window
3. Scroll the appropriate distance
### High Res screens

- enhance usability on high resolution screens

### Setlist

- be able to load a setlist and load each song with ctrl+arrow key in read-only mode.

### Mode switching

- be able to switch between live and song mode more easily than via options.

### Console mode

- have an interactive 'console' mode without the gui

### Midi-in note off

- At the moment, the length of the note is specified in the dialog box and doesn't come from the midi-in - should be easy to find...?

---

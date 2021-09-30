# ForayInto68k website in /docs/
Resources for System 6, 68k Macs

# RetroChallenge for October 2021 - Reverse engineer the Studio Session Format


## Goal: 
Load a Studio Session song file (along with its instruments) and play it back, close to the original in a custom game program (eg in an intro splash screen)

## Context: 
Studio Session from Bogas Productions released in 1986. It uses 11 kHz instrument sound samples of arbitrary sizes and mixes up to 6 tracks together to create music that went beyond the default Apple Sound Driver, whose most similar mode of usage featured 4 channels of 256 byte-long sound waves.

## Use case if the project comes to completion: 
This song format has a very mature song editor with the usual Mac GUI frills using standard musical notation. There are nifty tools that allows to re-use chunks of music (phrase library) and repeat some sections. If I can programmatically play back a song, this could be incorporated into a game programming project very easily. Some advanced music could be played back in a title screen or during a non-cpu intensive part of a game (cinematics for example). This was done commercially in some games like Tetris, Falcon F-16 and Vette!, all from Spectrum Holobytes. The code they used would be what the final form of this project strives to reach.

## Target Hardware Environment: 
same machines that used to run Studio Session, which is probably a stock Mac Plus with a 68000 and 1Mb of RAM

##Target Software Environment: 
A System version that supports the Sound Driver at first. If all goes well, target the next few versions of System which made use of the Sound Manager. I suspect this is a high step between these 2.

## Programming Tools: 
Symantec THINK C 6.0, THINK Reference, ResEdit, SoundCap (or others), Studio Session

## Demo as of September 2021:  https://www.youtube.com/watch?v=bBvUJi0LOD0

# Phase 1 (in progress):

## DONE:
### Load a song file
### Detect basic info: instrument list, master key, master tempo, most proprietary commands
### Use the Sound Driver square-wave synth to play back a channel

## TO DO:
### Create an interface that displays song info
### Select a channel to play back
### Very aggressively cut up the source code into many small files for future management
### Get some timing measurement routines to test out some optimizations

# Phase 2:

## TO DO:
### Use the 4-synth driver to select and play 4 channels at once
### Figure out how the notes are synchronized together, ie, what's the smallest time slice where note changes happen, instruments come in/out, etc.
### Figure out buffering used during playback - can the whole song be loaded at once, or is it done on the fly
### Figure out if sync needs to happen with video blanking (VBL) interrupts

# Phase 3:

## TO DO:
### Figure out how much memory is needed
### Figure out a mixing method to avoid saturation of the freeform synth driver - divide by 2, sqrt(2) or 6?
### Re-figure out buffering used during playback - can the whole song be loaded at once, or is it done on the fly
### Optimize data transfers to squeeze out some free CPU cycles as much as possible
### Explore using ASM blocks for some critical parts of the program as needed

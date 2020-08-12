## Inserting Music
First off, you want to get the Native Instrument Map for your game (FE6 doesn't
have one, you'll need some other instrument patch). 

Then get
[Sappy2EA](https://www.dropbox.com/s/nw5w6wqwny0wnrh/Sappy2EA.zip?dl=0), which
comes with a music installer and other useful things.

### Converting from MIDI
>####**Make sure your midi has no spaces or +- signs in the file name!**

Get yourself Mid2AGB and Sappy2EA. Drag midi onto Mid2AGB, receive .s file.
Drag .s file onto S2EA, receive event file. Then include it in your Music
Installer and add the macro to set the table entry (the label name should be
the same as the file name):

    SongTable(8,FE4Ch10,MapMusicGroup)
	#include "FE4Ch10.event"

In some cases, the label name will not match the file name. To check this,
open the .event file produced by S2EA, scroll down to the bottom and see
what the label with the song data is called.

Additionally, S2EA will by default output songs at max volume. To change
the master volume of the entire song, take a look at the top of the file
for the define with the master volume. Max volume is 127, min is 0.

	#define	song17_mvl  64

### Custom SFX
### About Song Groups


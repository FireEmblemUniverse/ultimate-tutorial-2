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

### Custom SFX
### About Song Groups


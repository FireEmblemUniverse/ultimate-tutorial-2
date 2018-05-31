## Inserting Portraits

Here's an example `Portrait Installer.event`:

    #include "Tools/Tool Helpers.txt"
    //this file defines the macro:
    //setMugEntry(number, data, mouth_x, mouth_y, eye_x, eye_y)
    
    Sigurd_Mug:
    #incext PortraitFormatter "sigurd.png"
    setMugEntry(0x51, Sigurd_Mug, 3, 5, 3, 3)

Easy, right?

In free space, you simply label the portrait and use #incext PortraitFormatter
to convert the PNG for insertion. Then use setMugEntry to set the portrait ID
and the tile locations for the eye and mouth frames.

### Formatting Portraits
Formatting portraits is the same between buildfiles and FEditor.

This is a hackbox. Your portrait should fit in this.

![Hackbox](https://i.imgur.com/2MpEGSA.png)

### Ripping Portraits

You can use FEditor to rip portraits and have them formatted ready to go. Alternatively you can download all the GBA portraits [**right here**](https://doc.feuniverse.us/static/resources/mugs.png).

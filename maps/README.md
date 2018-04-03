
### Inserting Maps

[Here's a good tutorial for making your map. Use it up to insertion. (By Markyjoe)](http://markyjoe.com/Tutorials/Tiled_Tutorial/Tutorial.html)

All right. I'm assuming you have your map ready. Under your main tile layer properties,
specify the following if applicable:
```
Name               Default Value   Notes
-----------------------------------------------------------------------------
Main                                    Required when there are multiple layers.
ChapterID         ChapterID       The chapter number/row in the chapter data editor
ObjectType1     ObjectType     The object set to use. Can also use ObjectType
ObjectType2           0                FE7 only
PaletteID           PaletteID         The palette to use
TileConfig         TileConfig       The tile configuration to use
MapID               map_id           The index of the map in the Event Pointer Table
MapChangesID map_changes  The index of the map changes in the Event Pointer Table
Anims1                   0                Tile Animation to use. Can also use Anims
Anims2                   0                FE8 only
```
Next, drag and drop onto TMX2EA.exe, and your .event file should come out.
#include that in the master map installer, #include the master installer,
and you should be good to go!

### World Map Editing (FE8)


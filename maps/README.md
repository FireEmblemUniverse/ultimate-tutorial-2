
## Inserting Maps

### Tile Changes
### Insertion
With your map and tile changes set up correctly, get
[TMX2EA](http://feuniverse.us/t/insert-tiled-maps-using-event-assembler/1830?u=circleseverywhere)
and put it in your Maps folder. When you run TMX2EA it will scan the folder and
subfolders for tmx files and convert them to .event files. #include those in
your Master Map Installer, and open them up to set the table entries (e.g. 0x4
is the Prologue map in FE8, 0x6 is the Prologue map changes). If you're
changing the tileset you need to update this in the Chapter Data Editor module
(for now, anyway).

### World Map Editing (FE8)


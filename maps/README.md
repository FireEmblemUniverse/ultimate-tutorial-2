
### Inserting Maps

[Here's a good map *making* tutorial. I suggest you read it up to insertion. (By Markyjoe)](http://markyjoe.com/Tutorials/Tiled_Tutorial/Tutorial.html)

The main helper tool you will use here will be [`tmx2ea`](http://feuniverse.us/t/tmx2ea-v2-0-released-insert-tiled-maps-using-event-assembler/1830). It is a tool that is able to translate `.tmx` files (Tiled map files) into insertable events. In addition to inserting maps, it is also able to insert map changes, and it will also automatically fill up chapter data for you.

Now let's assume you have your map ready. Under your main tile layer properties, specify the following if applicable:

```
Name               Default Value   Notes
-----------------------------------------------------------------------------
Main                               Required when there are multiple layers.
ChapterID          ChapterID       The chapter number/row in the chapter data editor
ObjectType1        ObjectType      The object set to use. Can also use ObjectType
ObjectType2        0               FE7 only
PaletteID          PaletteID       The palette to use
TileConfig         TileConfig      The tile configuration to use
MapID              map_id          The index of the map in the Event Pointer Table
MapChangesID       map_changes     The index of the map changes in the Event Pointer Table
Anims1             0               Tile Animation to use. Can also use Anims
Anims2             0               FE8 only
```

Next, I suggest you make a new subfolder in your Root folder. This is because you will need to have all your maps located there for `tmx2ea` to work at its best (because, much like `n2ea`, it will scan for map files in the folder it is in). I'll assume you'll call it `Maps`.

In your `Maps` folder, put in the `tmx2ea` executable along with you map file(s). Next, *run* `tmx2ea`. It will ask you whether you want to scan all subfolders for `tmx` files: tell it that you want. After it being done, you should be able to see a few new files in your `Maps` folder: One `event` and one `dmp` file for each of your map file, and `Master Map Installer.event`.

All you should need to do is to `#include` the master map installer file from your main buildfile, because (as its name implies) the master map installer event file *will* install every map scanned by `tmx2ea`.

After generating the master installer, you can use `tmx2ea` to update *specific* maps instead of all of them at once (to gain a little bit of time). To do that, simply drag your `tmx` file onto the `tmx2ea` executable and it should do its thing no problem.

### World Map Editing (FE8)


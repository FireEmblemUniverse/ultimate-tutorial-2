
## Inserting Misc Graphics

MASSIVE TODO

### Ripping images with GBAGE
### Chapter Name Graphics
FE8 uses graphics as chapter names, unlike FE7 which uses text.
Luckily for you, [there's a hack for that](http://feuniverse.us/t/fe8-chapter-titles-as-text/2065?u=circleseverywhere).
### Map Sprites
As you may already know, there are two types of map sprites: moving and standing.
These are treated separately with different graphics and tables. Let's start
with standing sprites.

First, we want to insert the graphical data simply like this.
```
ChampionSt:
#incext Png2Dmp ChampionSt.png --lz77
```
That --lz77 is very important as map sprites are lz77 compressed, but that's it.
Now to let the game know where the graphics are...
This is where the Standing Map Sprite Editor comes in. You can add entries to the end
of this table for each map sprite you're inserting. Put your label into the Pointer
to Graphics Section (for me, ChampionSt|IsPointer).
Then, we need to specify the size. Go ahead and use these in the table.
```
#define Large 0x02 // Use for 32x32 frames
#define Medium 0x01 // Use for 32x16 frames
#define Small 0x00 // Use for 16x16 frames
```
Finally, we need to specify the slot we put the sprite in in the Class Editor in the 
Map Sprite # (standing) slot.

For moving sprites, it works just a bit differently. We're going to insert our raw
graphical data in the same way.
```
ChampionMv:
#incext Png2Dmp ChampionMv.png --lz77
```
This is where it gets a little different. In the Moving Map Sprite Table, you see
it has 2 pointers we need. They are named a little stupidly in some versions so let
me clarify.

The first pointer is to the graphics we just inserted.
The second pointer is to data that handles its animation (OAM data).

OAM data? Sounds scary. Don't worry. We barely have to worry about it.
So now write your label (ChampionMv|IsPointer) into the first pointer, but this time,
the slot number has to match the class number. If you're overwriting the Revenant class,
the new moving map sprite has to go in the moving Revenant map sprite slot.

Then the OAM data. The best thing to do is not touch it. Test new the sprite before
touching the OAM pointer. If it looks fine, it's good. If it looks weird, then try a
different one from a vanilla class that has a similar sprite. I've never seen a moving
sprite that doesn't have vanilla OAM data that works for it.

Then that's it! Your map sprites are good to go.
### Custom CGs
### Battle Backgrounds
### Battle Frames (FE8)
Name frames are 7 tiles wide (1 more than fe7):
In game is arranged

      01 03 05 07 09 11 13
      02 04 06 08 10 12 14

Graphic is arranged  

      01 02 03 04 05 06 07
      08 09 10 11 12 13 14

Weapon frames are 8 tiles wide (1 more than fe7):
In game is arranged

      01 03 05 07 09 11 13 15
      02 04 06 08 10 12 14 16

Graphic is arranged

      01 02 03 04 05 06 07 08
      09 10 11 12 13 14 15 16

convert these images to bin files and compress using lz77

Format battle frame like the default
in wingrit use these settings for your battle frame:
![grit settings](https://i.gyazo.com/b153f107d63d24084884ebc715ce4708.png)

Then use FE8 Battle Frames Installer.txt with Event Assembler

You're done!


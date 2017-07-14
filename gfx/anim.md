## Inserting Animations

TODO

### Inserting existing animations

If your animation is already in .event format, just open it up and change `AnimTableEntry(0x0)` to whichever animation slot you are using, then `#include` it in free space.

If it is in FEditor format, download Animation Assembler and drag the
**extensionless file** onto AA.exe. Wait for it to finish processing, then
change AnimTableEntry as outlined above.

### Creating custom animations

This is more time consuming than it is difficult. My advice is to block out the
motions using stick figures, and then flesh out the animation once you're happy
with it.

I use Aseprite and Blender to animate, and it works pretty well.

### Battle Palette Editing

TODO

### Spell Animations

Download [Circles' Spell Animation
Creator](http://feuniverse.us/t/fe6-7-8-circles-spell-animation-creator-updated-to-v1-1/1946?u=circleseverywhere)
and drag your script onto `CSA_Creator.exe`. Then `#include` your created event
file at the end of the Master Spell Animation Installer, and `#include` THAT in
your buildfile.


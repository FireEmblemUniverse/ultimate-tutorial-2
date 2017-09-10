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

For the first step of this, you'll need to get a copy of FE Recolor. You'll also need Pal2EA for that, so grab that as well.

FERecolor is a program used to make palette changes for battle animations. We're doing our recolor and then getting those colors as a hex for later.

Open it up and go to Load Image. Open up the image for the class you want to work with. Once that's done, just modify your colors until you like how the unit looks.

Just make sure not to meddle with the box below the reset buttons. That's the order which will be needed for the next step.

When you've got your palette done, click Copy hex to clipboard and you'll get a hex string. Close the box, we're now moving to Pal2EA.



We're going to make a new .txt where we'll create our input to Pal2EA. I'm going to refer to this as Palette Input.txt. This is the file we'll give Pal2EA which will generate the .event's we actually insert.

#char(0x6F) "AlanCav" set{0x02,0x1,0x5}
	5553FF7FFF5B737FF431AA799E00F8009F26DE0017002A001D4736324E1DA514
	auto
	auto
	auto
	auto

This will probably be easier to explain with an example, so here it is.

#char(0x6F) means that we're inserting the palette into 0x6F in that table. You can find the list of slots in the same folder as the Animation nmm's. It's called Palette List.txt. 0x6F is an empty slot, they start from 0x6E.

"AlanCav" is something Pal2EA will print so you know it's processed this palette. Not necessary and you can put a string in between the quotes.

set[0x2,0x1,0x5) is a little more complicated.

The first thing is the character ID. In this case, I'm selecting Seth,

The second thing is the palette number. I don't think this really pops up elsewhere, but it's important here. Each character has up to 7 classes for palette association.

0x0 is trainee, 0x1 is the unpromoted class, 0x2 is the 2nd unpromoted class for trainee's, 0x3 is the first promotion option for the first unpromoted class, 0x4 is the 2nd for 0x1, etc.

In this case, it's going to Seth's normal unpromoted class.

The third thing is the actual class ID. 0x5 is the male Cavalier. Get this from a class list or something, this is pretty easy to find.

The giant string of hex below that is the palette that we copied from FERecolor and auto will just make Pal2EA associate the first palette in this command with that allegiance. The order goes Player, Enemy, NPC, Arena 4, Arena 1.

So you need a slot to insert the palette then you need to define the character, palette number, class and hex for the palette.

Once you've done that, drag Palette Input.txt onto Pal2EA and #include Palette Setup.event in your buildfile.

There's a bit more to Pal2EA, but you can look into the documentation for that.



### Spell Animations

Download [Circles' Spell Animation
Creator](http://feuniverse.us/t/fe6-7-8-circles-spell-animation-creator-updated-to-v1-1/1946?u=circleseverywhere)
and drag your script onto `CSA_Creator.exe`. Then `#include` your created event
file at the end of the Master Spell Animation Installer, and `#include` THAT in
your buildfile.


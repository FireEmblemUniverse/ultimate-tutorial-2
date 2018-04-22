## Inserting Animations

We're going to take out our handy Animation Assembler.exe. All we do is drag and drop
our FEdidor-formatted animations onto the exe, and a .event file should pop out.
Within the .event file, there will be a slot near the top to define which animation
slot you are using for this animation. Now go ahead and #include it!

Also, I suggest using {} with any outputted files. Labels within the .event file are
dependant on the file names of the frames, and many frames from different animations
have the same name.

Next, in a new file...

```
#define SwordAnim(Animation) "BYTE Swords 0x01 ; SHORT Animation"
#define SpearAnim(Animation) "BYTE Spears 0x01 ; SHORT Animation"
#define AxeAnim(Animation) "BYTE Axes 0x01 ; SHORT Animation"
#define HandAxeAnim(Animation) "BYTE HandAxe 0x00 ; SHORT Animation ; BYTE Tomahawk 0x00 ; SHORT Animation"
#define BowAnim(Animation) "BYTE Bows 0x01 ; SHORT Animation"
#define StaffAnim(Animation) "BYTE Staves 0x01 ; SHORT Animation"
#define AnimaAnim(Animation) "BYTE Anima 0x01 ; SHORT Animation"
#define LightAnim(Animation) "BYTE Light 0x01 ; SHORT Animation"
#define DarkAnim(Animation) "BYTE Dark 0x01 ; SHORT Animation"
#define UnarmedAnim(Animation) "BYTE Item 0x01 ; SHORT Animation"
#define SpecialAnim(Animation,Weapon) "BYTE Weapon 0x00 ; SHORT Animation"

```
So now we need to tell the game which animation to use for each weapon type.
For each class, in this new file, you want to set up something like the following:
```
MarshalAnim:
SwordAnim(MarshalSword)
SpearAnim(MarshalSpear)
AxeAnim(MarshalAxe)
HandAxeAnm(MarshalHandAxe)
UnarmedAnim(MarshalUnarmed)
WORD 0x0	// Seperator
```
I suggest putting all of these for each class in the same file.

Note that you need to specify the hand axe animation!
If you want to do a special animation, kind of like Hector with Armads, Eliwood
with Durandal, or Lyn with Sol Katti, you would add to the list something like...
```
SpecialAnim(MarshalSpecial,UberSpear)
```
Finally, we go into our class editor csv and put MarshalAnim|IsPointer into the
Battle Animation Pointer slot, and you should be good to go!

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
We're going to use [CSA_Creator.exe](http://feuniverse.us/t/fe6-7-8-circles-spell-animation-creator-updated-to-v1-1/1946?u=circleseverywhere) for this one. Drag and drop your FEditor-formatted
spell onto the .exe, and a .event file will be outputted. In the .event file,
specify the slot you're inserting the spell into. #include that file in the master
spell installer, then #include that in your buildfile.

Next we need to use the Spell Association Editor.
Find the item that you're replacing in the item slot. If you're adding a new
item slot to the Item Editor, just make a new slot to the end of the Spell Association
Editor. In the row with your item, specify the animation slot, and the flash color
on the map for when animations are off. All the other slots are straight-forward.

No need to mess with the Item Editor on this one. Yay.



## Engine Hacks

### Inserting ASM hacks

In this section we'll go over how one can insert assembly hacks using EA Buildfiles.

You're going to need the ASM beginner pack (where is it?). Included is `AssembleARM.bat` and (a very small subset of) DevkitARM (a common development kit for the GBA).

Assuming your `.asm` file works properly, all you should have to do is drag and drop
your file onto `AssembleARM.bat`, and it should output a `.dmp` file containing your assembled asm. All you need to do is to insert it: `ALIGN 4` (for good measure) and `#incbin` it, and you should be good to go. You're also going to want to put a label to be able to locate your routine(s) from other parts of your buildfile.

If this is something you `ASMC` (call through events), don't forget to add `1` to your routine pointer/label. That way, the game knows it's reffering to *Thumb* ASM.

Otherwise, you're probably going to want a hook. Check out `Hack Installation.txt` for different ways to hook your ASM. If your hook involves a `BL`, you need to insert your ASM within "`bl` range" (for example, in FE8U, in the free space range starting at 0x1C2270).

### Introduction to Assembly

[Try out this neat new tutorial by Tequila](http://feuniverse.us/t/gbafe-assembly-for-dummies-by-dummies/3563)!

### Using the Debugger

(this is also covered by Tequila's tutorial)


## Engine Hacks

### Inserting ASM hacks

You're going to need the ASM beginner pack. Included is ASSEMBLEARM.bat and DevkitPro.
Assuming your .asm file works properly, all you should have to do is drag and drop
it onto ASSEMBLEARM.bat, and it should output a .dmp file. ALIGN 4 and #incbin it,
and you should be good to go. You're also going to want to use a label to call it.

If this is something you ASMC, don't forget to add 0x01 to the pointer. That's
how the game knows it's reading THUMB.

Otherwise, you're probably going to want a hook.
Check out Hack Installation.txt for different ways to hook your ASM.
If your hook involves a BL, you need to ORG your ASM into BL range, the free space
range starting 0x1C2270.

### Introduction to Assembly
[Try out this neat new tutorial by Tequila](http://feuniverse.us/t/gbafe-assembly-for-dummies-by-dummies/3563)

### Using the Debugger


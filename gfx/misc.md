
## Inserting Misc Graphics

MASSIVE TODO

### Ripping images with GBAGE
### Chapter Name Graphics
FE8 uses graphics as chapter names, unlike FE7 which uses text.
Luckily for you, [there's a hack for that](http://feuniverse.us/t/fe8-chapter-titles-as-text/2065?u=circleseverywhere).
### Map Sprites
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


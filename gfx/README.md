
## Graphics

When a **graphic** is inserted in the GBA, it is broken up into 8x8 pixel
blocks called **tiles**. These tiles work together with **palettes** and
**TSA** in order to be displayed properly. Additionally, graphics come in two
main varieties, **sprites**, which are also called **objects**, and
**background** images. The differences between the two will be covered later
on. Finally, **graphics** can be **compressed** (such as the frames of a battle
animation) or **uncompressed** (item and weapon icons).

**Graphics** are, essentially, large grids, whereas each cell in the grid is a
pixel. Each pixel is given a number to represent which colour in the
**palette** it uses. Sometimes, **graphics** appear on screen just as the tiles
are laid out in the original image. Other times they make use of **TSA**.
**TSA** functions like a map that tells the GBA which **tile** goes where. 

**Palettes** are sets of halfwords (two bytes per colour) that denote the
colour of a pixel. Most, if not all **palettes** encountered will have 16
colours in them, taking up 32 (0x20) bytes of space. The first colour in a
**palette** is usually used as a transparent colour, meaning that pixels using
that colour are not displayed. 

Finally, some **tiles** in the graphic might be the same, or different images
might be made from a single set of **tiles**. To save space in the ROM, only
one copy of the tile will be saved. Therefore, we need something called **TSA**
that allows the game to put the tiles back together in the correct order,
similar to assembling a puzzle. Multiple sets of **TSA** allow for a variety of
images to be stitched together.

### Sprites & Backgrounds

The GBA has two ways to display graphics, as mentioned previously. They are
**Background** images and **Sprites**. Both have limitations and uses, so
understanding the difference is vital for any kind of graphical work. Larger
images are almost guaranteed to be **background** images. Dynamic images, like
map sprites or battle animation frames, are **sprites**.

#### Background Images

There are 4 **background layers**  (or **BG layers**) that the GBA has to work
with. Naturally, these are labeled **BG0**-**BG3**. Each one has different
abilities and uses.

![prologue screen](http://puu.sh/rGX81/7903256b06.png "What you see") 

Here's a screenshot from FE8's prologue. What you see is a combination of
**background layers** and **sprites**, but let's worry about the **background
layers** for now. The layers are stacked on top of each other to form a
cohesive screen. We call the order in which the **BG layers** are placed the
**priority** of the layer. A higher **priority** means that it will be covered
by things with a lower **priority**. Let's take a look at the **BG layers** you
see here.  ![BG layers](http://puu.sh/rGXRG/6bdf9eb8c1.png "0, 1, 3")

You might be thinking to yourself, *"Wait! You're missing a layer! There are
three here, not four,"* and you're right. These are, in order, **BG0**,
**BG1**, and **BG3**. I didn't include **BG2** because it was blank.  Here, the
**BG layers** are layered with **BG0** on top, followed by **BG1**, and then
**BG3**.

**Background layers** are built using three parts: **tilesets**, **TSA**, and
**BG palettes**. Both the **tileset** and **TSA** are written to the
`0x06000000` (**Video RAM** or **VRAM**) section of memory. Specifically,
**tilesets** are written to `0x06000000-0x06006000` and
`0x06008000-0x06010000`. **TSA** is written to `0x06006000-0x06008000`. In the
GBA Fire Emblem games, the `0x06008000-0x06010000` segment is usually reserved
for the game's map tilesets or scrolling menu backgrounds, while
  `0x06000000-0x06006000` is used for general images. 

**BG Palettes** are written to the `0x05000000` (**Palette RAM** or **PalRAM**)
section of memory. More info on them in the next section.

**BG images** can be large and are not suited for moving quickly, although
their individual tiles can be edited easily. There are settings for rotation,
alpha blending, scrolling, and other settings, but they are better left to be
covered by the links in the next paragraph. Menus, windows, cutscene
backgrounds, and many other images are all **BG images**.

Documents such as [Tonc](http://www.coranac.com/tonc/text/toc.htm) or
[GBATek](http://problemkaputt.de/gbatek.htm) are a fantastic resource for
understanding how to use and manipulate **BG layers** and **BG images**. Both
also refer to both **sprites** and **BG layers** differently. For the purposes
of this tutorial, terms you may have heard before, or may hear later, have been
used, such as **TSA**.

#### Sprites

**Sprites** have nearly the opposite characteristics: they're mobile, usually
small, and lack **TSA**. **Sprites**, or **objects**, are written to
`0x06010000-0x06018000` (**OVRAM** or **ObjRAM**). **Objects** are also
referred to as **OAM**, which stands for **Object Attribute Memory**, although
**OAM** is more correctly defined as the section of memory that control data
for **objects** is written. This section of memory is `0x07000000-0x07000400`.

**Sprites**, like **backgrounds**, can have effects applied to them, such as
alpha blending or rotation, but these are too advanced to cover in this basic
guide. If you'd like to learn more, give this section of
[Tonc](http://www.coranac.com/tonc/text/regobj.htm "Tonc") a read. 

Individually, **Sprites** are small, generally restrained to rectangles that
are 8x8 pixels to 64x64 pixels in size. Like **background images**, however,
you can have many sprites seem connected. One major difference between
**sprites** and **background images** is that **sprites** are not confined to a
tile grid.  

>####The positions of sprites are in pixels, not tiles!

This allows **sprites** to do complex things much more easily than **background
images**.

The control data, or **attributes**, of **sprites** control all of the features
of the **sprite**. There are four **attributes**, aptly named **attr0-3**. Each
**attribute** is a **halfword**, or two **bytes**. For a detailed breakdown of
**attributes**, see **Tonc**.


### Palettes

***Battle Sprite Palettes***
**Do FE7/FE6 version \*soon\*** (remind me to do the FE7/FE6 instructions
later) ~ Tera ***FOR FE8***
There is a nightmare module for setting the palettes in FE8 called the battle
palette association editor.  it comes in two parts; the first part is for
setting the class and the second part is for choosing the palette.  If the
character is not in a class listed in their class list, the game uses the
default palette.  ![Battle Palettes
Window](http://feuniverse.us/uploads/default/original/2X/5/58ea14b5a8feaf581fb85d6166ee103fbce64073.png)
In FE7 it was 2 palettes per character, but in FE8 its 1 palette per class and
7 classes per character. Basically, you go to the character's slot andset one
of the seven class slots to the desired class, and then go to the other part
and set the palette (trainee palette is used by the trainee class and etc.)

### TSA or Tile Maps

Nintenlord's compressor and/or grit

### Compression

Link to wiki article on LZ77


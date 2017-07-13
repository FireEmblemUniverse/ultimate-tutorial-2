
## Nightmare Modules

You may have heard of a program called **Nightmare**, which can be used to make
changes to things like character stats, item properties, and so on. Fortunately
for you, **you won't need to worry about it!** You do need to download the
appropriate set of **Nightmare Modules** for your game, but you won't need
the actual Nightmare program.

### [How Tables Work](#how-tables-work)

Nightmare modules essentially describe **data tables** in the ROM. They say
**where** the table is, how many **columns**, how many **rows**, and so on.
Using this information, we are able to understand what each bit of data in the
table **represents** and change it accordingly.

### [Using NMM2CSV](#using-nmm2csv)

When you download **NMM2CSV** you'll see that it is in fact made up of two
programs: N2C.exe and C2EA.exe.

#### N2C.exe

This program creates **.csv spreadsheets** from a ROM using Nightmare Modules
as a template. Essentially you simply place N2C.exe in the **same folder** as
your Nightmare Modules, and then **drag and drop** the rom you want to rip from
onto it.

#### C2EA.exe

This program **converts the spreadsheets** you got in the previous step into
Event Assembler compatible format, and also **generates an installer** so that
you can `#include` all of your spreadsheets in one go.

So the way to make changes is to first create your CSV spreadsheets using
N2C.exe. **You should only have to do this once!** Once you have the
spreadsheets, you can edit them using Microsoft Excel, LibreOffice, Google
Sheets... any spreadsheet program will do.

> ##### **Put your Nightmare Modules, N2C and C2EA into a new folder called Root\Tables.**

Next, you make the changes you want. In this example, I am going to give Eirika
a base Strength of 10. First, I open up `FE8 Character Editor.csv`:

![Table screenshot](http://puu.sh/rIHg9/3e88b7e1f3.png)

As you can see, each character is a **row** of the table, and each row is split
into **columns** for the properties we can edit. We are editing Eirika's Base
Strength, so we click that cell and type 10.

![Table screenshot](http://puu.sh/rIHmG/35ac32eaf0.png)

Then **save**, and run C2EA.exe. You don't need to drag or drop anything, just
run the program and it will process your Nightmare Modules and create a file
called `Table Installer.txt`. Add this file to your **ROM Buildfile** and the
next time you run `MAKE HACK.CMD`, the changes will be saved!

> #### **You *MUST* run C2EA again every time you make changes to the modules.**

> You can add C2EA into your MAKEHACK.cmd batch file using `cd "%~dp0Tables"` (or whatever subfolder c2ea is in) `c2ea "%~dp0FE8_clean.gba"` (the path to the clean rom is only needed if you are repointing a table)

### [Using Definitions](#using-definitions)

NMM2CSV comes with a file called `Table Definitions.txt`. This comes with a few
useful definitions like weapon and character abilities. You can also add your
own, depending on what you're doing.

The best part of this is that you can actually **use definitions** in your
spreadsheets! For example, let's take Eirika's Rapier and make it an
**indestructible, brave weapon**. Just for the sake of learning, of course.

This time, we open up `FE8 Item Editor.csv`.

![Table Screenshot](http://puu.sh/rIHGt/0e233961a2.png)

We find the row with Rapier, and find the `Weapon Ability 1` column. In this
case, we need to expand out the column width so that the full name is visible.
Then we click on the **cell** we need to edit, and enter the abilities we want
to have, added together. (You can also use `|`(bitwise OR) instead of `+`.)

> **Tip:** Use **View\>Freeze Panes** to keep the first row or column visible at
> all times. This is very helpful when you edit larger tables.

![Table Screenshot](http://puu.sh/rIHSm/4bb86393dd.png)

Once again, we can **save and run C2EA,** and the changes will be inserted the
next time we assemble.

### [Repointing and Expanding (\#inctext)](#repointing-and-expanding-inctext)

You can expand a table simply by adding some rows to the bottom. You can put
`INLINE LabelName` in the first cell to have the table inserted into free space
and labeled `LabelName`. Event Assembler comes with a tool called `PFinder.exe`
which can be used to find and replace pointers in the ROM.

When you run C2EA with a table that needs repointing, you can either drag a
clean rom onto the exe OR select the clean rom when prompted.

>Alternatively, you can add C2EA into your MAKEHACK.cmd and provide the clean
>rom as an argument like this: `cd "%~dp0Tables` (the folder where C2EA.exe is
>stored) `c2ea "%~dp0FE8_clean.gba` (the location of the clean rom)


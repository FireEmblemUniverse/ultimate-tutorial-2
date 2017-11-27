## Editing Text

Each piece of text in GBAFE is tied to a **text ID** up to
0xFFFF. This text contains a number of **control codes** that determine extra
data such as loading and moving faces. 

> ###Important:
> Text editing requires the ***Anti-Huffman Patch*** to be
> installed. This is included with the **FE8 Essential Fixes**, or as part of
> the **FEditor Autopatches for EA** if you are using FE7.

### Formatting Text Text is converted into binary data using a **text parser**.
We will be using the parser included with **Event Assembler**, but we will make
the process much simpler by using **textprocess.exe** to do all the hard work
for us.

Here is a very simple example of a text file called `UnitNames.txt`:

    # 0x212 RubyName
    Ruby[X]

There are three parts to each text entry. First, `# 0x212` is a **text ID**. It
happens to be the text ID that refers to Eirika's name.

The second part is an optional **definition**. In other words, when I need to
refer to this text ID later on, I can use `RubyName` and Event Assembler will
understand that to mean this text ID. If you leave out the definition, you can
still refer to it by the number `0x212`.

The final part is the actual text. You can see that we are changing Eirika's
name to Ruby. Finally we end the text with the control code `[X]`. This is a
special code that tells the game where the text stops.

Now, let's look at something a little more complicated.

    # 0x903
    [OpenFarLeft][LoadFace][0x02][0x01]
    Hello, how are you?[A]
    As for me, I'm talking[NL]
    words at you![A][X]

> #### The positions from left (flip for the right side):
> `[FarFarLeft]`\(offscreen) > `[FarLeft]` > `[Midleft]` > `[Left]`

`[LoadFace][0x02][0x01]` is used to load up portrait number 0x02. If you have
more than 0xFF portraits, the **higher digit carries over** to the [0x01], e.g.
portrait 0x17F would be `[LoadFace][0x7F][0x02]`. You only need `[LoadFace]` if
a portrait is actually being **loaded**. Otherwise, you can simply use
[Open(position)] to make the face at that position **active**.

### Inserting Text

Textprocess.exe works by dragging a text file onto the exe. It then converts
this text file for EA insertion and generates an **installer file** that you
can `#include` in your buildfile.

This textfile contains **all of the text changes** you want to make. For
example, we can take the two previous text changes and put them in a single
document, which I've called `text_buildfile.txt`.

    # 0x212 RubyName
    Ruby[X]
    
    # 0x903
    [OpenFarLeft][LoadFace][0x02][0x01]
    Hello, how are you?[A]
    As for me, I'm talking[NL] 
    words at you![A][X]
    
>####But wait, why is it called a **buildfile**?

You guessed it, you can `#include` other text files! Let's take a look at one
of the text buildfiles I used for a simple one chapter hack:

    #include "DQText.txt"
    
    #include "PrologueText.txt"

    #include "MiscText.txt"

You'll notice there aren't any actual text entries here, those are all split
into separate text files for organization. Peeking at PrologueText.txt, we can
see things like:

```
#0x664 BrownBoxPrologue
1 year ago[X]

#0x665 BrownBoxPrologue2
Present day[X]

# 0x1a2 Prologue_Objective_Long
Survive[X]

#0x19d Prologue_Goal_Window
Survive[X]
```

Now you may have noticed something else this has in common with an event
buildfile - whenever we process the text, it's **always the same file**.

Know what that means? **We can add it to MAKEHACK.cmd!**

Here's an example from my own:

```
cd %~dp0
copy FE8_clean.gba FE_Hack.gba

cd "%~dp0Tables"
c2ea "%~dp0FE8_clean.gba"

cd "%~dp0Text"
textprocess_v2 text_buildfile.txt

cd "%~dp0Event Assembler"
Core A FE8 "-output:%~dp0FE_Hack.gba" "-input:%~dp0ROM Buildfile.event"

pause
```

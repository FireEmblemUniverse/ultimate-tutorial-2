
## Buildfile Basics

### Baby's First Buildfile

Open up `ROM Buildfile.txt` and paste:

    #include eastdlib.event ORG 0x1000000

*Wow, what a great buildfile!* What does it do? Let's find out with an
**example**!

### Hello, World!

Create a **new text file** and type:

    String(Hello World!)
  
Now **save** that in Root as `Hello World.txt`. Go back to your `ROM
Buildfile.txt` and add this to the bottom:

    #include "Hello World.txt"

Now it's time to **assemble**. **Save** `ROM Buildfile.txt`, take your clean
ROM and **make a copy** of it. We'll edit this copy so that we always have a
clean ROM available in case something goes wrong.

![Event Assembler Window](http://puu.sh/ryp0V/59e19685bf.png)

In the **Text** field, select `ROM Buildfile.txt`. Set the **ROM** as the copy
you made earlier. Make sure Game matches the one you're working on. When that's
done, click **Assemble**!

You will see a friendly message:
>"No errors or warnings. Please continue being awesome."

Perfect. But what did it actually do? Open up the ROM in **HxD**, press
*Ctrl-G* and type `1000000` as the offset, ensuring that the `hex` option is
selected.

![Hex Editor View](http://puu.sh/ryUig/6763a68df3.png)

You should see a bunch of numbers, but on the right side you can see that they
translate to `Hello World!` **Congratulations, you inserted some data!**

But this is just the beginning of what buildfiles can do...

### Understanding \#include

What does `#include "some/file.txt"` do? Basically, it inserts the entire
contents of `some/file.txt` in place.

So in our ROM Buildfile, the line `#include "Hello World.txt"` becomes
`String(Hello World!)`

>#### **The file you #include can #include other files!**

### PUSH and POP

Let's take a step back and look at our `ROM Buildfile` again. What does `ORG
0x1000000` mean? **ORG** stands for **Origin** meaning the starting offset of
our data. In the previous example, we saw that our data was inserted to the
offset 0x1000000.

Imagine it as a **cursor** that tells Event Assembler where to insert at.
**ORG** lets you move the cursor to a specific position, where you can start
"typing", i.e. **inserting data**.

>**If we don't put an ORG at all**, Event Assembler just starts at offset 0, or
>the very beginning of the ROM. ***This breaks the ROM horribly!***

What happens if we `#include "Hello World.txt"` **twice**?

    #include eastdlib.event
    ORG 0x1000000
    #include "Hello World.txt"
    #include "Hello World.txt"
    
If you assemble this buildfile, you will see `Hello World!` twice at the end of
the data. The "cursor" doesn't stay where you put the ORG, it moves forward as
you insert data. After the first Hello World is inserted, the cursor is now at
the end of that data, ready to add the second Hello World.

Now, let's try something new. Make a new text file containing

    ORG 0x1000050
    String(Hellow Orld!)
    
and save it as `Hellow Orld.txt`. Now `#include` this in your buildfile
**between** the two `"Hello World.txt"` lines.

    #include eastdlib.event
    ORG 0x1000000
    #include "Hello World.txt"
    #include "Hellow Orld.txt"
    #include "Hello World.txt"

>#### We'll want to start fresh for this, so **delete** the ROM you've been
>assembling to and **make another copy** of the clean ROM.

Now assemble the buildfile again, and take a look in HxD.  As expected, you
have `Hello World!` at 0x1000000, and `Hellow Orld!HelloWorld!` at 0x1000050.
But what if we wanted the two Hello Worlds together?

**Go back to `Hellow Orld.txt`** and add `PUSH` to the top, and `POP` to the
bottom. **PUSH** creates a "bookmark" that remembers your position, and **POP**
jumps back to the last bookmark you created.

    PUSH
    ORG 0x1000050
    String(Hellow Orld!)
    POP

>#### You can **PUSH** multiple times, and each **POP** will take you to the **newest** bookmark you placed.

Assemble to a fresh ROM and this time, you'll see two `Hello Worlds` together,
and `Hellow Orld` on its own at 0x1000050.

### Definitions, Labels and Macros

It's now time to introduce you to one of the simplest, but  **most powerful** commands in Event Assembler:
`#define`!

    #define FreeSpace 0x1000000
    #include eastdlib.event
    ORG FreeSpace
    #include "Hello World.txt"

Can you figure it out? That's right, `#define` simply **replaces** one thing
with another.

Well, that's certainly **simple**. What's **powerful** about it?

How about this?

    #define FreeSpace 0x1000000
    #define TestMacro(offset) "ORG FreeSpace + offset; String(Hello World!)"
    TestMacro(0x10)
    
This is an example of a **macro**. Like a definition, it expands out into the second half.

    ORG FreeSpace+offset
    String(Hello World!)
    
However, the difference is that you can **set** the value of `offset` when you write the macro!

When you write `TestMacro(0x10)`, you're telling EA that **offset = 0x10**.
This expands out into:

    ORG 0x1000000+0x10 //FreeSpace = 0x1000000, offset = 0x10
    String(Hello World!)
    
However, if you had `TestMacro(0x100)`, it would instead become:

    ORG 0x1000000+0x100
    String(Hello World!)
    
You may have noticed that `TestMacro(offset)` looks **very similar** to something we've seen before. Yep, `String(text)` is **also a macro**!

One final thing. You now know that definitions are like **shortcuts** that you
create with `#define`. There is one more way to create a shortcut: **Labels.**

>#### A **Label** is a shortcut for an offset.

You can create a label like so:

    ORG 0x1000000
    #include "Hello World.txt"
    
    MyLabel:
    #include "Hellow Orld.txt"
    
    MESSAGE Hellow Orld is inserted at MyLabel
    
Assembling this will give you the following output:

> Finished.  
>    Messages:  Hellow Orld is inserted at 0x100000B
>
>    No errors or warnings.  Please continue being awesome.

As you can see, **a Label is an automatically defined offset**. In this case,
it tells you exactly where Hellow Orld begins. We'll be using labels a lot to
track where our data is inserted.

### MAKE HACK.cmd

You may have noticed that every single time we
assemble, we use the **same** text file, the **same** ROM, and the **same**
settings. Wouldn't it be nice if we could **save those settings**?

>#### Enter **MAKE HACK.cmd**!

Create a new text file and paste the following:

    cd %~dp0
    copy "FE8_clean.gba" "FE_Hack.gba"
    cd "%~dp0Event Assembler"
    Core A FE8 "-output:%~dp0FE_Hack.gba" "-input:%~dp0ROM Buildfile.txt"
    pause
    
(replace "FE8\_clean.gba" with your clean ROM, **both** instances of "FE\_Hack.gba" with your edited ROM, FE8 to FE7 if you're hacking that, and "ROM Buildfile.txt" with the name of your buildfile)

Save this as `MAKE HACK.cmd` in Root.

When you open this script, it will first **copy** and rename your clean rom.
Then it will **assemble** the buildfile to the ROM. Finally it will **pause**
when it's done so you can see the output and any error messages.

>#### In other words, **you can now build an entire hack from scratch in one click.**



## Aside: Editing a ROM

If you've done any ROMhacking before, such as in another community or even by
following older FE tutorials, you may be used to the idea that your *Working
ROM* is your entire project. In fact, many of the older tools you may see
people refer to, such as FEditor or Nightmare are designed to modify a ROM
*in-place* -- that is, you change something, hit save, your old ROM is gone
and an edited ROM has taken its place. This is akin to how most real file
editors work (open file, edit, hit save).

This is *not* how our project is going to work.

Those of you who've worked with gigantic projects before may have spotted an
issue with the old process. Namely, *what if I mess up*? This isn't so much of
a concern for, say, word documents, as you can undo, copy-paste, whatever to
restore your older version and fix mistakes. This is not so true for ROM
hacking, where our ROM can be modified by all sorts of tools, often in more
ways than we even realize. Mistakes can go undetected for weeks or even
*months* of work, resulting in one of two scenarios:

1. Restore from backup (assuming we even have one), necessitating those weeks
and months of work be redone onto the fixed ROM

2. Attempt to fix in-place, requiring possibly hours of research and debugging
to even *find* the bug, as well as potentially introducing more errors when a
fix is hacked on.

Needless to say, this is often a painful experience, and can even cause a
project to slow or stop entirely.

Instead, we're going to be rebuilding our project from scratch, every time we
change anything.

#### "Wait, what?"

Yeah, you heard me! *Every time we make a change to the project, we're going to
be remaking the new ROM from the raw base*.

Not by hand, of course.

The key to all of this is that *buildfile* you just made. As the name may
suggest, this buildfile is a *file* that says how to *build* our project. So
if we want to change the project, we just have to change the buildfile! This
means we get to take advantage of easy undo operations, human-readable changes
and even more advanced things like [Version Control](https://github.com/FireEmblemUniverse/CCB_Round1)! Fixing an old mistake is as simple as changing a few lines
in our buildfile (or its `included` files -- we'll get there).

Those of you with programming experience may realize that our buildfile is our
project's *source code*, and Event Assembler is our *compiler*. This way, the
project folder *is* our entire project, *not* the output ROM.


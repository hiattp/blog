---
layout: post
title:  "Power Your Wireless Apple Keyboard With USB"
date:   2014-10-30 12:13:26
categories: hacks apple
meta: "Foil trick not working to fix your dead Apple keyboard? Here's a more intense (but more effective) way to fix it."
---
![Apple Wireless Keyboard]({{ site.url }}/assets/wireless_keyboard.jpg)

I was forcibly sidetracked yesterday when my trusty Apple wireless keyboard suddenly
crapped out. I was trying to change the batteries---don't worry, they are
rechargeable---when a small plastic piece fell out of the battery tube, and
nothing I could do after replacing it would make the keyboard power back on (I'm
guessing I'm not the first to have [this problem][foil-fix]).

Now, I like this keyboard. It maps exactly to the Macbook Pro layout so my
muscle memory isn't thrown off by switching back and forth. And I don't mind
shelling out Apple premiums because their products are worth it, but I hate to
replace what is otherwise a
perfectly good device (*sans* power source). I happened to have a spare USB
charger from some former iPhone, so I decided to see how well the two play
together.

### Step 1: Strip For Me

I've never seen the inside of a USB cable but I know mine puts out about 5V at
1A (which sounds about right for something that normally runs on 3 AA batteries),
so I assumed I'd find the good ole red/black combo in there somewhere.
I was surprised to find three exposed wires instead of the black,
but my guess is that those will do the job.

![Exposed USB Cable]({{ site.url }}/assets/usb_cable.jpg)

### Step 2: Pull Out

If you pop open the back of the keyboard near the power button you'll see the brain
that runs this show. It is connected in four ways:

1. The important-looking blue tape with lots of connection points
2. The power plug on the top with wires that head back to the batteries (unhook that from
   the board)
3. The power control with wires that head to the power button
4. A small screw near the power button

There was also a piece of plastic near the power button that you need to hold
back while you carefully pull the brain up and out of the keyboard after
disconnecting everything.

![The Brain]({{ site.url }}/assets/circuit_board.jpg)

### Step 3: Can't Stop, Won't Stop.

Now you cut the original power wires, since you'll want to reuse the bit that
plugs into the brain. Then you just attach that to the USB cable.

![Joining the Wires]({{ site.url }}/assets/joined_wires.jpg)

### Step 4: Finishing Touches

Now we just need to tidy up, plug it in and put it back.

![Plug It In]({{ site.url }}/assets/plug_in.jpg)

I didn't have solder handy, so I just wrapped things up with tape.

![Wrap Up]({{ site.url }}/assets/wrap_up.jpg)

I cut the end off of the brain's cover to make it compatible with the new
design.

![Put It Back]({{ site.url }}/assets/put_in.jpg)

I thought the Apple UX team might frown on exposed wires (nothing extra tape won't fix).

![Tape It Up]({{ site.url }}/assets/tape_over.jpg)

### Step 5: Turn Me On

The moment of truth, fire it up! It turns out that powering the keyboard is
easy, but getting the "important-looking blue tape" from Step 2 back into place is a
challenge (so you might have power but no functionality without finessing that
connection).

![Turn It On]({{ site.url }}/assets/turn_on.jpg)

### Step 6: Happy Ending

At this point you'll either have a newly functional keyboard or a wasted hour
and some extra mac replacement keys. There's no second place in hacking.

![Happy Ending]({{ site.url }}/assets/happy_ending.jpg)


[foil-fix]:     http://griffintechnology.com/blog/tips-and-tricks/how-to-revive-a-dead-apple-wireless-keyboard-using-a-gum-wrapper/

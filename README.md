# 4-Digit Combination Cryptex

This is a pull-apart combination cryptex, basically a tube that only comes apart if you dial the right 4-digit code. Not a shackle padlock, the kind where the whole middle section slides out once it's unlocked. I built it as a portfolio piece for grad school, and the point for me wasn't just making something that looks like a lock, it was actually understanding how the mechanism works well enough to build and explain it myself.

## The idea

I didn't want to just copy a shape off Makerworld and call it done. I started out looking at padlocks, then switched to this pull-apart cryptex style once I found a reference I actually liked.

I'd tried to build a combination lock once before, a totally different shaft-and-wheel design, and it taught me something the hard way: a lock can look completely right and still be broken, because a piece that's supposed to move ends up fused to a piece that's supposed to stay still. Mine locked up so badly it couldn't open OR close. That stuck with me, so this time around I made a point of checking every version in software before printing anything, specifically hunting for that exact kind of mistake.

## How it works

There are four wheels, each with one notch cut into it, and the notch's position is what sets that wheel's digit. They sit on the outside of a fixed center shell, which has a straight slot cut down it. The vault part (where your stuff actually goes) has a small pin near the top that rides in that slot. When you pull the vault, the pin travels up through all four wheels. It only makes it through a wheel if that wheel's notch happens to line up with the pin. Get even one digit wrong and the pin just slams into solid plastic and the vault won't budge.

No springs anywhere, nothing to wear out. And the wheels stay on the outside the whole time, so you can always reach and turn them, whether it's open or closed.

## First try, didn't work

The first version I built had the wheels mounted on a shaft attached to the lid, so they'd drop down inside the storage tube when you closed it. Every check I ran on it passed, and the actual lock logic was solid. But I missed something obvious until after I'd already printed it: once it was closed, the wheels were buried inside the tube, so there was no way to dial it without yanking it half open first. The logic was right, the design around it wasn't. Passing all my checks only told me the parts weren't colliding, not that the thing made any sense to use.

The version in this repo fixes that. The wheels now live permanently on the outside of the fixed shell, which is how a real cryptex is supposed to work. Same pin-and-notch logic as before, just actually usable.

## Checking it before printing

The whole thing is modeled in Fusion 360, fully parametric with user parameters, so changing one number updates everything downstream instead of redrawing anything. Before I export anything to print, I check the geometry directly in the assembly: interference detection between the pin and each wheel, plus a motion study that drags the vault through its full travel, stuff like "does a correctly dialed wheel let the pin through with zero overlap," "does a wrong digit actually jam solid," and "if three wheels are right and one's wrong, does it still block" so there's no partial credit.

That process caught real mistakes before I ever got near a printer, including one that was basically the same failure as my first-ever lock: at one point the pin's resting spot was sitting in a part of the shell wall that didn't have the slot cut through it, which means it physically couldn't have closed. Good thing I caught that on screen instead of finding out with a print in my hand.

Right now everything passes every check I've thrown at it. I kept a running checklist of them in the design history, so if I change a dimension later I can walk back through it instead of trusting my own eyeballing of the drawing.

## What didn't work: changing the combo yourself

Right now you can't change the combination after it's printed. It's set by which wheel you print for each slot (each wheel's notch position is just a parameter on that body, so I set the four digits, say 4, 2, 0, 6, and regenerate those four wheels to get new ones). That's a real limitation. An actual resettable combination lock usually uses a separate set of pins you can move to reprogram each wheel without printing new parts.

I wanted that and tried to build it myself. Got stuck and eventually set it aside. If I'm honest, I think the reason is I jumped into modeling it before I'd actually worked out how the reset pins would lock back into place once you'd set them, without recreating the same "the part that's supposed to move is stuck to the part that's supposed to stay still" problem I built this whole thing to avoid in the first place. It's a genuinely harder problem than the fixed-combo version, so I'm just saying so instead of acting like it's done.

If I come back to this, the idea is a second set of pins, one per wheel, that you push in or out to pick which digit each wheel's permanent notch lines up with, then lock in place with a collar you twist afterward. That's the part I need to actually think through before touching CAD again, not while I'm in the middle of modeling it.

A couple other directions I keep coming back to, none of them worked out yet: instead of loose pins, each wheel could get its own small set screw that rides in a shallow keyway, so tightening it locks that wheel's offset without anything floating free to fuse itself in place later. Or skip the collar entirely and use a detent ring, little bumps on the inside of the wheel that click into one of several fixed stops, which is closer to how a real bike lock resets its code. The set-screw version feels the most buildable to me since it's one less moving part to get wrong, but I haven't modeled either one far enough to know if it actually avoids the stuck-together problem or just moves it somewhere else.

## Files

`cryptex.stl` is the Fusion 360 model, with all the dimensions as user parameters, so changing one updates everything downstream. It's also where the interference checks and the motion study live, and it's what the exports below come from. `print_ready/` is what you slice: the shell, the vault, the 4 wheels, and the retaining collar, exported straight from that model. `assembled_view/closed/` and `assembled_view/open/` are the same parts pre-positioned so you can see how it all fits together without building anything.

## Printing

PETG over PLA, it holds up better at the layer lines. Thick walls and a solid amount of infill on the shell and vault. Print the shell and vault standing up on their long axis. Wheels print flat, bore facing up.

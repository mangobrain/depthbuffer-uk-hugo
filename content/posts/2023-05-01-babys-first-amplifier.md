---
title: "Baby's First Eurorack Amplifier"
date: 2023-05-01T12:46:20+01:00
icon: article
draft: true
images: ['/post-thumbnails/diy-amp.jpg']
tags:
- memento potato
- electronics
toc: true
---
For a long time, I thought electronics wasn't for me: it was this arcane mixture
of black magick and hardcore mathematics, in which everything has to be designed
and assembled _perfectly_ or _nothing will work_. Well, it turns out that's not
entirely true. It may be true if you're building life-saving medical devices, or
circuit boards for digital devices with high-speed signalling (like a PC or
smartphone motherboard) where
[the actual physical length of connections matters](https://resources.altium.com/p/all-about-your-pcb-trace-length-how-long-too-long),
but not in the only kind of electronics that actually matters: DIY analogue
audio gear.

Open that article, marvel at the squiggly lines in the picture, scroll until you
start seeing equations, then close it again.

We won't be doing that here. Where we're going, we don't need analysis. This is
cargo cult electronics. And that's OK. Because I reckon as long as you learn a
few basic building blocks, and have an intuitive understanding of how they work,
and the confidence & curiosity to try out different combinations, you can get
pretty far. Just [don't start thinking you're an expert](https://en.wikipedia.org/wiki/Dunning%E2%80%93Kruger_effect).

## One Problem, Four Components

To illustrate my point, let's take a simple problem, four components arranged
into two basic building blocks, and make a working, useful circuit.
* __Problem__
  * Plugging the audio out from a normal line out socket straight into
    my modular synth gives me really, really quiet sound
* __Components__
  * Resistors
  * Capacitors
  * Diodes
  * Op-amps
* __Building blocks__
  * Eurorack power interface
  * Non-inverting amplifier

Sure, there are a few other bits, like pin headers & jack sockets, but those are
just fancy-looking wires: they have a specific shape, designed to let you plug
in specific things (ribbon cables, patch cables, etc.), but electrically, all
they do is make connections between bits of metal. If you really wanted to, you
could make a pair of headphones that required you to solder three wires every
time you wanted to plug them in.

### Electricity; an Illustrated Glossary

TODO move to bottom, or separate article?

This is basic stuff. You probably already know it, but maybe not, and in any
case a refresher can't hurt.

* __V__ is for volts. Always capital V, after [Alessandro Volta](https://en.wikipedia.org/wiki/Alessandro_Volta). A measure of
  electric _potential energy_: it only really has meaning when comparing two
  things, and it has to have somewhere to go for that energy to do useful work.
  * Atoms in materials have a default stable state, in which they typically have
    the same number of electrons and protons. A material is _negatively charged_
    if it has more electrons than normal; those electrons won't be bound to any
    specific atom, and can move around. Conversely, it's _positively charged_ if
    it has fewer electrons than normal: the protons in atoms with a deficit will
    attract unbound electrons.
    TODO Pictures
  * We can put a number on how much negative energy we transfer to a balloon by
    rubbing it on a jumper (giving it extra electrons), but it isn't
    particularly useful to try and count how many electrons the balloon or
    jumper have in their uncharged, resting states. (Nobody designs circuits
    with _one specific battery_ in mind, knowing how much charge that battery
    contains; they design them to work with _any_ battery that, when fully
    charged, has a 9V potential difference between its terminals. Also, imagine
    trying to answer how many electrons there are in a socket connected to the
    mains.)
  * After being charged, the balloon will happily sit there doing balloon stuff,
    until you bring it near something with less charge, like someone's hair or
    a fingertip.
    TODO: Friction, electrons, zap picture
  * If it's always relative, how can we have a "9V battery"? 9 volts compared
    to what? Well, batteries always have two terminals, so a rating like this
    tells you there's a 9V difference in charge between the positive and
    negative terminal.
* __A__ is for amps. Again, always capital A, after [André-Marie Ampère](https://en.wikipedia.org/wiki/Andr%C3%A9-Marie_Amp%C3%A8re). A
  measure of current, or the _rate at which charge is moving_.
  * That balloon we rubbed? As long as it isn't touching anything, no charge
    is moving, so current is 0A. Then you poke it and get shocked: current
    went above 0A briefly - specifically, for as long as it took for the
    voltage between the balloon and your finger (their _potential difference_)
    to drop back to 0V.
* __Ground__ is a circuit's chosen reference point for zero volts.
  * Because voltage is always measured between two things, there is also no
    fixed concept of 0V. But in a circuit with a power supply, if you know
    the maximum voltage you can generate between your supply terminals, it
    makes sense to define 0V as the half way point, and measure relative to
    that.
  * When making toy circuits like blinking LEDs, it's common to use two 9V
    batteries connected end to end: the positive end of one is the +9V supply,
    the negative end of the other is the -9V supply, and the point in the
    middle where they touch is ground.
    TODO Draw this.
  * So called because the Earth itself, the literal ground, is a pretty
    convenient, near-infinite zero volts reference point: you can pump electrons
    into it or draw electrons out of it at will without filling it up or running
    out.
    * This is not "free energy"; for that charge to do work, it needs some
      impetus to move. Think of a hydroelectric dam: lakes don't just magically
      radiate free electricity, but allow a raised body of water to fall under
      gravity, and you can use that motion to drive a turbine. You can't pull
      electrons from the ground at will, you need something charged to hook it
      up to.
  * Also a verb: to "ground" something means to return it to its uncharged
    state, removing excess electrons (negative charge) or resupplying an
    electron deficit (positive charge) to its atoms such that they return to
    their normal, default state.
* __Ω__ is for _ohms_, after [Georg Ohm](https://en.wikipedia.org/wiki/Georg_Ohm). A measure of _resistance_, i.e.
  the degree to which a material _impedes_ the flow of charge through it. The
  higher it is, the harder electrons find it to travel, reducing current.
  * Often written out, or omitted entirely, in favour of just using [SI prefixes](https://en.wikipedia.org/wiki/Metric_prefix) as a kind of shorthand:
    a "10k resistor" means 10 kilo-ohms, or 10000 ohms.
    TODO Resistor
* A __short circuit__ or __short__. Elecricity will travel the path of least
  resistance. If you take a circuit where the only path between the terminals of
  the power supply goes through a bunch of components, it'll flow through those
  components; if you accidentally touch a wire directly from one part of the
  circuit to another that bypasses a bunch of components - giving the electrons
  a _shortcut_, if you will - those components won't get power.
  * Also a verb: to _short_ something is to temporarily create a low resistance
    path between two points; for example, making a high-voltage capacitor safe
    to handle by _shorting it to ground_, discharging it.
  TODO: LED lights up, LED doesn't light up
* The __±__ symbol means "plus or minus". A ±5V signal means charge is flowing
  backwards and forwards, maxing out at 5 volts above ground in one diretion,
  5 volts below it in the other.
* __Vpp__ means _voltage peak-to-peak_. A ±5V signal could also be referred to
  aso 10Vpp, because there is a difference of 10 volts between the highest and
  lowest points.
  TODO: +/-5V = 10Vpp, 0..10V = 10Vpp

## To the Google Machine!

I'm going to assume a certain amount of knowledge about what a modular synth
is, but try to make the fewest assumptions possible about electronics
knowledge. Let's pull some magic numbers off the Interwebs, and worry about
explaining them later (if at all) - because that's how I'm figuring this stuff
out, and my whole point here is that you can do the same.

### Why is the audio quiet in the first place?
Well, it turns out that Eurorack
uses audio signals anywhere between [±5V](https://modwiggler.com/forum/viewtopic.php?t=96737)
and [±10V](https://www.reddit.com/r/synthdiy/comments/8iex2l/eurorack_voltage_standards/),
depending on who you ask. Jack sockets on "normal" audio kit, on the other hand,
will be [somewhere between ±0.447V and ±1.736V](https://en.wikipedia.org/wiki/Line_level#Nominal_levels).
(To clarify: I'm talking about "line out" sockets here, not headphone sockets.
These use the same connectors, but trying to look up voltage levels for
a headphone socket gets me no straight answer, but hints that the answer is
[much](https://en.wikipedia.org/wiki/Headphone_amplifier) more [nuanced](https://www.sweetwater.com/insync/speaker-level/), so let's just forget about that.)

![Voltage reference for line-level audio](/article-images/diy-amp/line-level.png)

(Image credit [AlanM1](https://commons.wikimedia.org/wiki/User:AlanM1); used
under [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/) / SVG exported to PNG.)

## Aside: Eurorack, an Exercise in Just the Right Amount of Jank

Conflicting voltage info? Re-used connectors? Consumer vs. "pro", "line" vs.
"ref"? Having been around for so long, the world of audio electronics seems to
be full of these kinds of rough edges and unwritten rules. If you're going to
walk this path, you'll have to be fine with truth-by-consensus, hone your BS
detector, and reconcile yourself to the fact that you'll be making stuff that
works in certain conditions, because there's no such thing as working
everywhere. But as long as those conditions are _the conditions you have_, you
can build stuff that _works for you_.

I can't say for certain, but I strongly suspect that the Eurorack "standard" has
far more to do with what's cheap, readily available, and works in common,
DIY-friendly voltage levels than it does with engineering. It didn't spring
fully formed from the ether, but nor is it really a standard in the ISO or ANSI
sense of the word. For starters, it all began with one person: Dieter Doepfer.
From reading [a couple](https://www.soundonsound.com/people/modular-profile-dieter-doepfer)
of [interviews](https://www.ableton.com/en/blog/dieter-doepfer-completing-the-circuit/)
and skimming [the Wikipedia page](https://en.wikipedia.org/wiki/Doepfer) for the
eponymous company he founded, he certainly has form, but it seems like cost was
a big factor in module designs - and the explosion of popularity was unexpected.

Basically, Doepfer made (and is still making) the A-100 modular system, and some
combination of timing, price, availability (or lack thereof) of analogue &
modular synths from other manufacturers, saw it take off enough for other people
to start making compatible modules - for varying degrees of "compatible".

### The Infamous Power Connectors

Nowhere are the trade-offs and quirks more noticeable than in the power supply
cables & pin-outs.

![Eurorack 16 & 10-pin power pin-outs](/article-images/diy-amp/euro-power-jank.png)

This has... issues.

There are two kinds of connector: 16 pin, and 10 pin. In the original A-100
system, the ribbon cables used could transport CV & gate signals as well as
power, allowing some degree of built-in default patching between modules; but
basically every other module maker ignores these, to the point that most
purpose-built ribbon cables have a 16 pin PSU end and a 10 pin module end, not
even connecting 6 of the pins. Some modules - mostly ones incorporating digital
signal processing, I think - use the 5V rail; the majority don't, to the point
that many PSUs don't even provide a 5V rail. The pins are all doubled up (or
sextupled, in the case of ground) for no reason other than, as far as I can
tell, not carrying too much power over the thin (approx. quarter millimetre
diameter) wires in the cable. Not all cables & connectors have notches/ridges;
some just have a red stripe on the -12V end, and some kind of indication on the
PCB of where the stripe should be. (I haven't seen it first hand, but I've heard
tales of connectors with the notch - and hence the stripe - installed
"backwards". It's probably become less common over time, but I can believe it in
the standard's early years, because this isn't a dedicated cable design, just
bog-standard ribbon cable.)

TODO Insert photos of ribbon cable & unkeyed connectors on Microbus PSU

### Consequences

Plugging a ribbon in backwards to a well-designed module will simply mean it
doesn't turn on. Doing the same to a less-well-designed module may break it.

As touched on earlier, voltage ranges for audio, envelopes, and other control
signals aren't standardised across module manufacturers, other than being
somewhere between +12V and -12V. Within those limits, too much voltage generally
won't fry anything other than the most poorly-designed gear, but it can have
audio quality implications: send a ±10V waveform into a VCA that tops out at
±8V and you'll be clipping & distorting before you even get to the volume knob
on the output. Which might be the sound you want, but for someone who doesn't
and doesn't know why it's happening, the initial impression is simply that
Eurorack sounds like shit. (It can, but it can also sound good.)

Pitch control is better: higher voltage = higher notes, starting at 0V and
increasing 1 volt per octave. That's one thing everyone agrees on.

This is without even getting into debates over whether or not modules with metal
faceplates should be hooked up to ground, the fact that jack sockets momentarily
create a short circuit between signal & ground when plugging & unplugging
cables (not just a Eurorack problem, but one it inherits by its choice of cheap,
common patch cables), and various other things I'm not qualified to have an
opinion on.

Rant over.

None of this matters though: we're not electrical engineers, we're musicians!
It works well enough; the bleeps go bleep, the bloops go bloop, the parts are
cheap (though fully-assembled, well-designed modules often aren't), everyone's
happy.

(If you happen to be both, and find this section offensive, there are other standards
that are apparently better in various ways: MOTM, Modcan, DotCom... but I know
almost nothing about them other than they're less prolific. The best technology
doesn't always win.)

## Back to the Matter at Hand

Anyway, where was I? Yeah. Audio signal voltage levels. It's a mess.

### If in Doubt, Measure

I hooked up my cheap crappy oscilloscope to the line out of my Zoom H6, and the
audio out of my Raspberry Pi 4 - the two devices I most care about using to
quickly pipe external audio into my rack - and got (unsurprisingly) something
close to "consumer line level": ±0.447V, or 0.894Vpp.

I've decided I want to bump that up to ±5V, or 10Vpp. Because this isn't about
precision, boosting things by a factor of 10 or 11, to get to peaks of plus
or minus 4.9ish volts, is good enough.

## The Electrons Must Flow

Let's take a step back. What even is electricity? Electrons flow through wires,
energy is transferred. Or do they? Maybe they do, but only on the outer surface
of wires. Maybe they do but _really really slowly_, but somehow this doesn't
stop the field generated _outside_ the wire from moving really really fast, and
it's the field that does most of the work anyway.

(If you aren't familiar with Veritasium and ElectroBOOM on YouTube, I highly
recommend [this set of videos going back & forth](https://youtube.com/playlist?list=PLQsAxLlU34zx39noDAVxQsTkAzPNMvrIh)
over exactly that sort of stuff. Turns out none of this is obvious even to
people far, far cleverer than I.)

Why does current flow _from negative to positive_ when surely the other way
round would make a ton more sense? [Historical accident.](https://xkcd.com/567/)

### The Hydraulic Analogy

TODO Continue from here

### Limits of the Analogy

## Operational Amplifiers

### TL07x Rules of Thumb

## Recap

## Tools & Materials

## Breadboarding

## Moving to Prototype Board

## Summary

### Know your Inputs
### If in Doubt, Measure
### Rules of Thumb
### Reusable Building Blocks
### Learn by Doing

## Epilogue

### How to Skim-read a Datasheet
### DIY Synth Lego

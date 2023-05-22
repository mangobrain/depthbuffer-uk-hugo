---
title: "DIY Euro-amp Part 2 - Eurorack: Artisanal Jank"
date: 2023-05-21T18:04:00+01:00
icon: article
draft: false
images: ['/post-thumbnails/diy-amp.jpg']
tags:
- memento potato
- electronics
- diy euro amplifier
toc: true
---
This article is part of my series on building a Eurorack audio amplifier, to
go from line-out on a field recorder or Raspberry Pi to my modular synth rack.
To start from the beginning, [click here](/posts/2023-05-21-babys-first-amplifier/).

This is part of my [Memento Potato project](/posts/2023-04-22-memento-potato/),
in which I am ostensibly producing [my third album](https://depthbuffer.bandcamp.com/album/memento-potato) and releasing each track as & when it's done,
but also using it as a vehicle for tons of other things I've wanted to
build/film/explain/nerd out about along the way.

Picking up where we left of...

## Why is the audio quiet in the first place?

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

![Eurorack 16 & 10-pin power pin-outs >](/article-images/diy-amp/euro-power-jank.png)

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

![A pile of patch cables & various volt-per-octave sockets on modules](/article-images/diy-amp/v-oct.jpg)

This is without even getting into debates over whether or not modules with metal
faceplates should be hooked up to ground, the fact that jack sockets momentarily
create a short circuit between signal & ground when plugging & unplugging
cables (not just a Eurorack problem, but one it inherits by its choice of cheap,
common patch cables), and various other things I'm not qualified to have an
opinion on.

![A 3.5mm TRS patch cable and socket, labeled to show how the signal gets shorted to ground when plugging in](/article-images/diy-amp/jack-short.jpg)

Rant over.

None of this matters though: we're not electrical engineers, we're musicians!
It works well enough; the bleeps go bleep, the bloops go bloop, the parts are
cheap (though fully-assembled, well-designed modules often aren't), everyone's
happy. In my opinion, the benefits of these compromises in terms of cost,
availability, ease of manufacture, DIY friendliness, etc. outweigh the
downsides; and given Eurorack's popularity, I'd say I'm not alone in this.

(If you happen to be both a musician and an electrical engineer, and find this section offensive, there are other standards
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

## To Be Continued

Part 3: [The Hyrdaulic Analogy](/posts/2023-05-21-hydraulic-analogy/)

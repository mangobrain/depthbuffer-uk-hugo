---
title: "Repurposing the Mellotron as an expressive virtual acoustic instrument"
date: 2022-02-22T19:15:50Z
icon: article
draft: false
tags:
- article
- production
- tutorial
---
Ah, the glorious, wonderful
[Mellotron](https://en.wikipedia.org/wiki/Mellotron). Where would I be without
it? I've made no secret of my love for this quirky lo-fi beauty, even if I am
unlikely to ever play or own a real one. The flute & strings on To Hell and
Back, choir on Manchild, various pads and "filler" layers on multiple tracks,
and almost the entirety of Good Taste were made possible by a software
recreation of it.

As a low-tech, analogue, mechanical, keyboard-operated sampler, the original
was hardly known for its expressive capabilities: sure, each key of each sample
bank has its own dedicated tape strip, in contrast to the limitations of early
soundtrackers on the Amiga _et al._ which typically just had one sample per
instrument, played faster or slower to generate different pitches. But the
quality of those sounds is limited by both the quality of the original
recording (most of the original banks being 50-odd years old) and the tape
itself (see previous parentheses), and despite being a keyboard-controlled
instrument, there's no velocity sensitivity: you press a key and it plays
a tape, subject only to master tone & volume controls.

According to Wikipedia, pressing the keys harder would bring the play heads
into greater contact with the tape surface, giving rise to some form of
"aftertouch" - but does this actually work well in practice? Will it really
play louder or softer based on how hard the head is pressed against the tape?
Does tape even work that way!? I have no idea, but I'm pretty dubious. I'd love
to get my hands on one and find out.

In the modern world of "in the box", software-based music production, however,
using digitised copies of these tape banks in conjunction with expressive MIDI
controllers gives rise to some interesting possibilities.

## Synths + robotically perfect sequencing, or acoustic instruments + expressive performance - or... both?

In the year-and-a-bit I've been making & releasing music, one trend I've
noticed in my own tastes is away from the tightly sequenced, pristine audio one
tends to get when producing primarily with trackers & softsynths, towards more
expressive, natural sounds. This can mean many things, but to me, the two most
important are:
1. Incorporating the sounds of traditional acoustic instruments along side
synths and samples
2. Injecting more expression into sequenced phrases using performance capture

Expanding on the second: for example, having the confidence to actually play a
melody line at tempo on a MIDI keyboard and only correct the most egregious
mistakes in editing, rather than sequence everything note-by-note (I'm not a
great keyboard player); or for me, as a lapsed oboist, using my
[EWI](https://www.akaipro.com/ewi4000s) for note input and hooking the stream
of MIDI breath control data up to various parameters.

"But that's nothing special," I hear you say. "That's just using the equipment
as it was actually meant to be used."

Well... yes. You're not wrong. But as someone raised on a diet of old-school
sample-based trackers on the one hand, woodwind playing on the other, who still
struggles to think of a MIDI keyboard as an actual playable instrument rather
than a convenient note input device, the idea that _you can actually capture
expressive input for softsynths_ - followed by the realisation that _I actually
have the necessary gear to do it_ - was a minor epiphany.

## Side-stepping the expensive, niche world of virtual acoustic instruments

But for a hobbyist DIY producer, with no access to a band or session musicians,
and dubious abilities to play anything not shaped like an oboe or recorder,
it's number one that is really the sticking point.

Piano is fairly well covered. There are countless ways to get half-decent piano
sounds out of software, whether sampled or physically modelled. My current
favourites are the Electric Blue & Electric Red instruments that ship stock
with Renoise for Rhodes-esque electric pianos, and the Ratio & Spindle sample
libraries [available for free](https://www.orchestraltools.com/sinefactory) as
gateway drugs for Orchestral Tools' SINE player.

Guitar in various forms is also not hard to get reasonable results on a
shoestring budget, if you're willing to temper your expectations. The "lead
guitar" solo at the 3:07 mark in
[Battleground](https://depthbuffer.bandcamp.com/track/battleground) was
actually
[a free physically-modelled acoustic guitar synth](https://plugins4free.com/plugin/1065/)
run through Renoise's stock amp sim; it isn't going to fool anyone into
thinking it's the real thing, but it's not bad for zero outlay. The bass guitar
on
[Bigger than Bonnie and Clyde](https://depthbuffer.bandcamp.com/track/bigger-than-bonnie-and-clyde)
was the also-free
[Ample Bass P Lite](https://www.amplesound.net/en/pro-pd.asp?id=19) plugin,
coupled with a sample from Freesound for the slide right at the start, both
again layered through varying degrees of effects to hide some of the worse
sins. The acoustic guitar strumming at 1:32 in
[To Hell and Back](https://depthbuffer.bandcamp.com/track/to-hell-and-back) was
another one of the free Ample plugins, sequenced by feeding chords into its
built-in "auto strummer".

My new favourite thing to do is actually run a clavinet VST on creative
settings through effects designed for guitar processing. You'll get to hear
that on Serotonin Syndrome, which - all being well - will be the closing track
on my second album, whenever that is eventually finished & released.

### The more expressive the instrument, the harder it is to emulate

There are [many](https://keyboardkraze.com/best-electric-guitar-vsts/) free &
paid options for guitar synths, both modelled and sampled. If you're a
guitarist, what I'm about to say will come as no surprise whatsoever; but if
like me you aren't, then when you really start investigating in earnest, you'll
quickly come to a few realisations:
* Electric lead & bass guitar sounds are as much about the FX as the "raw"
instrument; you can cover a _lot_ of sins with the right processing chain
* Authenticity of a final phrase is not just about the sound, it's about the
method: guitars are physical objects, with attributes that completely define
the pitch range and playing styles available; the best guitar synth in the
world won't fool anyone if played straight from a MIDI keyboard with no
consideration for "what would a guitarist do?"
* Orthogonal to the raw instrument tone and FX chain, there are many, many ways
to _operate_ the instrument. You can do so many things when you have real,
tangible strings under your fingers: pick slides, bends, hammer ons/pull offs,
slap bass... again, I'm not a guitarist, so this is not anywhere close to
exhaustive.

This last point is the kicker. The real thing is nuanced, and the more of these
nuances you want to be able to recreate, the more capable a synth you'll need
(often translating simply as "bigger sample library", with more of these play
styles captured in the raw material), and the harder you'll need to work to
apply them in sequences.

At some point, especially as a hobbyist who isn't making a profit from it,
you'll compromise: you'll get close enough, and stop.

If you really want a screaming, face-melting electric guitar solo in your next
track, get a guitar(ist).

### My nemesis: brass

Anyway. Slowly circling back to the topic at hand. Similar issues afflict brass
instruments: the real thing is so expressive, it's difficult to fake well. I
really, really wanted to have some kind of trumpet or sax solo on Bonnie and
Clyde, but the more I looked into it, the more disappointed I became.

[Quality](https://www.orchestraltools.com/store/collections/big-band-horns)
[brass](https://www.native-instruments.com/en/products/komplete/cinematic/symphony-series-brass/)
[sample](https://impactsoundworks.com/product/straight-ahead-jazz-horns/)
[libraries](https://www.chris-hein-shop.com/chris-hein-horns-compact-33-0.html)
[are](https://www.soundsonline.com/hollywood-pop-brass)
[expensive](https://fablesounds.com/broadway-big-band/). And that's not even
accounting for the range of expression you might want if trying to actually
articulate a solo, rather than backing: both
[sample-based](https://www.aaronventure.com/infinite-brass) and
[physically modelled](https://audiomodeling.com/swam-engine/solo-brass/trumpets/)
options exist, but again, they aren't cheap. Similar to the guitar situation,
the real instruments are, in the hands of capable musicians, simply capable of
_so much_ expression; the more of that expression you want to recreate
virtually, the more extensive a sample library/physical model you will require,
along with the requisite time investment programming your sequences.

The cheapest options I've found are:
* [Embertone Sensual Sax](https://www.embertone.com/instruments/sensualsax.php),
but that requires the "full" version of Kontakt, so the $20 list price on that
page
[isn't the full story](https://www.native-instruments.com/en/pricing/kontakt-6/).
  * (Side note: so many things ship as Kontakt sample libraries that I should
          probably make that investment at some point... but right now, I'd
          rather use the money towards starting to get some real, non-software
          synths. It would make sense if I was actually making my living doing
          this - taking commissions, or doing scoring, or producing for real
          recording artists - but I'm not, so I'm not feeling it right now.)
* [Duplex Saxophones](https://www.orchestraltools.com/store/collections/duplex-saxophones)
from Orchestral Tools. The whole package is expensive, but individual
instruments less so, and they're hosted in their SINE Player software, which
does not impose additional cost.

What I've actually been doing is using the free Rotary sample pack,
[available at the same place](https://www.orchestraltools.com/sinefactory) as
the Spindle and Ratio piano sample libraries I mentioned earlier, and papering
over the cracks by using it sparingly & smothered in "lo-fi" FX.

For the solo in the B&C instrumental break, I caved and used a (virtual)
clavinet instead.

Again, my advice to you is: if you _really_ want a screaming, face-melting sax
or trumpet solo on your next track, either be prepared to do your research and
make the necessary investments of time & money, or bring in the real thing.

## You said this was a Mellotron article!

Yes, I have heavily digressed, I know. I do that a lot, and this is my site, so
get used to it, because I probably won't rein it in. ;)

Anyway, now that I've set the scene, let's bring it back together. Convincingly
faking expressive acoustic instruments is hard, yet I increasingly find myself
wanting to incorporate those sounds. The Mellotron has great "lo-fi" woodwind
sample libraries - flutes, clarinets, oboes, etc. - if you can live with the
nature of said samples. Real Mellotrons are not really known for their
expressive capabilities, but virtual ones have more parameters that can be
automated, if you have a controller capable of giving you expressive automation
inputs, which I do.

My weapons of choice: Renoise, an EWI 4000S, and a copy of
[M-Tron Pro Complete](https://www.gforcesoftware.com/products/m-tron-pro/).
Yes, I am aware that I've just dedicated an entire section to bemoaning the
cost of virtual acoustic instruments, then linked to a near-£300 virtual
instrument that isn't designed to compete in that space, but personally, I have
so many uses for Mellotron sounds that this investment made much more sense to
me than a similar amount for one or two convincing single instruments.

### MIDI Mapping in Renoise

The workflow goes something as follows:
1. Load up M-Tron Pro in Renoise
2. Find your oboe, clarinet, flute, etc. sample library of choice
3. Add an
    [instrument automation](https://tutorials.renoise.com/wiki/Meta_Devices)
    meta-device to a track
4. Map the instrument automation device to your Mellotron parameters of choice
5. Map the MIDI breath control CC from your EWI or similar breath controller
    (or _&lt;insert CC of choice&gt;_ from _&lt;insert device of choice&gt;_)
    to the instrument automation device using Renoise's MIDI mapping, hit
    record, and perform
6. Turn on "record mapped parameters to automation" in the MIDI mapping
    dialogue, for higher-resolution capture and easier editing afterwards
7. If necessary, edit the resulting data in the automation editor to correct
    any particularly egregious mistakes, or help alleviate audible stepping by
    switching envelope type from "points" to "lines" or "curves" to smooth
    things out

Personally, I've found that mapping breath control to low-pass filter cut-off
produces more pleasing results than a straight mapping to master volume or
sustain level.

#### Pros & cons

On the one hand, all the limitations of the Mellotron itself still apply: one
sample per pitch, no dedicated legato mode, low-quality samples, no fancy
performance techniques in the sample library. You'll be emulating simple
performance of simple melodies, and papering over the cracks by combining the
end result with the other layers in your final mix. This is a matter of taste.

On the other hand, if you can live with these limtations, you'll have a
veritable lo-fi chamber ensemble at your fingertips. Another unexpected
benefit: any vibrato imparted on the samples by the original performer comes
for free, and sounds natural. This could be a bad thing if you _don't_ want
that, but I like it.

#### The results

{{< audio src="/media/stbtd/mellotron-stbtd-snippet.mp3" >}}

Above is a little snippet from Sixpence to Bury the Dead - another track you
will hopefully, eventually, find on my second album - incorporating a trio of
clarinet, flute, and oboe. I think it sounds rather nice.

#### I read all that for twenty seconds?

Yup. Deal with it.

## A plea to Renoise developers: direct MIDI mapping please!

As a final parting gift, I give to you: the ridiculous workflow required to map
MIDI breath control to parameters in Renoise. It has a perfectly capable MIDI
input monitor, so I can see exactly what I want to map, and know exactly what
I want to map it to; but as far as I know, it only supports creating of
mappings via live "MIDI learn" functionality: you can't just type in what you
want to map, you have to enter learn mode, click the parameter you want to
map, generate the desired CC - tweak the desired knob, hit the desired button,
blow into the desired breath controller, etc. - then leave learn mode again.

For buttons and knobs, this probably works rather well. For bulky woodwind
controllers, especially ones that output all kinds of other unrelated control
data when starting & stopping notes, it's a right faff.

{{< youtube nUXlBnwXJWk >}}

Please, please, _please_ can we get direct, non-learn-based mapping in a future
update? Or, if I'm being an idiot, and someone knows a better way to do this,
please let me know on Twitter!

I know there's an approximately 0% chance of any Renoise developers reading
this. But, if you don't ask, you don't get.

---
layout: post
title: "Something About LEDs"
description: "LED strips make life better... if you have a soldering iron."
tags: [sample post, video]
categories: [intro]
---

## I'm new to lighting, what is that?

LED stands for [*Light Emitting Diode*](https://en.wikipedia.org/wiki/Light-emitting_diode). It is type of electrical device that serves two functions: first and foremost it emits light at various colors depending on the material it is made from, secondly it prevents current from passing backwards across itself (thus being a diode). LEDs are impressively efficient for their size.

| A-1 Lumens Per Watt | Incandescent | Fluorescent | LED   |
|--------------------:|:------------:|:-----------:|:-----:|
| 800 lumens          | 50 watts     | 13W         | 8.5W  |
| 1600L               | 100W         | 26W         | 19W   |
| 3200L               | 200W         | 32W         | 35.5W |

One may notice that fluorescent lamps are not linear in the above chart. Right now if you want a light a large area, fluorescent tubes are still the most cost effective way to go when you only consider the lumens per watt, but they don't scale down very well. For smaller functions LED lighting will consume less energy.

LEDs are extremely easy to manipulate, unlike incandescent (which require a vacuum or a neutral gas of some kind to prevent a burnout) or fluorescent lamps (which requires high voltage and a starting circuit) LEDs are low voltage and can be installed easily onto a printed circuit board. LEDs are very commonly found on PCBs of all stripes and walks of life, used as indicators for power, processor states, or some other status that needs to be seen. The brighter LEDs can often be found printed on long conductive strips.

## LED strips

LED strips change the game. These strips are how you get the above mention lumens per watt, being able to produce as much as 600 lumens per meter for a good one (calculations above assumed 540/meter) and usually consuming one amp per meter at 12V (for a total of 12W) these strips a powerful tool for creating interesting, stylish, or simply creative home lighting setups. These strips can also be found in even more interesting and creative kinds such as RGB, temperature changing, and addressable versions. RGB lights have one each of a red, green, and blue LED squashed into a single lamp, with each color being powered independently. These lights can produce essentially any color. Temperature changing strips are similar, but simply produce "white" that can be changed depending on how the strip is powered. Lastly, and most interestingly, is addressable strips. Addressable strips have controllers that can independently change the color and brightness of a groups of three LEDs or individual LEDs depending on the strip. Addressable strips are by far the most fun to play around with due to their ability to display complex changing patterns.

I acquired a 5 meter spool of dumb<sup>(not RGB, not addressable)</sup> white LEDs about a year ago. This one of the most useful and fun purchases that I have ever made, and I have long since consumed all 5 meters on various projects. I have 2 meters in total on the side of my house serving as a far more effective porch light, I have a half glued some into every car I drive on a regular basis, stuck a tiny strip in the bathroom and dimmed it for the middle of the night, installed some around the inner edge of girlfriends vanity to make a powerful ring light, and a dimmable length under the hutch of desk.

## This sounds neat, how do I get started?

You should get a soldering iron. There are no-solder options in the world, but they are, by far, the worse option, besides learning to solder is a useful skill and led strips are actually a good place to start.

To start with you need a power supply. *Not all power supplies are created equal!* You need a 12V supply that is rated to at least as many amps as you have meters of LED strip.

![led-strip-closeup]
![tinned-strip]
1. Cut the end off of your power supply and strip the wires.
2. Flux the pads.
3. Put down a little solder onto each of the pads, positive and negative, be careful not to accidentally bridge them.
4. Put a little solder onto the wires you intend to attach.
5. While pressing the tinned wire into the pad, touch the pad briefly with the soldering iron, this will flow the solder on the pad and wire together, and create a strong electrical connection.
![soldered-strip]

That's it! you've soldered a wire to your strip!

[led-strip-closeup]:images/leds/led-strip-closeup.jpg
[tinned-strip]:images/leds/tinned-strip.jpg
[soldered-strip]:images/leds/soldered-strip.jpg
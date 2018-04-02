---
layout: post
title: "Something About Home Security (pictures coming soon)"
description: "LED strips make life better... if you have a soldering iron."
tags: [modding, soldering, raspberry pi, security, DIY]
categories: [security]
---

## So expensive...

My girlfriend and her roommate are splitting soon after which she will be living on her own. She asked me to look into the cost of a home security system, and oh god... they are not cheap. For those of you who don't know, the way that a modern alarm works is a sort of step-by-step, as long as the alarm is armed do:

1.  Check for the presence a person
2.  Wait a moment for the person to attempt to disarm the alarm
3.  Sound the alarm, alert the security provider
4.  The provider attempts to contact the owner to check for a false alarm
5.  The provider alerts the police

The cost of all this is pretty high, at least in my opinion. [This Safewise article](https://www.safewise.com/home-security-faq/how-much-does-a-security-system-cost) outlined the cost of installing a new security system and it's way outside my price range and hers, plus a monthly subscription that would be at least a hassle, and at most just unfordable. That being said, I don't think I need to afford it. Each of these steps, on their own, is actually pretty simple in my opinion, so my plan is to replicate the full functionality of a home security system for a fraction of the cost, and if possible without any monthly subscription.

For this project I know that I'm going to the be using a raspberry pi for it's low power consumption, cost, and broad support community. Beyond that all I have is my project goals to go by:

1.  The system will detect the presence of people
2.  The system will audibly announce the opening of doors and windows
3.  The system will alert the owner of the opening of doors and windows via sms
4.  The system will alert the owner and me when a person is in the apartment that has failed to disarm the alarm
5.  The system will have an uninterruptible power supply

Stretch goals:

1.  The system will automatically arm and disarm in the presence or absence of a paired bluetooth device
2.  The system will accept commands via sms
3.  The system will be capable of sending live photos and videos of its surroundings on command
4.  The system will capable of firing the alarm on queue (panic button)
5.  As a backup the system will be capable of using the 3g in addition to wired internet connectivity

### 1. The system will detect the presence of people

Security systems handle this one of a few ways. I've seen those that simply check for the opening of windows and doors using hall sensors, and I've seen those that use ultrasonic or infrared motion sensors to check for changes inside a room, checking for the presence of people regardless of doors being open or closed. The raspberry pi can handle motion sensors, and motion sensors aren't very expensive, but she has a cat that could set it off, so I'm going to opt for just hall sensors. I'm not expecting anyone to tunnel through a wall so getting all the windows and doors should be good enough.
Everyone who makes system like these uses unipolar sensors. Unipolar sensors are active in the presence of a south magnetic field and inactive without it. Bipolar sensors activate with a south field, and then stay active until they are exposed to a north field.
I will need to design a circuit for the hall sensors. I don't want to have a ton of wires everywhere, just one. Therefor I need to design a door/window sensor module that I can daisy-chain. I'll be using RJ-45 jacks on the sensor modules, making pin 1 ground and the remaining pins I will make into a 3 x 4 input matrix by installing a pass through for all the pins and cycling both groups on each module. Each jack on the body of the alarm will be able to handle up to 12 sensors, and I can further matrix the pins on the jacks into a 6 x 8 matrix handling a total of 48 sensors while using 14 pins, which will leave enough pins leftover for other functions, such and button input and audio output (it will be a pi zero, it needs to use GPIO for audio). I walked through my ~1800 square foot house and counted a total of 17 windows and doors, two which were double windows which would want two sensors. I don't need 48 hall sensors for a one-person apartment in the middle of Knoxville, I expect it to have one door and two windows. Never the less I'm going ahead with the 48-sensor capable plan because even if I don't use all of them at first I may be able to re-purpose them later for other things kinds of sensor such as something to detect broken windows.

### 2. The system will audibly announce the opening of doors and windows

Depending on how this is handled it could be an annoyance or the simplest part of the build. For me it's the latter. I'm using an under-the-shelf clock radio that I found at a thrift store for $5. I considered it just about ideal because it solved a few problems all at once, it:

 - provides a safe and decent-looking mounting solution
 - is discrete, doesn't look like a alarm to destroy or something expensive to steal
 - has a built-in amplifier circuit and speakers so I can use that instead of an external solution
 - has plenty of room for all the additional hardware after removing the CD player, she doesn't have any CDs anyway

This particular clock radio (GPX model KC318S) has three states: FM Radio, CD, and Aux input. None of these output audio all the time, the moment you switch away to a different mode, your audible alarm is gone. In order to get audio at all times I took the main board off it's mount and backtracked the audio out to the speakers until I found the amplifier. There is a heat sink glue to the amp, so I had to get creative here. First to make sure I didn't fry anything I turned on the radio and used a multimeter to figure out which pin is the power input, then I shorted the other input pins to ground one by one until I figured out which ones were the un-amplified inputs and I soldered the wires to those and to the ground. Success! Plugging in the other ender of the wire I just attached to my phone I get audio output through the radios speakers regardless of what mode the radio is in. It does need to be on, but that's no big deal, you can just turn it to CD and it's otherwise silent. Bonus, I bypassed some other part of the radio and the audio out from the alarm will play at full volume regardless of that setting. It's honestly a bit too loud like that and I fear for the health of the speakers, but I can just reduce the volume to ~70% in software.
While I'm still modifying the clock radio I might as well tackle a stretch goal. I drilled a 3/4 inch hole just under the slot for the CD tray and stuck the lens of a pi camera 1.3 through it. I'll handle what sort of pictures or video to take and when later in software, for now it'll just be there.

### 3. The system will alert the owner of the opening of doors and windows via sms

This is where is gets just a little bit shaky. I haven't started programming yet, but I'm pretty sure that I'm going to be using an API that I found in someone else's github project. This will involve creating a dedicated Google account for the device (which I have already done) along with an app specific password (also done), and then tying in the API with that information to log in and send messages. This a pretty big cornerstone of the alarm, because text messaging is probably the easiest way for a computer to alert me or her of something happening. I hope that this API will be able to handle receiving and reading text messages also, thus the stretch goal of accepting commands via sms.

### 4. The system will alert the owner and me when a person is in the apartment that has failed to disarm the alarm

More of the same as step 3, except that I will be adding myself to the list of people to alert, and if possible this will be a phone call either instead of or in addition to the sms.

### 5. The system will have an uninterruptible power supply

This is another one that I've already dealt with. On amazon you can get a range of different UPS hats for the raspberry pi. Mine is [this one](https://www.amazon.com/Makerfocus-Raspberry-2500mAh-Lithium-Battery/dp/B01MQYX4UX). It came with a 2500mAh battery, but to be honest I don't know how long that will last. At 5v the pi zero w will go through about 400mA which will probably drain that battery in a little under 4 hours, good but not good enough. For a weeks or two now I have been collecting 18650 cells from dead laptop batteries, I've recycled something like 30 dead cells and I have around 13 good ones. By soldering two in parallel (this metal doesn't take to solder very well) and taping them together I have created... around 3000mAh. Oh well. I guess 5 hours is better that 4, and the power grid in Knoxville doesn't normally go down for long durations anyway.
The UPS by itself doesn't actually do very much beyond protecting the micro SD card from corruption due to improper shutdown, after all if the power goes out, audible alarms do too. This ties in to the other stretch goal: I have be playing with the concept of adding a 3g adapter so the device will still have the sms and calling functionality in the event of a power failure. Not a bad plan, but it will incur a monthly fee to do so. On the other hand if I do I could add other responsibilities to it such as maintaining working wifi through the apartment if the power or the other ISP fails. I know that Google fi will probably be my go-to option for this if I choose to do so, just because it's as simple and inexpensive as it is.

### Other stretch goals

Since I'm planning on using a pi zero w there will be a built-in bluetooth radio. Pairing a phone to automatically disarm the alarm when the phone comes home seems like a good idea, at least on the face of it. It takes code-authentication and replaces it with token authentication, which I like. It adds a layer of failure in that if she forgets her phone at home the alarm will be disarmed and will not alert me, she will not be aware of door and window alerts, and she will not have here phone to remotely arm it, leaving her to have to contact me without here phone so that I can remotely arm it.
The panic button is barely a stretch goal. I already plan on having physical inputs at least so having one of them panic is a no-brainer.
Lastly sending live photos and videos is an interesting option. It's one more method of just checking on things in a passive way. Hopefully I want the system to accept a command via sms, take the picture or shoot a few seconds of video, and then send it right back the person who sent to command. There will be list of authorized numbers, of course, I don't really want random people taking pictures willy nilly of the inside of the apartment.

## Other thoughts

I'm thinking of mounting the whole system in her bedroom. Ideally what I want is for the door and window announcements to be loud enough to wake her up every time. Beyond that, right now I'm stuck just waiting for the pi zero w to ship. Outside of value packs containing the zero w, it's really very hard to get a hold of right now. I think there's been a shortage of those units since their introduction. I could use a pi 3, or 3B+ but honestly I just don't think that I need the computing power enough to justify the expense of one of those.
I've also had a powered USB hub sitting in my bedroom doing nothing for close to 2 years now. I'm planning to hook that up with its four ports sticking out the front to power a phone by, because the pi zero w kit I ordered comes with a 2.5 amp supply, enough to power the zero w and charge a couple phones at once, so why not add a feature. I can see it being useful to be able to plug in a mouse and keyboard anyway.
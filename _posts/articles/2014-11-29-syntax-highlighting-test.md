---
layout: article
title: "Pulse Wave Phase"
modified:
categories: supercollider-code
excerpt: "A short minimalist electronic composition."
tags: []
image:
  feature: 
  teaser: 
  thumb: 
date: 2014-11-29T22:08:14-05:00
---

*A short minimalist electronic composition.*

```

//////////////////////
// Pulse Wave Phase //
//////////////////////

//These are the sounds I'm using.
//There are three voices.


(
//Two of these voices use pulse waves.
SynthDef(\nespulse, {|att=0.001, sus=0.1, rel=0.03, freq=440, wdt=0.5, amp=0.3, out = 0, pan = 0|
	var env, snd;
	env = EnvGen.kr(Env.linen(att, sus, rel), doneAction:2);
	snd = LFPulse.ar(freq, 0, wdt, env*amp);
	Out.ar(out, Pan2.ar(snd, pan));
}).add;

//The third voice is a triangle wave, the bass.
SynthDef(\nesbass, {|att=0.001, sus = 0.2, rel=0.03, freq=440, amp=0.5, out = 0, pan = 0|
	var env, snd;
	env = EnvGen.kr(Env.linen(att, sus, rel), doneAction:2);
	snd = LFTri.ar(freq, 0, env*amp)!2;
	Out.ar(out, Pan2.ar(snd, pan));
}).add;
)

(
//Pulse Wave Voice 1
Pbind(
	\instrument, \nespulse,
	\midinote, Pseq([
		    //Notes of the MIDI scale.
		Pseq([
			51, 55, 62, 55,
			51, 55, 62, 55,
			51, 55, 62, 55,
			53, 55, 62, 55,
			48, 55, 62, 55,
			48, 55, 62, 55,
			48, 55, 62, 55,
			47, 55, 62, 55,
		], 6),
		    //This section will be played 6 times in a row before the next one begins.
		Pseq([
			51, 55, 62, 55,
			51, 55, 62, 55,
			51, 55, 62, 55,
			53, 55, 62, 55,
			48, 55, 62, 55,
			48, 55, 62, 55,
			48, 55, 62, 55,
			53, 55, 62, 55,
		], 6),
	], inf)-Pseries(0, 0.0001, inf),
	        //When SuperCollider plays through the entire list of notes,
	        //it will start again from the beginning,
	        //repeating the list infintely.

	\dur, Pstutter(32,
		    //Each note in the following pattern will be played 32 times.

		Pseries(0.25, -0.0025, inf)),
	        //The value for duration is 0.25 of a second - four notes can be played in the space of a second.
	        //After 32 repeats - Pstutter(32, 0.25) - the value changes by -0.0025,
	        //making the length of each note 0.0025 seconds shorter.

	        //In this way, the piece accelerates.

	\amp, Pseries(0.02, 0.0001, 768),
	        //With each note, the piece becomes 0.0001 louder.
	        //Because the pattern only repeats 768 times,
	        //this voice will stop playing its infinite loop after the 768th note.
	\sus, Pkey(\dur),
		    //The amount of time that each note is sustained is equal to the duration of each note.
	\pan, -1,
	\wdt, 0.5,

).play;

//Pulse Wave Voice 2
//will be almost identical to Pulse Wave Voice 1,
//but note 2 key differences:
Pbind(
	\instrument, \nespulse,
	\midinote, Pseq([
		Pseq([
			51, 55, 62, 55,
			51, 55, 62, 55,
			51, 55, 62, 55,
			53, 55, 62, 55,
			48, 55, 62, 55,
			48, 55, 62, 55,
			48, 55, 62, 55,
			47, 55, 62, 55,
		], 6),
		Pseq([
			51, 55, 62, 55,
			51, 55, 62, 55,
			51, 55, 62, 55,
			53, 55, 62, 55,
			48, 55, 62, 55,
			48, 55, 62, 55,
			48, 55, 62, 55,
			53, 55, 62, 55,
		], 6),
	], inf)+Pseries(0, 0.0001, inf),
	\dur, Pstutter(32, Pseries(0.25, -0.0024, inf)),
	        //1. The duration pattern is offset by a smaller value in Voice 2 than in Voice 1,
	        //   so while both voices accelerate, Voice 1 does so at a larger rate than Voice 2.
	        //   In this way, the voices phase out from one another.

	\amp, Pseries(0.02, 0.0001, 764),
	\sus, Pkey(\dur),
	\wdt, 0.125,
	\pan, 1,
	        //2. Both voices have a default pulse wave width of 0.5.
	        //   For Voice 2, though, I specified a different value: 0.125.
	        //   This way, the voices are somewhat easier to tell apart,
	        //   making the phasing effect more obvious.
).play;

//Triangle Wave Voice//
Pbind(
	\instrument, \nesbass,
	\midinote, Pstutter(4,
		Pseq([Pseq([Pn(39, 3), 41, Pn(36, 3), 38], 4),
		Pn(41, 16),
	], inf)),
	\dur, Pseq([Pstutter(32, Pseries(0.25, -0.0025))],inf),
	\amp, Pseries(0.15, 0.0002, 768),
	\sus, Pkey(\dur)*0.9,
).trace.play;
)

s.record;
s.stopRecording;

```

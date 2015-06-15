---
layout: article
title: "Demo Reele"
modified:
categories: music
excerpt: "from The Legend of Zelda: Oracle of Ages"
tags: []
image:
  feature: Bryan-Ochalla.jpg
  credit: Bryan Ochalla
  creditlink: https://www.flickr.com/photos/bochalla/7062053233/in/photolist-bL3Sov-5Xvz1r-4PrsU-62fsM1-qjtXKH-4PrsA-oyYreW-nL7fZb-9cWX9-qoiutY-nqDF43-nNqeRn-ozaKd1-oc6p6b-nAECZu-q4m7Ti-4Prsf-6HebzJ-mo74B-qyDsou-AGLwR-rvH5pb-6D8kZ-7yDhkT-7yDhfr-7yH5i7-7yDh3B-6h5Xwj-Eocyn-3kWJbH-2jdmB-q4m7xi-qbzXBw-nNqeWx-2FPu43-ddTwUe-sUmL6-gxkB2J-qg4fEA-bFkMe-nNqf6R-nNptir-bL3RSg-fBL2Qx-bBbddu-5fjM8-reFq7P-paLDRg-AGLwF-ekzm2R
  teaser: Bryan-Ochalla.jpg
  thumb:
date: 2015-5-21
---
A sound-design/music makeover for gameplay footage from The Legend of Zelda: Oracle of Ages.  All sounds and music were created from scratch in SuperCollider and arranged into the four "channels" of GameBoy Color sound in Ardour.

Footage originally captured by [Roxas9408](https://www.youtube.com/watch?v=2PTcmMBhcRQ).

####Code
{% highlight javascript linenos=table %}
/////////////////////////////////////////////////////////////
//                                                         //
// Code for The Legend of Zelda: Oracle of Ages Demo Reele //
//                                                         //
/////////////////////////////////////////////////////////////

//Synths
(
//Square Wave Channel
//- can have up to 2
SynthDef(\nespulse,{|att=0.001,sus=0.1,rel=0.03,amp=0.3,freq=440,freqdev=0,wdt=0.5,out|
	var env,snd;
	env=EnvGen.kr(Env.linen(att,sus,rel),doneAction:2);
	snd=LFPulse.ar(freq+freqdev,0,wdt,env*amp)!2;
	Out.ar(out,snd);
}).add;


//Triangle Wave Channel
//-most chiptune composers used it as a bass voice since it technically can't sustain notes
//-but I like this sound the best and try to maximize its use
SynthDef(\nesbass,{|out,att=0.001,sus=0.1,rel=0.03,amp=0.5,freq=440|
	var env,snd;
	env=EnvGen.kr(Env.linen(att,sus,rel),doneAction:2);
	snd=LFTri.ar(freq,0,env*amp)!2;
	Out.ar(out,snd);
}).add;


//White Noise Channel
//-for sound effects (and often times percussion, though not in this case)
SynthDef(\nesperc, { |out, amp=0.3, att = 0.005, sus=0.01, rel = 0.01|
	var snd;
	snd = WhiteNoise.ar()!2;
	snd = HPF.ar(snd, 2000);
	snd = snd * EnvGen.ar(Env.linen(att, sus, rel), doneAction:2);
	OffsetOut.ar(out, snd*amp);
}).add;
)
/////Square Channel Sounds/////

//Rupee Get
(
Pbind(
	\instrument, \nespulse,
	\midinote, Pseq([92,94]),
	\ctranspose, 0,
	\dur, 1/24,
	\att, 0,
	\sus, 0,
	\rel, Pkey(\dur)*0.9,
	\wdt, 0.125,
).play;
)

//Talking
(
Pbind(
	\instrument, \nespulse,
	\midinote, Prand([Pxrand([68, 70, 72],2), \rest], 300),
	\ctranspose, -12,
	\dur, 1/30,
	\att, 0,
	\sus, 0,
	\rel, Pkey(\dur)*1,
	\wdt, 0.125,
).play;
)


/////Triangle Channel Sounds/////

//Pause
(
Pbind(
	\instrument, \nesbass,
	\midinote, Pseq([80,82,84,91]),
	\ctranspose, 0,
	\dur, 1/24,
	\att, 0,
	\sus, Pkey(\dur)*0.9,
	\rel, 0,
).play;
)


//Select
(
Pbind(
	\instrument, \nesbass,
	\midinote, Pseq([77,82]),
	\ctranspose, 0,
	\dur, 1/24,
	\att, 0,
	\sus, Pkey(\dur)*1,
	\rel, 0,
).play;
)


//Choose
(
Pbind(
	\instrument, \nesbass,
	\midinote, Pseq([80,79,77,75,77]),
	\ctranspose, 12,
	\dur, 1/24,
	\att, 0,
	\sus, Pkey(\dur)*1,
	\rel, 0,
).play;
)


//Unpause
(
Pbind(
	\instrument, \nesbass,
	\midinote, Pseq([82,87,84,79]),
	\ctranspose, -12,
	\dur, 1/24,
	\att, 0,
	\sus, Pkey(\dur)*0.9,
	\rel, 0,
).play;
)


//Drown
(
Pbind(
	\instrument, \nesbass,
	\midinote, Pseq([90, 80, 70, 60, 50]),
	\ctranspose, 0,
	\dur, 1/24,
	\att, 0,
	\sus, 0,
	\rel, Pkey(\dur)*1,
	\wdt, 0.5,
).play;
)


/////Noise Channel Sounds/////

//Door
//-altered in GarageBand using the BitCrusher plug-in
(
Pbind(
	\instrument, \nesperc,
	\freq, Pseq([3000, 2500]),
	\dur, 1/12,
	\sus, 0.01
).play;
)


//Sword
(
Pbind(
	\instrument, \nesperc,
	\freq, Pseq([100, 200, 300, 400]),
	\dur, 1/24,
	\att, 0.01,
	\sus, 0.05,
	\rel, 0.01,
).play;
)


/////Music/////

//Overworld
//-Since each channel can only play one note at a time
// I recorded each track separately,
// giving me the ability to cut musical voices out
// when their respective channels were needed for a sound effect.
(
Pbind(
	\instrument, \nesbass,
	\midinote, Pstutter(4, Pseq([68, 70, 72, 79, 70, 75, 72, 67, 65, 70, 72, 79, 69, 76, 72, 67]+12, inf)),
	\dur, 1/8,
	\att, 0,
	\sus, Pkey(\dur)*Pseq([0.1, 0.2, 0.3, 0.4],inf),
	\rel, 0,
	\amp, Pseq([0.3, 0.2, 0.1, 0.05], inf),
).play;

Pbind(
	\instrument, \nespulse,
	\midinote, Pseq([
		Pseq([44, 51, 60, 51], 7), Pseq([44, 51, 58, 51], 1),
		Pseq([43, 53, 58, 53], 4), Pseq([41, 53, 57, 53], 4),
		Pseq([44, 51, 60, 51], 7), Pseq([44, 51, 58, 51], 1),
		Pseq([43, 53, 58, 53], 4), Pseq([41, 53, 57, 53], 4),
	], inf),
	\dur, 1/8,
	\att, 0,
	\sus, 0,
	\rel, Pkey(\dur)*0.9,
	\amp, 0.1,
	\wdt, Pstutter(2, Pseq([0.25, 0.5, 0.125, 0.5], inf)),
).play;

Pbind(
	\instrument, \nespulse,
	\midinote, Pseq([
		Pseq([\rest, 68], 8),
		Pseq([\rest, 67], 4), Pseq([\rest, 65], 4),
		Pseq([\rest, 65], 4), Pseq([\rest, 63], 4),
		Pseq([\rest, 65], 8),
	], inf),
	\dur, 1/4,
	\att, 0,
	\sus, Pkey(\dur)*0.2,
	\rel, Pkey(\dur)*0.2,
	\amp, 0.1,
	\wdt, 0.125,
).play;
)


/////Shop/////
(
Pbind(
	\instrument, \nesbass,
	\midinote, Pstutter(3, Pseq([56, 58, 60, 67, 58, 63, 60, 55, 53, 58, 60, 67, 57, 64, 60, 55], inf)),
	\ctranspose, 24,
	\dur, Pseq([1, 1/2, 1/2]/6.5, inf),
	\amp, Pseq([0.3, 0.2, 0.15], inf)*0.8,
).play;
)


/////Item Get/////
(
Pbind(
	\instrument, \nespulse,
	\midinote, Pseq([Pn(72, 2), Pn(74, 2), Pn(79, 6)], 1),
	\ctranspose, 12,
	\dur, Pseq([Pn(1/8, 9), ], inf),
	\att, 0,
	\sus, Pkey(\dur)*1,
	\rel, 0,
	\wdt, 0.25,
	\amp, Pseq([0.3, 0.25, 0.2, 0.1, 0.3, 0.25, 0.2, 0.15, 0.1, 0.05], inf),
).play;

Pbind(
	\instrument, \nespulse,
	\midinote, Pseq([Pn(72, 2), Pn(72, 2), Pn(74, 6)], 1),
	\ctranspose, -12,
	\dur, Pseq([Pn(1/8, 9), ], inf),
	\att, 0,
	\sus, Pkey(\dur)*1,
	\rel, 0,
	\wdt, 0.25,
	\amp, Pseq([0.3, 0.25, 0.2, 0.1, 0.3, 0.25, 0.2, 0.15, 0.1, 0.05], inf),
).play;

Pbind(
	\instrument, \nesbass,
	\midinote, Pseq([Pn(68, 2), Pn(68, 2), Pn(70, 6)], 1),
	\ctranspose, -12,
	\dur, Pseq([Pn(1/8, 9), ], inf),
	\att, 0,
	\sus, Pkey(\dur)*1,
	\rel, 0,
	\wdt, 0.25,
	\amp, Pseq([0.3, 0.25, 0.2, 0.1, 0.3, 0.25, 0.2, 0.15, 0.1, 0.05], inf),
).play;
)


s.record;
s.stopRecording;
{% endhighlight %}

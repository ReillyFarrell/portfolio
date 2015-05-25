---
layout: article
title: "Arrow Key Ocarina"
modified:
categories: supercollider-code
excerpt: "Virtual instrument inspired by Ocarina of Time"
tags: []
image:
  feature:
  teaser:
  thumb:
date: 2015-5-21
---

###How to Play
| Key             | MIDI Note Assignment |
|:---------------:|:--------------------:|
| Spacebar        | D5                   |
| Down Arrow Key  | F5                   |
| Right Arrow Key | A5                   |
| Left Arrow Key  | A5                   |
| Up Arrow Key    | D6                   |


####Code
```
//Virtual Ocarina (alto, one octave)
//inspired by The Legend of Zelda: Ocarina of Time

(
w = Window.new("Play away!");
w.view.background = Color(0.1,0.4,0.1,0.8);
w.front;
// w.onClose({ "wow".postln });

x = {CombN.ar(SinOsc.ar([74,83,81,77,86].midicps*MouseY.kr(1.1,0.9),0,KeyState.kr([49,123,124,125,126],0,1,0)*MouseY.kr(0.3,0.1)),0.1,0.1,MouseX.kr(0,1))!2}.play;

CmdPeriod.doOnce({w.close});
)

//Up    - D6
//Left  - B5
//Right - A5
//Down  - F5
//Space - D5

//Control Pitch Bend+Dynamics with MouseY

//Do you want to hear what I just said again?
//Yes
//No  <--
```

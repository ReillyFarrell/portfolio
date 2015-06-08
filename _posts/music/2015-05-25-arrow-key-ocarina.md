---
layout: article
title: "Arrow Key Ocarina"
modified:
categories: music
excerpt: "Virtual instrument inspired by Ocarina of Time"
tags: []
image:
  feature:
  teaser: Brenderous.jpg
  thumb:
date: 2015-5-21
---
Simple code for a simple virtual instrument in [SuperCollider](http://supercollider.github.io/).  This code plays an array of sine waves with five different MIDI note values.  Each note in the array has a respective KeyState assignment.  Once the code is evaluated, SuperCollider will play all five notes continuously, but the volume for each is set to zero until KeyState recognizes input from an assigned key (i.e.: D5, the spacebar note, D5, is always running, but you won't hear it until you press the spacebar and release the sound).

####How to Play
- Use the spacebar and arrow keys to play.
- Move the mouse up or down to bend pitch and volume.
- Move the mouse left or right for a dryer or more echoic sound.

| Key             | MIDI Note Assignment |
|:---------------:|:--------------------:|
| Spacebar        | D5                   |
| Down Arrow Key  | F5                   |
| Right Arrow Key | A5                   |
| Left Arrow Key  | A5                   |
| Up Arrow Key    | D6                   |


####Code

{% highlight javascript linenos=table %}
//Virtual Ocarina (alto, one octave)
//inspired by The Legend of Zelda: Ocarina of Time

(
w = Window.new("Play away!");
w.view.background = Color(0.1,0.4,0.1,0.8);
w.front;

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
{% endhighlight %}

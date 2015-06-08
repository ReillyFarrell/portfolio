---
layout: article
title: "Arrow Key Ocarina"
modified:
categories: music
excerpt: "virtual instrument inspired by Ocarina of Time"
tags: []
image:
  feature: Brenderous.jpg
  credit: Brenderous
  creditlink: https://www.flickr.com/photos/brenderous/4385634645/in/photolist-pshcEE-bkoZvR-pWmMw5-pNwf5d-3ry39-dNnoLt-btww2r-dZR7R1-9G1rm8-9KXssH-cWR1if-ezT3MD-rpN5oM-cuVeLL-aFC7Jn-5YPfb6-7Fxwor-aF2nBx-dMuwP4-dqzJq-h1RyJA-2iiTWN-6oSeVY-9aUGQH-7jdisF-nWdXLS-9FfbjK-nat2E7-pTfecC-r8FKTM-cuUA6Q-4pZMH4-dhhHbk-3P9C2h-cuUViy-r2GRN8-aNEg8F-5hMCZW-9aBKW-6iXJMq-6qAEyw-5EqZez-iXqupY-f1H2DQ-6giYU-8fkLUH-dMtzCW-nx6oid-bEYSpA-nx6ofY
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

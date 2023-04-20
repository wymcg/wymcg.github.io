---
layout: posts
title:  "Replacing Vid2led"
date:   2023-04-19 20:01:00 -0400
---
> What was Vid2led, and why am I replacing it?

![Penn State IEEE's 2018 THON letters](../../../assets/images/replacing-vid2led/thon-letters.jpg){: style="float: right; padding: 10px" width="52%"}
THON is the largest student-run philanthropy in the world, where student groups from all around the Penn State community raise money for pediatric cancer.
At the event, it's customary for student groups that raised money for the event to create letters to advertise their presence at the event. 
Normally, these letters are simple pink insulation foam cutouts, occasionally with some colored lights for flair.
For most of my undergraduate career, I was involved with the Penn State IEEE Student Chapter, and we tended to go a little overboard with the letters.
To my knowledge, we were the first club to integrate individually addressable RGB LEDs into our letters, which we used to great effect.

They kicked ass. The picture doesn't do it justice.

![Penn State IEEE's 2018 THON letters](../../../assets/images/replacing-vid2led/ieee-letters.jpg)

After using them at THON and several workshops, though, the letters were fragile and tattered. We needed a replacement. 
So, for THON 2023, we ditched the tired foam letter format and decided to go big with a 3x5 foot LED matrix.

Initially, we had planned to use [WLED](https://kno.wled.ge/) to drive the matrix. 
The club wasn't prepared to put the work in to develop custom animations, and WLED showed promise in early prototypes.
Unfortunately, a few weeks before THON it became clear WLED wasn't going to cut it. 
Even worse, even if we could get something together in time, we probably wouldn't have enough time to make it do very much.

That's when I had an idea. What if, instead of programming the matrix to run some sort of predefined pattern, we programmed it to display videos?

I promise the idea isn't as stupid as it sounds. 
At the time, we didn't have many people on the team who had experience with making LED patterns with libraries such as [FastLED](https://fastled.io/). 
What we *did* have, though, is people who could edit videos and an LED matrix which was essentially a giant (although admittedly low-res) TV screen.
I got to work making the project, which I had started calling [vid2led](https://github.com/wymcg/vid2led).

By some miracle I got it working in time for THON. 
It used OpenCV to read and downscale video frames on the fly, and although it was unwieldy and ugly, it worked, and the team got to work making videos to show on the matrix.

Again, it kicked ass. The GIF doesn't do it justice.

![My personal favorite video we used on the matrix](../../../assets/images/replacing-vid2led/kirby-matrix.gif){:style="display:block; margin-left:auto; margin-right:auto"}

Vid2led worked great, but it was bloated and unstable, and needed some work if we wanted to use it long-term.
At the same time, once the rest of the club saw what an LED matrix like this could do, ideas came in from all sides.
The ideas were great, but most of them were interactive in nature.
It was becoming clear that Vid2led wouldn't cut it long-term.

[Matricks](https://github.com/wymcg/matricks) is my long-term solution. 
Matricks uses the WASM-based [Extism](https://extism.org) project to allow users to define any matrix functionality they want (within a sandbox).
Matricks aims to be more stable, transparent, and flexible than Vid2led, and even this early in development, it shows extreme promise in all three of these goals.
In early tests, I've been able to quickly define complex LED matrix behaviors, including using pre-existing Rust libraries and making REST API calls to set LED matrix state.

I'm extremely encouraged by the progress Matricks has made even in this early stage, and I'm excited to see what the team can do with it. 
If you'd like to contribute, check out the [issues on GitHub](https://github.com/wymcg/matricks/issues)!

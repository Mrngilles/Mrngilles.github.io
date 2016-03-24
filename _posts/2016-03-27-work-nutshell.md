---
layout: post
title: My work in a nutshell
description: "What I do for a living, what I want to do and why do I write"
modified: 2016-03-24
tags: [general]
---

# Who am I ?

I recently decided to start writing a blog, for multiple reasons,
which I will detail for you. But first, let me introduce myself. I am
a french guy living in Dijon (Really good wine here), and am actually
doing my PhD in optics, focusing on *optical fibers*. I mix experiments
and simulations on a daily basis. And for all of this, I use **Python**
(and more precisely, python 3). I am about to get married to a
wonderful woman who might have saved my live and opened me to a whole
new world, and I am very happy about it !

I chose to start this blog for multiple reasons. Among them, are the
will to improve myself on a personal and professional level, the wish
to communicate with other people in the community, the wish to learn
from everyone of you and the wish to share what I learn and love.

# What will I be talking about ?

My focus for now will be to create a follow-up of my development of a
[Cython](http://www.cython.org/) library for the simulation of the
propagation of optical signals in an optical fiber. I often do this
kind of simulations during my work. However, I usually have to rewrite
(or copy and modify) the whole simulation code, depending on whether I
want to add or remove physical effects, reduce the simulation time,
increase the accuracy of the simulation... I want a clean library with
the most important functions for simulation, the simulation methods,
the different physical effects that can be included, automatic saving
of the results and all that could be of use for anyone wanting to use
the library.

I wish to develop it as a [Cython](http://www.cython.org/) module
because these simulations can take quite a lot of time. I already use
[Numpy](http://www.numpy.org) and try to improve the speed of my code
as much as possible. However, using [Cython](http://www.cython.org/)
would probably improve the speed quite significantly. Also, I never
got around using [Cython](http://www.cython.org/), so this will help
me learn as I go along.

So I will be focusing on the process of development, on my learning's
day by day, and give updates about what I have been doing. I will
probably also talk about my development environment, as I think it is
something very important to take into account, for every
developer. Also, just because I love it ! I am deeply passionate by
open-source, particularly python and Linux. And I plan to get this
library out under the GNU GPLv3 license, making it available for
everyone, and most importantly, open for improvement to everyone. It
will also increase the chance that if I ever decide not to maintain it
anymore, someone can take my place as a maintainer.

After developing this library, I also plan to make a *simulation code
generator*. What I mean by that, is to create a
*library/module/something not defined* so that a
[Cython](http://www.cython.org/) code containing a custom simulation
(with the desired physical effects, simulation method, simulation
parameters...) is created on demand. Once the simulation is
*automatically* written, it will be launched with a single
command. This would probably increase the simulation speed, removing
unnecessary condition checking, generating more static code.

An other goal will be to parallelize both these previous methods so
the simulation can be launched on clusters. This will probably be
tricky, as one simulation step must use the previous step to advance
in the calculation. Having multiple simulation (which is quite
frequent if you want to observe the evolution of a parameter) will be
the easiest to parallelize, as all those simulations will be
completely independent.

In order to have a good development work flow, I will try to work in
**Behavior Driven Development**. I still need to learn about it (I
only know *Test Driven Development* for now) but I hope to be able to
learn quite a lot along the way.

I hope that we will be able to help each other ! Don't hesitate to
contact me directly for any question, remark, critic, or even just to
talk. I would really love to hear from you.

Next post, I will set up my work environment, including the setup of
my repository for the project, installing everything needed in a
virtual environment, getting the tests ready to run (with coverage),
and probably a Docker container (I absolutely love those!) to test in
a more isolated environment, and also to test that the install
procedure does not break.

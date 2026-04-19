---
date: '2026-04-19T12:12:13+07:00'
lastmod: '2026-04-19 15:02:28+07:00'
draft: false
title: 'No Casual Order'
tags: [notes]
---

In my last few posts I have been summarizing papers I've read into
digestable components, and I've hit a point where I cannot faithfully
deconstruct them perfectly. So I'm having writer's block at the moment
for my next post.

So I'm trying a new concept: publishing what inspired me as notes!

## Quantum Correlations with No Causal Order

As always, all credits to the authors, all mistakes are my own.

This paper[^1] presents a look into the weirdness of quantum mechanics
that I've felt missing since quantum teleportation, the notion of
causal structure or lack thereof. In short, with only local quantum
mechanics, you don't need to assume the world has global cause-effect
structure.

[^1]: Oreshkov, O., et al. (2013). Quantum Correlations with No Causal Order. https://doi.org/10.1038/ncomms2076

Assume the world is made up of "laboratories." Each one is isolated
from the world. Each lab receives an input system,
performs some sort of "experiment" on it and returns an output system.

{{< figure
  src="./laboratory-setting.png"
  alt="A laboratory, with an input system, the experiment and output system"
  class="insert-image"
  height="auto"
>}}

Since we're assuming local causality and local quantum mechanics,
a lab has to get an input *before* returning the output in order for
the output to be correlated to the input.

If Bob wants his results to be correlated with Alice's results, he
has to be causally *after* Alice. And therefore, you can only have
unidirectional causal relations. If Bob's result is correlated with
Alice's, Alice has to perform her experiment first. If Alice wants
her result to be correlated with Bob's, he has to perform his experiement
first.

{{< figure
  src="./alice-signal-bob.png"
  alt="Alice's lab sending output to Bob's"
  class="insert-image"
  height="auto"
>}}

A third option is correlation "together," which is both experiments
are correlated with the same input. At most these "causally separable
processes" can only be unidirectional, and a global causal relation can
be assumed.

{{< figure
  src="./causally-separable-processes.png"
  alt="Causally separable processes: states, channels, and channels with memory"
  class="insert-image"
  height="auto"
>}}

This paper presents a set of "causally non-separable processes" which
arises from this framework. Which seem to let us violate classical 
boundaries of probability.

{{< figure
  src="./causally-non-separable-processes.png"
  alt="Causally non-separable processes: postselection, local loops, channels with local loops, global loops"
  class="insert-image"
  height="auto"
>}}

The paper closes by drawing parallels to general relativity which generaliszes
the concept of flat spacetime to curved spacetime, hinting at a possible
connection between both fields.

I won't pretend to understand all the math (this is a "note" after all),
but I can see that it's definitely interesting how little we know. 
Many aspects of quantum mechanics definitely challenge the notion of
causality. Entanglement for example, 
[seem to let us communicate faster than light](/posts/2026/node-to-node-links#digression-bell-state-analyzer),
and the quantum eraser experiment letting us "erase the past." Both of
these have their own little caveats, but my point is that there is more
to see, and the puzzle pieces don't fall together that nicely.

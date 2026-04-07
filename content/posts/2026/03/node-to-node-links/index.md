---
date: '2026-04-07T18:08:05+07:00'
lastmod: '2026-04-07T21:27:48+07:00'
draft: false
title: 'Node-to-Node Links'
---

A quantum network is fundamentally, a system of interconnected quantum repeaters, each
one exchanging qubits with another. In my [last post](/posts/2026/quantum-networking/), 
we had a quick overview of the quantum network system, so in this post, let's talk more
about the links between repeaters themselves.

As with all quantum computing, this is largely theoretical and subject to change when
a physical adaptation of quantum networks is realized. This post was largely a summary
of work by Jones, C. et al. [^1] all credit goes to them and any errors are my own.

[^1]: Jones, C., et al. (2016). Design and Analysis of Communication Protocols for Quantum Repeater Networks. https://doi.org/10.1088/1367-2630/18/8/083015

## Entanglement Between Neighbors

A critical first step of performing entanglement routing is to share entanglement pairs
between neighboring nodes, whether they may be repeaters or end devices. This can be done
by one of 3 different protocols: `Meet-In-The-Middle` `Sender-Receiver` or 
`Midpoint Source`.

For this mental exercise, we examine this set up: a single link in a quantum network. 
We have a single link able to send quantum information, and a classical link able to
send classical information.

{{< figure
  src="./quantum-link.png"
  alt="A link in a quantum network from node A to B, made up of one quantum and one classical link"
  class="insert-image"
  width="700"
  height="auto"
>}}

## Digression: Bell State Analyzer

A structure that we'll see quite often in these diagrams is the humble bell state
analyzer.

{{< figure
  src="./bell-state-analyzer.png"
  alt="A bell state analyzer and its internals"
  class="insert-image"
  height="auto"
>}}

To summarize, a bell state analyzer (BSA) is a device which measures a pair of entangled 
particles and determines which bell state it is in. This measurement, as with all
quantum measurements, has a side effect of collapsing those set of particles into
bell state pairs, a set of well-known entanglement pairs, namely,
$|\Phi^+\rangle$, $|\Phi^-\rangle$, $|\Psi^+\rangle$, and $|\Psi^-\rangle$.
It also returns the result of the measurement as classical output. One constraint
that the BSA has is that both particles have to arrive at the exact same time, 
(the coincidence detection) so its inputs are subject to tight timing requirements.

For our purposes, a BSA is the device which does entanglement swapping. Input one part
of two pairs of entangled particles and the remaining parts are entangled.

{{< figure
  src="./bell-state-analyzer-measurement.png"
  alt="A bell state analyzer measuring an entangled pair leaving the remains entangled"
  class="insert-image"
  height="auto"
>}}

If you think about it, this set up seems to show you can send particles faster than
the speed of light! If you can get the timing exactly right, the particles
only travel half the distance, but the entanglement covers the whole distance.

You have entanglement across both lines, but you don't know *which* entanglement the
BSA measured. Since the entanglement of the measured particles correspond to the
entanglement of the remaining particles, both sides need to know the result of
the measurement. You need to send a classical signal signal back to both ends to 
confirm the entanglement and which entanglement. This is called **Heralding** and a
necessary part of quantum networks as you will see.

## Meet-In-The-Middle

{{< figure
  src="./meet-in-the-middle.png"
  alt="Two nodes sending photons to a central bell state analyzer. All three connected together with a classical circuits"
  class="insert-image"
  width="700"
  height="auto"
>}}

This is considered the most simple and straight forward protocol. In this set up, A and
B are placed a distance apart, with a bell state analyzer at the center. A and B are
time-synchronized.

The entanglement process is thus:

1. A and B each generate an entangled particle pair
independently. 
2. Each one sends one part of their pair to the BSA.
3. The BSA will receive both particles at the same time, and 
swaps them. Note that the swapping process happens passively by the BSA.
4. The heralding signal is then sent back to both nodes classically, 
thereby completing the entanglement process.


## Sender-Receiver

{{< figure
  src="./sender-receiver.png"
  alt="A sender node sending photons to a receiver node with a bell state analyzer. Both connected with a classical circuit"
  class="insert-image"
  width="700"
  height="auto"
>}}

The sender-receiver protocol is simply the meet-in-the-middle protocol
with the bell state analyzer moved to the receiver node.
The advantages this setup provides over meet-in-the middle is that
if the entanglement fails, the receiver knows right away, thereby
freeing quantum memory of one node. The other node's quantum memory
however, will be locked for the entire run. One other advantage is
that it's self contained. No center node is required.

## Midpoint-source

{{< figure
  src="./midpoint-source.png"
  alt="Two nodes, each with BSMs, and a central entangled source sending photons to both nodes. The two nodes are connected with a classical circuit."
  class="insert-image"
  width="700"
  height="auto"
>}}

The last protocol is the midpoint-source protocol. As the name suggests,
the source is in the middle and measurement is done at both ends.

The midpoint generates entangled protons and sends them to both ends.
The end nodes each have BSAs and swaps its own entangled pair with
the received photon, independently. The results are then classically
communicated both ways.

This may seem insane at first, you need two BSAs and a center node, and
you also need to communicate classically both ways. but its gains are
justified. It leverages the fact that photon sources are a
more mature technology than BSAs so having sources at the middle is 
less of a problem. Measuring at the endpoints also locks quantum memory
for a shorter time much like sender-receiver, but for both ends. This
faster failure also allows more trials, and a faster clock speed.

## Conclusion

Quantum entanglement generation is quite fascinating in that
its quite a bit more complicated than sending physical bits. The medium
is fragile and time sensitive, and we've not even started talking
about error correction!


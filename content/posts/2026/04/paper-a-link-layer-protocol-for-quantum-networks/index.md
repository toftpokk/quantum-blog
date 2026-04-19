---
date: '2026-04-07T18:14:07+07:00'
# lastmod: '2026-04-07T18:14:07+07:00'
draft: true
title: 'Paper: A Link Layer Protocol for Quantum Networks'
---

I had the opportunity to read "A Link Layer Protocol for Quantum Networks"
(Dahlberg, 2019) [^1]. I'll outline the paper here for my own future
reference, go read the full paper for the full context. All credits to
them, and all mistakes are my own.

[^1]: Dahlberg, A., et al. (2019). A Link Layer Protocol for Quantum Networks. https://doi.org/10.1145/3341302.3342070

This paper proposes a set of link layer protocols for quantum networking.
My [last post](/posts/2026/node-to-node-links/) outlined the physical
layer of the network stack, and this paper proposes the link layer.

{{< figure
  src="./quantum-network-stack.png"
  alt="Quantum vs classical network responsibilities"
  class="insert-image"
  height="auto"
>}}

I've illustrated the responsibilities each layer of the network has
compared to a classical network as per the paper. This is somewhat
misleading since a quantum network requires a classical control plane to
operate, and there's not exactly consesus on the quantum network stack,
but it gets the point across.

- The physical layer deals with the hardware of sending photons. It's
  responsible for timing, synchronization, and each entanglement attempt
- The data link layer is responsible for robust entanglement. Meaning
  when an entanglement is requested by an upper layer and it should make
  that happen.
- The network layer is responsible for long distance entanglement. The
  joining and management of each entangled segment, and also the routing.
- The transport layer is responsible for transmitting qubits
- The application is any quantum application: quantum computing, simulations
  etc.

## Physical Layer

This paper presents both the physical and link layers of a quantum
network. The proposed protocol uses the
[midpoint heralding protocol](/posts/2026/node-to-node-links/#meet-in-the-middle),
(from here on referred to as MHP) but any other physical layer should be
possible.

The physical layer's operation is divided into timeslots, each one
is a single MHP cycle.

The physical layer is a protocol built on top of the physical infrastructure,
and the link layer protocol is hardware agnostic. The physical layer in
this paper uses the
but any physical layer is possible.

It's operation is divided into timeslots, each running 1 MHP cycle.
  
## Link Layer

The link layer is a service that takes in requests and creates an
entangled link. This is done by prompting the physical layer to attempt
entanglement until it succeeds.


{{< figure
  src="./link-layer-quantum-entanglement.png"
  alt="Network layer sending a create request to the link layer, and the link layer triggering the physical layer and relaying the result"
  class="insert-image"
  width="700"
  height="auto"
>}}

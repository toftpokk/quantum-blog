---
date: '2026-07-26T16:34:03+07:00'
lastmod: '2026-07-26T16:34:03+07:00'
title: 'Paper: A Link Layer Protocol for Quantum Networks'
tags: [notes]
---

I had the opportunity to read "A Link Layer Protocol for Quantum Networks"
(Dahlberg, 2019) [^1]. I'll outline the paper here for my own future
reference, go read the full paper for the full context. All credits to
them, and all mistakes are my own.

{{< figure
  src="./a-link-layer-protocol-overview.png"
  alt="Link Layer Protocol vs Other Layers"
  class="insert-image"
  height="auto"
>}}

[^1]: Dahlberg, A., et al. (2019). A Link Layer Protocol for Quantum Networks. https://doi.org/10.1145/3341302.3342070

This paper proposes a link layer protocol for quantum networking, 
called the EGP, entanglement generation protocol.
My [last post](/posts/2026/node-to-node-links/) outlined the physical
layer of the network stack in theory. This paper realizes both
the physical and link layer protocols in tangible form.

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

- **The Physical Layer**: deals with the hardware of sending photons. It's
  responsible for timing, synchronization, and each entanglement attempt
- **The Data Link Layer** is responsible for robust entanglement. Meaning
  when an entanglement is requested by an upper layer and it should make
  that happen.
- **The Network Layer** is responsible for long distance entanglement. The
  joining and management of each entangled segment, and also the routing.
- **The Transport Layer** is responsible for transmitting qubits
- **The Application Layer** is any quantum application: quantum computing, simulations
  etc.

This paper presents both the physical and link layers of a quantum
network. The proposed physical protocol uses the
[midpoint heralding protocol](/posts/2026/node-to-node-links/#meet-in-the-middle),
(from here on referred to as MHP) but any other physical layer should 
be possible.

## Physical Layer

The physical layer's operation is divided into timeslots, each one
is a single MHP cycle.

{{< figure
  src="./physical-layer.png"
  alt="The Physical Layer Midpoint Heralding Protocol Cycle"
  class="insert-image"
  width="700"
  height="auto"
>}}

The diagram looks quite complicated, but it breaks down into three steps

- The node's physical layer polls the link layer to see if it needs to
  create an entanglement (1 and 2)
- The node sends a photon to the heralding station, sending additional
  metadata, the queue ID, which we'll get to later (3 and 4)
- The heralding station swaps the photon and if the metadata is correct
  and it receives the photons in time, it does a quantum swap sending
  the results back to the node, which the physical layer relays to the
  link layer (SWAP, 5, and 6)
  
The choice of polling in this protocol is interesting.

{{< figure
  src="./physical-layer-timeline.png"
  alt="A Timeline of Multiple Midpoint Heralding Protocol Cycles"
  class="insert-image"
  width="700"
  height="auto"
>}}

Plotting this in a timeline as above, we can see that the link layer
can have multiple ongoing entanglement requests.
And the physical layer, being time-slotted, can fulfill a request
at full throttle. Thereby, making these two layers fully independent.

The trade-off is the time delay between the generation itself and the
response, which is guarateed to be a cycle or more, as illustrated.
Also, there can be only one entanglement generation per time slot.

This cycle pattern is not new. It's used in various classical 
protocols as well. I want to draw parallel to bluetooth which uses
slotting to split a channel between transmission and reception.

## Link Layer

The link layer is a service that takes in requests and creates an
entangled link. This is done by prompting the physical layer to attempt
entanglement until it succeeds.

{{< figure
  src="./link-layer-quantum-entanglement.png"
  alt="The Entanglement Generation Protocol's Relationship with Other Components"
  class="insert-image"
  width="700"
  height="auto"
>}}

From the last post, we know that a heralding station is just a bell
state analyzer. It requires photons to arrive at the exact same time
to swap them. So how does the physical layer know which slot to send
photons so that they arrive on time? The midpoint heralding protocol
does not answer this, as we've seen. The responsibility of coordination
lies with the entanglement generation protocol.

A key component of the entanglement protocol which does this is the
distributed queue. A distributed queue is a queue which is distributed
among nodes all nodes. When a CREATE request comes from a higher layer,
the master node decides the queue order and passes along this information
to the slave nodes. The MHP will then be able to create entanglement
on the right photons.

The quantum MMU is the storage component of the equation, storing the
'static' half of the entanglement pair.

Finally, the fidelity estimation unit measures the fidelity of the
entanglement pair after this process. This fidelity property warrants
a post about quantum fidelity, but essentially, it's a measure of the
quality of the entanglement from noise, decoherence, etc.

The protocol itself is quite straight forward, with complexity from
the multiple components, and the different error cases.

- a CREATE request from a higher level protocol is invoked, and the node
  adds it to the distributed queue
- When the MHP polls, the scheduler selects an entanglement request
  to be made, generating a pair from the MMU to be swapped.
- When the MHP replies, store the result, and emit an OK back to the
  higher level protocol, including the fidelity estimate

Error cases include, timeouts, rejection, among others.

If you're used to classical networking, it would seem like the protocol
is not really sending any information. It's generating an entanglement
pair within itself, swapping, and returning OK. That's because the entire
point is to create an entanglement channel between two points. When you
start passing information, namely qubits, you don't send anything
through these repeaters, only using the resulting entanglement.

It will be clearer with the higher levels of the quantum network stack.

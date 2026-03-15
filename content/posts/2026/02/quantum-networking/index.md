---
date: '2026-02-22T21:13:12+07:00'
lastmod: '2026-03-14T12:15:31+07:00'
draft: false
title: 'Quantum Networking'
---

Quantum computing, much like classical computing is limited when doing
computation on a single machine. Today, you don't really feel that since
only having 1000 physical qubits on a single machine is the state of the
art [^1]. But for future use cases and with more qubits to work with,
more importantly increased resource requirements, having a way to
communicate between them is a neccessity. This is why some are working
towards quantum communication, including myself.

[^1]: IBM Condor is 1,121 qubits. https://en.wikipedia.org/wiki/IBM_Condor

Since qubits are very fragile things, and with physical limitations
for example, the no-cloning theorem which forbids copying of qubits,
qubits are very hard to work with. Sending them between locations
hundreds of kilometers apart practically guarantees loss of information.
So, the agreed upon method for sending qubits is by using entanglement.

{{< figure
  src="./a-b-diagram.png"
  alt="Two computers communicating over a network"
  class="insert-image"
  width="700"
  height="auto"
>}}

## Entanglement
The idea is, instead of computer A sending qubits to computer B directly,
the two computers entangle qubits with eachother and send the target
qubit via quantum teleportation. This allows the connection to fail
and recover without losing any information. Entanglement may fail over
and over, but you won't lose data. It also lets you decouple the network 
logic and the sending of data from eachother. You can use any network
path, redo or purify as much as you want and still guarantee the qubit
is delivered. This also opens up more complex operations like multiplexing,
and purification which we will talk about later.

Creating this entanglement is the crux of quantum networking. Much like
classical networking, there are a myriad of ways to establish a
connection between parties and maintain it.

{{< figure
  src="./a-b-entanglement-2.png"
  alt="Entanglement swapping between two computers"
  class="insert-image"
  width="700"
  height="auto"
>}}

## The Quantum Repeater

{{< figure
  src="./a-b-repeater.png"
  alt="Two computers communicating through a repeater"
  class="insert-image"
  width="700"
  height="auto"
>}}

Much like the sending of qubits themselves, entangled particles are
also fragile over long distances. That is why a repeater is needed.

A quantum repeater differs from a classical repeater because of the
quantum nature of the quantum data itself. As qubits cannot be copied
entangled or otherwise, a quantum repeater has to use a different
strategy: entanglement swapping.

When entangled particles are sent to a repeater, it "swaps" them.
This swapping results in entangled particles from both ends becoming
entangled.

{{< figure
  src="./entanglement-swapping.png"
  class="insert-image"
  alt="Entanglement swapping process"
  height="auto"
>}}

Quantum repeaters and entanglements form the backbone of a quantum
network. We will talk more about how repeaters coordinate with eachoter
and how it forms the quantum network as a whole.

---
date: '2026-02-22T21:13:12+07:00'
# lastmod: '{{ .Date }}'
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
thousands of kilometers apart practically guarantees loss of information.
So, the agreed upon method for sending qubits is by using entanglement.

{{< figure
  src="./quantum-networking-1.png"
  alt="Two computers communicating over a network"
  width="700"
  height="auto"
>}}

## Entanglement
The idea is: instead of computer A sending qubits to computer B directly,
the two computers entangle qubits with eachother and send the target
qubit via quantum teleportation. This lets the connection be able to fail
and recover without losing any information. Entanglement may fail over
and over, but you won't lose data. It also lets you decouple the network 
logic and the sending of data from eachother. You can use any network
path, redo or purify as much as you want and still guarantee the qubit
is delivered.

Creating this entanglement is the crux of quantum networking. Much like
classical networking, there are a myriad of ways to establish a
connection between parties and maintain it.

{{< figure
  src="./quantum-networking-2.png"
  alt="Entanglement swapping between two computers"
  width="700"
  height="auto"
>}}

## Quantum Repeater

{{< figure
  src="./quantum-networking-3.png"
  alt="Two computers communicating through a repeater"
  width="700"
  height="auto"
>}}

Much like the sending of qubits themselves, entangled particles are
also fragile over long distances. That is why a repeater is needed.

A quantum repeater is a device which does a few things[^2]. First it
creates two entangled pairs, between the repeater and both computers
connected to it. Second, it does entanglement swapping between those
two connections. Third, it handles errors. Finally, it participates
in network operations. Let's break this down.

[^2]: Meter, R.V. (2021). A Quantum Internet Architecture. https://arxiv.org/abs/2112.07092

Creating the base entanglements is just creating two pairs of
entangled particles, keeping one particle of each pair and sending the
others to either side. This is commonly done by using bell pairs


[^X]: Jones, C. et al. (2016). Design and analysis of communication protocols for quantum repeater networks. doi:10.1088/1367-2630/18/8/083015


---
layout: single
title:  "Entanglement barriers in dual-unitary quantum circuits"
date:   2022-06-19
---

*The unwieldy title belies surprisingly simple and deep behaviour, pertaining to how quantum entanglement propagates over time in a 1D system of interacting qubits. This review is intended to capture the essence of the results first reported in [this PRB paper](https://journals.aps.org/prb/abstract/10.1103/PhysRevB.104.014301), but will forgo the gory mathematical details. The interested (masochistic?) reader is invited to peruse the original paper [here](https://doi.org/10.48550/arXiv.2103.12794).*

**Introduction and motivation**

Quantum entanglement is the fundamental hallmark that distinguishes the quantum world from the classical. Famously described by Einstein as ‘spooky action at a distance’, it expresses the fact that, in general, measuring one part of a composite system will affect any subsequent measurements on another part. This is a consequence of the collapse of the wavefunction. 

For simplicity, the paper considers a one dimensional system of qubits[^1]: the quantum analog of the classical binary bit, which can exist as a superposition of two possible states. This might include e.g. the spin of an electron or the polarisation of a photon. 

The number of possible states in such a system undergoes a combinatorial explosion as the number of constituent qubits increases, growing as $2^N$ for $N$ qubits. This is an example of the so-called ‘curse of dimensionality’. It makes the system's behaviour, including its quantum entanglement, very difficult to describe -- especially when spins are permitted to interact.


One useful task is to characterise the *dynamics of quantum entanglement*, i.e. how it propagates and changes in time. We consider a system being driven *out of equilibrium*, meaning energy is pumped into it, and with *local interactions*, so that spins only 'talk' to others that are nearby. This is intrinsically interesting because it's very hard[^2]. It is also practically important: entanglement is the fundamental resource of quantum computing, and understanding its behaviour is likely to be essential to using it with any purpose.


A good subcase to consider is the quantum entanglement of the reduced density matrix[^3]. This is because it’s known to have zero entanglement at both early times (by choosing an unentangled initial state) and late times (when we’ve pumped in lots of energy and the system has 'thermalised'). The entanglement of this particular quantity begins and ends at zero; we just have to characterise the shape of the so-called *entanglement barrier* in between. 

**Problem setup**

This remains a very general question -- in fact, prohibitively so -- and we need to be more specific to make progress. In particular, we must pin down 1) the nature of our initial state, and 2) how it evolves in time.

A good choice is to start with a so-called 'matrix product state', which is a low-entanglement state composed of a series of matrices multiplied together. For simplicity, it can be constructed from a pair of alternating matrices. It has this compact graphical representation, where you can think of the emerging 'legs' as associated with a particular spin. 

![Initial state](/hello/assets/initial_state.jpeg){: .align-center style="width:60%;"}
 
We evolve it in time (i.e. encode its interactions) by multiplying the state by 'time-evolution gates'. For a local, periodic Hamiltonian, the result for the new state after time $t$ looks like this[^4],

![Evolved state](/hello/assets/evolved_state.jpeg)

The red quantum gate encodes all the dynamics of the system. To emphasise: we take the initial state, represented by a ton of matrices multiplied together in one axis (space), and evolve it by multiplying in the other axis (time) with time-evolution operators, the number of which corresponds to the time elapsed.

We demand two further technical but very important conditions: *solvability* of the initial state and *dual-unitarity* of the evolution matrix. Both are reasonably non-restrictive but are needed to make the problem concrete. They can be represented by these mathematical expressions:

![Solvability](/hello/assets/conditions.jpeg){: .align-center style="width:60%;"}


Now we know the form our state adopts at different times, we can calculate the entanglement entropy[^5] $S(t)$ using the mathematical form

$$
S(t)=-\log \textrm{Tr}(P(t)^2)
$$ 

where $P(t)$ is the 'super-operator' constructed from the reduced density matrix, itself reduced to one subsystem of interest. This is mathematically technical and very jargon-heavy, but the important thing is that, using the dual-unitarity rule, the entanglement at a given time can be represented by this graphical form.

![Entropy expression](/hello/assets/full_form.jpeg)

$t$ is the number of time steps elapsed, and $l$ and $x$ are related to the size of the subsystem we're interested in. 

**Counting loops in spacetime**

At this point, we're all but done. An intractable mathematical problem has been reduced to taking the diagram above and using simple graphical rules of dual-unitarity and solvability to contract it down. At any given time, you end up with a number of closed loops in spacetime, each contributing a factor of 2 to the final result [^6]. You just have to count the loops. 

Following it through, you end up with this graph. 

![Entropy graph](/hello/assets/graph.jpeg)

The quantum entanglement initially rises linearly, plateaus, then falls to zero. The exact behaviour of the decline phase depends on the choice of dual-unitary quantum gate; I've included a couple of examples described in detail in the paper. 

Remarkably, the result is exact: a very rare trait in non-equilibrium quantum mechanics. 

**Comments**

What I like about this work is that we take a complex mathematical problem and convert it into something geometrical and intuitive. Something opaque, technically demanding and jargon-heavy boils down to a pictorial puzzle, using 3 simple rules to simplify a diagram in a game of quantum Tetris. You end up with some number of closed loops, which you count to measure the entanglement (more loops = more entangled). The result is elegant, general, deep and informative. 

I like the fact that the motivation is almost aesthetic. With a small set of judicious assumptions and a clever geometric framing, a strikingly simple and far-reaching result emerges from a sea of unforgiving mathematics. It reminds me of the philosophy of Feynman diagrams, or the famous ‘warped rubber sheet’ intuition of General Relativity.

I’d love to see what over hitherto intractable quantities might be amenable to this kind of neat geometrical thinking — e.g. entropic quantities in Machine Learning, which are often approximated (and not always well!) during Bayesian optimisation.

[^1]: The generalisation to 'qudits', which instead have $N>2$ levels, is actually very straightforward and is done in the paper.
[^2]: Technical elaboration: historically, analytic results in nonequiliblirum many-body quantum physics have proved elusive. Progress has been made in integrable theories by mapping problems onto free fermonic systems, but these are characterised by an infinite number of conservation laws so more generic (chaotic) systems may display qualitatively different features. Study of the class of random unitary quantum circuits, able to probe quantum dynamics beyond integrability and incorporate local interactions, provides an alternative approach. Our results, derived using the dual-unitary class of lattice model, give a further exact benchmark for entanglement dynamics in many-body quantum systems.
[^3]: Formally, this is the `operator space entanglement entropy' (OSSE), because the reduced density matrix is an operator rather than a state. But this makes little practical difference -- you just 'vectorise' the operator, heuristically by folding the matrix into a vector, then calculate the entanglement entropy as usual.
[^4]: Here, we've adopted a so-called 'binary drive' approach, dividing each timestep into two halves where alternate pairs of sites are coupled. It's popular in the literature but isn't the only choice.
[^5]: Specifically, the Renyi entropy.
[^6]: This is because the closed loop represents a trace over an $N \times N$ identity matrix, with $N=2$ in the case of qubits. 

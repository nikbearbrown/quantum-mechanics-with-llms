# Quantum Mechanics+1: Interactive Simulations with Claude and D3

**Nik Bear Brown** · Bear Brown, LLC · 2026
**Series:** +1 Series — AI-Augmented Undergraduate STEM

*A simulation-first textbook for the second course in undergraduate quantum mechanics. Pair with Griffiths. Every chapter ends with an LLM Exercise that produces a working D3.js simulation you can modify in real time.*

---

## What this book is

Undergraduate quantum mechanics is hard not because the math is hard but because the objects have no classical analogues, and a textbook composed entirely of equations gives the student no way to develop intuition for objects whose behavior contradicts every classical instinct. Interactive simulation closes the gap. A student who has watched a wave packet spread, tuned a potential well, animated a probability collapse, seen Larmor precession run at a real frequency, and tracked the Bloch vector spiraling inward under decoherence has physical intuition that no amount of lecture can supply.

The **+1 layer** is what makes this book different from Griffiths or Shankar: at the end of every chapter, an LLM Exercise block produces a working D3.js simulation. You read it, verify it, modify it, and answer the chapter's exploration tasks by watching the simulation respond. Claude writes the SVG that displays your question. You decide what the question is.

The central argument: *the simulation is a question*. Every simulation in this book is constructed to answer one specific physics question the standard textbook does not put in front of you. The Bloch sphere with ensemble-measurement mode is constructed to answer "is the Heisenberg uncertainty principle about disturbance or about preparation?" The hydrogen orbital visualizer with $r_{mp}$ and $\langle r\rangle$ marked separately is constructed to answer "is the orbital a path?" Your job is to answer.

## Who this book is for

Junior or senior physics, chemistry, or engineering majors taking a second course in quantum mechanics. You've had modern physics or an introductory QM course (photoelectric effect, Bohr model, de Broglie). You're comfortable with calculus through ODEs. Linear algebra is helpful but not required — introduced as needed in Chapter 4. You can paste a prompt into Claude.

Not for: a first exposure to QM; a graduate-level course; a course in computational physics or D3.

## How to read it

Cover to cover, in order, the first time. The chapters compound: Chapter 4's Robertson derivation reappears in Chapter 6's spin uncertainty, in Chapter 7's hydrogen radial-momentum trade-off, and in Chapter 11's tunneling-time question. **Run every simulation.** The book without the simulations is a book about physics intuition without the physics intuition.

Each chapter ends with five closing features in order: a mechanism deep-dive, exercises (at least one Apply-or-above and one that produces an artifact), "What would change my mind," "Still puzzling," and the LLM Exercise (the simulation). Read them in that order.

## Table of Contents

**Front matter** — Title · Copyright · Dedication · Preface (~750 words)

**Chapter 0 — Introduction** (~2,000 words; cold open at MIT, central argument, chapter map, AI essai, closing return)

### Act One — The Quantum World

| # | Title | Signature simulation |
|---|-------|----------------------|
| 0 | How to Use the Simulations | Free-particle Gaussian wave packet — three-stacked-panel ($\|\psi\|^2$, Re ψ, Im ψ) |
| 1 | The Wave Function | Three-panel + live $\sigma_x\sigma_p/(\hbar/2)$ readout |
| 2 | The Time-Independent Schrödinger Equation | Energy diagram with $\psi_n$ + dynamic $\|\Psi\|^2$ + "draw your own $\psi(x,0)$" |
| 3 | The Harmonic Oscillator | $\psi_n$ + coherent-state mode (Gaussian that doesn't spread) |

### Act Two — Formalism and Standard Systems

| # | Title | Signature simulation |
|---|-------|----------------------|
| 4 | Formalism: Dirac Notation and Operators | Bloch sphere + measurement-statistics mode (Robertson bound from ensemble) |
| 5 | Quantum Mechanics in Three Dimensions | Spherical harmonics polar cross-section + pseudo-3D mesh |
| 6 | Spin | Bloch sphere + Stern-Gerlach + Larmor precession at $\omega_L = \gamma B_0$ |
| 7 | The Hydrogen Atom | 3D orbital visualizer with $r_{mp}$ and $\langle r\rangle$ marked separately + transitions panel |
| 8 | Identical Particles | Two-particle $\|\psi(x_1, x_2)\|^2$ heat map + Pauli node along $x_1 = x_2$ |
| 9 | Time-Independent Perturbation Theory | Anharmonic oscillator with PT-divergence warning + Stark $n=2$ four-level matrix |
| 10 | Time-Dependent Perturbation Theory and Transitions | Rabi oscillation exact-vs-PT collision + continuum → Golden Rule transition |

### Act Three — Methods and Modern Connections

| # | Title | Signature simulation |
|---|-------|----------------------|
| 11 | The WKB Approximation and Tunneling | Crank-Nicolson tunneling wave packet — "the visualization that cannot be replicated in print" |
| 12 | Entanglement and Quantum Information | Bell-inequality simulator with live $S$ value flipping background on $\|S\|>2$ |
| 13 | Capstone: Quantum Mechanics in Research | Router-tabs explorer: decoherence Bloch + surface code + NV-ODMR + topology |

**Back matter** — Acknowledgments · About the Author · Per-chapter Notes · References (~85 entries) · On the Absence of an Index · Glossary (~30 terms) · Errata

## About the Author

**Nik Bear Brown** is an Associate Teaching Professor at Northeastern University's College of Engineering. He teaches data science, AI, computational physics, visualization, virtual environments, and graduate courses on AI-augmented learning. He is the architect of the **Brutalist** system for AI-assisted creative production — the renderer-agnostic framework whose D3 simulation module is this book and whose other modules include *Brutalist After Effects × Claude*, *Brutalist Blender × Claude*, and *Brutalist Remotion × Claude*. PhD in computer science (UCLA), with computational and systems biology as major field and AI/statistics as minor fields. He writes at [nikbearbrown.com](https://www.nikbearbrown.com) and [skepticism.ai](https://www.skepticism.ai). Reach him at [bear@bearbrown.co](mailto:bear@bearbrown.co).

## Companions

**Pair with a primary text.** Griffiths *Introduction to Quantum Mechanics* (3rd ed.) is the canonical pairing — every chapter of this book maps explicitly to Griffiths sections in the Reading Map. Liboff *Introductory Quantum Mechanics* and Shankar *Principles of Quantum Mechanics* also work.

**Brutalist system documentation:** [brutalist.art](https://www.brutalist.art/). Chapter 0 builds your local CLAUDE.md / DESIGN.md / PROJECT.md from scratch. The system docs explain the renderer-agnostic architecture in more depth.

**Medhavy integration:** [medhavy.com](https://www.medhavy.com/) (मेधावी — Sanskrit for "intelligent" or "intellectually brilliant"). An AI-powered intelligent textbook platform that indexes this book semantically. Search a concept and Medhavy surfaces the chapter that teaches it.

## Copyright

Copyright © 2026 Nik Bear Brown. All rights reserved.

Published by Bear Brown, LLC.

No part of this publication may be reproduced, distributed, or transmitted in any form or by any means without the prior written permission of the publisher, except in the case of brief quotations in critical reviews and certain other noncommercial uses permitted by copyright law. See [LICENSE.md](./LICENSE.md) for full terms.

ISBN: [INSERT ISBN]
First edition: 2026.

## Contact

Permissions · Errata · Adoption · Course integration: [bear@bearbrown.co](mailto:bear@bearbrown.co)

---

*The simulation is a question. Your job is to answer it.*

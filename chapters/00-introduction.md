# Introduction

A junior at MIT, two weeks before finals, asked her quantum mechanics TA a question that she had not been able to find the answer to in three months of working through Griffiths. She had derived the wave functions of the hydrogen atom on paper. She had integrated $|\psi_{100}(r)|^2$ and computed the expectation value $\langle r\rangle = 3a_0/2$. She knew the answer to the question on the problem set. What she did not know — what she had not been taught how to find out — was where the electron actually was. Not the position eigenvalue. Not the expectation value. The thing the orbital was a picture of. Was the electron at $a_0$? Was it at $3a_0/2$? Did it move between them? Did "between" even mean anything? She had three months of correct calculations and no physical picture. The TA, who had her PhD in condensed-matter theory, opened a window in her browser, typed a prompt into Claude, and produced an interactive simulation of the 1s orbital with a radial probability slider and live markers for $r_{mp} = a_0$ and $\langle r\rangle = 3a_0/2$. The student looked at the screen for forty seconds. Then she said, "Oh. So those are two different facts about the same distribution." Three months of calculation collapsed into intuition in less than a minute, because for the first time she had been allowed to *see* what she had been computing.

This book is about the gap between the math of quantum mechanics and the intuition for what the math describes.

The central argument: undergraduate quantum mechanics is hard not because the mathematics is hard but because the objects have no classical analogues, and a textbook composed entirely of equations and prose gives the student no way to develop intuition for objects whose behavior contradicts every classical instinct they have. Interactive simulation closes that gap. A student who has watched a wave packet spread, tuned a potential well, animated a probability collapse, seen Larmor precession run at a real frequency, and tracked the Bloch vector spiraling inward under decoherence has physical intuition that no amount of lecture can supply. The simulations are not decoration on the equations. The simulations *are* the second half of the explanation.

This book is for the second-semester quantum mechanics student. You have had modern physics or an intro quantum course. You know about the photoelectric effect and the Bohr atom. You can solve a first-order ODE. You can probably tell me what an eigenvalue is. You have heard of the Schrödinger equation. You may or may not have linear algebra. You have not yet built physical intuition for what wave functions actually do.

## What this book is

A textbook for the second course in undergraduate quantum mechanics, designed to be paired with a standard reference text (Griffiths *Introduction to Quantum Mechanics*; Liboff *Introductory Quantum Mechanics*; Shankar *Principles of Quantum Mechanics*). The vocabulary it teaches is the standard vocabulary — wave functions, operators, Dirac notation, the hydrogen atom, perturbation theory, entanglement. The work it adds is the **+1 layer**: at the end of every chapter, an LLM Exercise block produces a working D3.js simulation the student can modify in real time to develop physical intuition the math by itself cannot supply.

Fourteen chapters, one chapter per week of a 15-week semester. Each chapter ends with:

1. **A CLAUDE.md snippet** — the coding constitution for that chapter's simulation, governing language, library, layout conventions, and what the model must verify.
2. **A simulation prompt** — copy-paste-ready into Claude, producing a working D3 simulation that takes ~5 minutes to generate and 0 minutes to modify thereafter.
3. **Exploration tasks** — specific parameter changes the student makes, with specific physics questions the simulation answers.
4. **Extension prompts** — follow-up prompts adding one feature or connecting to the next chapter.

The simulations are not optional. They are the load-bearing pedagogy. Skip them and the book is half a book.

## What this book is not

It is not a first exposure to quantum mechanics. You should have completed modern physics or its equivalent before opening Chapter 1.

It is not a graduate quantum mechanics text. Sakurai and Cohen-Tannoudji do that job; this book does not.

It is not a course in computational physics. You will not learn finite-element methods, density-functional theory, or Monte Carlo simulation. You will learn to direct Claude to write working D3 simulations and to verify what Claude wrote.

It is not a course in D3 or in web development. You will write very little code yourself. You will read what Claude writes, verify it physically, and request modifications. The book is about physics judgment, not coding.

It is not a replacement for Griffiths or another rigorous reference. Pair this book with one. Use this book's simulations to build intuition; use the reference text to develop technical command.

Prerequisites: calculus through ODEs; introductory physics (waves, electromagnetism); one prior semester of modern physics or intro QM (photoelectric effect, Bohr model, de Broglie). Linear algebra helpful but not required — introduced as needed in Chapter 4. Basic comfort with a command line and pasting prompts into Claude.

## A central concept that runs throughout

Watch for one phrase across the chapters: **the simulation is a question**. Every simulation in this book is constructed to answer one specific physics question that the standard textbook does not put in front of you. The Chapter 4 Bloch sphere with ensemble-measurement mode is constructed to answer "is the Heisenberg uncertainty principle about disturbance or about preparation?" The Chapter 7 hydrogen orbital visualizer with $r_{mp}$ and $\langle r\rangle$ marked separately is constructed to answer "is the orbital a path?" The Chapter 11 Crank-Nicolson tunneling animation is constructed to answer "what does a wave packet actually do at a barrier?" Treat every simulation as a question the chapter is asking. The exploration tasks are the chapter's way of asking that question to you. Your job is to answer.

## A running thread: the four-move prompt

A second concept that recurs: every simulation prompt follows the same four-move structure. **Move 1 — physical setup**: what system, what Hamiltonian, what initial state. **Move 2 — what the simulation must show**: which observables, which panels, which sliders, what visual mapping. **Move 3 — what the simulation must verify**: normalization preservation, expectation-value drift, dispersion-relation correctness, the named LLM failure modes. **Move 4 — what the extension is**: the one specific feature to add that connects to the next chapter or to a research direction. By Chapter 13 you will write these four moves without consulting the template. That is the working skill.

## How this book is organized

Fourteen chapters in three acts.

**Act One — The Quantum World (Chs 0–4): from "I passed modern physics" to "I understand what a wave function does."**

- **Chapter 0** sets up the Brutalist system (CLAUDE.md, DESIGN.md, PROJECT.md) and gets you from zero to a working free-particle wave-packet simulation before any new physics.
- **Chapter 1** introduces the wave function and the Born rule, with a simulation that displays $\sigma_x \sigma_p / (\hbar/2)$ as a live readout.
- **Chapter 2** derives the time-independent Schrödinger equation from the infinite square well and lets you draw your own initial superposition.
- **Chapter 3** solves the harmonic oscillator two ways (ladder operators and analytic) and introduces coherent states as non-spreading Gaussians.
- **Chapter 4** pivots to the abstract formalism — Dirac notation, Hermitian operators, the Robertson uncertainty derivation — visualized through a Bloch sphere with measurement-statistics mode.

**Act Two — Formalism and Standard Systems (Chs 5–10): from "I can solve the box" to "I can solve any central-force problem."**

- **Chapter 5** extends to three dimensions with central potentials and the spherical-harmonics visualizer.
- **Chapter 6** introduces spin, the Pauli matrices, and Larmor precession at $\omega_L = \gamma B$ with concrete clinical-MRI numbers.
- **Chapter 7** solves the hydrogen atom and shows the $r_{mp} \neq \langle r\rangle$ contrast that the MIT student saw in the opening scene.
- **Chapter 8** introduces identical particles, the Slater determinant, and the helium singlet-triplet splitting.
- **Chapter 9** introduces time-independent perturbation theory with the Stark effect on $n=2$ hydrogen as the degenerate-PT worked example.
- **Chapter 10** introduces time-dependent perturbation theory and derives Fermi's golden rule (correctly attributed to Dirac 1927) with Rabi oscillation as the visual pivot.

**Act Three — Methods and Modern Connections (Chs 11–13): from "I can solve textbook problems" to "I can attack real physics."**

- **Chapter 11** introduces WKB and tunneling, with a Crank-Nicolson wave-packet animation that cannot be replicated in print.
- **Chapter 12** introduces entanglement, Bell states, and the CHSH inequality — with a Bell-violation simulator that displays the live $S$ value with the Tsirelson bound marked.
- **Chapter 13** is the capstone, mapping the formalism you've built to five current research directions (decoherence, quantum computing, error correction, NV magnetometry, topology) via a router-tabs simulation explorer.

## How to read this book

Cover to cover, in order, the first time through. The chapters compound: Chapter 4's Robertson derivation is invoked in Chapter 6's spin uncertainty, in Chapter 7's hydrogen radial-momentum trade-off, and in Chapter 11's tunneling-time question. Reading out of order leaves the simulations dependent on machinery you have not yet built.

Run every simulation. The book without the simulations is a book about physics intuition without the physics intuition.

Every chapter ends with five closing features. Read them in order:

1. **The mechanism deep-dive in Section 4 or 5.** The chapter's load-bearing derivation. Step through with a pen.
2. **The exercises (Section 6).** At least one Apply-or-above. At least one produces an artifact.
3. **What would change my mind (Section 7).** One paragraph naming the specific empirical finding that would force revision of the chapter's central claim. This is the chapter applying its own method to itself.
4. **Still puzzling (Section 8).** Two-to-four open questions the chapter raises but does not resolve. Honest about the limits.
5. **The LLM Exercise (Section 9).** The simulation. Run it. Modify it. Answer the exploration tasks.

## A note about AI

This book is about using AI to learn quantum mechanics. It is also about what AI cannot supply.

The Claude system (and others — ChatGPT, Gemini, Llama) will produce a working D3 simulation of any quantum-mechanical system you can describe precisely. That capability did not exist five years ago. It exists now, and it changes the shape of undergraduate quantum mechanics pedagogy in one specific way: the bottleneck has moved upstream. The hard part is no longer "how do I write a simulation of the harmonic oscillator." The hard part is now "do I understand the harmonic oscillator well enough to specify what the simulation must show, and to verify that what it produces is correct?"

That second question — *can you verify what the model wrote?* — is the load-bearing skill this book teaches. Every simulation prompt in this book contains a verification block: what the simulation must conserve (normalization, expectation values), what the simulation must reproduce (known exact results), what specific physical errors the LLM tends to make at this concept (sign errors, normalization drift after parameter changes, FFT convention mismatches, painter's-algorithm sorting failures, Hermite-polynomial overflow at high $n$, units silently swapped). The student who knows what to check is the student who can use Claude well. The student who does not know what to check ends up with polished, professional, plausible code that computes the wrong thing.

This matters most in undergraduate physics specifically. A polished plot of "the harmonic oscillator wave function" with the wrong normalization, or with $\psi$ plotted where the chapter meant $|\psi|^2$, or with $v_g$ swapped with $v_p$, looks correct to a student who has not yet developed the visual reflex for what the correct answer should resemble. The simulation could ship a misconception more powerful than any wrong sentence in a textbook, because the student sees the plot and updates their intuition from it. The cost of a wrong simulation is higher than the cost of a wrong sentence; the simulation is what the student remembers. So the discipline of verification — built into every LLM Exercise as a non-negotiable Move 3 — is the discipline that makes the +1 pedagogy work.

The Brutalist system you build in Chapter 0 (CLAUDE.md, DESIGN.md, PROJECT.md) is the apparatus that holds this boundary. CLAUDE.md tells Claude what coding rules to follow: D3 v7, SVG only, vanilla JS, no Canvas, function-style, parameter exposure, real-time redraw via requestAnimationFrame. DESIGN.md tells Claude what the simulation must look like: Viridis for densities, RdBu for signed amplitudes, axis labels, slider styling, legend conventions. PROJECT.md tells Claude what state the project is currently in: chapter, sim variant, parameter ranges, verifications passed, open issues. These three files travel with you through all fourteen chapters. They are why the simulations in Chapter 12 look like the simulations in Chapter 1 — same conventions, same verification discipline, same boundary.

The boundary is the point. Claude does not decide what the physics means. You do. Claude does not decide what to verify. You do. Claude does not decide whether the simulation is correct. You do. The simulation is your question, made interactive. The model writes the SVG that displays your question. The model does not answer the question. That work is irreducibly yours.

Quantum mechanics has always been a discipline that punished students who confused calculation with understanding. The simulations make the gap between calculation and understanding more visible, faster, more often. This is not a substitute for the textbook. It is a substitute for the unbridgeable distance between what you can calculate and what you can see.

## Closing return

It is December. The MIT student from the opening scene has her oral exam in three days. She is sitting at her kitchen table at 11:18 p.m. with her Griffiths open to Chapter 4 and her laptop open to Claude. She types: *"Build me a hydrogen orbital visualizer that shows the radial probability $P(r) = r^2 |R_{n\ell}|^2$ with the most-probable radius and the expectation value marked as separate vertical lines. Let me change n and ℓ with sliders."* Forty seconds later the simulation is in front of her. She drags the $n$ slider from 1 to 2 to 3. She drags $\ell$ through its allowed values. She watches $r_{mp}$ and $\langle r\rangle$ move apart. She types her notes for her oral exam.

She will pass. Not because she watched the simulation. Because she now understands what she has been computing.

The next chapter is yours.

Let's go.

---

**Tags:** quantum mechanics, undergraduate physics, interactive simulations, D3.js, Claude, AI-augmented learning, Brutalist system, +1 series, Griffiths companion, second-semester QM, physics pedagogy, wave function, Schrödinger equation, hydrogen atom, entanglement, Bell inequality

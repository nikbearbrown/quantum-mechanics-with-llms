# Research Notes: Chapter 00 — How to Use the Simulations
**Source:** TIKTOC.md chapter entry (lines 70–107)
**Notes file:** 00-how-to-use-the-simulations_notes.md
**Corresponding chapter:** chapters/00-how-to-use-the-simulations.md (not yet written)
**Generated:** 2026-05-13

---

## Chapter summary (from TIKTOC.md)

**One-line:** Students build the three Brutalist governing files and produce their first QM simulation — a free particle wave packet — before reading any physics content.

**Chapter description:** This chapter has one job: get the student from zero to a working, modifiable D3 quantum mechanics simulation before they encounter any new physics. It introduces Claude, the Brutalist system, and the four-move prompt structure through the lens of a free particle wave packet — the simplest quantum object that shows something interesting. By the end, the student has `CLAUDE.md`, `DESIGN.md`, and `PROJECT.md` in their working directory, a working simulation they can modify, and a mental model of how the LLM exercises in every subsequent chapter will work.

**Core concepts:**
- The Brutalist system: CLAUDE.md (coding constitution), DESIGN.md (visual constitution), PROJECT.md (project state)
- The four-move prompt structure: Show / Say / Constrain / Verify
- D3 v7 for physics simulation: SVG canvas, parameter sliders, requestAnimationFrame, real-time redraw
- The free particle wave packet as first simulation object: Gaussian envelope, plane wave carrier, group vs. phase velocity
- The verification stack: format check, physics check (does the wave packet spread?), browser test
- The instruction budget: why CLAUDE.md and DESIGN.md are separate files

**Key vocabulary:** wave packet, group velocity, phase velocity, Gaussian envelope, D3, SVG, CLAUDE.md, DESIGN.md, PROJECT.md, four-move prompt, verification stack

**What the student builds:** CLAUDE.md, DESIGN.md, PROJECT.md, and `00-wave-packet.html` — free particle Gaussian wave packet with sliders for k₀, σ, and time evolution speed; shows spreading in real time.

**Simulation physics:** Free particle Gaussian wave packet: ψ(x,0) = A exp(ik₀x) exp(-x²/4σ²). Time evolution via dispersion relation ω(k) = ℏk²/2m. Show |ψ(x,t)|² spreading. Sliders: σ, k₀, time step. Display: real part, imaginary part, probability density on three stacked SVG panels.

**Connection to Chapter 1:** The wave packet spreading is the physical motivation for Chapter 1's question: what does the wave function mean?

---

## A. Conceptual foundations

### 1. The Brutalist system (Bear's framework)

The Brutalist system is the project's name for the three-file convention that governs every simulation in the book. The files exist before the code does; the code is generated against them.

- **CLAUDE.md — coding constitution.** A persistent file that tells Claude (or any LLM) what kind of code to produce: D3 v7 only, single-file HTML, SVG canvas dimensions, parameter sliders on `input` events, `requestAnimationFrame` for animation, dark-mode media query, normalization indicator that warns when |∫|ψ|² dx − 1| > 0.01. This is the *rules of the workshop* — Claude reads it on every prompt and produces code that conforms.
- **DESIGN.md — visual constitution.** Color conventions (|ψ|² in blue, Re ψ in orange, Im ψ in gray-dashed, V(x) in red, energy levels in green, classical turning points purple-dashed), typography, layout, dark/light mode behavior. Pulled out of CLAUDE.md because *visual* decisions and *behavioral* decisions break differently — when the student wants a different aesthetic for an exam project, they edit DESIGN.md and CLAUDE.md is untouched.
- **PROJECT.md — project state.** What's been built, what chapter the student is on, which simulations exist, which were modified and how. The file Claude reads first to remember the working context. This is the project's *short-term memory*.

The reason the three files are separated rather than one combined CLAUDE.md is the *instruction budget*: every token of instruction Claude reads costs attention against the actual physics request. Splitting concerns means the chapter-3 prompt doesn't pay the cost of re-reading the entire visual style guide.

### 2. The four-move prompt structure (Show / Say / Constrain / Verify)

Bear's prior textbooks use the same four-move pattern; the book reuses it as the canonical structure for every LLM Exercise.

- **Show** — paste the relevant artifact (the equation, the current code, the data) into the prompt. Don't describe it; show it. Vague problem descriptions are the number-one cause of bad code.
- **Say** — say what you want, in one sentence, with the audience and the use case. "I want a single HTML file I can open in Chrome that lets me drag a slider to change σ and see |ψ|² spread in real time."
- **Constrain** — name the constraints. D3 v7, single file, no build step, dark mode, sliders update on `input`. Constraints reduce hallucination because they shrink the space Claude has to search.
- **Verify** — ask Claude how to check the output. "Tell me three things I should look at to verify the wave packet is evolving correctly." This converts the LLM from oracle to collaborator.

The four-move structure is the bridge between the Brutalist files and a working simulation. CLAUDE.md handles the *constrain* move globally; the chapter prompt handles *show* and *say*; the *verify* output is what the student grades themselves against.

### 3. D3 v7 as the simulation substrate

D3 (Data-Driven Documents) v7 is the JavaScript library for binding data to the DOM and applying data-driven transformations. ([d3js.org](https://d3js.org/), [Bostock et al. 2011 IEEE TVCG](https://vis.stanford.edu/papers/d3)) For this book D3 v7 is chosen for three reasons that should be named explicitly:

- It runs in any browser with one CDN script tag — no `npm install`, no build step, no local server. A student at 11pm can save an HTML file and double-click it.
- It uses SVG (vector) rather than canvas/WebGL, which matches the *line-drawing* nature of 1D QM: wave functions are curves, potentials are curves, probability densities are curves. SVG is the right primitive.
- It treats data and DOM symmetrically — `selection.data(array).join("path")` — which maps cleanly onto "I have an array of |ψ(x)|² values and I want each one to drive a pixel."

The student is not learning D3 as a career skill. They are learning enough D3 to read what Claude produces and to make local edits. The course commitment is: scales, selections, the `data().join()` pattern, range inputs, and `requestAnimationFrame`. Nothing more.

### 4. The free particle as the first physical object

The free particle (V(x) = 0 everywhere) is the simplest interesting quantum object because the time-independent Schrödinger equation has plane-wave solutions ψ_k(x) = exp(ikx) with continuous k. A *single* plane wave is not normalizable and not physical. A *wave packet* — a superposition of plane waves with a Gaussian weight in k — is. The Gaussian wave packet (Griffiths *Introduction to Quantum Mechanics* 3rd ed., §2.4, Problem 2.21) is the canonical worked example:

ψ(x, 0) = (1/(πa²))^{1/4} exp(−x²/(2a²)) exp(ik₀x)

Under free-particle evolution iℏ ∂ψ/∂t = −(ℏ²/2m) ∂²ψ/∂x², this packet evolves to a Gaussian whose width grows in time:

|ψ(x,t)|² = (1/√(2π) σ(t)) exp(−(x − v_g t)²/(2σ(t)²)), with σ(t)² = a²/2 + ℏ²t²/(2ma²).

Two velocities appear and they are different — that is the *whole point*:

- **Phase velocity** v_p = ω/k = ℏk/(2m) — the speed at which a single plane-wave crest moves.
- **Group velocity** v_g = dω/dk = ℏk/m = p/m — the speed at which the *envelope* (the probability density) moves.

For a non-relativistic massive particle, v_g = 2 v_p. The envelope moves twice as fast as the wave crests. A student who has seen this on screen will never confuse the two again.

### 5. The verification stack

The chapter introduces the three checks that travel with every simulation in the book:

- **Format check** — does the file open in a browser without error? (Open browser DevTools, look for red.)
- **Physics check** — does it conserve what it should? For the free particle: normalization should hold (∫|ψ|² dx ≈ 1), and the envelope should spread, not contract, and not move backward.
- **Behavioral check** — does the slider do what it claims? Pulling σ to a smaller value should produce a *narrower* initial packet that spreads *faster*. (The inverse Fourier relation σ_x σ_k ≈ 1/2 is the reason.)

Verification is a chapter-zero habit because once the student is doing the physics, they will trust the simulation and stop checking. This is when LLM hallucinations cause the worst learning damage. The verification stack is the immune response.

---

## B. Domain examples and cases

### Example 1: A working Gaussian wave packet
The complete physics: ψ(x, 0) = (1/(πa²))^{1/4} exp(−x²/(2a²)) exp(ik₀x), with a = 1 nm, k₀ = 10 nm⁻¹, mass = electron mass. At t = 0 the packet is centered at x = 0 with width a. After t = 1 fs the packet centroid has moved to v_g t = (ℏ k₀ / m)(10⁻¹⁵ s) ≈ 1.16 nm and the width has grown by a calculable factor. The student computes both and checks them against what the simulation shows.

### Example 2: The same packet with k₀ = 0
A *stationary* Gaussian — no carrier wave, just an envelope at rest. The envelope still spreads (this is the surprise). Spreading is not motion; it is uncertainty growing over time. This is the case that distinguishes quantum spreading from classical drift.

### Example 3: Comparison with classical mechanics
A classical particle at known position with known momentum just *moves*. The position is sharp; the velocity is sharp; the position later is sharp. The quantum particle cannot have both at once (σ_x σ_p ≥ ℏ/2, Heisenberg 1927; [verify Heisenberg's original *Zeitschrift für Physik* citation: Heisenberg, W. (1927). *Z. Phys.* 43, 172–198]). The simulation makes this concrete: as the initial width a shrinks, the spread rate ℏt/(ma) grows. Trying to localize the particle costs you predictability later.

### Failure case: the LLM hands back a static plot
A common failure mode: the student asks Claude for "a wave packet" and gets a still picture of a Gaussian rather than an animation. The chapter teaches the student to *show* by pasting the time-dependent equation and *say* "animate using requestAnimationFrame, update every 16 ms, expose a time slider and a pause button." Specificity in the prompt produces specificity in the code. This is the chapter-zero version of the lesson the whole book reinforces.

---

## C. Connections and dependencies

- **Prerequisites the chapter assumes:** the student has completed one semester of intro QM and modern physics. Specifically, they know what a wave is, they have seen the de Broglie relation p = ℏk, and they have computed Fourier transforms in a math course. They are *not* assumed to know what |ψ|² means as probability — Chapter 1 establishes that.
- **What the chapter must NOT do:** introduce the Born rule, normalization, expectation values, or the time-dependent Schrödinger equation as concepts to be learned. Those belong to Chapter 1. The wave packet here is a *visual object* the student watches; the *interpretation* is Chapter 1's job.
- **Bridge to Chapter 1:** "You watched |ψ|² spread. The question Chapter 1 answers is: what is |ψ|² actually telling you about a particle?"
- **Carry-forward:** the three Brutalist files travel with the student to every subsequent chapter. The four-move prompt structure is reused in every LLM Exercise block.

---

## D. Current state of the field

Browser-based QM simulation is a mature but uneven domain.

- **PhET Interactive Simulations** (University of Colorado Boulder, founded by Carl Wieman; [phet.colorado.edu](https://phet.colorado.edu/)) hosts the most cited QM visualizations — *Quantum Tunneling and Wave Packets*, *Quantum Wave Interference*, *Bound States*. PhET sims are Flash-legacy ported to HTML5; they are designed by physics-education researchers and tested with thousands of students. Adams et al. (2008), "A Study of Educational Simulations Part I — Engagement and Learning," [*Journal of Interactive Learning Research* 19(3)](https://www.learntechlib.org/p/24230/), document the design principles. Wieman, Adams & Perkins (2008), "PhET: Simulations That Enhance Learning," [*Science* 322, 682–683](https://www.science.org/doi/10.1126/science.1161948), is the canonical citation for the PhET pedagogical case.
- **Falstad's Quantum Mechanics applet** ([falstad.com/qm1d](https://www.falstad.com/qm1d/)) is the older, more flexible 1D solver. It does not teach the student to *build* anything.
- **Open Source Physics / OSP** ([compadre.org/osp](https://www.compadre.org/osp/)) Java/JavaScript simulations, Christian and Belloni; the *Physlet Quantum Physics* book is a precursor in spirit to this one but uses canned simulations rather than student-generated code.
- **D3-based physics demos:** Mike Bostock's [Observable notebooks](https://observablehq.com/@mbostock) include some PDE solvers; nothing canonical exists for QM. This is one reason the book has a place.

The gap this book fills: PhET-quality interactivity, but the student writes (or generates and edits) the code. The interactivity is not consumed; it is *built*. That is the educational shift the +1 system bets on.

---

## E. Teaching considerations

### Misconceptions to pre-empt

- **"The LLM-generated simulation is the answer."** No — the *interaction* with the simulation is the answer. A simulation watched without parameter sweeps teaches nothing.
- **"The wave packet is the electron."** No — the packet is a *description* of where the electron might be found. Chapter 1 lands this; Chapter 0 just plants the seed.
- **"Spreading means the packet falls apart."** No — total probability stays 1; the distribution flattens. The packet doesn't dissolve; the localization decays.
- **"The Brutalist files are administrative overhead."** No — they are the reason every chapter's prompt produces consistent, debuggable code. Without them, the student rewrites the conventions every week.

### Pedagogical pacing
The chapter is the longest in the book by intent. It moves slowly through the first installation, then accelerates. The student should not encounter Chapter 1 until they have a working `00-wave-packet.html` they have already modified twice (changed σ, changed k₀). The modification is the learning event.

### Address the "I don't know JavaScript" reader
Acknowledge directly: most physics majors have not written JavaScript. The chapter does not teach JavaScript. The chapter teaches the student to *read* what Claude wrote, find the line with `sigma = ...`, change the number, and reload. That is enough.

---

## F. Library files relevant to this chapter

- Griffiths, *Introduction to Quantum Mechanics* (3rd ed., Cambridge 2018), §2.4 (the free particle) and Problem 2.21 (the Gaussian wave packet). The Griffiths derivation is the closest match to what the simulation visualizes. Solution Manual entry for Problem 2.21 supplies the explicit σ(t) formula.
- Liboff, *Introductory Quantum Mechanics* (4th ed.), Chapter 6 on the free particle and wave packets — secondary reference for an alternative derivation. The pantry copy is image-OCR garbled; use only for spot-checking against Griffiths.
- *Quantum Physics for Beginners* (pantry pop-sci sources) — useful for *misconception examples* (these books often perpetuate "the wave function is the particle"). Read against, not with.
- `_lib_QM-Into-the-Light-Beginners.md` — pantry bookmap; useful for the chapter's pop-science register check, not for technical content.
- `_lib_The-Blind-Spot.md` — pantry bookmap; relevant for the broader argument about *seeing* phenomena vs. describing them. Could feed a sentence in the chapter's framing about why simulation matters.
- `00-claude-prompting-tips.md` — pantry draft from Bear's earlier work; the four-move structure (Show / Say / Constrain / Verify) is established there and *reused* here. This chapter assumes the reader has internalized that structure or learns it on the fly.

## F.5 Simulation pedagogy and D3 specifics

### What the simulation must show
A free-particle Gaussian wave packet in three stacked panels (or a toggleable single panel):
1. **Re ψ(x, t)** — orange line oscillating under a slow envelope.
2. **Im ψ(x, t)** — gray dashed line, π/2 out of phase.
3. **|ψ(x, t)|²** — blue filled curve, the *probability density*. This is the panel the student watches.

The panel must update continuously. The eye must see the envelope drifting (group velocity) while individual crests inside it slide past (phase velocity). When σ is small at t = 0, the spread rate is fast; when σ is large, the packet barely spreads on the visible timescale. The slider for k₀ shifts the centroid speed; the slider for σ shifts the spread rate. A reset button restores t = 0.

Stretch features (in the extension prompt): a momentum-space panel showing |φ(k)|² (constant in time for free evolution, since [Ĥ, p̂] = 0 in V = 0). This is the punchline of the chapter — *something* is conserved even as the position spread grows.

### D3 v7 patterns and SVG elements
- `d3.select("svg")` for canvas selection.
- `d3.scaleLinear().domain([x_min, x_max]).range([margin.left, width − margin.right])` for the position axis; analogous for ψ values.
- `d3.line().x(d => xScale(d.x)).y(d => yScale(d.psi))` for the wave-function curve.
- `selection.datum(data).attr("d", line)` to redraw the path each frame — *not* full enter/update/exit; for a single line with a moving array, `datum` is correct and faster.
- `d3.axisBottom(xScale)` and `d3.axisLeft(yScale)` for axes, rendered once on mount.
- HTML `<input type="range">` sliders bound with `.on("input", ...)`. The `input` event fires continuously as the student drags; `change` fires only on release, which is the wrong UX for a live physics control.

### Real-time redraw
- Single `requestAnimationFrame` loop. State: `t`, `dt`, `paused`. Each frame: advance t by dt, recompute the ψ(x, t) array on the grid (N ≈ 200 points is plenty for visual smoothness), update the three SVG paths via `.attr("d", line)`. Total work per frame: O(N). At 60 fps, comfortable on any laptop.
- For the free particle, the closed-form solution is available — no need to integrate the PDE numerically. Use the analytic Gaussian time evolution. This is the chapter's gift: the simulation is *exact*, not a numerical approximation. Later chapters (TISE, finite well) will introduce numerics; for now, the math hands you the answer and you just plot it.
- Pause/play button. Time step slider (logarithmic, 10⁻¹⁸ s to 10⁻¹² s) so the student can see slow spreading and fast spreading.

### Parameter sliders and ranges (suggested)
- σ (initial Gaussian width): 0.1 nm to 5 nm.
- k₀ (central wavenumber): −20 nm⁻¹ to +20 nm⁻¹.
- dt (time step): 10⁻¹⁸ s to 10⁻¹² s, log scale.
- Mass: dropdown (electron, proton, [verify] — undergrad physics students usually find electron more concrete).
- Reset and pause buttons.

### Pedagogical research on simulation as a teaching tool
- **PhET — Wieman group, University of Colorado Boulder.** Carl Wieman won the 2001 Nobel Prize in Physics (Bose-Einstein condensation, with Cornell and Ketterle, [nobelprize.org](https://www.nobelprize.org/prizes/physics/2001/summary/)) and has spent the post-Nobel half of his career on physics-education research. The PhET program's core finding: students learn more from *interactive engagement* than from passive demonstration. The interactivity must be *productive failure* — letting the student try the wrong parameter and see why it fails. (Hake 1998, "[Interactive-engagement versus traditional methods](https://www.compadre.org/portal/items/detail.cfm?ID=2099)," *Am. J. Phys.* 66, 64–74, is the canonical empirical anchor; effect size ~2σ between traditional and interactive courses.)
- **Adams, W. K., Reid, S., LeMaster, R., McKagan, S. B., Perkins, K. K., Dubson, M., & Wieman, C. E. (2008).** Two-part study on PhET design principles: [Part I (engagement)](https://www.learntechlib.org/p/24230/) and Part II (interview methodology). Findings: simulations are most effective when they offer *productive interactivity* (the student manipulates and sees consequences) and *implicit scaffolding* (the design constrains exploration to physically meaningful regions).
- **Lavi, R., & Marshall, J. A.** appear in the brief as a research handle — I cannot locate a specific Lavi & Marshall paper on physics simulations with confidence and have not invented one. [verify: ask Nik for the specific reference; possibly Lavi, R., Tal, M., & Dori, Y. J. (2021), "Perceptions of STEM Alumni and Students on Developing 21st Century Skills Through Methods of Teaching and Learning," *Studies in Educational Evaluation* 70, but this is not specifically a simulation paper.]
- **Singh, C., & Marshman, E. (2015), "[Review of student difficulties in upper-level quantum mechanics](https://journals.aps.org/prper/abstract/10.1103/PhysRevSTPER.11.020117)," *Phys. Rev. Phys. Educ. Res.* 11, 020117.** This is the canonical PER review for upper-division QM and is cited in Chapter 1 as well.

### The four-move Claude prompt structure (chapter-specific)
For the wave-packet build:
- **Show:** paste the Gaussian wave packet equation, paste CLAUDE.md and DESIGN.md as context.
- **Say:** "Produce `00-wave-packet.html` — a single file I open in a browser. It shows |ψ(x,t)|², Re ψ, Im ψ on three stacked SVG panels with sliders for σ, k₀, and a time control."
- **Constrain:** "D3 v7 via CDN. requestAnimationFrame loop. Sliders on `input`. Dark mode via prefers-color-scheme. Use the analytic Gaussian time evolution, not numerical integration of the PDE. Normalization indicator that warns if |∫|ψ|² dx − 1| > 0.01."
- **Verify:** "Tell me three things to check: (a) at t = 0 the packet should be centered at x = 0 with width σ. (b) the centroid should move at v_g = ℏk₀/m. (c) σ(t) should grow as √(σ² + (ℏt/(2mσ))²). Print these three predicted values in the UI so I can compare against the rendered position."

### Known failure modes when an LLM generates physics simulation code
- **Wrong dispersion relation.** Claude has been observed to use ω(k) = ck (electromagnetic) instead of ω(k) = ℏk²/(2m) (massive non-relativistic) for the free-particle phase. The verification step *must* compute v_g and v_p and check the 2:1 ratio.
- **Static rendering of a "wave packet"** — a Gaussian drawn at one time and not animated. Catch with a behavior check: drag the time slider, the curve must move.
- **Normalization drift.** When the LLM tries to integrate the PDE numerically and gets the discretization wrong, ∫|ψ|² dx drifts. The normalization indicator in CLAUDE.md catches this. For the analytic Gaussian, this should never happen — if it does, the LLM has subtituted a numerical scheme without saying so. [verify suspicion: have seen this in informal testing; flag for Nik.]
- **Phase velocity drawn as group velocity.** Claude sometimes animates the *whole* curve at v_p, which makes the envelope look like it moves at the wrong speed. The fix is to compute the analytic Gaussian directly, which carries the correct v_g and v_p separately.
- **Re ψ and Im ψ swapped or in phase.** Im ψ should lead Re ψ by π/2 (for a positive k₀); they should never coincide. A visual check.
- **Scale/units silently wrong.** Claude defaults to "natural units" without telling the student. Mitigation: CLAUDE.md says *display in SI internally; convert to natural units for the axis labels and say so.*
- **SVG performance collapse at large N.** Using one `<circle>` per data point at N = 1000 causes frame drops. The CLAUDE.md rule "use a single `<path>` per curve, not one element per point" prevents this.

---

## G. Gaps and flags

- **[verify]** the Heisenberg 1927 *Zeitschrift für Physik* citation (volume 43, pp. 172–198, year 1927). I have stated this from memory; Nik should confirm against the original.
- **[verify]** the Lavi & Marshall reference cited in the brief — I have not located a specific paper with this combination of authors and cannot generate a citation without inventing one. Nik should supply.
- **[verify]** Adams et al. 2008 — there are two PhET design papers from 2008; the *Journal of Interactive Learning Research* 19(3) reference covers Part I. The second part is in the same journal. I have not personally verified the DOI; the URL works as of [verify date].
- **Gap:** I have not pulled a primary source for the *specific* claim that group velocity equals 2 × phase velocity for a non-relativistic massive particle. This is undergraduate textbook material (Griffiths §2.4) but should be cited cleanly.
- **Gap:** the chapter will need a section explaining the difference between "the LLM made the code" and "I understand what the code does." The student should be able to point to the line in `00-wave-packet.html` that implements the dispersion relation. The chapter should produce *one annotated walk-through* of the generated code, line by line, after the build. This is the bridge from generation to comprehension.
- **Flag for Nik:** the LLM-failure list in F.5 is partly from anecdotal experience and partly inference. Worth a single test run before the chapter is written — actually generate a wave-packet sim with the four-move prompt and log what goes wrong. The chapter is more honest if the failure modes are observed, not predicted.
- **Flag:** the chapter is structurally different from every other chapter in the book — it has *no physics deep-dive* in the Feynman sense; the physics deep-dive is offloaded to Chapter 1. Make this explicit in the opening so the reader doesn't expect the four-move method to land here in the usual way.

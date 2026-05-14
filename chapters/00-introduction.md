# Chapter 0 — How to Use the Simulations
*Watching Before Understanding.*

> You will build three governing files, paste a four-move prompt into Claude, and have a working free-particle wave packet animating in your browser before this book mentions a single new piece of physics.

---

There is a difference between knowing the name of something and knowing what it does.

I want to show you a wave packet before we talk about what it means. Not a picture of one — those are in every textbook and you have already seen them. I want you to watch one move. I want you to drag a slider that changes its width and see what happens to how fast it spreads. I want you to notice, on your own, before I say anything about it, that there seem to be two different speeds living inside the same object: the blob drifts one way, and the ripples inside the blob slip through it another way. That observation — made by *you*, with your hands on the controls — is worth three weeks of reading about it.

This chapter does not teach new physics. The wave packet we build here will be derived properly in Chapters 1 and 2. What this chapter does is hand you the apparatus: three plain text files and a four-sentence prompt structure, the same structure you will use every chapter. We use the wave packet as the vehicle because it is the simplest quantum object that does something worth watching, and because the thing it does — spreading in a specific, calculable way while its center translates at a different speed than its internal oscillations — turns out to be a pocket-sized version of almost every interesting idea in the book.

By the end of this chapter you will have a file called `00-wave-packet.html` open in a browser, a Gaussian wave packet spreading across your screen in real time, and three Markdown files — `CLAUDE.md`, `DESIGN.md`, `PROJECT.md` — that will travel with you for the rest of the semester. That is the whole assignment.

---

## The three files

The apparatus is embarrassingly simple. Three plain text files you keep in the same folder as your simulations. That is all.

Here is the principle behind them: an LLM has no memory between sessions. Every time you open a new conversation and ask for a simulation, you are starting from scratch. Left to itself, the model will make different choices about libraries, drawing surfaces, units, and color conventions every single time. By Chapter 7 your simulations will look like they were written by twelve different people using twelve different toolkits, and when something breaks — and something always breaks — you will have no consistent vocabulary for describing what went wrong.

The three files solve this by being explicit about decisions that would otherwise be made silently. Not clever. Not elegant. Just written down, in plain text, where you can read them.

<!-- → [TABLE: three-column summary of the three Brutalist files — columns: file name, governs, what breaks without it — one row each for CLAUDE.md, DESIGN.md, PROJECT.md; student should be able to glance at this and state each file's single responsibility] -->

**`CLAUDE.md`** is the coding constitution. It tells the model what is and is not allowed: which library (D3 v7, from a CDN, no build step), which drawing surface (SVG, not Canvas, not WebGL), how parameters are exposed (HTML range sliders firing on the `input` event), how animation works (`requestAnimationFrame`), and what the verification indicator looks like ($\int |\psi|^2 \, dx$ printed in a corner, colored red if it strays from 1 by more than 1%). Every simulation in the book is generated with this file present. The rules are not arbitrary — each one is there because someone, at some point, got the wrong answer without it.

The SVG rule deserves a moment. Everything you will plot in this course is a curve: a wave function, a potential, a probability density. SVG draws curves natively. You describe the path mathematically and SVG renders it; scaling, zooming, and axis labeling are handled by the library. Canvas would force you to maintain a pixel buffer and re-implement all of that by hand. WebGL is powerful enough to render a AAA video game; it is magnificently ill-suited to a 1D probability density. SVG is the right primitive. We commit to it and do not revisit the decision.

The normalization indicator requires more explanation because students consistently underestimate it. Every frame, the simulation computes $\int |\psi|^2 \, dx$ using the trapezoidal rule on the numerical grid. The result should be $1.000$. If it reads $0.973$ or $1.048$, something is wrong — the LLM has introduced a normalization error, or you have pushed a parameter outside its physical range, or there is a bug in the time evolution. The indicator is the simulation's lie detector, and the reason it must be present on every single frame is that normalization errors often appear slowly, growing over many frames until the physics is visibly corrupted. Without the indicator you will watch the corruption happen and not know it is happening.

**`DESIGN.md`** is the visual constitution. It is separated from `CLAUDE.md` because visual decisions and physical decisions break in different ways. When the packet spreads wrong, that is a physics bug; you open `CLAUDE.md`. When the colors are hard to read, that is a design bug; you open `DESIGN.md`. The conventions are: probability density $|\psi|^2$ in blue (filled), real part in orange (solid line), imaginary part in gray (dashed line), potential in red, energy levels in green, classical turning points in purple dashed. For two-dimensional plots — density maps, probability surfaces — we use perceptually uniform colormaps exclusively: Viridis for unsigned quantities, RdBu centered on zero for signed quantities. The research on this is unambiguous: rainbow and HSV palettes distort the data by mapping equal numerical differences to unequal perceived differences. Viridis is monotone in luminance and reads correctly in grayscale and for color-blind viewers. We use it because it tells the truth, not because it looks nice.

**`PROJECT.md`** is the project notebook. A few hundred words, updated every time you finish a simulation: what was built, what was verified, what is broken. Its purpose is simple. Three months from now, when you ask the model to modify the Chapter 5 simulation to add a perturbation slider, it will have no memory of Chapter 5. `PROJECT.md` is the memory. The students who skip maintaining it are the students who, in November, cannot remember what parameter range they used in September and have to regenerate everything from scratch.

Why three files and not one? Token economy, and separation of concerns. When you ask for a hydrogen-atom radial-equation solver in Chapter 7, you do not want the model to re-read six pages of slider-styling rules before thinking about quantum numbers. `CLAUDE.md` and `PROJECT.md` are pasted directly; `DESIGN.md` is referenced by name. The visual rules are still in force — the model knows the file exists — but they are not burning context on a problem that is fundamentally about physics.

<!-- → [INFOGRAPHIC: prompt-context diagram showing a Chapter 7 request — three boxes representing CLAUDE.md (pasted, full text), PROJECT.md (pasted, full text), and DESIGN.md (referenced by name only) feeding into a central "LLM context window" box; the DESIGN.md arrow is visually lighter/dashed to show it contributes constraints without consuming tokens; label the diagram "Instruction budget: what gets pasted vs. referenced"] -->

---

## The four-move prompt

A prompt to an LLM is a specification, not a wish. The difference matters. A wish is "build me a wave packet simulation." A specification is a document with four identifiable parts: what you are showing the model, what you want it to produce, what constraints govern the production, and how you will verify the output is correct. The four-move structure — **Show, Say, Constrain, Verify** — is the one this book uses for every LLM Exercise. It is the reason most simulations work on the first or second try.

<!-- → [INFOGRAPHIC: four-panel horizontal flow diagram of the Show → Say → Constrain → Verify sequence — each panel contains the move name, a one-sentence description, and a concrete example drawn from the wave-packet prompt; arrows between panels; the Verify panel visually doubles back to the output with a "rubric" label, showing that Verify is a check on the result, not just another input] -->

**Show** means paste the artifact. The equation, the existing code, the data file. Not a description of it — the thing itself. If you want the wave function $\psi(x, 0) = (1/\pi a^2)^{1/4} e^{-x^2/(2a^2)} e^{ik_0 x}$, put the LaTeX in the prompt. Writing "a Gaussian wave packet" and hoping the model picks the right normalization convention will produce wrong code about a third of the time. The model has to guess what you meant, and its guesses are drawn from a distribution that includes every normalization convention ever published.

**Say** means state what you want in one sentence, with the use case explicit. *"I want a single HTML file I can double-click in Chrome that lets me drag a slider to change $\sigma$ and watch $|\psi|^2$ spread in real time."* The use case — double-click, Chrome, drag a slider — determines the shape of the output. Without it the model might give you a Python notebook, or a React component that requires a build system, or a static image.

**Constrain** means name the rules. D3 v7. Single file. No build step. SVG only. Sliders on the `input` event. Normalization indicator visible. For simulations in this book, most of the constraints live in `CLAUDE.md` and the prompt references that file rather than restating everything. The only constraints that go in the prompt itself are ones specific to the chapter — this simulation uses a logarithmic time-step slider; that one needs a mass dropdown. Constraints reduce hallucination because they shrink the space the model has to search. A model that cannot choose between SVG and Canvas will sometimes choose Canvas. Remove the choice.

**Verify** means ask the model how to check the output. This is the move most people skip, and skipping it is the reason most people accumulate bugs they do not notice until they matter. Ask: *"Tell me four things I should look at in the browser to verify this simulation is evolving correctly."* You get back a rubric. For the wave packet: the centroid should move at $v_g = \hbar k_0 / m$, the width should grow as $\sigma(t) = \sqrt{a^2/2 + \hbar^2 t^2 / (2 m^2 a^2)}$, normalization should hold to within 1%, and the phase velocity visible inside the packet should be half the group velocity. You apply this rubric to the rendered output. If check (b) fails — the centroid is moving at $v_p$ instead of $v_g$ — you know exactly what the bug is and where to look for it.

The verification step converts the model from oracle to collaborator. An oracle gives you an answer and you trust it or you don't. A collaborator gives you an answer *and a way to check it*. The LLM-generated simulations in this book will occasionally be wrong. The four-move prompt does not prevent that. What it does is ensure that when the code is wrong, the verification rubric tells you it is wrong before you build two more chapters on top of it.

---

## What you are about to watch

Before the LLM Exercise, a brief account of the physics — not a derivation, which comes in Chapters 1 and 2, but enough to know what you are looking for.

A free particle — no potential, just kinetic energy — with mass $m$ and central momentum $p_0 = \hbar k_0$ is prepared at $t = 0$ in a Gaussian state of width $a$:

$$\psi(x, 0) = \left(\frac{1}{\pi a^2}\right)^{1/4} \exp\!\left(-\frac{x^2}{2a^2}\right) \exp(i k_0 x).$$

The prefactor is a normalization constant chosen so $\int |\psi|^2 \, dx = 1$. The Gaussian envelope localizes the particle; the plane-wave carrier $e^{ik_0 x}$ gives it a direction. At $t = 0$ this is symmetric, peaked at $x = 0$.

The free-particle Hamiltonian is $\hat{H} = \hat{p}^2 / (2m)$, and its key property is the *dispersion relation*: each plane-wave component $e^{ikx}$ has a frequency $\omega(k) = \hbar k^2 / (2m)$. This relation is quadratic in $k$. That quadratic dependence is the single fact responsible for the spreading.

Here is why. The initial wave packet is not a single plane wave — it is a superposition of many plane waves, each with a slightly different $k$, weighted by a Gaussian in $k$-space. Under time evolution, each component acquires a phase $e^{-i\omega(k)t}$. Because $\omega(k)$ is quadratic, different components accumulate different phases at different rates. After any nonzero time, the components are no longer perfectly aligned. They partially cancel at the edges of the packet. The packet spreads.

<!-- → [INFOGRAPHIC: two-panel diagram illustrating the dephasing mechanism — left panel shows several sinusoidal components at t=0 aligned to form a Gaussian envelope; right panel shows the same components at t>0 shifted by different amounts (faster for larger k), now partially canceling at the edges; label the constructive-interference region "packet center" and the cancellation zones "spreading tails"; caption: "Why the packet spreads: each Fourier component has a different frequency under a quadratic dispersion relation"] -->

The closed-form result for $|\psi(x,t)|^2$ is another Gaussian, but wider:

$$|\psi(x, t)|^2 = \frac{1}{\sqrt{2\pi}\,\sigma(t)} \exp\!\left(-\frac{(x - v_g t)^2}{2\sigma(t)^2}\right),$$

where

$$\sigma(t)^2 = \frac{a^2}{2} + \frac{\hbar^2 t^2}{2 m^2 a^2}.$$

The centroid moves at the **group velocity** $v_g = \hbar k_0 / m = p_0 / m$. This is the classical answer: the particle moves at momentum divided by mass. But the individual wave crests inside the packet move at the **phase velocity** $v_p = \omega(k_0)/k_0 = \hbar k_0 / (2m)$, which is exactly half $v_g$.

$$\frac{v_g}{v_p} = 2.$$

This is the thing to watch in the simulation. The blue blob — $|\psi|^2$, the thing you can actually measure — drifts to the right at $v_g$. Inside it, the orange ripples of Re $\psi$ slide through the blob at $v_g - v_p = v_p$, meaning in the rest frame of the blob the ripples move *backward*. Wave crests appear to be born at the front of the packet, travel backward through it, and disappear at the back. They are not carrying anything physical. They are phase. The blob carries the momentum; the ripples are a side effect of the Fourier decomposition.

<!-- → [IMAGE: annotated screenshot or rendered frame of the 00-wave-packet.html simulation — shows the three-panel SVG output with the blue |ψ|² blob, orange Re ψ ripples, and gray Im ψ dashes; arrows annotating v_g (pointing at blob centroid trajectory) and v_p (pointing at a wave crest inside the blob); caption: "The blob moves at v_g; the crests inside it move at v_p = v_g/2. In the blob's rest frame, the crests slide backward"] -->

One worked example, to make the scales concrete. An electron ($m = 9.109 \times 10^{-31}$ kg), prepared in a 1 nm Gaussian with $k_0 = 10$ nm$^{-1}$:

$$v_g = \frac{\hbar k_0}{m} = \frac{(1.055 \times 10^{-34})(10^{10})}{9.109 \times 10^{-31}} \approx 1.16 \times 10^6 \text{ m/s.}$$

That is about 0.4% of the speed of light — non-relativistic, as assumed.

The spreading time scale: the packet doubles in width when $\sigma(t) = 2\sigma(0) = \sqrt{2}\,a$, which requires

$$\frac{\hbar^2 t^2}{2m^2 a^2} = \frac{3a^2}{2} \implies t = \sqrt{3}\,\frac{ma^2}{\hbar} \approx 15 \text{ fs.}$$

In 15 femtoseconds, the electron packet has drifted 17 nm to the right and doubled in width. For a proton of the same initial width, the same calculation gives a spreading time longer by $m_p/m_e \approx 1836$, so about 27 picoseconds. For a marble it is longer than the age of the universe. Quantum spreading is not a mystery; it is a calculation, and the calculation tells you the scales at which it matters.

<!-- → [TABLE: comparison of spreading times across particle masses — rows: electron (m = 9.1×10⁻³¹ kg), proton (m = 1.7×10⁻²⁷ kg), dust grain (m ~ 10⁻¹⁵ kg), marble (m ~ 10⁻² kg); columns: mass, doubling time t_double = √3 · ma²/ℏ for a = 1 nm, verdict (observable / picoseconds / geological / cosmological); student should see the mass dependence is the entire story] -->

One more thing to notice, which the simulation makes vivid even though the derivation is in Chapter 2. Set $k_0 = 0$ in the slider. The packet does not translate — $v_g = 0$, there is no mean momentum. But it still spreads. Spreading is not motion. Spreading is the growth of position uncertainty, and it happens even for a particle sitting still. The extension exercise at the end of the LLM section adds a fourth panel showing $|\phi(k)|^2$, the momentum-space probability density. There you will see the complementary fact: the momentum distribution does not change in time, because for a free particle, momentum is conserved. Position spreads because momentum has a distribution; the distribution of momentum does not change because nothing is acting on the particle. Chapter 1 will name the formal relationship between those two facts. Here you just watch them.

<!-- → [INFOGRAPHIC: side-by-side comparison of position space and momentum space at two time points (t=0 and t=T) — left column: |ψ(x,t)|² Gaussian widening over time; right column: |φ(k,t)|² Gaussian staying constant; connecting caption: "Position uncertainty grows; momentum uncertainty is frozen. The Fourier pair trades one for the other, but free evolution changes only the phase — not the amplitude — in k-space"] -->

---

## LLM Exercise — your first simulation

This is the chapter's deliverable. You will produce three Markdown files and one HTML file. Open Claude and paste the four prompts below in order. The prompts are written to be paste-ready; do not edit them on the first run.

### Part A — The `CLAUDE.md` prompt (the coding constitution)

```
You are helping me build a series of interactive quantum mechanics simulations
in D3.js v7. I am going to give you a coding constitution that you will follow
on every simulation request in this project. Save the following as CLAUDE.md
in the project root, verbatim:

---
# CLAUDE.md — Coding Constitution for QM+1 Simulations

## Runtime and stack
- Single HTML file the user can double-click. No build step. No npm. No server.
- D3.js v7 loaded from https://d3js.org/d3.v7.min.js via a <script> tag.
- Vanilla JavaScript only. No React, no Vue, no jQuery.
- ES2020+ syntax (arrow functions, const/let, template literals, optional chaining).

## Drawing surface
- SVG only. No HTML canvas. No WebGL.
- One <path> element per curve. Never one element per data point.
- Axes drawn with d3.axisBottom / d3.axisLeft.
- Layout: explicit margin object {top, right, bottom, left}.

## Simulation core
- Functions, not classes, for the physics. computeWavefunction(x, t, params)
  returns a typed array.
- SI units internally. Display in physical units (nm, fs, eV) with labels.
- Complex storage as {re, im} objects OR two parallel Float64Arrays.
- Use analytic time evolution where a closed form exists. Numerical PDE
  integration only with a unitary scheme (Crank-Nicolson), never explicit Euler.

## Parameter exposure
- HTML <input type="range"> sliders. Event: "input", not "change".
- Every parameter has a visible numeric readout that updates live.
- Sliders labeled with their physical units.

## Animation
- Single requestAnimationFrame loop. State: {t, dt, paused}.
- Pause/play button. Reset button (returns to t = 0).
- Target 60 fps. If the per-frame work exceeds 16 ms, reduce grid resolution
  and warn in the console.

## Verification (required for every simulation)
- A normalization indicator at the top of the page: "∫|ψ|² dx = 1.000".
  If the integral strays from 1 by more than 0.01, color the readout red.
- Print at least three predicted physical values in the UI ("v_g = ...",
  "σ(t) = ...", etc.) so the user can compare against the live simulation.

## Accessibility and dark mode
- Respect @media (prefers-color-scheme: dark).
- Color choices conform to DESIGN.md (separate file).
- Sliders keyboard-navigable. ARIA labels on all interactive elements.

## What NOT to do
- Do not use canvas, WebGL, or any image-based rendering.
- Do not use any library other than D3 v7.
- Do not silently switch to natural units (ℏ = 1, m = 1). If natural units
  help, say so in a comment AND display a unit-conversion note in the UI.
- Do not use explicit Euler for time evolution of the Schrödinger equation.
---

When I ask for a simulation in subsequent prompts, you will read this file
as the binding constitution. If a chapter prompt conflicts with this file,
the chapter prompt wins for that simulation only; flag the conflict in
your response.

Output: confirm you have saved CLAUDE.md, and echo the first 10 lines back
to me so I can verify the save was clean.
```

### Part B — The `DESIGN.md` prompt (the visual constitution)

```
Now save the following as DESIGN.md in the same project root, verbatim:

---
# DESIGN.md — Visual Constitution for QM+1 Simulations

## Color tokens (CSS variables)
- --color-psi-sq:   #1f77b4   (probability density, filled)
- --color-re-psi:   #ff7f0e   (real part of ψ, solid line)
- --color-im-psi:   #888888   (imaginary part of ψ, dashed line)
- --color-potential:#d62728   (V(x), solid)
- --color-energy:   #2ca02c   (energy levels, horizontal solid)
- --color-turning:  #9467bd   (classical turning points, dashed vertical)
- --color-axis:     CanvasText (follows prefers-color-scheme)
- --color-bg:       Canvas     (follows prefers-color-scheme)

## Colormaps for 2D plots
- Unsigned densities (|ψ|², probability surfaces): Viridis.
- Signed amplitudes (Re ψ, perturbation matrices): RdBu centered on 0.
- Never rainbow / jet. Never HSV-cycling palettes.

## Typography
- Numeric readouts in a monospace font (system-ui-monospace).
- Labels and prose in the platform's default sans-serif.
- Math labels use Unicode (ψ, ℏ, σ, π) directly. No MathJax in axis labels.

## Layout
- Stack panels vertically when comparing curves (Re ψ on top of Im ψ on top
  of |ψ|², sharing x-axis).
- Sliders in a fixed panel below or beside the plots.
- Normalization indicator pinned top-right.

## Slider styling
- Range slider with visible thumb and a numeric input next to it for precise
  values. Both update each other.
- Show min, current, max as small text under the slider.

## Legend and units
- Every axis labeled with its physical units in parentheses, e.g. "x (nm)".
- Curves labeled in a small legend in the upper-left of each panel.
- The y-axis of |ψ|² is labeled "|ψ|² (1/nm)" — densities have units.

## Dark / light mode
- All colors above must be readable on both light (#fff) and dark (#111)
  backgrounds. Adjust opacity, not hue, when switching.
---

Confirm save and echo the first 10 lines.
```

### Part C — The `PROJECT.md` prompt (project state)

```
Now save the following as PROJECT.md in the same project root:

---
# PROJECT.md — Quantum Mechanics +1 Simulations

**Owner:** [your name]
**Course:** QM II, Spring [year]
**Status:** Chapter 0 in progress.

## Built so far
- (none yet)

## Verified
- (none yet)

## Open issues
- (none yet)

## Conventions in use
- Units: SI internally, displayed in nm, fs, eV.
- Default mass: electron, m = 9.109 × 10⁻³¹ kg.
- Default grid: N = 200 points on x ∈ [-20 nm, +20 nm] for free-particle work.
---

Confirm save.
```

### Part D — The simulation prompt (Show / Say / Constrain / Verify)

```
SHOW.
The free-particle Gaussian wave packet has the closed-form solution

  ψ(x, 0) = (1/(πa²))^(1/4) · exp(−x²/(2a²)) · exp(i k₀ x)

evolving under Ĥ = p̂²/(2m) to

  |ψ(x, t)|² = (1/(√(2π) σ(t))) · exp(−(x − v_g t)²/(2 σ(t)²))

with σ(t)² = a²/2 + ℏ²t²/(2 m² a²), v_g = ℏk₀/m, v_p = ℏk₀/(2m).

The wave function itself at time t (analytic) is

  ψ(x, t) = (1/(πa²))^(1/4) · (a / γ(t))^(1/2) ·
            exp(i k₀ x − i ω₀ t) ·
            exp( − (x − v_g t)² / (2 γ(t)²) )

where γ(t) = a · (1 + i ℏ t / (m a²))^(1/2) is complex and you should
compute Re ψ and Im ψ from this complex form. ω₀ = ℏ k₀² / (2m).

Use the CLAUDE.md and DESIGN.md saved earlier as binding context.

SAY.
Produce a single file named 00-wave-packet.html. It opens in a browser and
shows three stacked SVG panels sharing an x-axis:
  - Top: Re ψ(x, t)  (orange line)
  - Middle: Im ψ(x, t)  (gray dashed line)
  - Bottom: |ψ(x, t)|²  (blue filled curve)
Sliders below the plots:
  - σ (initial Gaussian width): 0.1 nm to 5 nm, default 1 nm
  - k₀ (central wavenumber): −20 nm⁻¹ to +20 nm⁻¹, default 10 nm⁻¹
  - dt (time step per frame): 10⁻¹⁸ s to 10⁻¹² s, logarithmic, default 10⁻¹⁵ s
  - Mass: dropdown {electron, proton}, default electron.
Buttons: play/pause and reset (returns to t = 0).

CONSTRAIN.
- D3 v7 from CDN. SVG only. Vanilla JS.
- N = 200 grid points on x ∈ [−20 nm, +20 nm].
- Use the analytic complex Gaussian above. Do NOT integrate the TDSE
  numerically. The closed form is exact.
- Normalization indicator pinned top-right. Recompute every frame with
  the trapezoidal rule; red if |I − 1| > 0.01.
- Print three predicted values in the UI:
    v_g = ℏ k₀ / m  (in m/s)
    v_p = ℏ k₀ / (2m)  (in m/s)
    σ(t) = √(a²/2 + ℏ²t²/(2 m² a²))  (live, in nm)
  next to a live readout of the centroid measured from the simulation
  (∫ x |ψ|² dx). The two centroid values should agree to <1%.

VERIFY.
After writing the file, tell me four things to check in the browser:
(a) at t = 0 the centroid is at x = 0 and the width is a/√2.
(b) the centroid moves at v_g; verify by reading the live readout
    at t = 10 fs against the predicted value.
(c) σ(t) grows as √(a² + (ℏt/(ma))²) / √2 — verify by reading the live
    σ(t) at t = 10 fs against the predicted value.
(d) the normalization indicator stays at 1.000 ± 0.01 throughout.

Then list any known failure modes for an LLM generating this code (wrong
dispersion relation, static plot, normalization drift, v_p/v_g swap,
Re/Im phase confusion, silent unit swap, SVG-per-point performance
collapse, missing units on axes). Confirm which you have actively
guarded against.
```

### Part E — Exploration tasks

After the simulation is rendering correctly:

1. **Set $k_0 = 0$.** The packet does not translate — $v_g = 0$ — but it still spreads. Note what this tells you about the difference between momentum and uncertainty.

2. **Set $\sigma = 0.2$ nm, then $\sigma = 2$ nm**, both with $k_0 = 10$ nm$^{-1}$. Run for 5 fs each. The narrower packet spreads visibly faster. The formula $\sigma(t)^2 = a^2/2 + \hbar^2 t^2 / (2 m^2 a^2)$ has $a$ in the denominator of the second term — narrower initial packets have a wider $k$-space distribution, and the faster-moving components pull the tails out sooner.

3. **Watch the inside of the packet.** Set $k_0 = 5$ nm$^{-1}$, $\sigma = 2$ nm, time step $10^{-16}$ s/frame. The blue blob moves right at $v_g$. The orange Re $\psi$ ripples move right at $v_p = v_g/2$. In the rest frame of the blob, the ripples move backward. They are not particles; they are phase.

4. **Note the classical limit.** The centroid of $|\psi|^2$ moves at $v_g = p_0/m$, exactly as a classical particle would. The quantum and classical positions agree. The quantum *width* does not have a classical analogue. That asymmetry — classical motion, no classical counterpart to spreading — is the puzzle that Chapter 1 begins to resolve.

### Part F — Extension prompt

```
Modify 00-wave-packet.html to add a fourth SVG panel below the existing
three: the momentum-space probability density |φ(k, t)|², where
φ(k) is the spatial Fourier transform of ψ(x).

For the free Gaussian, the analytic result is

  |φ(k, t)|² = (a²/π)^(1/2) · exp(−a² (k − k₀)²)

which is INDEPENDENT OF t. The momentum-space packet does not spread,
because [Ĥ, p̂] = 0 in V = 0 — momentum is conserved.

Add a line of text under this panel reading: "Notice: σ_k is constant
in t. This is momentum conservation, made visible."

Verify: σ_k from the simulation should match 1/(a√2) to within 1%.

Keep all other features as-is. Do not regress the existing three panels.
```

When the fourth panel renders correctly, you have seen the argument of Chapter 1 in its visual form: position spread grows because the particle has a distribution of momenta; the distribution of momenta does not change because nothing is acting on the particle. Chapter 1 will name the relationship between those two facts. Chapter 2 will show you what changes when there is a potential.

---

## Exercises

**Warm-up**

**0.1** State in one sentence each what `CLAUDE.md`, `DESIGN.md`, and `PROJECT.md` govern. Then state what each file is *not* for — i.e., what kind of decision belongs in a different file. *(Tests: can state each file's single responsibility and its boundary)*

**0.2** The free-particle dispersion relation is $\omega(k) = \hbar k^2 / (2m)$. Compute $v_g = d\omega/dk$ and $v_p = \omega/k$ at a general wavenumber $k$. Show algebraically that $v_g = 2v_p$. Now do the same for a photon, where $\omega = ck$. What does the equality $v_g = v_p$ for a photon tell you about whether a photon wave packet spreads? *(Tests: can derive group and phase velocity from a dispersion relation; can interpret the result)*

**0.3** Name the four moves of the prompt structure used in this chapter. For each move, write one sentence explaining what goes wrong in the simulation if you skip it. *(Tests: can recall Show / Say / Constrain / Verify and articulate why each is load-bearing)*

---

**Application**

**0.4** A proton wave packet is prepared with $a = 1$ nm and $k_0 = 10$ nm$^{-1}$, using $m_p = 1.673 \times 10^{-27}$ kg. Compute: (a) the group velocity $v_g$; (b) the time $t_{\times 2}$ for the packet to double in width; (c) the centroid position at $t = t_{\times 2}$. Compare each result to the electron values computed in the chapter. *(Tests: can apply the spreading and velocity formulas to a different particle; can interpret the mass dependence)*

**0.5** Open `00-wave-packet.html`. Set $k_0 = 0$ and run the simulation. (a) Confirm that the centroid does not move. (b) Measure $\sigma(t)$ at $t = 5$ fs from the live readout and compare to the formula $\sigma(t) = \sqrt{a^2/2 + \hbar^2 t^2 / (2m^2 a^2)}$. (c) In two sentences, explain why a packet with zero mean momentum still spreads. *(Tests: can distinguish translation from spreading; can apply the σ(t) formula numerically)*

**0.6** In the simulation, locate the three lines of code that implement: (a) the dispersion relation $\omega(k) = \hbar k^2/(2m)$; (b) the computation of $\sigma(t)$; (c) the trapezoidal-rule normalization integral. Write a one-paragraph annotated walkthrough of these three lines. *(Tests: can read LLM-generated code and locate the physics; can connect code to formula)*

**0.7** The verification rubric in Part D lists four checks. Run the simulation and apply each check at $t = 10$ fs with default parameters ($a = 1$ nm, $k_0 = 10$ nm$^{-1}$, electron). Record what the live readouts show and whether each check passes. If a check fails, describe what you would look at in the code first. *(Tests: can apply the verification stack to a live simulation; can translate a failed check into a debugging hypothesis)*

---

**Synthesis**

**0.8** The `CLAUDE.md` constitution requires the analytic closed form for the wave packet and explicitly forbids numerical TDSE integration for this chapter. (a) Explain why an analytic solution is available here but will not be available in Chapter 2. (b) If numerical integration were used instead, which of the four verification checks would be most sensitive to a poorly chosen time step, and why? *(Tests: can distinguish when analytic vs. numerical methods apply; can reason about error sources in numerical time evolution)*

**0.9** Suppose you want to modify `00-wave-packet.html` for a new chapter where the particle is relativistic: $\omega(k) = \sqrt{(ck)^2 + (mc^2/\hbar)^2}$. (a) Which of the three Brutalist files would you modify, and what specifically would you change? (b) Would $v_g = 2v_p$ still hold? Derive $v_g$ and $v_p$ for the relativistic dispersion and compare their ratio. *(Tests: can apply the Brutalist system to a modification task; can compute velocities from a new dispersion relation)*

---

**Challenge**

**0.10** The normalization indicator in this simulation is computed with the trapezoidal rule on $N = 200$ grid points over $x \in [-20, 20]$ nm. Estimate the discretization error in the normalization integral as a function of $N$ and the packet width $a$. For what values of $a$ (very narrow or very wide relative to the grid spacing) would you expect the indicator to fail even when the physics is correct? How would you modify the verification rubric to catch this class of error? *(Tests: can reason about numerical integration accuracy; can identify a failure mode in the verification stack itself)*

---

It does not teach JavaScript. It teaches you to read and modify what the model produces. Whether that is enough preparation for the harder chapters — Chapter 7 on the hydrogen atom, Chapter 11 on perturbation theory — is something the course will reveal. My honest expectation is that for most of the chapters, reading the generated code carefully and applying the verification stack will be sufficient. For the harder ones, you may need to look something up. That is also fine; knowing *what* to look up is more useful than knowing everything in advance.

The verification stack catches arithmetic errors. It does not catch conceptual errors that produce numerically plausible output. A simulation that swaps "Re $\psi$" and "Im $\psi$" will pass every quantitative check — normalization still integrates to 1, the centroid still moves at $v_g$, the width still grows correctly. The only defense against that class of error is knowing what the right picture looks like before you look at the wrong one. That is why this chapter asks you to compute the group and phase velocities by hand, work through the spreading-time calculation for an electron, and predict the 10 fs centroid position before running the simulation. The numbers in Part D's verification rubric should not be a surprise; they should be what you already calculated.

The Brutalist system — three files, one prompt structure — is the chapter's real subject. The wave packet is the occasion to install it. By Chapter 2, this apparatus will be invisible; you will use it without thinking about it, the same way you use dimensional analysis without thinking about it. That invisibility is the goal.

---

*Voice flag: this chapter is structurally different from the rest of the book. No new physics is derived here; the wave packet mechanics are properly treated in Chapters 1 and 2. The next chapter restores the standard chapter anatomy.*

# Chapter 0 — How to Use the Simulations

> You will build three governing files, paste a four-move prompt into Claude, and have a working free-particle wave packet animating in your browser before this book mentions a single new piece of physics.

---

## 1. What this chapter is doing

This chapter has one job. By the end of it, you have a file called `00-wave-packet.html` open in a browser, a Gaussian wave packet spreading across your screen in real time, and three Markdown files — `CLAUDE.md`, `DESIGN.md`, `PROJECT.md` — that will travel with you for the rest of the book. No new physics is taught here. The wave packet is the simplest non-trivial quantum object, and you have seen it before in some form. We are using it as a vehicle to install the apparatus this textbook depends on. Chapter 1 will tell you what the wave packet *means*; this chapter shows you how to put one on screen so Chapter 1's question is concrete.

The structure of this chapter is therefore unusual. There is no deep-dive into a new mechanism. The mechanism we unpack — Gaussian time evolution under the free-particle Hamiltonian — is one you will see properly derived in Chapter 1 and Chapter 2. Here it is a *given*. What we build instead is the workflow: the three Brutalist files, the four-move prompt, and the verification stack. These tools recur in every chapter. Spend the longer-than-usual time it takes to set them up correctly; the cost is paid once.

## 2. Learning objectives

By the end of this chapter you will be able to:

- **(Understand)** State, in one sentence each, what `CLAUDE.md`, `DESIGN.md`, and `PROJECT.md` do, and why they are three files rather than one.
- **(Apply)** Use the four-move prompt structure (Show / Say / Constrain / Verify) to request a simulation from Claude that compiles on the first try in most cases.
- **(Apply)** Read a D3 v7 simulation file and locate the lines that implement the physics (the dispersion relation, the time evolution, the normalization check).
- **(Analyze)** Distinguish group velocity from phase velocity in a Gaussian wave packet visually and numerically.
- **(Evaluate)** Apply the three-check verification stack (format, physics, behavior) to any LLM-generated simulation and name what each check catches.
- **(Create)** Produce a working `00-wave-packet.html` that animates the free-particle Gaussian with sliders for $k_0$, $\sigma$, and time.

## 3. The motivating problem

You have probably been told that a particle in quantum mechanics is described by a wave function $\psi(x, t)$. You have probably been told that $|\psi|^2$ is a probability density. You have very likely *not* watched one. There is a difference between knowing the words and having seen the object behave. Here is the puzzle this chapter sets:

A particle of mass $m$ — say, an electron — is prepared at $t = 0$ with a Gaussian probability distribution of width $a$ centered at $x = 0$, with a central momentum $\hbar k_0$. Classically, this is a particle at a fuzzy position moving to the right at speed $\hbar k_0 / m$. Question: where is it at time $t$?

The classical answer is a Gaussian of the same width, centered at $x = \hbar k_0 t / m$. The quantum answer is *not the same Gaussian moved over*. The quantum Gaussian spreads. The width grows. After long enough, it covers a region many times wider than the original packet. The center moves at one speed; the individual crests inside the packet move at *another* speed; the two are not equal. None of this is intuitive. All of it is correct.

Reading about this is one thing. Watching $\sigma(t)$ grow on screen while you drag a slider is another. The point of building the simulation before reading Chapter 1 is to put the strange object in front of you so that when Chapter 1 explains what it means, you have a referent.

## 4. The Brutalist system — three files, one apparatus

The "Brutalist" name is borrowed from architecture, where it refers to a style that exposes its structural materials rather than hiding them behind decoration. The Brutalist system in this book is the same idea applied to code: the rules governing the simulations live in plain Markdown files you can read, edit, and version-control. There is no hidden configuration. Nothing is buried in a tool you do not own.

Three files do all the work.

### 4.1 `CLAUDE.md` — the coding constitution

This is the file Claude reads before every coding prompt. It tells Claude what kind of code is allowed and what is not. You write it once and reuse it across every simulation in the book. The rules below are the ones this book commits to. You can extend them; you should not silently override them, because the failure modes you would re-discover are the ones already documented.

The constitution names: the runtime (modern browser, no build step), the library (D3 v7 only, loaded by CDN), the drawing surface (SVG, not Canvas, not WebGL), the parameter exposure convention (HTML `<input type="range">` sliders firing on `input`), the animation loop (`requestAnimationFrame`), the file structure (single HTML file the user can double-click), the units convention (SI internally, displayed in physical units with labels), and the normalization indicator (every simulation prints $\int|\psi|^2\,dx$ and warns if it strays from 1 by more than 1%).

Three of these deserve a moment.

**SVG, not Canvas.** A 1D wave function is a curve. A potential is a curve. A probability density is a curve. SVG draws curves natively, with one `<path>` element per curve and a vector representation that scales cleanly. Canvas would force you to manage a pixel buffer and re-implement axes and labels. WebGL is overkill. SVG is the right primitive for the problems in this book, and it is the primitive D3 v7 is built around.

**Functions, not classes.** A simulation is mostly a pure function from parameters to a curve. Wrapping it in a class hides this and creates lifecycle problems (when do you instantiate? when do you destroy?). Plain functions — `computeWavefunction(x, t, params)` returning an array — are easier to read, test, and modify. The book commits to functional style for the simulation core.

**Normalization indicator.** Every simulation displays $\int |\psi|^2\,dx$ in a corner of the screen. It should read $1.000$. If it drifts, something is wrong — either the LLM has introduced a numerical error, or you have changed a parameter outside the physical range, or there is a bug. The indicator is the simulation's lie detector. Do not let any chapter's simulation ship without it.

### 4.2 `DESIGN.md` — the visual constitution

`DESIGN.md` governs what the simulation *looks like*: colors, fonts, axis labels, slider styling, light/dark mode. It is separated from `CLAUDE.md` because visual decisions and behavioral decisions break differently. If you decide partway through the semester that you want a different palette for an exam project, you edit `DESIGN.md` alone; the simulation behavior is untouched.

The color rules this book commits to:

- Probability density $|\psi|^2$ in blue (filled). It is the panel you watch.
- Real part $\mathrm{Re}\,\psi$ in orange (solid line). It oscillates.
- Imaginary part $\mathrm{Im}\,\psi$ in gray (dashed). Same envelope, $\pi/2$ phase shift.
- Potential $V(x)$ in red (solid).
- Energy levels $E_n$ in green (horizontal solid).
- Classical turning points in purple (dashed vertical).
- Axes and text in a neutral foreground color that follows `prefers-color-scheme`.

For two-dimensional plots — density maps, probability surfaces — we use perceptually uniform colormaps. **Viridis** for unsigned densities (it is monotonic in luminance, so it reads correctly in grayscale and for color-blind readers). **RdBu** for signed amplitudes (red-positive, blue-negative, centered on zero). These choices are not aesthetic — they preserve perceptual ordering. The colormap research (Kovesi 2015, [arXiv:1509.03700](https://arxiv.org/abs/1509.03700); Borland & Taylor 2007, *IEEE CG&A* 27, 14–17) is unambiguous: rainbow palettes lie about the data; Viridis and its kin do not.

### 4.3 `PROJECT.md` — the project state

`PROJECT.md` is the file Claude reads to remember the project. It is short — a few hundred words — and lists: which chapter you are on, which simulations exist, which parameter ranges were used, what has been verified, what is broken. Every time you finish a simulation, you add a line. Every time you fix a bug, you note it. Think of it as the project's lab notebook.

This is the file students forget exists. Don't. The reason `PROJECT.md` matters is the same reason a research lab keeps a notebook: tomorrow's you will not remember what today's you did. When Claude is asked "modify the Chapter 5 simulation to add a perturbation slider" three months from now, the model has no memory. `PROJECT.md` is the memory.

### 4.4 Why three files, not one

The natural question: why not put everything in one `CLAUDE.md`? Because of what we will call the *instruction budget*. Every token of instruction Claude reads costs attention against the actual physics request. When you ask in Chapter 7 for a hydrogen-atom radial-equation solver, you do not want the model to spend half its attention re-reading slider styling rules. Splitting concerns means the chapter-7 prompt loads `CLAUDE.md` (behavior) and `PROJECT.md` (state) and references `DESIGN.md` by name without ever quoting it. The visual rules are still in force; they just aren't burning context.

The same separation helps you. When the simulation looks wrong, you ask: is this a behavioral problem (wrong physics, wrong animation) or a visual problem (wrong color, wrong layout)? You know which file to open. The split is for debugging as much as for token economy.

**Misconception, addressed inline.** *"The Brutalist files are bureaucracy."* No. They are the reason every chapter's prompt produces consistent, debuggable code. Without them, you re-discover the same conventions every week, and your simulations look like twelve different students wrote them. The files are the *opposite* of bureaucracy: they make the rules explicit so you stop relitigating them.

## 5. The four-move prompt — Show, Say, Constrain, Verify

A prompt to Claude is not a wish. It is a specification. The four-move structure below is the one this book uses for every LLM Exercise. It is short, it is testable, and it is the reason most of the chapter simulations work on the first or second try rather than the seventh.

**Show.** Paste the artifact. The equation, the current code, the data. Don't describe it; show it. Vague problem descriptions are the number-one cause of bad LLM-generated code, because the model has to guess what you meant and the guess is often wrong. If you want the wave function $\psi(x, 0) = (1/(\pi a^2))^{1/4}\, e^{-x^2/(2a^2)}\, e^{i k_0 x}$, put the LaTeX in the prompt. Don't write "a Gaussian wave packet" and hope.

**Say.** Say what you want, in one sentence, with the audience and the use case. *"I want a single HTML file I can open in Chrome that lets me drag a slider to change $\sigma$ and see $|\psi|^2$ spread in real time."* The use case ("drag a slider," "open in Chrome") fixes the shape of the deliverable. Without it, Claude might give you a Python notebook.

**Constrain.** Name the constraints. D3 v7. Single file. No build step. Dark mode supported. Sliders fire on `input`. Normalization indicator visible. Constraints reduce hallucination because they shrink the space the model has to search. The constraints in this book live in `CLAUDE.md`; the prompt only names *additional* constraints specific to the chapter.

**Verify.** Ask Claude how to check the output. *"Tell me three things I should look at to verify the wave packet is evolving correctly."* This is the move that distinguishes a prompt from a wish. It converts Claude from oracle to collaborator. You get back a list — for the wave packet, something like *(a) the centroid should move at $v_g = \hbar k_0 / m$; (b) the width should grow as $\sigma(t) = \sqrt{\sigma_0^2 + (\hbar t / (2m\sigma_0))^2}$; (c) normalization should hold to within 1%*. You now have a rubric. You apply it to the rendered output. If a check fails, you know what to fix.

The verification step is the chapter-zero habit. Once you are doing the physics, you will trust the simulation and stop checking. That is when LLM hallucinations cause the worst damage. The verification stack is the immune response.

## 6. The free particle — physics you need for the simulation

You will see this material derived properly in Chapters 1 and 2. Here we state the results and use them.

### 6.1 The Gaussian wave packet at $t=0$

$$\psi(x, 0) = \left(\frac{1}{\pi a^2}\right)^{1/4} \exp\!\left(-\frac{x^2}{2 a^2}\right) \exp(i k_0 x).$$

Two ingredients. The Gaussian envelope $\exp(-x^2/(2a^2))$ localizes the particle around $x=0$ with width $a$. The plane-wave carrier $\exp(i k_0 x)$ gives it a central momentum $p_0 = \hbar k_0$, where $k_0$ is the central wavenumber. The prefactor $(1/(\pi a^2))^{1/4}$ is chosen so that $\int |\psi(x,0)|^2\,dx = 1$. You can verify this with one Gaussian integral: $\int_{-\infty}^{\infty} \exp(-x^2/a^2)\,dx = a\sqrt{\pi}$, so $\int |\psi(x,0)|^2\,dx = (1/(\pi a^2))^{1/2} \cdot a\sqrt{\pi} = 1$. Good.

### 6.2 Time evolution — the dispersion relation

The free particle ($V = 0$) has Hamiltonian $\hat{H} = \hat{p}^2/(2m) = -(\hbar^2/(2m))\,\partial^2/\partial x^2$. Each plane wave $e^{ikx}$ is an eigenfunction of $\hat{H}$ with eigenvalue $\hbar \omega(k)$, where the *dispersion relation* is

$$\omega(k) = \frac{\hbar k^2}{2m}.$$

This is non-relativistic and massive. A photon would have $\omega = c k$; this is not a photon. The quadratic dependence of $\omega$ on $k$ is what makes the wave packet spread.

A Gaussian wave packet is a superposition of plane waves with a Gaussian weight in $k$. Each plane wave evolves under its own phase $e^{-i \omega(k) t}$. Because different $k$'s have different $\omega$'s, the components dephase relative to one another and the packet spreads. The closed-form result (Griffiths §2.4, Problem 2.21) is another Gaussian, with the centroid translated and the width grown:

$$|\psi(x, t)|^2 = \frac{1}{\sqrt{2\pi}\,\sigma(t)} \exp\!\left(-\frac{(x - v_g t)^2}{2 \sigma(t)^2}\right),$$

with

$$\sigma(t)^2 = \frac{a^2}{2} + \frac{\hbar^2 t^2}{2 m^2 a^2}.$$

The width $\sigma(t)$ grows monotonically from $\sigma(0) = a/\sqrt{2}$. For long times, $\sigma(t) \approx \hbar t / (\sqrt{2}\, m\, a)$. The spread rate is *inversely* proportional to the initial width $a$: a narrower initial packet spreads faster. This is the Fourier-pair relation $\sigma_x \sigma_k \sim 1/2$ in disguise (see Chapter 1).

### 6.3 Group versus phase velocity — the chapter's surprise

Two velocities live in the packet. They are not the same.

The **phase velocity** is the speed at which a single plane wave crest moves:

$$v_p = \frac{\omega(k_0)}{k_0} = \frac{\hbar k_0}{2 m}.$$

The **group velocity** is the speed at which the envelope (and the centroid of $|\psi|^2$) moves:

$$v_g = \left.\frac{d\omega}{dk}\right|_{k_0} = \frac{\hbar k_0}{m} = \frac{p_0}{m}.$$

Take the ratio:

$$\frac{v_g}{v_p} = \frac{\hbar k_0 / m}{\hbar k_0 / (2m)} = 2.$$

The envelope moves *twice as fast* as the individual wave crests inside it. In the simulation, you will see this: the blue $|\psi|^2$ blob drifts to the right at $v_g$, and inside it, the orange Re $\psi$ ripples slip backward through the blob at $v_g - v_p = v_p$. The crests appear to be born at the front of the packet, travel back through it, and die at the back. They are not particles; they are phase. The blob is what carries momentum.

**Misconception, addressed inline.** *"Phase velocity is the speed of the particle."* No. Phase velocity is the speed of a single Fourier component, which is not by itself normalizable and not by itself physical. The particle, to the extent that a quantum particle has a speed at all, moves at $v_g = p/m$. The $v_p = p/(2m)$ that you might be tempted to associate with "the wave" is half the answer.

## 7. Worked example — an electron in a 1 nm wave packet

Let us put numbers on it. Pick an electron: $m = 9.109 \times 10^{-31}$ kg. Pick a width: $a = 1$ nm = $10^{-9}$ m. Pick a central wavenumber: $k_0 = 10$ nm$^{-1}$ = $10^{10}$ m$^{-1}$. Use $\hbar = 1.055 \times 10^{-34}$ J·s.

**Group velocity.**

$$v_g = \frac{\hbar k_0}{m} = \frac{(1.055 \times 10^{-34})(10^{10})}{9.109 \times 10^{-31}}\ \mathrm{m/s} \approx 1.16 \times 10^{6}\ \mathrm{m/s}.$$

About 0.4% of the speed of light. The non-relativistic assumption holds.

**Spreading time scale.** The packet's width has doubled when $\sigma(t) = 2 \sigma(0) = \sqrt{2}\, a$, i.e. when

$$\sigma(t)^2 - \frac{a^2}{2} = \frac{3 a^2}{2} \implies \frac{\hbar^2 t^2}{2 m^2 a^2} = \frac{3 a^2}{2} \implies t = \sqrt{3}\,\frac{m a^2}{\hbar}.$$

Plugging in: $t \approx 1.73 \cdot (9.109 \times 10^{-31})(10^{-9})^2 / (1.055 \times 10^{-34}) \approx 1.5 \times 10^{-14}$ s = 15 fs. In about 15 fs the packet doubles in width.

**Position after $t = 15$ fs.** $v_g t \approx (1.16 \times 10^{6})(1.5 \times 10^{-14}) \approx 1.7 \times 10^{-8}$ m = 17 nm. So in 15 fs the packet has drifted 17 nm to the right and doubled in width.

**The lesson.** Quantum particles on these scales (electron, nanometer, femtosecond) spread *fast*. The same calculation for a proton of the same width gives a spreading time longer by $m_p/m_e \approx 1836$, so $\sim 27$ ps. Same calculation for a marble: spreading time longer than the age of the universe. Quantum spreading is observable only for objects whose mass × length² is small in units of $\hbar$ × time-of-interest. **The limit.** This calculation assumed a free particle. In a potential, the packet does something else; that is Chapter 2 onward.

## 8. Exercises

**Exercise 0.1** — *(Remember / Understand)*. State in one sentence each what `CLAUDE.md`, `DESIGN.md`, and `PROJECT.md` do. Now state what each file is *not* for. (Hint: visual decisions belong in `DESIGN.md`, not `CLAUDE.md`.)

**Exercise 0.2** — *(Apply)*. The dispersion relation for a non-relativistic massive particle is $\omega(k) = \hbar k^2 / (2m)$. Compute the group velocity $v_g = d\omega/dk$ and the phase velocity $v_p = \omega/k$ at a general $k$. Verify $v_g = 2 v_p$. Now do the same for a photon ($\omega = c k$): show that $v_g = v_p = c$. What does the agreement of $v_g$ and $v_p$ tell you about a photon's "spreading"?

**Exercise 0.3** — *(Analyze)*. A proton wave packet ($m_p = 1.673 \times 10^{-27}$ kg) is prepared with $a = 1$ nm and $k_0 = 10$ nm$^{-1}$. Compute its group velocity, its doubling time, and its position after 15 fs. Compare to the electron values in Section 7. Why is the proton "more classical" on these scales?

**Exercise 0.4 (production)** — *(Create)*. Complete the LLM Exercise in Section 9. Save the resulting `00-wave-packet.html` and modify it: set $k_0 = 0$ and run the animation. The packet does not move, but it still spreads. Explain in two sentences what this tells you about the difference between "motion" and "uncertainty growth."

**Exercise 0.5** — *(Evaluate)*. Open the file Claude produced in Exercise 0.4. Find the line of code that implements the dispersion relation. Find the line that draws the SVG path for $|\psi|^2$. Find the line that updates the normalization indicator. Write a one-paragraph annotated walkthrough of these three lines. *(If you cannot find any of the three: that is a bug. The chapter's verification stack should have caught it. Re-run the prompt.)*

## 9. LLM Exercise — your first simulation

This is the chapter's deliverable. You will produce three Markdown files and one HTML file. Open Claude (or another capable LLM) and paste the four prompts below in order. The prompts are written to be paste-ready; do not edit them on the first run.

### Part A — The `CLAUDE.md` prompt (the coding constitution)

````markdown
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
- Do not use any library other than D3 v7. (Math.js and fft-js may be added
  later with explicit prompt approval.)
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
````

### Part B — The `DESIGN.md` prompt (the visual constitution)

````markdown
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
````

### Part C — The `PROJECT.md` prompt (project state)

````markdown
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
````

### Part D — The simulation prompt (four moves: Show / Say / Constrain / Verify)

````markdown
SHOW.
The free-particle Gaussian wave packet has the closed-form solution

  ψ(x, 0) = (1/(πa²))^(1/4) · exp(−x²/(2a²)) · exp(i k₀ x)

evolving under Ĥ = p̂²/(2m) to

  |ψ(x, t)|² = (1/(√(2π) σ(t))) · exp(−(x − v_g t)²/(2 σ(t)²))

with σ(t)² = a²/2 + ℏ²t²/(2 m² a²), v_g = ℏk₀/m, v_p = ℏk₀/(2m).

The wave function itself at time t (analytic, derived in Griffiths §2.4
Problem 2.21) is

  ψ(x, t) = (1/(πa²))^(1/4) · (a / γ(t))^(1/2) ·
            exp(i k₀ x − i ω₀ t) ·
            exp( − (x − v_g t)² / (2 γ(t)²) )

where γ(t) = a · (1 + i ℏ t / (m a²))^(1/2) is complex and you should
compute Re ψ and Im ψ from this complex form. ω₀ = ℏ k₀² / (2m).

Use the CLAUDE.md and DESIGN.md saved earlier as binding context.

SAY.
Produce a single file named `00-wave-packet.html`. It opens in a browser and
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
- Normalization indicator pinned top-right. Display as "∫|ψ|² dx = 1.000".
  Recompute every frame with the trapezoidal rule on the grid; red if
  |I − 1| > 0.01.
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
````

### Part E — Exploration tasks

After the simulation is rendering correctly:

1. **Set $k_0 = 0$.** The packet should not translate. Confirm: $v_g = 0$. But the packet still spreads. *Spreading is not motion.* Write down what this distinguishes.
2. **Set $\sigma = 0.2$ nm, $k_0 = 10$ nm$^{-1}$.** Run for 5 fs. Now set $\sigma = 2$ nm, $k_0 = 10$ nm$^{-1}$. Run for 5 fs. The narrower packet spreads visibly faster. *Why?* Use $\sigma(t)^2 = a^2/2 + \hbar^2 t^2 / (2 m^2 a^2)$ to explain.
3. **Watch the inside of the packet.** Set $k_0 = 5$ nm$^{-1}$, $\sigma = 2$ nm. Slow the time step to $10^{-16}$ s/frame. The blue blob moves right at $v_g$. The orange Re $\psi$ ripples inside it move right at $v_p = v_g / 2$. In the rest frame of the blob, the ripples appear to move *backward*. State whether this is physical motion of anything or a phase effect.
4. **Compare to classical.** A classical electron at $x=0$ with momentum $\hbar k_0$ moves at $v_g$ and stays a point. Run the simulation, take a screenshot at $t = 0$ and $t = 30$ fs, and overlay where the classical particle would be. The quantum centroid agrees with classical position; the quantum width does not.

### Part F — Extension prompt

````markdown
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
````

When this extension renders correctly, you have seen the punchline of the chapter: position spread grows because momentum has a distribution; momentum has a distribution because the packet is localized; neither side of the Fourier pair will let the other be sharp. Chapter 1 will name this.

## 10. What would change my mind

I claim that interactive simulation produces faster conceptual learning than reading alone, and the strongest evidence is Hake's 1998 meta-analysis ([*Am. J. Phys.* 66, 64–74](https://www.compadre.org/portal/items/detail.cfm?ID=2099)), which found roughly a 2σ effect size for interactive engagement over traditional lecture in introductory mechanics. If a careful replication in upper-division quantum mechanics — comparing students who built simulations against students who used the same conceptual exercises without simulations, with matched pre-tests on the QMCS (McKagan et al. 2010, [*Phys. Rev. ST PER* 6, 020121](https://journals.aps.org/prper/abstract/10.1103/PhysRevSTPER.6.020121)) — found no difference or a reversal, I would have to revise the central pedagogical claim of this book. The PhET evidence (Wieman, Adams & Perkins 2008, [*Science* 322, 682–683](https://www.science.org/doi/10.1126/science.1161948)) is suggestive but the LLM-generated branch of this book has not been tested.

## 11. Still puzzling

- The Brutalist file split (CLAUDE / DESIGN / PROJECT) is principled but the boundaries are not always obvious: when does a slider's keyboard-accessibility rule belong in CLAUDE.md vs. DESIGN.md? I have argued for behavior-vs-appearance, but accessibility crosses both.
- The verification stack catches arithmetic errors. It does not catch *conceptual* errors that produce numerically plausible output. For example: a simulation that swaps the labels "Re $\psi$" and "Im $\psi$" will pass every quantitative check. The visual check is the only defense, and it requires the student to *already* know what the right picture looks like.
- LLM-generated simulation code drifts in style between sessions even with `CLAUDE.md` in the prompt. The book commits to the Brutalist files as a stabilizer, but I do not have a clean answer for "the simulation worked last week and now it doesn't." Re-running the same prompt is part of the workflow; the chapter has not yet documented the failure mode well.
- The chapter does not teach JavaScript. It teaches the student to read and modify what Claude produces. Whether that is enough for the harder chapters (Chapter 7, hydrogen; Chapter 11, perturbation theory) is something the course's first run will reveal.

**Tags:** wave-packet, group-velocity, phase-velocity, D3, Brutalist-system, four-move-prompt, PhET, verification-stack

---

*Voice flag: this chapter is structurally different from the rest of the book — no physics deep-dive in the Feynman sense; the deep-dive is offloaded to Chapter 1. The next chapter restores the standard chapter anatomy.*

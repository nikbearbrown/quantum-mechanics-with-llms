# Chapter 11 — The WKB Approximation and Tunneling

> A semiclassical approximation that delivers one of the most consequential predictions in physics — and the chapter where you watch a quantum wave packet pass through a wall it has no business passing through.

---

## 1. What this chapter is doing

Quantum tunneling is not exotic. It is the reason the sun shines. It is the reason a USB stick remembers what you put on it. It is the reason a scanning tunneling microscope can image individual atoms. It is the mechanism behind alpha radioactivity, every Josephson junction in a superconducting qubit, the deuterium-tritium fusion process at the core of stars, and the cosmological problem of false-vacuum decay. Tunneling is one of the most physically consequential predictions of quantum mechanics, and the WKB approximation is the tool that makes it tractable.

The chapter delivers four things. First, the WKB ansatz — write the wave function as $\psi = e^{iS/\hbar}$ and expand $S$ in powers of $\hbar$. Second, the tunneling formula $T \approx \exp[-(2/\hbar)\int\sqrt{2m(V-E)}\,dx]$ — the Gamow factor, dominant exponential in barrier penetration, the object that explains 24 orders of magnitude of alpha-decay halflives. Third, the Bohr-Sommerfeld quantization condition $\oint p\,dx = (n+1/2)h$ — the WKB version of bound states. Fourth, a worked alpha-decay calculation that reproduces the Geiger-Nuttall law from first principles.

The simulation is the chapter's centerpiece. You will build three nested visualizations: stationary transmission $T(E)$ for a rectangular barrier (exact vs. WKB on a log axis), general-barrier WKB tunneling with a shape selector, and — the heart of the chapter — an *animated Gaussian wave packet hitting a barrier* computed via the Crank-Nicolson method. The wave packet splits into a reflected piece and a transmitted piece. You watch the transmitted piece emerge. *This is the visualization that cannot be replicated in print.* Every classical intuition you had about barriers will be gone after you watch it once.

## 2. Learning objectives

By the end of this chapter you should be able to:

- Derive the WKB ansatz $\psi(x) \approx (C/\sqrt{p(x)})\exp[\pm(i/\hbar)\int p\,dx']$ by expanding $S(x)$ in powers of $\hbar$.
- State the validity condition $|d\lambda_{dB}/dx| \ll 1$ (potential varies slowly on the de Broglie wavelength scale).
- Sketch the connection formulas at a classical turning point and identify the role of the Maslov index.
- Apply the tunneling formula $T \approx e^{-2\gamma}$ to a rectangular and a Coulomb barrier.
- Derive the Bohr-Sommerfeld quantization condition $\oint p\,dx = (n+1/2)h$ as the bound-state WKB.
- Compute the Gamow factor for alpha decay and reproduce the Geiger-Nuttall correlation.
- Build a D3 simulation that animates a Gaussian wave packet via Crank-Nicolson and shows tunneling in real time.

## 3. Motivating problem

A polonium-212 nucleus has a halflife of about $3 \times 10^{-7}$ seconds. A thorium-232 nucleus has a halflife of about $1.4 \times 10^{10}$ years. Both decay by emitting an alpha particle through what looks like the same physical mechanism. The ratio of halflives is roughly $10^{24}$ — twenty-four orders of magnitude.

How can a single mechanism produce such an enormous dynamic range? In 1911 and 1912, Hans Geiger and John Mitchell Nuttall plotted alpha-decay halflives against alpha-particle energies for many isotopes and discovered an empirical correlation: $\log\tau_{1/2}$ is approximately linear in $1/\sqrt{E_\alpha}$ for fixed daughter charge $Z$ ([Geiger & Nuttall, *Phil. Mag.* 22, 613, 1911; 23, 439, 1912](https://doi.org/10.1080/14786441108637153) [verify]). A straight line on a log-vs-inverse-square-root plot. It was a beautiful empirical fact with no theoretical explanation.

The classical picture made things worse. An alpha particle approaching a nucleus sees a Coulomb potential. At the nuclear radius $R \approx 7\,\text{fm}$ for heavy nuclei, the Coulomb barrier is on the order of $V_{\text{max}} \approx 30\,\text{MeV}$. A typical emitted alpha has $E \approx 5\,\text{MeV}$. Classically, the alpha is below the barrier; classically, it cannot get out. It does not have the energy.

In 1928, George Gamow, working in Göttingen and using brand-new quantum mechanics, computed the probability of an alpha particle *tunneling* through the Coulomb barrier ([Gamow, "Zur Quantentheorie des Atomkernes," *Z. Phys.* 51, 204, 1928](https://link.springer.com/article/10.1007/BF01343196), submitted 29 July 1928). Independently and within a day, Ronald Gurney and Edward Condon at Princeton submitted the same idea to *Nature* ([*Nature* 122, 439, 1928](https://www.nature.com/articles/122439a0); fuller treatment in [*Phys. Rev.* 33, 127, 1929](https://journals.aps.org/pr/abstract/10.1103/PhysRev.33.127)). Both groups got the same answer: the tunneling probability is exponentially sensitive to barrier height, barrier width, and particle energy, and the resulting decay rate spans the 24-decade range of observed halflives.

Two further questions sit in this puzzle. *How does a particle "tunnel"? Where is it inside the barrier?* (The pop-science answer — "energy borrowing through the uncertainty principle" — is wrong, and the chapter will say so.) *Why is the rate so exponentially sensitive?* The first answer is in the math; the second is the entire point. By the end of the chapter you will understand both, and you will have watched a wave packet split in two as it hits a wall.

## 4. Concept block — the WKB ansatz

### 4.1 An exact rewriting

The time-independent Schrödinger equation in one dimension:

$$-\frac{\hbar^2}{2m}\,\psi''(x) + V(x)\psi(x) = E\psi(x)$$

Define the local classical momentum:

$$p(x) = \sqrt{2m(E - V(x))}$$

In the classically allowed region ($E > V$), $p(x)$ is real. In the classically forbidden region ($E < V$), $p(x)$ is imaginary; write $|p(x)| = \sqrt{2m(V - E)}$ for the magnitude.

Now write the wave function exactly as

$$\psi(x) = \exp\!\left[\frac{i}{\hbar}S(x)\right]$$

This is just a *definition* of $S(x)$ — it is exact for any $\psi$, the function $S$ is in general complex. Substitute into the Schrödinger equation:

$$\psi' = \frac{i}{\hbar}S'\psi, \quad \psi'' = \left[\frac{i}{\hbar}S'' - \frac{1}{\hbar^2}(S')^2\right]\psi$$

So

$$-\frac{\hbar^2}{2m}\left[\frac{i}{\hbar}S'' - \frac{(S')^2}{\hbar^2}\right]\psi + V\psi = E\psi$$

$$\frac{(S')^2}{2m} - \frac{i\hbar}{2m}S'' = E - V(x)$$

This is the *exact* equation for $S(x)$. It is nonlinear and not easier than the original Schrödinger equation. But it is in a form that allows a controlled expansion in $\hbar$.

### 4.2 Expand in powers of $\hbar$

Write

$$S(x) = S_0(x) + \frac{\hbar}{i}S_1(x) + \left(\frac{\hbar}{i}\right)^2 S_2(x) + \cdots$$

Substitute and match powers of $\hbar$.

**Order $\hbar^0$.** The leading equation gives

$$\frac{(S_0')^2}{2m} = E - V(x) \;\Longrightarrow\; S_0'(x) = \pm p(x)$$

So

$$S_0(x) = \pm\int p(x')\,dx'$$

The two signs correspond to right- and left-moving waves in the classically allowed region; to growing and decaying exponentials in the forbidden region.

**Order $\hbar^1$.** Collecting the next-order terms:

$$\frac{2 S_0' S_1'}{2m} - \frac{i}{2m}S_0'' \cdot \frac{1}{i} \cdot i = 0$$

After bookkeeping (and being careful with the factor of $1/i$ in the expansion):

$$S_1'(x) = -\frac{1}{2}\frac{p'(x)}{p(x)} \;\Longrightarrow\; S_1(x) = -\frac{1}{2}\ln p(x)$$

So $e^{(\hbar/i)\cdot S_1/\hbar} = e^{-S_1\cdot i} = (\text{ignoring the }i)\, 1/\sqrt{p(x)}$ up to phase. Carefully tracking signs and phases (a calculation worth doing once and pinning), the result is

$$\boxed{\psi_{\text{WKB}}(x) \approx \frac{C}{\sqrt{p(x)}}\exp\!\left[\pm\frac{i}{\hbar}\int p(x')\,dx'\right]}$$

in the classically allowed region, and

$$\boxed{\psi_{\text{WKB}}(x) \approx \frac{C}{\sqrt{|p(x)|}}\exp\!\left[\pm\frac{1}{\hbar}\int|p(x')|\,dx'\right]}$$

in the classically forbidden region. (Griffiths §9.1; Liboff §7.10 [verify].)

### 4.3 What the prefactor is doing

The factor $1/\sqrt{p(x)}$ has a clean classical interpretation. The classical probability of finding the particle in $[x, x+dx]$ is proportional to the time it spends there, which is $dx/v(x) \propto 1/p(x)$. So $|\psi_{\text{WKB}}|^2 \propto 1/p(x)$ — the wave function spends time in proportion to where the classical particle spends time. This is the *semi*-classical part of "semiclassical." The phase oscillates quantum-mechanically; the envelope tracks classical mechanics.

### 4.4 Where WKB is valid

The expansion above assumes higher-order terms are small. The next-order correction $S_2$ involves $S_0''/(S_0')^2 = p'/p^2$. So WKB is valid where

$$\left|\frac{\hbar\,p'(x)}{p^2(x)}\right| \ll 1$$

Equivalently, defining the local de Broglie wavelength $\lambda(x) = h/p(x)$:

$$\left|\frac{d\lambda}{dx}\right| \ll 1$$

The potential must vary slowly across one de Broglie wavelength. WKB works when $\hbar$ is small (semiclassical limit), or equivalently when the action is large relative to $\hbar$.

The validity condition fails *exactly* at classical turning points ($E = V(x_0)$), where $p \to 0$ and $\lambda \to \infty$. The wave function near a turning point cannot be approximated by either the oscillating or the decaying WKB form — it transitions from one to the other. The fix is the *connection formula*.

## 5. Concept block — connection formulas and Bohr-Sommerfeld

### 5.1 Connection formulas (sketch)

Near a classical turning point $x_0$ where $E = V(x_0)$, linearize the potential:

$$V(x) \approx V(x_0) + V'(x_0)(x - x_0)$$

The Schrödinger equation in this linear potential is the *Airy equation*:

$$\psi''(z) = z\psi(z)$$

(after a rescaling). Its solutions are the Airy functions $\text{Ai}(z)$ and $\text{Bi}(z)$, which oscillate for $z < 0$ (the classically allowed side) and decay (or grow) for $z > 0$ (the forbidden side). Match the asymptotic forms of $\text{Ai}$ on each side of the turning point to the WKB forms on each side, and you get the connection formulas.

For a turning point at $x = a$ with classically allowed region to the *left* and forbidden region to the *right*:

$$\frac{2C}{\sqrt{p(x)}}\cos\!\left[\frac{1}{\hbar}\int_x^a p\,dx' - \frac{\pi}{4}\right] \;\longleftrightarrow\; \frac{C}{\sqrt{|p(x)|}}\exp\!\left[-\frac{1}{\hbar}\int_a^x|p|\,dx'\right]$$

The $\pi/4$ phase at each turning point is the *Maslov index* contribution — a subtle but real consequence of the matching procedure. (Bender & Orszag, *Advanced Mathematical Methods for Scientists and Engineers*, 1978, Chapter 10 [verify] — the canonical reference for the matched-asymptotic derivation.)

The chapter does not derive the matching in full; the calculation is technically involved and the reward-per-effort is low for a first pass. What you need is the result: each turning point contributes a phase of $\pi/4$, and that phase is the input to the Bohr-Sommerfeld quantization condition.

### 5.2 Bohr-Sommerfeld quantization

For a particle bound between two classical turning points $a$ and $b$ ($V(x) < E$ in between, $V > E$ outside), single-valuedness and normalizability of the WKB wave function require the phase integral over one classical period to be an integer multiple of $2\pi$, plus the Maslov contribution of $\pi/4$ at each turning point.

Adding it up:

$$\frac{1}{\hbar}\oint p\,dx - \frac{\pi}{4} - \frac{\pi}{4} = (n+1) \pi - \pi = n\pi$$

Rearranging:

$$\boxed{\oint p(x)\,dx = 2\int_a^b p(x)\,dx = \left(n + \tfrac{1}{2}\right) h, \quad n = 0, 1, 2, \ldots}$$

This is the **Bohr-Sommerfeld quantization condition**. The integer comes from counting wave function nodes; the $1/2$ comes from the Maslov index (the two $\pi/4$ contributions at the turning points). Old Bohr-Sommerfeld 1913–1916 had $nh$, with no Maslov correction; the upgrade came when WKB was put on rigorous footing.

For the harmonic oscillator, this formula gives $E_n = (n + 1/2)\hbar\omega$ — *exactly*, not just to leading order in $\hbar$. The same formula gives, for the hydrogen atom in the Coulomb potential, the Bohr energies $E_n = -E_1/n^2$ exactly. These coincidences are why Bohr-Sommerfeld worked as well as it did before quantum mechanics existed; WKB shows that they are *not* coincidences but consequences of the symmetry of these particular potentials. For most other potentials, Bohr-Sommerfeld is leading-order accurate only.

## 6. Concept block — the tunneling formula

### 6.1 Through a barrier

Consider a particle with energy $E$ incident on a barrier $V(x) > E$ between two turning points $a$ and $b$. The classically forbidden region is the interval $[a, b]$. In that region, the WKB wave function decays exponentially. Following the wave through the barrier and out the other side, and using the connection formulas to match the exponentially decaying form to the oscillating form on each side, the transmission coefficient is

$$\boxed{T \approx \exp\!\left[-\frac{2}{\hbar}\int_a^b\sqrt{2m(V(x) - E)}\,dx\right] = e^{-2\gamma}}$$

The exponent

$$\gamma = \frac{1}{\hbar}\int_a^b\sqrt{2m(V(x) - E)}\,dx$$

is the **Gamow factor**. Three features of this formula deserve attention.

*Exponential sensitivity.* The transmission depends *exponentially* on barrier parameters. A small change in barrier height, width, or particle energy is amplified into a giant change in $T$. This is the reason alpha-decay halflives span 24 orders of magnitude and the reason an STM can image individual atoms.

*The barrier shape integrates into the formula.* Square barriers, parabolic barriers, Coulomb barriers — all get the same treatment. You just compute the integral.

*The exponent dominates the prefactor.* The full WKB formula has prefactors of order unity that depend on the details of barrier matching, but the exponential carries the physics. When estimating tunneling rates, computing $\gamma$ and exponentiating is enough.

### 6.2 Rectangular barrier — exact vs. WKB

The rectangular barrier ($V = V_0$ between $x=0$ and $x=L$, zero outside) is the calibration point. The *exact* transmission coefficient, derived by matching plane waves across the barrier (Griffiths Example 2.7; Liboff §7.7):

$$T_{\text{exact}} = \left[1 + \frac{V_0^2\sinh^2(\kappa L)}{4E(V_0 - E)}\right]^{-1}, \quad \kappa = \frac{\sqrt{2m(V_0 - E)}}{\hbar}$$

For $\kappa L \gg 1$ (thick or tall barrier), $\sinh(\kappa L) \approx e^{\kappa L}/2$:

$$T_{\text{exact}} \approx \frac{16 E(V_0 - E)}{V_0^2}\,e^{-2\kappa L}$$

The WKB prediction (since $V$ is constant, the integral is trivial):

$$T_{\text{WKB}} = e^{-2\kappa L}$$

So WKB gets the *exponential* right and misses the prefactor by an $O(1)$ factor that depends on $E/V_0$. *This is the most important fact in the chapter.* The exponential carries the physics; the prefactor is a smooth function of order unity that the leading WKB does not capture. The simulation will let you put $T_{\text{exact}}$ and $T_{\text{WKB}}$ on the same log plot and watch the two curves run parallel with constant offset.

## 7. Concept block — alpha decay and the Geiger-Nuttall law

### 7.1 The Coulomb barrier

Model an alpha particle as a pre-formed cluster bouncing inside a nucleus of radius $R$. Inside the nucleus, the alpha sees a strong nuclear potential that confines it. Outside the nucleus, the alpha sees a Coulomb potential from the daughter nucleus (charge $Z' = Z - 2$, where $Z$ is the parent):

$$V(r) = \frac{2(Z-2)e^2}{4\pi\epsilon_0 r}, \quad r > R$$

The alpha has energy $E > 0$ (the decay $Q$-value); the Coulomb barrier extends from $r = R$ outward to $r = r_c$ where $V(r_c) = E$:

$$r_c = \frac{2(Z-2)e^2}{4\pi\epsilon_0 E}$$

For uranium-238 ($Z = 92$, daughter charge $90$, $E_\alpha \approx 4.2\,\text{MeV}$), $r_c \approx 60\,\text{fm}$. The nuclear radius is $R \approx 7.4\,\text{fm}$. The alpha is below the Coulomb barrier by a factor of about 8.

### 7.2 The Gamow integral

Compute the Gamow factor:

$$\gamma = \frac{1}{\hbar}\int_R^{r_c}\sqrt{2m_\alpha\!\left[\frac{2(Z-2)e^2}{4\pi\epsilon_0 r} - E\right]}\,dr$$

Substitute $r = r_c\sin^2\theta$. The integral becomes (after some algebra)

$$\gamma = \sqrt{\frac{2m_\alpha E}{\hbar^2}}\,r_c\!\left[\arccos\sqrt{R/r_c} - \sqrt{R/r_c(1 - R/r_c)}\right]$$

For $R \ll r_c$ (typical for heavy nuclei),

$$\gamma \approx \frac{\pi}{2}\sqrt{\frac{2m_\alpha E}{\hbar^2}}\,r_c - 2\sqrt{\frac{2m_\alpha E}{\hbar^2}}\sqrt{Rr_c}$$

Using $r_c \propto 1/E$ in the first term:

$$\gamma \approx \frac{\pi(Z-2)e^2}{4\epsilon_0\hbar}\sqrt{\frac{m_\alpha}{2E}} - \text{correction}$$

The decay rate is

$$\Gamma \sim \nu_0\,e^{-2\gamma}$$

where $\nu_0 \sim v/(2R)$ is the attempt frequency — how often the alpha bounces against the inside of the barrier ($\sim 10^{21}\,\text{Hz}$ for typical nuclear parameters). Taking the log of the halflife:

$$\log_{10}\tau_{1/2} = -\log_{10}\Gamma + \text{const} \approx A(Z) + \frac{B(Z)}{\sqrt{E_\alpha}}$$

This is the **Geiger-Nuttall law**. A plot of $\log\tau$ vs. $1/\sqrt{E}$ for alpha emitters of fixed daughter $Z$ is a straight line. The empirical observation from 1911 is *derived* from the WKB tunneling formula. The 24-decade dynamic range is the dynamic range of an exponential.

### 7.3 Putting numbers to it

For $^{238}$U: $Z = 92$, $E_\alpha = 4.2\,\text{MeV}$, $m_\alpha = 6.6\times 10^{-27}\,\text{kg}$. Plugging in:

$$\gamma \approx 43$$

So $e^{-2\gamma} \approx e^{-86} \approx 4 \times 10^{-38}$. The attempt frequency $\nu_0 \approx 5 \times 10^{21}\,\text{Hz}$. So the decay rate is $\Gamma \sim 2 \times 10^{-16}\,\text{s}^{-1}$, giving a halflife of $\tau_{1/2} = \ln 2/\Gamma \approx 10^{16}\,\text{s} \approx 3 \times 10^8\,\text{years}$. The experimental halflife is $4.5 \times 10^9$ years — within an order of magnitude of the back-of-envelope WKB estimate. **An order of magnitude on a quantity spanning 24 orders of magnitude is excellent.** The remaining factor of 15 comes from finer-grained prefactors and from the pre-formation probability of the alpha cluster inside the nucleus.

This is one of the high-water marks of quantum mechanics applied to nuclear physics. A first-principles back-of-envelope calculation reproduces a halflife of billions of years.

## 8. Concept block — three more applications

### 8.1 Scanning tunneling microscopy

Gerd Binnig and Heinrich Rohrer at IBM Zurich built the first STM in 1981. The first successful image of an atomically resolved Si(111) 7×7 surface reconstruction appeared in [*Phys. Rev. Lett.* 49, 57 (1982)](https://journals.aps.org/prl/abstract/10.1103/PhysRevLett.49.57); the earlier vacuum-tunneling demonstration appeared in [*Appl. Phys. Lett.* 40, 178 (1982)](https://aip.scitation.org/doi/10.1063/1.92999). Binnig and Rohrer shared the 1986 Nobel.

Mechanism: bring a metal tip within a few angstroms of a conducting sample. Apply a small bias voltage (mV scale). Electrons tunnel through the vacuum gap. The tunneling current depends exponentially on the tip-sample distance $d$:

$$I \propto e^{-2\kappa d}, \quad \kappa = \frac{\sqrt{2m_e\phi}}{\hbar} \approx 0.51\,\text{Å}^{-1}\sqrt{\phi/\text{eV}}$$

where $\phi$ is the work function (4–5 eV for typical metals). With $\kappa \approx 1\,\text{Å}^{-1}$, a 1-Å change in $d$ changes $I$ by a factor of $e^2 \approx 7.4$ — almost an order of magnitude per atomic radius.

This is the *reason* STM is atomically resolved. A typical surface has features of sub-angstrom amplitude; the exponential transduction turns those features into measurable current swings. The exponential is the measurement.

### 8.2 Stellar nuclear fusion

Arthur Eddington conjectured in 1920 that stellar energy came from hydrogen fusion, but the classical objection was severe: at the Sun's core temperature ($\sim 1.5\times 10^7\,\text{K}$, $kT \sim 1\,\text{keV}$), the average proton-proton thermal energy is roughly $10^{-3}$ of the Coulomb barrier at the nuclear-contact distance ($\sim 1\,\text{MeV}$). Classically, fusion is forbidden in stars.

Robert Atkinson and Friedrich Houtermans, in [*Z. Phys.* 54, 656 (1929)](https://link.springer.com/article/10.1007/BF01341723) [verify], applied Gamow's tunneling formula to stellar fusion. The fusion rate is the product of the *Maxwell-Boltzmann tail* (which gives the probability of a proton having an unusually high energy) and the *Gamow penetration factor* (which gives the probability of tunneling through the Coulomb barrier at that energy). The product peaks at an energy intermediate between the thermal energy and the barrier height — the **Gamow peak** — where most of the fusion occurs. The fusion rate in any star is computed by integrating this product over relative kinetic energies. Every star burns by tunneling.

### 8.3 Flash memory

A floating-gate transistor stores a bit by trapping electrons on a polysilicon gate isolated by a thin (5–10 nm) silicon-dioxide layer. Writing: a high voltage drives electrons *through* the oxide and onto the floating gate by Fowler-Nordheim tunneling. Reading: the trapped charge changes the transistor threshold voltage. Erasing: the voltage is reversed and the electrons tunnel back out.

Fowler-Nordheim tunneling through a triangular oxide barrier gives current density

$$J \propto \mathcal{E}^2\exp\!\left[-\frac{K}{\mathcal{E}}\right]$$

where $\mathcal{E}$ is the oxide electric field and $K$ depends on the barrier height (electron affinity of the oxide). The original analysis is [Fowler & Nordheim, *Proc. R. Soc. A* 119, 173 (1928)](https://royalsocietypublishing.org/doi/10.1098/rspa.1928.0091) [verify]; the entire device geometry of flash memory (Kahng & Sze 1967 [verify]) is an exercise in engineering this exponential. Roughly every storage technology in your laptop, phone, and SSD is *built* around tunneling rates.

### 8.4 Failure case — cold fusion

Martin Fleischmann and Stanley Pons announced in March 1989 that they had observed "cold fusion" — deuterium-deuterium fusion at room temperature in a palladium electrochemical cell. The claim required deuteron tunneling rates far above what the Gamow factor allows. Compute it: at room temperature ($kT \approx 0.025\,\text{eV}$), the Gamow factor for D-D tunneling through the Coulomb barrier at the nuclear-contact distance gives $e^{-2\gamma} \sim 10^{-75}$. No chemical environment can boost this number by even ten decades, let alone seventy. The fusion rate predicted by tunneling theory falls short of the claimed power output by more than seventy orders of magnitude.

This is the textbook example of *the exponential dominates*. Chemistry cannot lower a nuclear-scale Gamow factor enough to recover the cold-fusion claim. The back-of-envelope tunneling estimate falsifies the claim with room to spare. The point is not to litigate Fleischmann-Pons; the point is that knowing how to compute a Gamow factor is enough to evaluate any "novel nuclear effect at room temperature" claim quantitatively.

### 8.5 The honest open case — quantum biology

Per-Olov Löwdin proposed in [*Rev. Mod. Phys.* 35, 724 (1963)](https://journals.aps.org/rmp/abstract/10.1103/RevModPhys.35.724) that protons in the hydrogen bonds of Watson-Crick DNA base pairs can tunnel between their two tautomeric positions, occasionally flipping a base into a mismatched form that causes a point mutation during replication. The mechanism is over 60 years old and remains contested. Recent open-system simulations ([Slocombe et al., *Commun. Phys.* 5, 109, 2022](https://www.nature.com/articles/s42005-022-00881-8) [verify]) suggest the mechanism may be viable for G:C pairs but not A:T.

This is the chapter's honest-about-uncertainty case. The math is the same Gamow factor you have learned. The biology — whether proton tunneling actually contributes to mutation rates in living cells — is not settled. The methodology for telling settled tunneling stories from speculative ones is exactly the back-of-envelope rate estimate you have learned. *Use it on every quantum-biology claim you read.*

## 9. Worked examples and exercises

### Worked example — STM current ratio

A tip is 5 Å above a metal surface with work function $\phi = 4\,\text{eV}$. Compute $\kappa = (1/\hbar)\sqrt{2m_e\phi}$:

$$\kappa = \frac{\sqrt{2 \cdot 9.1 \times 10^{-31}\,\text{kg} \cdot 4 \cdot 1.6 \times 10^{-19}\,\text{J}}}{1.05 \times 10^{-34}\,\text{J·s}} \approx 1.0 \times 10^{10}\,\text{m}^{-1} = 1.0\,\text{Å}^{-1}$$

The current at 5 Å: $I(5) \propto e^{-10}$. At 6 Å: $I(6) \propto e^{-12}$. Ratio: $I(5)/I(6) = e^2 \approx 7.4$. A one-angstrom increase in tip-sample distance drops the tunneling current by a factor of 7. This is what makes STM see atoms.

### Exercises

**Warm-up.**

1. State the WKB validity condition in terms of the local de Broglie wavelength. Explain in one sentence why it fails at a classical turning point.

2. Verify that for the harmonic oscillator $V(x) = (1/2)m\omega^2 x^2$, the Bohr-Sommerfeld condition $\oint p\,dx = (n+1/2)h$ gives $E_n = (n+1/2)\hbar\omega$ exactly. (Hint: compute the phase-space area for an ellipse of energy $E$.)

3. For a particle of energy $E < V_0$ incident on a square barrier of height $V_0$ and width $L$, write down both the exact transmission $T_{\text{exact}}$ and the WKB transmission $T_{\text{WKB}}$. Take the limit $\kappa L \gg 1$ and identify the prefactor difference.

**Application.**

4. Compute the WKB transmission coefficient for an electron with $E = 1\,\text{eV}$ incident on a rectangular barrier of height $V_0 = 5\,\text{eV}$ and width $L = 5\,\text{Å}$. Report $T$ in scientific notation; do not give a number in linear units.

5. Estimate the Gamow factor for an alpha particle ($m_\alpha = 4u$) of energy $E_\alpha = 5\,\text{MeV}$ tunneling through the Coulomb barrier of a daughter nucleus with $Z' = 82$ (lead). Use the approximation $\gamma \approx (\pi Z' e^2 / 4\epsilon_0\hbar)\sqrt{m_\alpha/2E_\alpha}$. Estimate the halflife using attempt frequency $\nu_0 = 10^{21}\,\text{Hz}$.

6. For STM with a 4-eV work function, what is the percentage change in tunneling current per 0.1-Å change in tip height? Justify why this sensitivity makes STM the right technique for atomic-resolution imaging of a surface with sub-angstrom topography.

**Synthesis.**

7. The **Gamow peak** in stellar fusion. The fusion rate per unit time per particle pair is the integral over relative energies $E$ of:
$$\text{rate}(E) \propto e^{-E/kT} \cdot e^{-b/\sqrt{E}}$$
where the first factor is the Maxwell-Boltzmann tail (probability of relative energy $E$) and the second is the Gamow factor with $b$ depending on the charges and masses. Show that the integrand peaks at $E_G = (bkT/2)^{2/3}$ — the **Gamow peak energy**. For pp fusion in the Sun ($T \approx 1.5\times 10^7\,\text{K}$), compute $E_G$ and compare to $kT$. The ratio $E_G/kT$ tells you why fusion is dominated by the high-energy tail of the thermal distribution.

8. **The Geiger-Nuttall log-vs-inverse-square-root plot.** Find experimental halflives and alpha energies for at least five alpha emitters of the same daughter charge $Z'$ (e.g., the uranium isotopes that decay to $Z'=90$). Plot $\log_{10}\tau_{1/2}$ vs. $1/\sqrt{E_\alpha}$. Verify the linear correlation.

**Challenge.**

9. The **double barrier and resonant tunneling.** Consider two identical rectangular barriers of width $L$ separated by a well of width $W$. For an incident particle of energy $E < V_0$, show that at certain *resonance energies* the transmission $T \to 1$ even though the transmission through either barrier alone is exponentially small. (Hint: the resonance condition is essentially the bound-state condition for the inter-barrier well; constructive interference between back-and-forth reflections amplifies the transmitted amplitude.) This is the principle behind the **resonant tunneling diode** ([Esaki & Tsu, *IBM J. Res. Dev.* 14, 61, 1970](https://ieeexplore.ieee.org/document/5392421) [verify]).

10. The **tunneling time problem.** How long does the wave packet "spend" inside the barrier? Define a tunneling time and compute it for the wave packet in the simulation you will build below. Compare to (a) $L/v_{\text{group}}$, (b) the Büttiker-Landauer dwell time, (c) the more recent attosecond-streaking measurements (Eckle et al., *Science* 322, 1525, 2008 [verify]; Eisenbud-Wigner phase time). This is an open problem in QM; do not expect to settle it, but name what you measured and what it means.

## 10. What would change my mind

The chapter rests on three claims. First, that WKB is a controlled $\hbar$-expansion valid in the semiclassical regime. Second, that the tunneling formula $T \approx e^{-2\gamma}$ captures the dominant exponential physics across many orders of magnitude in $T$. Third, that the back-of-envelope Gamow factor is *the* tool for evaluating any claim involving barrier penetration in atomic, nuclear, or condensed-matter physics.

If a precision measurement in a clean tunneling system — STM with carefully characterized work function and tip geometry, alpha decay of a well-understood isotope, Josephson-junction tunneling current — disagreed with the WKB prediction by more than an order of magnitude after accounting for the prefactor, the framework would be in trouble. So far no such disagreement is on the table. Cold fusion was the most dramatic claim of a violation; it remains unsupported by reproducible evidence, exactly as the Gamow factor predicts.

What the chapter does *not* settle is the right way to extract subleading prefactors and finite-$\hbar$ corrections. Exact WKB (Voros, Pham), resurgent analysis, instanton methods — these are active areas of mathematical physics. The framework here is leading-order. The leading order is enough for the physics that matters in this chapter; the corrections matter when you push for high precision.

## 11. Still puzzling

How long does the particle spend inside the barrier? The "tunneling time" question has resisted clean resolution since Hartman raised it in 1962. There are at least four well-defined definitions in the literature — dwell time, phase time, Büttiker-Landauer time, Larmor clock — and they give different numerical answers, sometimes by orders of magnitude. Recent attosecond-streaking experiments measure something; what they measure is debated.

The pop-science answer ("the particle 'borrows' energy from the vacuum for a brief time and pays it back") is wrong in detail. Energy is conserved at every measurement; the wave function in the barrier is *not* an eigenstate of energy with $E < V$, it is just the WKB exponential decay of an eigenstate with $E$. There is no clock inside the barrier in the conventional sense. The framework of this chapter does not give a tunneling time, and I do not know which of the proposed times is the physically right one. The framework is incomplete here, and saying so honestly is the Feynman move.

## 12. LLM Exercise — the tunneling simulator

You are going to build the chapter's signature simulation: three nested panels including an *animated Gaussian wave packet* that hits a barrier and splits into reflected and transmitted parts. This is the visualization that cannot be replicated in print. The deliverable is `11-tunneling-simulator.html` in your working directory.

### Part 1 — Update `PROJECT.md`

```
Append a new entry to PROJECT.md describing this chapter's simulation:

Chapter 11 — The WKB Approximation and Tunneling
Deliverable: 11-tunneling-simulator.html
Status: in progress

The simulation has three nested modes selectable by tabs:

Mode A — Stationary T(E) for rectangular barrier.
Plot T vs. E/V_0 on a LOG y-axis from 10^-12 to 1.
Two curves:
  - Exact transmission T_exact = [1 + V_0^2 sinh^2(kappa L)/(4 E (V_0 - E))]^-1
  - WKB: T_WKB = exp(-2 kappa L) for E < V_0; for E > V_0 fall back to
    classical T = 1 with interference fringes from exact.
On the log axis, the two curves run parallel below the barrier (same
exponential slope) with constant offset of order unity. Pedagogical
purpose: WKB nails the exponent, misses the prefactor.

Mode B — General WKB for arbitrary barrier shape.
Selector for barrier shape: rectangular, triangular, parabolic, double-
barrier. For each, plot V(x) on the left and T(E) on the right (log
y-axis). Compute T_WKB numerically by integrating
sqrt(2m(V(x) - E)) over the classically forbidden region for each E.
For the double barrier, watch resonant tunneling peaks emerge: T -> 1
at certain E values even though each individual barrier is opaque.

Mode C — Animated wave packet (Crank-Nicolson).
The pedagogical centerpiece. A Gaussian wave packet
psi_0(x) = (1/(2 pi sigma_x^2)^(1/4)) * exp(-(x - x_0)^2/(4 sigma_x^2))
       * exp(i p_0 (x - x_0) / hbar)
with center x_0 to the left of the barrier and momentum p_0 to the right.
Evolve the time-dependent Schrodinger equation using Crank-Nicolson:
  (1 + i H dt / 2 hbar) psi(t+dt) = (1 - i H dt / 2 hbar) psi(t)
On a spatial grid of 500 points with absorbing boundaries.
Display |psi(x, t)|^2 as a filled area chart; the barrier V(x) as a
shaded region; the energy E = E_0 = p_0^2 / 2m as a horizontal line.
Play/pause/reset controls. Time slider for scrubbing.

Controls (Mode C):
- V_0 slider (barrier height)
- L slider (barrier width)
- p_0 slider (incident momentum)
- sigma_x slider (wave-packet width)
- Time t (play/pause/scrub)

Natural units: hbar = m = 1. Spatial grid from -50 to +50 in natural
units. Barrier centered at x = 0.
```

### Part 2 — The CLAUDE.md amendment

```
Append to CLAUDE.md the following physics rules for Chapter 11 simulations:

WKB AND TUNNELING PHYSICS RULES

1. EXACT RECTANGULAR BARRIER. For E < V_0 (sub-barrier):
     T_exact = 1 / (1 + (V_0^2 / (4 E (V_0 - E))) * sinh^2(kappa L))
   with kappa = sqrt(2 m (V_0 - E)) / hbar. For E > V_0:
     T_exact = 1 / (1 + (V_0^2 / (4 E (E - V_0))) * sin^2(k_2 L))
   with k_2 = sqrt(2 m (E - V_0)) / hbar.

2. WKB FOR RECTANGULAR BARRIER. T_WKB = exp(-2 kappa L) for E < V_0;
   T_WKB = 1 for E > V_0 (no tunneling, classical transmission). The
   subleading prefactor 16 E (V_0 - E) / V_0^2 is NOT included in
   leading-order WKB; flag this on the plot as "WKB misses prefactor."

3. WKB FOR GENERAL BARRIER. T_WKB = exp(-2 gamma) where
     gamma = (1 / hbar) * integral_a^b sqrt(2 m (V(x) - E)) dx
   with a, b the classical turning points where V(x) = E. Compute the
   integral by Simpson's rule on a 1000-point sub-grid of the forbidden
   region.

4. CRANK-NICOLSON. On a uniform spatial grid x_i with spacing dx,
   discretize the Hamiltonian:
     H psi |_i = -hbar^2/(2 m dx^2) * (psi_{i+1} - 2 psi_i + psi_{i-1})
              + V(x_i) psi_i
   Build the tridiagonal matrices A = I + i H dt / (2 hbar) and
   B = I - i H dt / (2 hbar). Each time step solves A psi_new = B psi_old.
   Use Thomas algorithm for tridiagonal solve (30 lines; do NOT pull in
   numeric.js).

5. ABSORBING BOUNDARIES. Add an imaginary potential
     V_abs(x) = -i V_max * f((|x| - x_abs)/(L_box - x_abs))
   with f(s) = s^2 for s > 0 and 0 for s < 0, where x_abs is the start
   of the absorber (about 80% of the box edge) and V_max is chosen so
   that the absorber damps the wave packet over its width. Without this,
   the wave packet reflects off the box walls.

6. NORMALIZATION CHECK. After each Crank-Nicolson step, compute
   sum |psi(x_i, t)|^2 dx. In the absence of absorbing boundaries this
   should equal 1 within 1e-6. With absorbing boundaries, the norm
   decreases over time as the absorber "eats" the wave packet — this
   is expected.

7. INITIAL WAVE PACKET. Gaussian with width sigma_x (typical: 2 in
   natural units), center x_0 (typical: -20), momentum p_0 (typical:
   sqrt(2 m E) with E around V_0/2).

8. TIME STEP. Choose dt such that hbar * dt / (m dx^2) <= 1 for
   numerical stability. With dx = 0.2, dt = 0.05 is safe.

KNOWN FAILURE MODES:
(a) Crank-Nicolson tridiagonal Thomas-algorithm bugs. Write 30 lines,
    test against analytic Gaussian dispersion in free space first.
(b) Forgetting absorbing boundaries. The wave packet reflects off the
    edges and confuses the picture.
(c) Time step too large -> divergence in the imaginary part of the wave
    function.
(d) Plotting T on a linear y-axis. The whole point is the exponential
    suppression; LOG y-axis only.
(e) For Mode A, plotting only T_WKB without T_exact. The pedagogy
    requires both curves on the same plot.
(f) Barrier height not visible behind the wave packet (z-order). Render
    barrier as a translucent fill BEHIND the wave function.
```

### Part 3 — The simulation prompt

```
You are working in my directory which contains CLAUDE.md, DESIGN.md, and
PROJECT.md. Read all three first.

Build 11-tunneling-simulator.html: a single self-contained HTML file
using D3 v7 from a CDN and d3-simple-slider. No other dependencies.
Three modes selectable by tabs: "Stationary T(E)", "WKB barrier shape",
and "Wave packet (CN)".

STATIONARY T(E) MODE
Single SVG 1100 x 600. Plot T vs. E/V_0 on a LOG y-axis from 10^-12 to 1.
X-axis: E/V_0 from 0 to 2.5 (so we see both below and above barrier).
Two curves:
  - T_exact (solid black)
  - T_WKB (dashed teal)
Vertical reference line at E/V_0 = 1 (barrier height) labeled "barrier top."
For E < V_0, the two curves run parallel; the offset is the missing
prefactor. For E > V_0, only T_exact has interference fringes.

Controls: V_0 (1 to 10), L (1 to 10) in natural units.

WKB BARRIER SHAPE MODE
Single SVG 1100 x 600 split into two panels:

Left panel (550 wide): potential V(x). Selector for barrier shape:
- Rectangular: V = V_0 for |x| < L/2, 0 else
- Triangular: V = V_0 (1 - 2|x|/L) for |x| < L/2, 0 else
- Parabolic: V = V_0 (1 - (2x/L)^2) for |x| < L/2, 0 else
- Double barrier: two rectangular barriers of width L_b separated by W

Right panel (550 wide): T_WKB(E) on LOG y-axis from 10^-12 to 1.
For double barrier, watch resonant tunneling peaks emerge.

Controls: V_0, L, W (only for double barrier), shape selector.

WAVE PACKET MODE
Single SVG 1100 x 600. Single main plot:
- X-axis: position x from -50 to +50 in natural units.
- Y-axis: amplitude / probability density.
- Barrier V(x) drawn as a translucent gray fill behind the wave function.
- Horizontal dashed line at energy E = p_0^2 / 2m, with E/V_0 label.
- Wave function |psi(x, t)|^2 drawn as a filled area in blue.

Below the plot: t = current time, sum |psi|^2 dx (should be ~ 1 minus
absorber loss), and computed instantaneous "transmission" R(t) = integral
of |psi|^2 for x > L/2 + buffer.

Buttons: Play, Pause, Reset.
Controls: V_0, L, p_0, sigma_x.

GLOBAL
For Mode C, pre-compute the entire (x, t) grid of psi(x, t) when the
user clicks Play (or releases a slider). Crank-Nicolson on 500 spatial
points x 2000 time steps takes 2-5 seconds in JS. Cache the result;
playback is just iterating through stored frames at 60fps.

Implement the Thomas tridiagonal solve in pure JavaScript (about 25
lines). Implement complex arithmetic on a (re, im) pair (no library).

Runtime sanity checks to console:
- Mode A: at E/V_0 = 0.5, V_0 = 5, L = 5, T_exact should equal a
  specific value (compute it once and pin); T_WKB should be off by
  a factor of order unity.
- Mode C: before the wave packet reaches the barrier, sum |psi|^2 dx
  should equal 1 within 1e-5.
- Mode C: after the wave packet has fully passed through (or been
  absorbed), the fraction R = integral right of barrier, T = integral
  left of barrier, should satisfy R + T + absorbed = 1.

Comments at every non-trivial physics step. Pure functions for the
WKB integral and the Crank-Nicolson step.
```

### Part 4 — Exploration tasks and extension prompt

Run the simulation and answer the following:

1. Stationary mode. Set $V_0 = 5$, $L = 5$. Note that the exact and WKB curves are parallel on the log axis below the barrier. Read off the offset: $T_{\text{exact}}/T_{\text{WKB}}$ at $E/V_0 = 0.5$. Compare to the analytical prediction $16 E(V_0 - E)/V_0^2 = 16 \cdot 0.5 \cdot 0.5 / 1 = 4$. The simulation should give a factor of about 4.

2. Stationary mode. Vary $L$ from 1 to 10. The slope of $T(E)$ on the log axis steepens. This is the exponential sensitivity to barrier width. Quantify: by what factor does $T$ at $E/V_0 = 0.5$ change when $L$ doubles?

3. Barrier-shape mode. Switch to the double-barrier configuration. Watch for resonant tunneling peaks where $T \to 1$. Find one of these peaks and identify the energy. (The condition: the inter-barrier well supports a bound state at that energy.)

4. Wave packet mode. Set $V_0 = 5$, $L = 5$, $p_0 = 2$ (so $E = 2$, well below $V_0$). Play. The wave packet hits the barrier, most of it reflects, a small piece emerges on the right. The transmitted bump should be visibly attenuated relative to the reflected one. *Watch this run; this is the moment to record what you see in your own words.*

5. Wave packet mode. Increase $p_0$ to $\sqrt{2\cdot 5} \approx 3.16$ (so $E = V_0$). The wave packet hits the barrier; you should see substantial transmission and reflection — both fragments comparable in amplitude. Increase $p_0$ further (so $E > V_0$); the wave packet mostly transmits with small reflection fringes.

6. Wave packet mode. Try a very wide wave packet ($\sigma_x = 10$) and a very narrow one ($\sigma_x = 1$). The wide packet has narrow momentum spread and gives the cleanest tunneling picture; the narrow packet has broad momentum spread and shows mixed tunneling/over-barrier behavior. Explain why in your own words.

**Extension prompt:**

```
Modify 11-tunneling-simulator.html to add a Geiger-Nuttall mode:

GEIGER-NUTTALL MODE
Compute the alpha-decay halflife as a function of alpha energy for a
fixed daughter charge Z_daughter (slider, integer 80 to 92). Use the
Coulomb-barrier Gamow factor:
  gamma(E) = (1/hbar) integral_R^{r_c} sqrt(2 m_alpha (V(r) - E)) dr
with V(r) = 2 Z_daughter e^2 / (4 pi eps_0 r), R = 1.2 * A^(1/3) fm
(use A = 2 Z_daughter + a slider for neutron excess), r_c = V/E inverse.
Plot log10(tau_1/2) vs. 1/sqrt(E_alpha) for E_alpha from 4 to 9 MeV.
Should yield a straight line — the Geiger-Nuttall correlation.

Overlay experimental data for at least 5 actual isotopes (look up from
NNDC or Wikipedia tables); plot as marker points. Compare slope and
intercept to the WKB prediction.

Update PROJECT.md to mark Chapter 11 as complete and note that this
simulation closes Act Three — the methods chapters that took the
student from "I can solve textbook problems" to "I can attack real
physics."
```

---

*Sources consulted: Griffiths §9.1–9.3 (WKB approximation, connection formulas, alpha decay; 3e Chapter 9, 2e Chapter 8 [verify edition]) and Chapter 2 (rectangular-barrier exact solution); Liboff §7.7 (rectangular barrier), §7.10 (WKB approximation); Gamow, "[Zur Quantentheorie des Atomkernes](https://link.springer.com/article/10.1007/BF01343196)," *Zeitschrift für Physik* 51, 204 (1928); Gurney & Condon, "Wave Mechanics and Radioactive Disintegration," *Nature* 122, 439 (1928), and "[Quantum mechanics and radioactive disintegration](https://journals.aps.org/pr/abstract/10.1103/PhysRev.33.127)," *Phys. Rev.* 33, 127 (1929); Geiger & Nuttall, *Phil. Mag.* 22, 613 (1911); 23, 439 (1912) [verify]; Binnig & Rohrer, "[7×7 Reconstruction on Si(111) Resolved in Real Space](https://journals.aps.org/prl/abstract/10.1103/PhysRevLett.49.57)," *Phys. Rev. Lett.* 49, 57 (1982); Atkinson & Houtermans, *Z. Phys.* 54, 656 (1929) [verify]; Löwdin, "[Proton Tunneling in DNA](https://journals.aps.org/rmp/abstract/10.1103/RevModPhys.35.724)," *Rev. Mod. Phys.* 35, 724 (1963); Slocombe et al., "[An open quantum systems approach to proton tunnelling in DNA](https://www.nature.com/articles/s42005-022-00881-8)," *Commun. Phys.* 5, 109 (2022) [verify]; Fowler & Nordheim, *Proc. R. Soc. A* 119, 173 (1928) [verify]; Bender & Orszag, *Advanced Mathematical Methods for Scientists and Engineers* (1978), Chapter 10 [verify].*

*Tags: wkb-approximation, tunneling, gamow-factor, alpha-decay, geiger-nuttall, scanning-tunneling-microscopy, crank-nicolson, quantum-biology, d3-simulation*

*Status: draft for Nik's review. The Crank-Nicolson wave-packet animation is the chapter's signature visualization — pedagogical move that cannot be done in print. Several `[verify]` flags throughout — see specifically Geiger-Nuttall original citation, Atkinson-Houtermans 1929, Slocombe 2022, Bender-Orszag edition and chapter, Fowler-Nordheim 1928, Griffiths edition mapping.*

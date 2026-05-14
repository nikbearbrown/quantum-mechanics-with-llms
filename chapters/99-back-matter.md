---

## Acknowledgments

The students at Northeastern who ran early versions of the chapter simulations and told me, often pointedly, which ones were confusing — you are the reason every chapter now has explicit verification moves. Particular thanks to the INFO 7390 / GIGO cohort who broke the Crank-Nicolson tunneling animation in seven different ways and made me write the absorbing-boundary discussion. The teaching assistants who fact-checked the Griffiths chapter references against the third-edition problem numbers caught more drift than I want to admit.

The Brutalist system that governs the simulation code in every chapter is the joint development of conversations with collaborators across the *with LLMs* series, the AImagineering course, and the Humanitarians AI fellows. The discipline of CLAUDE.md / DESIGN.md / PROJECT.md as the three load-bearing files emerged from those conversations.

The pedagogical-research literature that backs the book's premise — PhET / Wieman / Adams / McKagan on interactive simulations in physics — does the empirical work this book builds on. The book extends their finding (interactive sims build intuition the math alone does not supply) one step further: that with AI-generated simulations, the student becomes the simulation author, not the simulation user. That step is the +1 layer.

David Griffiths wrote the undergraduate quantum mechanics textbook this book is designed to pair with. I have used his text in my teaching since I started teaching quantum mechanics. Pair this book with his and you have the second-semester course.

---

## About the Author

**Nik Bear Brown** is an Associate Teaching Professor at Northeastern University's College of Engineering, where he teaches data science, AI, computational physics, visualization, virtual environments, and graduate courses on AI-augmented learning. He is the architect of the **Brutalist** system for AI-assisted creative production — a renderer-agnostic framework whose modules include the D3 simulation work that this book is built on, as well as *Brutalist After Effects × Claude*, *Brutalist Blender × Claude*, and *Brutalist Remotion × Claude*. The framework lives at [brutalist.art](https://www.brutalist.art/).

His Ph.D. is in computer science from UCLA, with major field in computational and systems biology and minor fields in artificial intelligence and statistics. He holds a master's in Information Design and Data Visualization and an MBA from Northeastern. Before academia he was a molecular biologist at DNAX Research Institute and Cetus Corporation; he did a part-time postdoc in deep learning at Harvard Medical School while teaching at Northeastern.

His connection to physics began with biochemistry at UC Santa Cruz and continued through computational and systems biology at UCLA. He has been teaching variants of computational physics, AI-for-engineering, and visualization at Northeastern for over a decade, and watched dozens of physics majors hit the intuition wall this book is designed to close.

He is the author of the *with LLMs* textbook series, the founder of [Humanitarians AI](https://www.humanitarians.ai/) (a 501(c)(3) supporting OPT and H-1B fellows in production-scale AI work), and the architect of **[Irreducibly Human](https://irreducibly.xyz)** — a curriculum series and book project about the cognitive capacities the AI era most urgently requires humans to develop. He writes at [nikbearbrown.com](https://www.nikbearbrown.com) and [skepticism.ai](https://www.skepticism.ai); reach him at [bear@bearbrown.co](mailto:bear@bearbrown.co).

Pronouns: they/them. Fun fact: once ran away with the circus, did sumo wrestling, and worked as a photojournalist.

---

## Notes

### Chapter 0 — How to Use the Simulations
1. PhET Interactive Simulations: [phet.colorado.edu](https://phet.colorado.edu). Wieman, Adams, Perkins 2008, *Science* 322, 682–683.
2. Hake 1998 "Interactive-engagement versus traditional methods: A six-thousand-student survey of mechanics test data," *Am. J. Phys.* 66, 64–74.
3. D3.js v7 documentation: [d3js.org](https://d3js.org). Bostock et al. 2011 IEEE TVCG on the original D3 design.
4. Brutalist system: [brutalist.art](https://www.brutalist.art/).

### Chapter 1 — The Wave Function
1. Born 1926, "Zur Quantenmechanik der Stoßvorgänge," *Z. Phys.* 37, 863–867. Probabilistic interpretation of $|\psi|^2$.
2. Heisenberg 1927, "Über den anschaulichen Inhalt der quantentheoretischen Kinematik und Mechanik," *Z. Phys.* 43, 172.
3. McKagan et al. 2010 *PRST-PER* on undergraduate wave-function misconceptions.

### Chapter 2 — The Time-Independent Schrödinger Equation
1. Schrödinger 1926 four-paper series, *Annalen der Physik* 79–81. Original derivation of the equation.
2. Bohr 1913, "On the Constitution of Atoms and Molecules," *Philosophical Magazine* 26, 1–25. The quantization that Schrödinger derived from continuity.
3. Esaki & Tsu 1970 *IBM J. Res. Dev.* on semiconductor superlattices as engineered square wells.

### Chapter 3 — The Harmonic Oscillator
1. Glauber 1963, "Coherent and Incoherent States of the Radiation Field," *Phys. Rev.* 131, 2766. Coherent states.
2. Dirac 1930, *The Principles of Quantum Mechanics*. Original algebraic method.
3. Lamoreaux 1997 *PRL* 78, 5 on Casimir effect — the harmonic-oscillator zero-point energy observable.

### Chapter 4 — Formalism: Dirac Notation and Operators
1. Robertson 1929 *Physical Review* 34, 163. The general uncertainty inequality from Cauchy-Schwarz.
2. Heisenberg 1927 *Z. Phys.* 43, 172. The original (epistemic) microscope argument.
3. Marshman & Singh 2017 *EJP* 38, 025705 on Dirac-notation pedagogy.
4. Ozawa 2003 *Phys. Rev. A* 67, 042105 on the modern preparation vs. measurement-disturbance separation.

### Chapter 5 — Quantum Mechanics in Three Dimensions
1. NIST Digital Library of Mathematical Functions Ch. 14: [dlmf.nist.gov/14](https://dlmf.nist.gov/14). Spherical harmonics.
2. Arfken, Weber & Harris, *Mathematical Methods for Physicists*. Standard reference for the radial-equation machinery.
3. Karaçöp & Doymuş 2013 on prospective-teacher misconceptions about atomic orbitals.

### Chapter 6 — Spin
1. Stern & Gerlach 1922, *Z. Phys.* 9, 349. Quantization of spin angular momentum.
2. Uhlenbeck & Goudsmit 1925, "Ersetzung der Hypothese vom unmechanischen Zwang durch eine Forderung bezüglich des inneren Verhaltens jedes einzelnen Elektrons," *Naturwiss.* 13, 953. The spin proposal.
3. Pauli 1927, *Z. Phys.* 43, 601. Pauli matrices.
4. Dirac 1928, "The Quantum Theory of the Electron," *Proc. Roy. Soc. A* 117, 610. Spin from relativistic QM.
5. Friedrich & Herschbach 2003 *Physics Today* on the Stern-Gerlach experiment.
6. Fan, Myers, Sukra & Gabrielse 2023, *PRL* 130, 071801. The current best electron $g-2$ measurement.

### Chapter 7 — The Hydrogen Atom
1. Bohr 1913, *Phil. Mag.* 26, 1–25. The Bohr model.
2. Pauli 1926, *Z. Phys.* 36, 336. The SO(4) algebraic solution of hydrogen.
3. Lamb & Retherford 1947, "Fine Structure of the Hydrogen Atom by a Microwave Method," *Phys. Rev.* 72, 241. The Lamb shift.
4. Pohl et al. 2010, *Nature* 466, 213. The proton radius puzzle.
5. Bezginov et al. 2019, *Science* 365, 1007. Modern 2S-2P measurement.
6. Ahmadi et al. 2018, *Nature* 557, 71. Antihydrogen 1S-2S spectroscopy.

### Chapter 8 — Identical Particles
1. Pauli 1940, "The Connection Between Spin and Statistics," *Physical Review* 58, 716. Spin-statistics theorem.
2. Slater 1929, *Phys. Rev.* 34, 1293. The Slater determinant.
3. Anderson et al. 1995, *Science* 269, 198. Rb-87 Bose-Einstein condensation.
4. Davis et al. 1995, *PRL* 75, 3969. Na Bose-Einstein condensation.
5. Chandrasekhar 1931, *Astrophysical Journal* 74, 81. White dwarf mass limit.
6. Bartolomei et al. 2020, *Science* 368, 173. Anyon experimental observation.

### Chapter 9 — Time-Independent Perturbation Theory
1. Dyson 1952, *Phys. Rev.* 85, 631–632. The asymptotic nature of QED perturbation series.
2. Bender & Wu 1969 on divergence of anharmonic-oscillator perturbation theory.
3. Stark 1913 *Annalen der Physik*; Lo Surdo 1913 — simultaneous discovery dispute documented in Leone, Paoletti & Robotti 2004 *Physics in Perspective*.
4. Lamb & Retherford 1947 (above) for hydrogen fine structure as the perturbation-theory worked example.

### Chapter 10 — Time-Dependent Perturbation Theory and Transitions
1. **Dirac 1927**, "The Quantum Theory of the Emission and Absorption of Radiation," *Proc. Roy. Soc. A* 114, 243. The actual origin of what is now called "Fermi's golden rule" — Dirac derived it twenty years before Fermi named it.
2. Fermi 1950, *Nuclear Physics: A Course Given by Enrico Fermi at the University of Chicago*. The coinage of "golden rule."
3. Einstein 1917, "Zur Quantentheorie der Strahlung," *Physikalische Zeitschrift* 18, 121–128. A and B coefficients.
4. Rabi, Zacharias, Millman & Kusch 1938 / 1939, *Phys. Rev.* 53/55. Molecular-beam magnetic-resonance experiments — Rabi Nobel 1944.
5. Maiman 1960, "Stimulated Optical Radiation in Ruby," *Nature* 187, 493–494. The first laser.

### Chapter 11 — The WKB Approximation and Tunneling
1. Gamow 1928, "Zur Quantentheorie des Atomkernes," *Z. Phys.* 51, 204. Alpha decay.
2. Gurney & Condon 1928 *Nature* 122, 439 + 1929 *Phys. Rev.* 33, 127. Independent alpha-decay treatment.
3. Wentzel 1926 *Z. Phys.* 38; Kramers 1926 *Z. Phys.* 39; Brillouin 1926 — independent WKB derivations.
4. Binnig & Rohrer 1982, "Surface Studies by Scanning Tunneling Microscopy," *PRL* 49, 57. The STM; Nobel 1986.
5. Löwdin 1963, "Proton Tunneling in DNA," *Reviews of Modern Physics* 35, 724.
6. Slocombe et al. 2022 *Comm. Phys.* 5, 109 — recent quantum-biology tunneling claims.
7. Bender & Orszag 1978, *Advanced Mathematical Methods for Scientists and Engineers*. The Maslov-index treatment.

### Chapter 12 — Entanglement and Quantum Information
1. EPR 1935, "Can Quantum-Mechanical Description of Physical Reality Be Considered Complete?" *Physical Review* 47, 777.
2. Bell 1964, "On the Einstein Podolsky Rosen Paradox," *Physics Physique Fizika* 1, 195.
3. Clauser, Horne, Shimony & Holt 1969, *PRL* 23, 880. The CHSH inequality.
4. Aspect, Dalibard & Roger 1982, *PRL* 49, 1804. Time-varying analyzers.
5. Hensen et al. 2015, *Nature* 526, 682. Loophole-free Bell test (Delft).
6. Giustina et al. 2015, *PRL* 115, 250401. Loophole-free Bell test (Vienna).
7. Shalm et al. 2015, *PRL* 115, 250402. Loophole-free Bell test (NIST).
8. Bennett, Brassard, Crépeau, Jozsa, Peres & Wootters 1993, *PRL* 70, 1895. Quantum teleportation.
9. Wootters & Zurek 1982, *Nature* 299, 802; Dieks 1982 *Phys. Lett. A* 92, 271. The no-cloning theorem.
10. Tsirelson 1980, *Lett. Math. Phys.* 4, 93. The Tsirelson bound.
11. Nielsen & Chuang 2010, *Quantum Computation and Quantum Information* (10th anniversary edition). Canonical textbook.
12. Nobel 2022 — Aspect, Clauser, Zeilinger. Citation at [nobelprize.org/prizes/physics/2022](https://www.nobelprize.org/prizes/physics/2022/).

### Chapter 13 — Capstone
1. Lindblad 1976, "On the Generators of Quantum Dynamical Semigroups," *Comm. Math. Phys.* 48, 119.
2. Zurek 2003, "Decoherence, einselection, and the quantum origins of the classical," *Reviews of Modern Physics* 75, 715.
3. Schlosshauer 2007, *Decoherence and the Quantum-to-Classical Transition*. Springer.
4. Preskill 2018, "Quantum Computing in the NISQ era and beyond," *Quantum* 2, 79.
5. Acharya et al. (Google Quantum AI) 2023, "Suppressing quantum errors by scaling a surface code logical qubit," *Nature* 614, 676.
6. Acharya et al. (Google Quantum AI) 2024 — below-threshold demonstration.
7. Doherty et al. 2013 *Physics Reports* on NV-center physics.
8. von Klitzing 1980 *PRL* 45, 494. The integer quantum Hall effect. Nobel 1985.
9. Kane & Mele 2005 *PRL* 95, 146802. Z₂ topological insulators.
10. Hasan & Kane 2010 *RMP* 82, 3045. Colloquium on topological insulators.
11. Shor 1994 *Proc. 35th FOCS*. Factoring algorithm.
12. NIST 2024 Post-Quantum Cryptography Standardization: FIPS 203 (ML-KEM), FIPS 204 (ML-DSA), FIPS 205 (SLH-DSA).

---

## References

Acharya, R., et al. "Suppressing Quantum Errors by Scaling a Surface Code Logical Qubit." *Nature* 614 (2023): 676–681.

Anderson, M. H., J. R. Ensher, M. R. Matthews, C. E. Wieman, and E. A. Cornell. "Observation of Bose-Einstein Condensation in a Dilute Atomic Vapor." *Science* 269 (1995): 198–201.

Aspect, Alain, Jean Dalibard, and Gérard Roger. "Experimental Test of Bell's Inequalities Using Time-Varying Analyzers." *Physical Review Letters* 49 (1982): 1804–1807.

Bell, John S. "On the Einstein Podolsky Rosen Paradox." *Physics Physique Fizika* 1 (1964): 195–200.

Bender, Carl M., and Steven A. Orszag. *Advanced Mathematical Methods for Scientists and Engineers I: Asymptotic Methods and Perturbation Theory*. Springer, 1978.

Bennett, Charles H., et al. "Teleporting an Unknown Quantum State via Dual Classical and Einstein-Podolsky-Rosen Channels." *Physical Review Letters* 70 (1993): 1895–1899.

Binnig, Gerd, and Heinrich Rohrer. "Surface Studies by Scanning Tunneling Microscopy." *Physical Review Letters* 49 (1982): 57–61.

Bohr, Niels. "On the Constitution of Atoms and Molecules." *Philosophical Magazine* 26 (1913): 1–25.

Born, Max. "Zur Quantenmechanik der Stoßvorgänge." *Zeitschrift für Physik* 37 (1926): 863–867.

Chandrasekhar, Subrahmanyan. "The Maximum Mass of Ideal White Dwarfs." *Astrophysical Journal* 74 (1931): 81–82.

Clauser, John F., Michael A. Horne, Abner Shimony, and Richard A. Holt. "Proposed Experiment to Test Local Hidden-Variable Theories." *Physical Review Letters* 23 (1969): 880–884.

Davis, K. B., et al. "Bose-Einstein Condensation in a Gas of Sodium Atoms." *Physical Review Letters* 75 (1995): 3969–3973.

Dirac, P. A. M. "The Quantum Theory of the Emission and Absorption of Radiation." *Proceedings of the Royal Society A* 114 (1927): 243–265.

Dirac, P. A. M. "The Quantum Theory of the Electron." *Proceedings of the Royal Society A* 117 (1928): 610–624.

Dirac, P. A. M. *The Principles of Quantum Mechanics*. 4th ed. Oxford University Press, 1958.

Dyson, Freeman J. "Divergence of Perturbation Theory in Quantum Electrodynamics." *Physical Review* 85 (1952): 631–632.

Einstein, Albert. "Zur Quantentheorie der Strahlung." *Physikalische Zeitschrift* 18 (1917): 121–128.

Einstein, Albert, Boris Podolsky, and Nathan Rosen. "Can Quantum-Mechanical Description of Physical Reality Be Considered Complete?" *Physical Review* 47 (1935): 777–780.

Fan, X., T. G. Myers, B. A. D. Sukra, and G. Gabrielse. "Measurement of the Electron Magnetic Moment." *Physical Review Letters* 130 (2023): 071801.

Friedrich, Bretislav, and Dudley Herschbach. "Stern and Gerlach: How a Bad Cigar Helped Reorient Atomic Physics." *Physics Today* 56, no. 12 (2003): 53–59.

Gamow, George. "Zur Quantentheorie des Atomkernes." *Zeitschrift für Physik* 51 (1928): 204–212.

Giustina, Marissa, et al. "Significant-Loophole-Free Test of Bell's Theorem with Entangled Photons." *Physical Review Letters* 115 (2015): 250401.

Glauber, Roy J. "Coherent and Incoherent States of the Radiation Field." *Physical Review* 131 (1963): 2766–2788.

Griffiths, David J. *Introduction to Quantum Mechanics*. 3rd ed. Cambridge University Press, 2018.

Hake, Richard R. "Interactive-Engagement versus Traditional Methods." *American Journal of Physics* 66 (1998): 64–74.

Hasan, M. Z., and C. L. Kane. "Colloquium: Topological Insulators." *Reviews of Modern Physics* 82 (2010): 3045.

Heisenberg, Werner. "Über den anschaulichen Inhalt der quantentheoretischen Kinematik und Mechanik." *Zeitschrift für Physik* 43 (1927): 172–198.

Hensen, B., et al. "Loophole-Free Bell Inequality Violation Using Electron Spins Separated by 1.3 Kilometres." *Nature* 526 (2015): 682–686.

Kane, C. L., and E. J. Mele. "Z2 Topological Order and the Quantum Spin Hall Effect." *Physical Review Letters* 95 (2005): 146802.

Klitzing, Klaus von, Gerhard Dorda, and Michael Pepper. "New Method for High-Accuracy Determination of the Fine-Structure Constant Based on Quantized Hall Resistance." *Physical Review Letters* 45 (1980): 494–497.

Lamb, Willis E., and Robert C. Retherford. "Fine Structure of the Hydrogen Atom by a Microwave Method." *Physical Review* 72 (1947): 241–243.

Liboff, Richard L. *Introductory Quantum Mechanics*. 4th ed. Addison-Wesley, 2003.

Lindblad, Göran. "On the Generators of Quantum Dynamical Semigroups." *Communications in Mathematical Physics* 48 (1976): 119–130.

Löwdin, Per-Olov. "Proton Tunneling in DNA." *Reviews of Modern Physics* 35 (1963): 724–732.

Maiman, T. H. "Stimulated Optical Radiation in Ruby." *Nature* 187 (1960): 493–494.

McKagan, S. B., K. K. Perkins, and C. E. Wieman. "Why We Should Teach the Bohr Model and How to Teach It Effectively." *Physical Review Special Topics — Physics Education Research* 4 (2008): 010103.

Nielsen, Michael A., and Isaac L. Chuang. *Quantum Computation and Quantum Information*. 10th anniversary ed. Cambridge University Press, 2010.

Pauli, Wolfgang. "Über den Zusammenhang des Abschlusses der Elektronengruppen im Atom mit der Komplexstruktur der Spektren." *Zeitschrift für Physik* 31 (1925): 765–783.

Pauli, Wolfgang. "The Connection Between Spin and Statistics." *Physical Review* 58 (1940): 716–722.

Pohl, Randolf, et al. "The Size of the Proton." *Nature* 466 (2010): 213–216.

Preskill, John. "Quantum Computing in the NISQ Era and Beyond." *Quantum* 2 (2018): 79.

Robertson, H. P. "The Uncertainty Principle." *Physical Review* 34 (1929): 163–164.

Schrödinger, Erwin. "Quantisierung als Eigenwertproblem (Erste Mitteilung)." *Annalen der Physik* 79 (1926): 361–376.

Shalm, Lynden K., et al. "Strong Loophole-Free Test of Local Realism." *Physical Review Letters* 115 (2015): 250402.

Shor, Peter W. "Algorithms for Quantum Computation: Discrete Logarithms and Factoring." *Proceedings of the 35th Annual Symposium on Foundations of Computer Science* (1994): 124–134.

Slater, John C. "The Theory of Complex Spectra." *Physical Review* 34 (1929): 1293–1322.

Stern, Otto, and Walther Gerlach. "Der experimentelle Nachweis der Richtungsquantelung im Magnetfeld." *Zeitschrift für Physik* 9 (1922): 349–352.

Tsirelson, Boris S. "Quantum Generalizations of Bell's Inequality." *Letters in Mathematical Physics* 4 (1980): 93–100.

Uhlenbeck, George E., and Samuel Goudsmit. "Ersetzung der Hypothese vom unmechanischen Zwang durch eine Forderung bezüglich des inneren Verhaltens jedes einzelnen Elektrons." *Die Naturwissenschaften* 13 (1925): 953–954.

Wieman, Carl E., Wendy K. Adams, and Katherine K. Perkins. "PhET: Simulations That Enhance Learning." *Science* 322 (2008): 682–683.

Wootters, William K., and Wojciech H. Zurek. "A Single Quantum Cannot Be Cloned." *Nature* 299 (1982): 802–803.

Zurek, Wojciech H. "Decoherence, Einselection, and the Quantum Origins of the Classical." *Reviews of Modern Physics* 75 (2003): 715–775.

---

## On the Absence of an Index

This is a Kindle and online book. It does not include a printed index. Three reasons.

First, e-reader search makes printed indexes obsolete for this format — every term in the book is one keystroke away, with results that scale to your reading window rather than to a static page count. Second, this book is integrated with **Medhavy** ([medhavy.com](https://www.medhavy.com/)) — मेधावी, from the Sanskrit for *intelligent* or *intellectually brilliant* — an AI-powered intelligent textbook platform that indexes the book semantically rather than alphabetically. Search Medhavy for a concept and it will surface the chapter that teaches the concept, not the page where the term first appears. Third, every chapter ends with an LLM Exercise block whose simulation prompt is the chapter's interactive index entry — paste it into Claude and the chapter becomes a working tool.

If you need to find something, search the e-reader. If you need to *use* something, run the chapter's simulation.

Come learn something with us.

---

## Glossary

**Born rule.** $P(x, t) = |\psi(x, t)|^2$. The probability density for finding the particle at position $x$ at time $t$. Postulated; not derived from the Schrödinger equation. Cited as Born 1926.

**Bra-ket notation.** Dirac's notation for states in Hilbert space. $|\psi\rangle$ is the state (ket); $\langle\phi|$ is the dual vector (bra); $\langle\phi|\psi\rangle$ is the inner product. Introduced rigorously in Chapter 4.

**Brutalist system.** A three-file framework (CLAUDE.md, DESIGN.md, PROJECT.md) for governing AI-generated simulation code. Holds the boundary between physics judgment (human) and code generation (model). Set up in Chapter 0; carries through all 14 chapters.

**Coherent state.** A specific superposition of harmonic-oscillator eigenstates that maintains a Gaussian shape and oscillates classically. The eigenstate of the lowering operator. Glauber 1963. Chapter 3.

**CHSH inequality.** Clauser-Horne-Shimony-Holt 1969. The form of Bell's inequality used in modern tests. Local hidden-variable theories satisfy $|S| \leq 2$; quantum mechanics allows $|S| \leq 2\sqrt{2}$ (the Tsirelson bound). Chapter 12.

**Decoherence.** The process by which quantum coherences are suppressed via entanglement with environmental degrees of freedom. Explains the quantum-to-classical transition without resolving the measurement problem. Zurek 2003. Chapter 13.

**Dirac notation.** See Bra-ket notation.

**Eigenvalue / eigenstate.** $\hat{O}|\psi\rangle = \lambda|\psi\rangle$. The state $|\psi\rangle$ is an eigenstate of operator $\hat{O}$ with eigenvalue $\lambda$. Measurements yield eigenvalues; the system is projected into the corresponding eigenstate.

**Entanglement.** A state of two or more subsystems that cannot be written as a product of individual states. Generates non-classical correlations that violate Bell inequalities. Chapter 12.

**Fermi's golden rule.** Transition rate from a discrete initial state to a continuum: $W_{i \to f} = (2\pi/\hbar) |\langle f|\hat{H}'|i\rangle|^2 \rho(E_f)$. Misnamed — derived by Dirac in 1927; named by Fermi in 1950. Chapter 10.

**Hamiltonian.** $\hat{H}$. The operator whose eigenvalues are the system's allowed energies and whose action generates time evolution via $i\hbar \partial_t |\psi\rangle = \hat{H}|\psi\rangle$.

**Hermitian operator.** $\hat{O}^\dagger = \hat{O}$. Real eigenvalues; orthogonal eigenstates for distinct eigenvalues. Observables correspond to Hermitian operators. NOT the same as "symmetric matrix" for complex matrices.

**LLM Exercise.** The book's signature feature. Section 9 of every chapter. A four-part block (CLAUDE.md prompt, simulation prompt, exploration tasks, extension prompt) that produces a working D3 simulation.

**Pauli matrices.** $\sigma_x, \sigma_y, \sigma_z$. The 2×2 Hermitian, trace-zero, unitary matrices that represent spin-1/2 operators. Generators of SU(2). Chapter 6.

**Probability current.** $J(x, t) = (i\hbar / 2m)(\psi \partial_x \psi^* - \psi^* \partial_x \psi)$. Satisfies the continuity equation $\partial_t|\psi|^2 + \partial_x J = 0$. Chapter 1.

**Robertson uncertainty.** $\sigma_A \sigma_B \geq (1/2) |\langle [\hat{A}, \hat{B}]\rangle|$. Robertson 1929. The general uncertainty principle derived from Cauchy-Schwarz on shifted operators. Intrinsic to the state, NOT a measurement-disturbance phenomenon. Chapter 4.

**Schrödinger equation.** $i\hbar \partial_t |\psi\rangle = \hat{H}|\psi\rangle$ (time-dependent); $\hat{H}|\psi\rangle = E|\psi\rangle$ (time-independent). Postulated, not derived. Chapter 2 + 3.

**Slater determinant.** $\psi = (1/\sqrt{N!}) \det[\phi_i(x_j)]$. Automatically antisymmetric under exchange of any two particles. Vanishes if any two single-particle states coincide — Pauli exclusion built in. Chapter 8.

**Spherical harmonics.** $Y_{\ell m}(\theta, \phi)$. Eigenfunctions of $\hat{L}^2$ and $\hat{L}_z$. Form a complete orthonormal basis on the sphere. Chapter 5.

**Stationary state.** An energy eigenstate. The probability density $|\psi|^2$ is time-independent; the wave function evolves only by a global phase $e^{-iEt/\hbar}$.

**Tsirelson bound.** $|S| \leq 2\sqrt{2}$. The maximum CHSH value allowed by quantum mechanics. Tsirelson 1980. Chapter 12.

**WKB approximation.** Semi-classical approximation in $\hbar$. Wave function $\psi \approx (1/\sqrt{p(x)}) e^{(i/\hbar) \int p \, dx}$. Foundation of the tunneling formula and Bohr-Sommerfeld quantization. Wentzel, Kramers, Brillouin 1926. Chapter 11.

**Wave function.** $\psi(x, t)$. A complex-valued probability amplitude. Not the particle. Not the energy distribution. Not directly observable. The thing whose squared modulus is the probability density.

---

## Errata

Reported errors and corrections are maintained at [nikbearbrown.com/qm-plus-1-errata](https://www.nikbearbrown.com) (link active after publication).

To report an error: [bear@bearbrown.co](mailto:bear@bearbrown.co).

⚡ Fun fact: I once ran away with the circus, was a photojournalist, and did sumo wrestling.

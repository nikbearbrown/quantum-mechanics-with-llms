# Chapter 5 — Quantum Mechanics in Three Dimensions

> Extend the Schrödinger equation to 3D, learn the universal machinery that solves *any* central-potential problem, and build a visualizer for the angular wave functions that govern every atom, planet, and cosmic-microwave-background mode.

---

## 1. What this chapter is doing

You have done quantum mechanics in one dimension. The infinite square well had two walls. The harmonic oscillator had a parabolic confining potential. Bound states, expectation values, ladder operators — every example came on a single number line.

Real physical systems live in three dimensions. The hydrogen atom is not a 1D problem. A neutron in a nucleus is not a 1D problem. A photon mode in a cavity is not a 1D problem. The chapter pivots us into 3D — and immediately discovers a piece of luck. The most physically important 3D problems have a special symmetry: the potential depends only on the radial distance $r$, not on direction. These are the **central potentials**. And for any central potential, the angular part of the Schrödinger equation has a *universal* solution — the spherical harmonics — that you solve once and then never have to solve again. The radial part remains as a 1D problem in $r$, which is exactly the kind of bound-state calculation you have been doing since Chapter 2.

So the program for this chapter is: set up 3D, separate variables in spherical coordinates, solve the angular equation once and for all, and reduce every central-potential problem to a 1D radial equation. The hydrogen atom (Chapter 7) will then be one specific choice of $V(r)$ plugged into the machinery you build here.

There is one more move worth flagging. The angular momentum operators $\hat{L}^2$ and $\hat{L}_z$ commute — they are **compatible observables** in the Chapter 4 sense — and their joint eigenstates are the spherical harmonics. The angular momentum machinery you would otherwise meet in isolation falls out of the separation of the 3D Schrödinger equation. The chapter gives you both at once.

## 2. Learning objectives

By the end of this chapter you should be able to:

- Write the 3D time-independent Schrödinger equation in spherical coordinates and identify the angular-momentum operator $\hat{L}^2$ inside it.
- Separate variables for a central potential $V(\vec r) = V(r)$ and obtain the angular equation $\hat{L}^2 Y = \hbar^2 \ell(\ell+1) Y$.
- Recognize the spherical harmonics $Y_{\ell m}(\theta, \phi)$ as the joint eigenstates of $\hat{L}^2$ and $\hat{L}_z$, with eigenvalues $\hbar^2\ell(\ell+1)$ and $\hbar m$.
- Verify the angular-momentum commutators $[\hat{L}_i, \hat{L}_j] = i\hbar\epsilon_{ijk}\hat{L}_k$ and $[\hat{L}^2, \hat{L}_i] = 0$.
- Apply the substitution $u(r) = rR(r)$ to reduce the radial equation to a 1D Schrödinger equation with effective potential $V_{\text{eff}}(r) = V(r) + \hbar^2\ell(\ell+1)/(2mr^2)$.
- Solve the 3D infinite spherical well using spherical Bessel functions and identify the level ordering 1s, 1p, 1d, 2s, 1f, ...
- Distinguish $|Y_{\ell m}|^2$ (the angular probability density) from "orbital shapes" in chemistry, and explain why $L^2 = \hbar^2\ell(\ell+1)$ rather than $\hbar^2\ell^2$.
- Build a D3 simulation that visualizes the spherical harmonics with both physics (complex) and chemistry (real) conventions, and operationalize $\hat{L}_z$ via the $\phi$-phase animation.

## 3. Motivating problem

Open a chemistry textbook to the page on atomic orbitals. You will see s-orbitals drawn as spheres, p-orbitals as dumbbells, d-orbitals as four-leaf clovers with one peculiar exception ($d_{z^2}$, the donut), f-orbitals as ornate flowery shapes. The pictures are everywhere. The story is: these are the orbitals the electrons "occupy."

Here is a question to ask before you accept the pictures. *What exactly is the picture showing?* Is it the wave function $\psi$? The probability density $|\psi|^2$? The angular part only, or the radial part included? Is the shape the *state* of the electron, or the *distribution* of where you would find the electron if you measured?

The answers, as you will see in this chapter, are precise and specific, and they undo a misconception that the chemistry-class pictures encourage. The shapes are $|Y_{\ell m}|^2$ (angular probability density), not the full wave function (which also has a radial factor). The "p-orbitals" in chemistry are not actually the $Y_1^{\pm 1}$ states of physics — they are *real* linear combinations of $Y_1^{\pm 1}$ and $Y_1^0$, chosen because they make pretty pictures aligned with Cartesian axes. The complex spherical harmonics that physics uses (eigenstates of $\hat{L}_z$, with definite $z$-component of angular momentum) and the real combinations chemistry uses (eigenstates of *no* component of angular momentum, but with definite spatial axes) are *different states* of the same energy.

A second motivating thread. The same mathematics — Legendre polynomials, spherical harmonics — that organizes atomic orbitals organizes the cosmic microwave background. Planck and WMAP report the CMB's temperature anisotropies as a power spectrum $C_\ell$ in spherical-harmonic coefficients (see the Planck 2018 cosmological parameters paper, *A&A* 641, A6 [verify exact DOI]). The same $\ell$ that distinguishes s, p, d, f orbitals labels the multipoles of the cosmos. Spherical harmonics are the universal language for functions on spheres — atomic, terrestrial, planetary, cosmic. Learning them properly here pays off in places no first QM course would suggest.

The 3D Schrödinger equation:

$$-\frac{\hbar^2}{2m}\nabla^2\psi(\vec r) + V(\vec r)\psi(\vec r) = E\psi(\vec r)$$

with $\nabla^2 = \partial_x^2 + \partial_y^2 + \partial_z^2$ in Cartesian coordinates. We will rewrite it in spherical coordinates, do separation of variables, and discover the structure that organizes nearly every bound-state problem you will meet for the rest of your career.

## 4. Concept block — spherical coordinates and the angular equation

### 4.1 The Laplacian in spherical coordinates

Spherical coordinates $(r, \theta, \phi)$ with $\theta \in [0, \pi]$ the polar angle from the $+z$-axis and $\phi \in [0, 2\pi)$ the azimuth in the $xy$-plane. The Laplacian becomes:

$$\nabla^2 = \frac{1}{r^2}\frac{\partial}{\partial r}\!\left(r^2\frac{\partial}{\partial r}\right) + \frac{1}{r^2\sin\theta}\frac{\partial}{\partial\theta}\!\left(\sin\theta\frac{\partial}{\partial\theta}\right) + \frac{1}{r^2\sin^2\theta}\frac{\partial^2}{\partial\phi^2}$$

(Griffiths §4.1.) Stare at this for a moment. There is a clean radial term — the first piece — and then an angular block — the second and third pieces — that is divided everywhere by $r^2$. Pull the $r^2$ out and the angular part is independent of $r$. Define:

$$\hat{L}^2 = -\hbar^2\left[\frac{1}{\sin\theta}\frac{\partial}{\partial\theta}\!\left(\sin\theta\frac{\partial}{\partial\theta}\right) + \frac{1}{\sin^2\theta}\frac{\partial^2}{\partial\phi^2}\right]$$

This is the square of the orbital angular momentum operator. The kinetic energy splits cleanly:

$$-\frac{\hbar^2}{2m}\nabla^2 = -\frac{\hbar^2}{2m}\cdot\frac{1}{r^2}\frac{\partial}{\partial r}\!\left(r^2\frac{\partial}{\partial r}\right) + \frac{\hat{L}^2}{2mr^2}$$

Kinetic energy = (radial kinetic energy) + (angular kinetic energy / $r^2$). The angular kinetic energy is $\hat{L}^2/(2mr^2)$ — *exactly* what you would write for a classical rotor: kinetic energy of rotation is $L^2/(2I)$ with moment of inertia $I = mr^2$. Same expression, now as operators.

### 4.2 Separation of variables for central potentials

If $V(\vec r) = V(r)$ depends only on $r$, try the product ansatz $\psi(r, \theta, \phi) = R(r)Y(\theta, \phi)$. Substitute into the Schrödinger equation, divide by $RY$, multiply by $r^2$. After some bookkeeping the equation splits:

$$\frac{1}{R}\frac{d}{dr}\!\left(r^2\frac{dR}{dr}\right) + \frac{2mr^2}{\hbar^2}[E - V(r)] = -\frac{1}{Y\hbar^2}\hat{L}^2 Y \cdot \hbar^2$$

Wait — let me be more careful. The way separation actually works: the left side depends only on $r$, the right side only on $(\theta, \phi)$. Each side must equal a constant, which we will call $\ell(\ell+1)$ for reasons that will become clear:

**Angular equation:**

$$\hat{L}^2 Y(\theta, \phi) = \hbar^2\ell(\ell+1)\,Y(\theta, \phi)$$

**Radial equation:**

$$\frac{1}{R}\frac{d}{dr}\!\left(r^2\frac{dR}{dr}\right) - \frac{2mr^2}{\hbar^2}[V(r) - E] = \ell(\ell+1)$$

The angular equation is the *universal* part. It is an eigenvalue equation for $\hat{L}^2$ on the unit sphere, and it does not know anything about which central potential you chose. Its solutions are the spherical harmonics $Y_{\ell m}(\theta, \phi)$ — solved once, in this chapter, valid for hydrogen, the 3D harmonic oscillator, the spherical well, the muonic atom, anything central. The radial equation has $V(r)$ in it; that is where the specific physics lives.

### 4.3 The angular solutions

Try a further separation $Y(\theta, \phi) = \Theta(\theta)\Phi(\phi)$. The $\phi$ equation comes out cleanly:

$$\Phi''(\phi) = -m^2\Phi(\phi)$$

with general solution $\Phi_m(\phi) = e^{im\phi}/\sqrt{2\pi}$. Single-valuedness — the requirement that $\Phi(\phi + 2\pi) = \Phi(\phi)$ — forces $m$ to be an integer.

The $\theta$ equation, after substituting $u = \cos\theta$, becomes the **associated Legendre equation**:

$$(1 - u^2)\frac{d^2 P}{du^2} - 2u\frac{dP}{du} + \left[\ell(\ell+1) - \frac{m^2}{1 - u^2}\right]P = 0$$

This is one of the famous equations of mathematical physics. Its physically acceptable solutions (regular at $u = \pm 1$, i.e., at the poles $\theta = 0, \pi$) are the **associated Legendre functions** $P_\ell^m(\cos\theta)$, which exist only when $\ell = 0, 1, 2, \ldots$ and $|m| \leq \ell$. The condition that $\ell$ is a non-negative integer is what *forces* the eigenvalue of $\hat{L}^2$ to take the discrete values $\hbar^2 \ell(\ell+1)$. The constraint $|m| \leq \ell$ falls out of requiring $P_\ell^m$ to remain finite.

Stitch the pieces together with the proper normalization (Griffiths §4.1.3; Liboff §9.3; NIST DLMF Ch. 14):

$$Y_{\ell m}(\theta, \phi) = \sqrt{\frac{2\ell+1}{4\pi}\,\frac{(\ell - |m|)!}{(\ell + |m|)!}}\;P_\ell^m(\cos\theta)\,e^{im\phi}$$

These are the **spherical harmonics**. They satisfy:

$$\int_0^{2\pi}d\phi\int_0^\pi\sin\theta\,d\theta\;Y_{\ell' m'}^*\,Y_{\ell m} = \delta_{\ell\ell'}\delta_{mm'}$$

They are orthonormal on the unit sphere. They form a complete basis for square-integrable functions on the sphere: any nice function $f(\theta, \phi)$ can be expanded as $f = \sum_{\ell m} c_{\ell m}Y_{\ell m}$ with $c_{\ell m} = \int Y_{\ell m}^* f\,d\Omega$.

### 4.4 The first few spherical harmonics

Worth tabulating explicitly:

- $Y_0^0 = \dfrac{1}{\sqrt{4\pi}}$ — constant. Total spherical symmetry. The s-orbital has no angular structure.

- $Y_1^0 = \sqrt{\dfrac{3}{4\pi}}\cos\theta$ — the physics $p_z$. Vanishes on the equator, maximal at the poles.

- $Y_1^{\pm 1} = \mp\sqrt{\dfrac{3}{8\pi}}\sin\theta\,e^{\pm i\phi}$ — note the minus sign for $m = +1$ (the **Condon-Shortley phase convention** — Griffiths follows it; some textbooks do not). The probability density $|Y_1^{\pm 1}|^2 = (3/8\pi)\sin^2\theta$ is the *same* for $m = +1$ and $m = -1$, and is independent of $\phi$ — it is rotationally symmetric about the $z$-axis. The two states differ only in the phase rotation $e^{\pm i\phi}$.

- $Y_2^0 = \sqrt{\dfrac{5}{16\pi}}(3\cos^2\theta - 1)$ — the $d_{z^2}$ orbital. Has nodes where $\cos\theta = \pm 1/\sqrt{3}$ (about $54.7°$ from the $z$-axis on either side). The famous "donut belt" in the middle is between those nodes.

Two facts to internalize:

1. $|Y_{\ell m}|^2$ is independent of $\phi$ — always. The $\phi$-dependence of $Y_{\ell m}$ is only in the phase $e^{im\phi}$, and the modulus squared kills the phase. The angular probability density is axially symmetric about the $z$-axis.

2. $Y_\ell^m$ has $\ell - |m|$ nodes in $\theta$ (zeros of $P_\ell^m$) and no nodes in $|Y|^2$ along $\phi$.

**Misconception 1.** *"Spherical harmonics *are* the orbital wave functions."* No. They are the *angular part* of the wave function. The full bound-state wave function for a central potential is $\psi(r, \theta, \phi) = R(r)Y_{\ell m}(\theta, \phi)$, where $R(r)$ depends on which $V(r)$ you chose. Spherical harmonics are universal across central potentials; radial wave functions are not. When a chemistry textbook draws "the 2p orbital," it is showing the *combined* radial-angular shape — usually as a 3D probability density surface — and conflating it with the angular factor.

**Misconception 2.** *"The chemistry-textbook p-orbitals are the $Y_1^m$."* They are real linear combinations:

$$p_x = -\tfrac{1}{\sqrt{2}}(Y_1^1 - Y_1^{-1}) \propto \sin\theta\cos\phi$$
$$p_y = \tfrac{i}{\sqrt{2}}(Y_1^1 + Y_1^{-1}) \propto \sin\theta\sin\phi$$
$$p_z = Y_1^0 \propto \cos\theta$$

(signs depend on the Condon-Shortley convention used). The chemistry $p$-orbitals are eigenstates of *Cartesian projections* of the position operator (loosely: they are aligned with $x$, $y$, $z$ in space), not eigenstates of $\hat{L}_z$. The physics $Y_1^{\pm 1}$ are eigenstates of $\hat{L}_z$ with eigenvalue $\pm\hbar$ — they carry definite *z*-component of angular momentum but no definite spatial direction. Both are valid bases for the $\ell = 1$ subspace; they describe the same set of physical states; you can write any $\ell = 1$ state in either basis. Chemistry prefers the real basis because it makes pretty axis-aligned pictures. Physics prefers the complex basis because it diagonalizes $\hat{L}_z$ — useful for angular-momentum bookkeeping. The simulation in this chapter will let you toggle between them and watch the basis change while the same physical state stays put.

## 5. Concept block — angular momentum and the operator picture

### 5.1 The angular momentum operators

Classical angular momentum $\vec L = \vec r \times \vec p$ becomes, in quantum mechanics, three Hermitian operators:

$$\hat{L}_x = \hat{y}\hat{p}_z - \hat{z}\hat{p}_y, \quad \hat{L}_y = \hat{z}\hat{p}_x - \hat{x}\hat{p}_z, \quad \hat{L}_z = \hat{x}\hat{p}_y - \hat{y}\hat{p}_x$$

In spherical coordinates, after some calculus,

$$\hat{L}_z = -i\hbar\frac{\partial}{\partial\phi}$$

This makes $\hat{L}_z$'s action on $Y_{\ell m}$ obvious — the $\phi$-dependence is $e^{im\phi}$, and

$$\hat{L}_z\,e^{im\phi} = -i\hbar\,im\,e^{im\phi} = m\hbar\,e^{im\phi}$$

so $\hat{L}_z Y_{\ell m} = m\hbar\, Y_{\ell m}$. The integer $m$, with $-\ell \leq m \leq +\ell$, is the **magnetic quantum number**, and $m\hbar$ is the eigenvalue of $\hat{L}_z$.

The other components $\hat{L}_x, \hat{L}_y$ have more complicated expressions in spherical coordinates and do not have $Y_{\ell m}$ as eigenstates. They do, however, satisfy:

$$\hat{L}^2 Y_{\ell m} = \hbar^2\ell(\ell+1)Y_{\ell m}$$

The spherical harmonic $Y_{\ell m}$ is a *joint* eigenstate of $\hat{L}^2$ and $\hat{L}_z$ but *not* an eigenstate of $\hat{L}_x$ or $\hat{L}_y$.

### 5.2 The angular momentum algebra

Compute $[\hat{L}_x, \hat{L}_y]$ from the canonical commutators $[\hat{x}_i, \hat{p}_j] = i\hbar\delta_{ij}$. A long but straightforward calculation (worked example 6.1) gives:

$$[\hat{L}_x, \hat{L}_y] = i\hbar\hat{L}_z$$

and cyclic permutations. Compactly:

$$[\hat{L}_i, \hat{L}_j] = i\hbar\epsilon_{ijk}\hat{L}_k$$

This is the **angular momentum algebra**. The three components do not commute among themselves — they are *incompatible* observables in the Chapter 4 sense, and the Robertson inequality applies. But each component commutes with $\hat{L}^2 = \hat{L}_x^2 + \hat{L}_y^2 + \hat{L}_z^2$:

$$[\hat{L}^2, \hat{L}_i] = 0, \quad i = x, y, z$$

By the compatibility theorem of Chapter 4, $\hat{L}^2$ and *any one* component (conventionally $\hat{L}_z$) can be simultaneously diagonalized. Their joint eigenstates are the spherical harmonics.

The same algebra — with $\hat{L}_\pm = \hat{L}_x \pm i\hat{L}_y$ as ladder operators — gives an algebraic derivation of the spectrum (Sakurai Ch. 3; Liboff §9). The fact that $\hat{L}^2$ has eigenvalues $\hbar^2\ell(\ell+1)$ rather than $\hbar^2\ell^2$ falls out of the algebra and is one of those things that look weird until you do the derivation. It is the same structural move as the harmonic-oscillator ladder operators of Chapter 3 — that algebra is *not* a one-time trick, it is the general way to extract spectra from commutators.

**Misconception 1.** *"$\hat{L}_x$ and $\hat{L}_y$ can't both be measured because the apparatus is in the way."* No — they cannot be simultaneously *sharp* because $[\hat{L}_x, \hat{L}_y] = i\hbar\hat{L}_z \neq 0$. The Robertson inequality gives $\sigma_{L_x}\sigma_{L_y} \geq \hbar|\langle L_z\rangle|/2$ — a statistical statement about ensemble spreads, not an apparatus limitation, *exactly* as we worked through in Chapter 4 with $\sigma_x$ and $\sigma_p$ on the qubit. The misconception is recurring: every time non-commuting observables appear, the "measurement-disturbance" story tries to creep back in. The Robertson framing is what does the actual work.

**Misconception 2.** *"$L^2 = (\ell\hbar)^2$."* No — it is $\hbar^2\ell(\ell+1)$. The extra $\ell$ matters. Consider: the maximum value of any single component is $|L_z|_{\max} = \ell\hbar$ (when $m = \pm\ell$). But $\sqrt{\langle L^2\rangle} = \hbar\sqrt{\ell(\ell+1)} > \ell\hbar$ for $\ell > 0$. The angular momentum "vector" can never be fully aligned with any axis — there is always some transverse component, related to the non-commuting algebra. Geometrically: even in the "maximally aligned" state $|\ell, m = \ell\rangle$, the angular momentum points along a cone, not along the $z$-axis. The half-angle of the cone is $\arccos(\ell/\sqrt{\ell(\ell+1)})$ — for $\ell = 1$, about $45°$.

This is a worth-pausing-on geometric fact. The Bohr-model picture, where the electron orbits in a definite plane, is dead on arrival in this geometry. The angular momentum has a definite magnitude and a definite $z$-component, and that is *all*. The $x$ and $y$ components are intrinsically indefinite. There is no "orbital plane."

## 6. Concept block — the radial equation and the centrifugal barrier

### 6.1 The substitution that does the work

With $\psi = R(r)Y_{\ell m}(\theta, \phi)$, the radial equation we obtained in §4.2 still has the inconvenient $r^2$ inside its first derivative. Define $u(r) = rR(r)$. Then a short calculation shows:

$$-\frac{\hbar^2}{2m}\frac{d^2 u}{dr^2} + \left[V(r) + \frac{\hbar^2\ell(\ell+1)}{2mr^2}\right]u(r) = E\,u(r)$$

This is a **1D Schrödinger equation in $u(r)$** on the half-line $r \in [0, \infty)$ with **effective potential**:

$$V_{\text{eff}}(r) = V(r) + \frac{\hbar^2\ell(\ell+1)}{2mr^2}$$

The extra term — positive, diverging at $r = 0$, falling off as $1/r^2$ at large $r$ — is the **centrifugal barrier**. For $\ell > 0$, it forces $u(0) = 0$ (to keep $R = u/r$ finite at the origin) and pushes probability away from the origin. For $\ell = 0$ (s-states), there is no barrier, and the wave function can have finite amplitude at the origin.

This recasting is *the* most powerful pedagogical move in the chapter. A 3D central-force problem is reduced to a 1D bound-state problem — exactly the kind you have been solving since Chapter 2 — with an extra centrifugal term added to the potential. The trade is: kill the explicit angle dependence by going to $u(r)$, pay for it with the effective potential.

**Misconception.** *"The centrifugal barrier is a real force pushing the electron out."* No, it is a kinetic energy contribution that *appears* as a potential-like term because we have already projected the wave function onto an angular momentum eigenstate. The full kinetic energy operator is $-\hbar^2\nabla^2/(2m)$. When you write the wave function as $R(r)Y_{\ell m}$, the angular part of the kinetic energy becomes $\hbar^2\ell(\ell+1)/(2mr^2)\cdot R(r)Y_{\ell m}$. Mathematically it sits in the same place as $V(r)$. Physically it is a *kinetic* energy term that depends on how much angular momentum the state carries. Students who saw centripetal forces in mechanics often confuse $\hbar^2\ell(\ell+1)/(2mr^2)$ with a force. It is not. It is part of the kinetic energy.

### 6.2 Boundary conditions

For bound states with $V(r) \to 0$ at infinity (Coulomb, Yukawa, finite spherical well):

- $u(0) = 0$ — to keep $R = u/r$ finite at the origin. (For $\ell = 0$, the boundary $u(0) = 0$ is automatic from the second-order ODE if $V$ is well-behaved at the origin and $R(0)$ is finite.)
- $u(r) \to 0$ as $r \to \infty$ — for normalizability.

The normalization of the full wave function:

$$\int|\psi|^2 d^3r = \int_0^\infty |R(r)|^2 r^2\,dr \cdot \int|Y_{\ell m}|^2\,d\Omega = \int_0^\infty |u(r)|^2\,dr = 1$$

— using $\int|Y_{\ell m}|^2 d\Omega = 1$. The radial probability density $|u(r)|^2$ is the probability per unit length of finding the particle at distance $r$ (integrated over all angles). The familiar peak at $r = a_0$ for the hydrogen 1s wave function is a peak of $|u|^2$, not of $|R|^2$.

### 6.3 The 3D infinite spherical well — a worked solvable example

Take $V(r) = 0$ for $r < a$ and $V = \infty$ for $r \geq a$. Inside the well, the radial equation is:

$$-\frac{\hbar^2}{2m}\frac{d^2 u}{dr^2} + \frac{\hbar^2\ell(\ell+1)}{2mr^2}u = E\,u$$

Define $k = \sqrt{2mE/\hbar^2}$ and substitute $\rho = kr$. The equation becomes:

$$\frac{d^2 u}{d\rho^2} - \frac{\ell(\ell+1)}{\rho^2}u + u = 0$$

with solutions related to **spherical Bessel functions** $j_\ell(\rho)$ via $u(r) = r j_\ell(kr)$. (Equivalently, $R(r) = j_\ell(kr)$.) The boundary condition at the wall is $u(a) = 0$, i.e., $j_\ell(ka) = 0$. So $ka$ is the $n$-th zero of $j_\ell$, denoted $\beta_{n\ell}$:

$$E_{n\ell} = \frac{\hbar^2 \beta_{n\ell}^2}{2ma^2}$$

For $\ell = 0$: $j_0(\rho) = \sin\rho/\rho$, with zeros at $\rho = \pi, 2\pi, 3\pi, \ldots$. So $\beta_{n0} = n\pi$ and $E_{n0} = n^2\pi^2\hbar^2/(2ma^2)$ — identical to the 1D infinite well, as expected (s-states have no angular structure).

For $\ell = 1$: $j_1(\rho) = \sin\rho/\rho^2 - \cos\rho/\rho$. Its first zero is at $\rho \approx 4.493$, giving $\beta_{1,1}/\pi \approx 1.430$. So $E_{1,1} \approx 1.430^2\,E_{1,0} \approx 2.046\,E_{1,0}$.

The level ordering goes 1s, 1p, 1d, 2s, 1f, 2p, 1g, 2d, ... — and this approximate spectrum is *the foundation of the nuclear shell model* (Mayer & Jensen 1949 [verify precise citations *Phys. Rev.* 75, 1969 and *Phys. Rev.* 75, 1766] showed that adding strong spin-orbit coupling to a spherical-well-like potential reproduces the observed magic numbers 2, 8, 20, 28, 50, 82, 126 — for which they shared the 1963 Nobel Prize in Physics).

**Misconception.** *"Higher $\ell$ means higher energy."* Not in general. It depends on $V(r)$. For the spherical well, higher $\ell$ usually has higher energy at the same $n$ — the centrifugal barrier raises the kinetic energy. For the hydrogen atom (Chapter 7), energy depends *only* on the principal quantum number $n$, not on $\ell$ — a special "accidental" degeneracy of the $1/r$ Coulomb potential, related to a deeper SO(4) symmetry that we will not derive here but will mention as a sidebar. For the 3D harmonic oscillator, energy depends on $2n_r + \ell$ — another accidental degeneracy. The right answer is always: solve the radial equation for the specific $V(r)$ and see what the spectrum does.

## 7. Worked examples

### 7.1 Verifying $[\hat{L}_x, \hat{L}_y] = i\hbar\hat{L}_z$

Start from definitions:

$$\hat{L}_x = \hat{y}\hat{p}_z - \hat{z}\hat{p}_y, \quad \hat{L}_y = \hat{z}\hat{p}_x - \hat{x}\hat{p}_z$$

Compute:

$$[\hat{L}_x, \hat{L}_y] = [\hat{y}\hat{p}_z - \hat{z}\hat{p}_y, \hat{z}\hat{p}_x - \hat{x}\hat{p}_z]$$

Expand bilinearly into four commutators:

$$= [\hat{y}\hat{p}_z, \hat{z}\hat{p}_x] - [\hat{y}\hat{p}_z, \hat{x}\hat{p}_z] - [\hat{z}\hat{p}_y, \hat{z}\hat{p}_x] + [\hat{z}\hat{p}_y, \hat{x}\hat{p}_z]$$

Use $[\hat{A}\hat{B}, \hat{C}\hat{D}] = \hat{A}[\hat{B}, \hat{C}]\hat{D} + \hat{A}\hat{C}[\hat{B}, \hat{D}] + [\hat{A}, \hat{C}]\hat{D}\hat{B} + \hat{C}[\hat{A}, \hat{D}]\hat{B}$ (a Leibniz-like rule) — or just expand each one.

Take the first term: $[\hat{y}\hat{p}_z, \hat{z}\hat{p}_x]$. The only non-zero canonical commutator hiding inside is $[\hat{p}_z, \hat{z}] = -i\hbar$. Working it out:

$$[\hat{y}\hat{p}_z, \hat{z}\hat{p}_x] = \hat{y}[\hat{p}_z, \hat{z}]\hat{p}_x = -i\hbar\,\hat{y}\hat{p}_x$$

Second term: $[\hat{y}\hat{p}_z, \hat{x}\hat{p}_z] = 0$ (no overlapping canonical pair).

Third term: $[\hat{z}\hat{p}_y, \hat{z}\hat{p}_x] = 0$.

Fourth term: $[\hat{z}\hat{p}_y, \hat{x}\hat{p}_z]$. The non-zero piece is $[\hat{z}, \hat{p}_z] = i\hbar$:

$$[\hat{z}\hat{p}_y, \hat{x}\hat{p}_z] = \hat{x}\,\hat{p}_y\,[\hat{z}, \hat{p}_z] = i\hbar\,\hat{x}\hat{p}_y$$

Sum:

$$[\hat{L}_x, \hat{L}_y] = -i\hbar\hat{y}\hat{p}_x + i\hbar\hat{x}\hat{p}_y = i\hbar(\hat{x}\hat{p}_y - \hat{y}\hat{p}_x) = i\hbar\hat{L}_z$$

The cyclic permutations follow identically. The whole 3D angular momentum algebra is squeezed out of $[\hat{x}_i, \hat{p}_j] = i\hbar\delta_{ij}$ by bookkeeping.

### 7.2 Explicit $Y_{\ell m}$ for $\ell = 0, 1$

For $\ell = 0$: $P_0^0(u) = 1$. Normalization gives $Y_0^0 = 1/\sqrt{4\pi}$. A constant on the sphere — the s-orbital angular factor.

For $\ell = 1, m = 0$: $P_1^0(u) = u$. So $\Theta_1^0(\theta) \propto \cos\theta$, and after normalization $Y_1^0 = \sqrt{3/(4\pi)}\cos\theta$.

For $\ell = 1, m = \pm 1$: $P_1^1(u) = -\sqrt{1 - u^2}$ (with the Condon-Shortley sign — Griffiths uses this; check yours). So $\Theta_1^{\pm 1}(\theta) \propto \sin\theta$, and:

$$Y_1^{\pm 1} = \mp\sqrt{\frac{3}{8\pi}}\sin\theta\,e^{\pm i\phi}$$

Verify orthogonality: $\int Y_1^{1*} Y_1^{-1}\,d\Omega = ?$ The $\phi$ integrals give $\int_0^{2\pi}e^{-i\phi}e^{-i\phi}\,d\phi = \int_0^{2\pi}e^{-2i\phi}\,d\phi = 0$, so the cross-overlap is zero. They are orthogonal — different $m$, different eigenstates of $\hat{L}_z$. The factor of $\mp$ comes from the Condon-Shortley convention; it carries through to the real-combination chemistry orbitals as the sign in front of $p_x$.

### 7.3 The 1s state of the 3D spherical well

Take $\ell = 0$, $n = 1$. From the analysis above, $j_0(\rho) = \sin\rho/\rho$, first zero at $\rho = \pi$. So $ka = \pi$, $k = \pi/a$, $E_{1,0} = \pi^2\hbar^2/(2ma^2)$. The radial function $R(r) = j_0(kr) = \sin(\pi r/a)/(\pi r/a)$. The transformed $u(r) = rR(r) = (a/\pi)\sin(\pi r/a)$ — *exactly* the ground state of the 1D infinite well of width $a$ (up to normalization). The s-state of the 3D spherical well, after the $u$ transformation, is identical to the 1D infinite-well ground state. That is the meaning of "the radial equation is just 1D in $u$."

Normalize: $\int_0^a |u|^2 dr = (a/\pi)^2 \cdot a/2 = a^3/(2\pi^2)$, so $u(r) = \sqrt{2/a}\sin(\pi r/a)$ after normalization. Then $R(r) = u/r = \sqrt{2/a}\sin(\pi r/a)/r$. The full wave function:

$$\psi_{1,0,0}(r, \theta, \phi) = R(r)Y_0^0 = \frac{1}{\sqrt{2\pi a}}\,\frac{\sin(\pi r/a)}{r}$$

Note the singular-looking $1/r$ behavior at $r \to 0$: $\sin(\pi r/a) \approx \pi r/a$ for small $r$, so $R(r) \to \sqrt{2/a}\cdot\pi/a = \pi\sqrt{2}/a^{3/2}$ — finite. The wave function does *not* diverge at the origin; the s-state has finite amplitude there. (This is the s-state's distinguishing feature, and it is the reason s-electrons feel relativistic effects more strongly in heavy atoms — they spend time at small $r$ where the nucleus is.)

## 8. Exercises

**Warm-up.**

1. Write the 3D Schrödinger equation in spherical coordinates for $V(r) = -e^2/(4\pi\epsilon_0 r)$ (the hydrogen atom). Identify the radial part and the angular part. Do *not* solve — Chapter 7 will.

2. Verify $\int|Y_0^0|^2\,d\Omega = 1$ explicitly. Then verify $\int|Y_1^0|^2\,d\Omega = 1$.

3. Compute $|Y_1^0(\theta, \phi)|^2$ and $|Y_1^1(\theta, \phi)|^2$. For each, sketch the polar plot of $|Y|^2$ as $r(\theta) = |Y|^2$. (The $p_z$ dumbbell along the $z$-axis; the $|Y_1^{\pm 1}|^2$ donut around the $z$-axis.)

**Application.**

4. Verify $\hat{L}_z Y_1^1 = \hbar\,Y_1^1$ by direct calculation: write $Y_1^1$ explicitly, apply $\hat{L}_z = -i\hbar\,\partial_\phi$.

5. Show that the real combinations $p_x \propto \sin\theta\cos\phi$ and $p_y \propto \sin\theta\sin\phi$ are *not* eigenstates of $\hat{L}_z$. Compute $\hat{L}_z p_x$ explicitly and show that it returns $-i\hbar p_y$ (or $+i\hbar p_y$, depending on sign convention). The chemistry basis sacrifices definite $L_z$ for definite spatial axes.

6. Apply the substitution $u(r) = rR(r)$ to the radial equation and verify that the centrifugal barrier $\hbar^2\ell(\ell+1)/(2mr^2)$ falls out exactly. Identify which derivative of $r^2 dR/dr$ produces the $\ell(\ell+1)/r^2$ term.

7. For the 3D infinite spherical well, look up (or compute) the first three zeros of $j_1(\rho)$ and $j_2(\rho)$. Use them to confirm the level ordering 1s, 1p, 1d, 2s. (You can use the fact that $j_\ell(\rho)$ for large $\rho$ behaves like $\sin(\rho - \ell\pi/2)/\rho$, so its $n$-th zero is approximately at $\rho \approx (n + \ell/2)\pi$.)

**Synthesis.**

8. Compute the angle of the "uncertainty cone" for the $|\ell, m = \ell\rangle$ state: $\cos\alpha = m/\sqrt{\ell(\ell+1)} = \ell/\sqrt{\ell(\ell+1)}$. Evaluate for $\ell = 1, 2, 3, 10, 100$. What happens as $\ell \to \infty$? Interpret physically.

9. Compute the matrix elements $\langle Y_1^0|\cos\theta|Y_1^0\rangle$ and $\langle Y_0^0|\cos\theta|Y_1^0\rangle$ by direct integration over the sphere. The first matters for the Stark effect; the second matters for dipole transitions. Selection rules in atomic transitions come from exactly this kind of integral.

10. Show that the s-states ($\ell = 0$) of the 3D spherical well have the same energies as the corresponding 1D infinite-well states (of the same width). Explain why this is a special feature of $\ell = 0$.

**Challenge.**

11. Build the angular momentum ladder operators $\hat{L}_\pm = \hat{L}_x \pm i\hat{L}_y$. Show that $[\hat{L}_z, \hat{L}_\pm] = \pm\hbar\hat{L}_\pm$. Use this to argue, by analogy with the harmonic-oscillator ladder of Chapter 3, that $\hat{L}_\pm$ shifts $m$ by $\pm 1$. (Sakurai Ch. 3 does this in detail.)

12. The Stark effect places an atom in a uniform electric field $\vec E$ along $\hat z$. The perturbing potential is $V_{\text{pert}} = eEz = eEr\cos\theta$. Note that $\cos\theta \propto Y_1^0$. Argue, using the angular integrals from problem 9, that to first order the only states connected by this perturbation are those differing by $\Delta\ell = \pm 1$ and $\Delta m = 0$. This is a selection rule, and it falls out of the angular-momentum algebra. (Chapter 9 will use this.)

13. The cosmic microwave background's temperature on the sky $T(\theta, \phi)$ is a function on the celestial sphere. Expand it in spherical harmonics: $T(\theta, \phi) = \sum_{\ell m} a_{\ell m} Y_{\ell m}(\theta, \phi)$. The power spectrum is $C_\ell = \langle|a_{\ell m}|^2\rangle$ (averaged over $m$). Argue, using rotational invariance, that the $C_\ell$ do not depend on $m$. What does an observed peak in $C_\ell$ at $\ell \approx 220$ correspond to physically? (Briefly look up the Planck 2018 results [verify A&A 641, A6 DOI] for context.)

## 9. What would change my mind

If a precision spectroscopic measurement consistently found energy levels of a clean central-potential system (say, a Rydberg atom in a known potential) that did *not* organize themselves by $\ell$ and $m$ quantum numbers as predicted by the separation of variables — that is, if the angular structure of bound states deviated from what the spherical-harmonic basis predicts — the chapter's whole framework would be in trouble. So far, every test has come back in the theory's favor. The most stringent recent tests are atomic-clock comparisons, which rely on precisely the angular-momentum algebra developed here and are now stable to roughly $10^{-18}$ in fractional frequency.

If a foundational analysis identified a 3D problem of broad interest that is *not* solvable by separation of variables in any coordinate system — and that has no exploitable symmetry — the centrality of this chapter's method would be diminished. The Stark effect is one such case (not separable in any coordinate system more clever than parabolic, and even that is special), but perturbation theory handles it. The bound-state problems that resist all the standard techniques are an active research area, but they are not what undergraduate atoms look like.

## 10. Still puzzling

The accidental degeneracy of the hydrogen atom — that energies depend only on $n$, not on $\ell$ — has an explanation: there is an extra conserved quantity, the Runge-Lenz vector, and a hidden SO(4) symmetry of the $1/r$ Coulomb potential. The same kind of accidental degeneracy in the 3D isotropic harmonic oscillator has an explanation: an SU(3) symmetry. Both are clean. What I do not understand, satisfactorily, is *why* these particular symmetries appear in these particular potentials and not others. The $1/r$ potential happens to be the unique potential (along with the harmonic) for which all bound orbits in classical mechanics close — Bertrand's theorem. The quantum degeneracy and the classical closed-orbit property are surely the same fact wearing different clothes, but I do not know a derivation that makes the connection feel inevitable rather than coincidental. The math is settled; the conceptual unity is not, for me.

## 11. LLM Exercise — the spherical harmonics visualizer

You are going to build a single-file D3 simulation that displays the spherical harmonics $Y_{\ell m}(\theta, \phi)$ in two synchronized panels — a polar cross-section and a pseudo-3D mesh on the sphere — with a toggle between physics (complex) and chemistry (real) conventions, and an animation mode that visualizes the $\phi$-phase rotation generated by $\hat{L}_z$. The deliverable is `05-spherical-harmonics.html`.

### Part 1 — Update `PROJECT.md`

```
Append a new entry to PROJECT.md describing the Chapter 5 simulation:

Chapter 05 — Quantum Mechanics in Three Dimensions
Deliverable: 05-spherical-harmonics.html
Status: in progress

The simulation visualizes Y_{l m}(theta, phi) with two side-by-side panels:

1. Left panel: polar cross-section at phi = 0. Plot r(theta) = |Y_{l m}|^2
   in polar coordinates, with theta measured from the +z axis. Lobes
   appear naturally - Y_1^0 gives a dumbbell, Y_2^0 a peanut-with-belt.
   Color: lobes filled with semi-transparent fill; outline darker. When
   "Re(Y)" mode is active, positive lobes are one color (e.g. blue) and
   negative lobes are another (e.g. red).

2. Right panel: pseudo-3D unit sphere with surface shaded by |Y|^2. The
   sphere is meshed in 30 latitude bands and 30 longitude bands, giving
   ~900 patches. Each patch is colored by |Y_{l m}|^2 at its center.
   Patches are sorted by mean projected depth (painter's algorithm) so
   that front-facing patches occlude back-facing ones in the SVG render
   order. View angles (alpha, beta) draggable.

   Alternative right-panel display: "balloon" mode, where each surface
   patch is moved radially outward by an amount proportional to
   |Y_{l m}(theta, phi)|^2, producing the familiar dumbbell / clover shapes
   in 3D rather than as a flat-sphere color map.

3. Bottom strip: eigenvalue display:
     L^2 = hbar^2 * l (l+1) = [value]
     L_z = hbar * m = [value]
     Nodes in theta: l - |m| - [list of nodal-cone angles]
     Convention: physics (complex Y) or chemistry (real combinations)

Controls:
- l selector (0 to 4)
- m selector (-l to +l, range updates when l changes)
- Convention toggle: "physics (complex)" vs "chemistry (real)"
- Display mode: "|Y|^2 (probability)" vs "Re(Y) (signed wave function)"
- Right panel display: "sphere with shading" vs "balloon"
- Animate phi-phase toggle: when enabled, multiply Y by exp(-i omega t)
  with omega = m (in natural units), so the phase wheel rotates at rate m.
  Visible on the right panel as a rotation of the wave-function color
  pattern when Re(Y) mode is active. The physical interpretation: this
  is the time evolution generated by L_z. m = 0 states are static
  (no phi rotation); higher |m| states rotate faster.

No three.js, no babylon, no math.js. Pure D3 SVG with hand-rolled
orthographic projection and painter's-algorithm depth sorting. Single
HTML file. This decision is documented in PROJECT.md to keep the
Brutalist system clean - one dependency, D3 v7 from CDN, no exceptions.
```

### Part 2 — The CLAUDE.md amendment

```
Append to CLAUDE.md the following physics rules for Chapter 5 simulations:

SPHERICAL HARMONICS PHYSICS RULES

1. Associated Legendre polynomials computed by recurrence:
     P_l^l(x) = (-1)^l * (2l-1)!! * (1-x^2)^(l/2)     [Condon-Shortley]
     P_{l+1}^l(x) = x * (2l+1) * P_l^l(x)
     (l - m + 1) * P_{l+1}^m(x) = (2l + 1) * x * P_l^m(x)
                                  - (l + m) * P_{l-1}^m(x)
   for l > m. The CONDON-SHORTLEY phase (the (-1)^l in the first line and
   the implicit (-1)^m in some other formulations) is the physics standard.
   Verify by computing Y_1^1 and checking it equals:
     Y_1^1 = -sqrt(3 / (8 pi)) * sin(theta) * exp(i phi)
   The minus sign matters.

2. Spherical harmonic:
     Y_l^m(theta, phi) = sqrt((2l+1) / (4 pi) * (l - m)! / (l + m)!)
                         * P_l^m(cos theta) * exp(i m phi)
   For m < 0, use Y_l^{-m}(theta, phi) = (-1)^m * conj(Y_l^m(theta, phi)).

3. Real combinations (chemistry convention):
     m > 0: Y_{l, m}^real = (1 / sqrt(2)) * (Y_l^{-m} + (-1)^m * Y_l^m)
     m = 0: Y_{l, 0}^real = Y_l^0
     m < 0: Y_{l, m}^real = (i / sqrt(2)) * (Y_l^m - (-1)^m * Y_l^{-m})
   Verify: the m=1 real combination is p_x ~ sin theta cos phi, and the
   m=-1 real combination is p_y ~ sin theta sin phi. Sanity-check that
   p_x has its maximum at theta = pi/2, phi = 0 (the +x direction).

4. Normalization sanity check (run at startup for each (l, m)):
   Riemann-sum the integral of |Y_{l m}|^2 over the sphere on a 100 x 100
   (theta, phi) grid with sin(theta) measure. The result should be 1
   within 0.01. If it is not, the normalization prefactor is wrong.

5. (1 - x^2) where x = cos(theta) can dip slightly negative due to
   floating-point near theta = 0 or pi. Clamp:
     sqrt_arg = max(0, 1 - x * x)
   before taking the square root in P_l^l.

6. Factorial: use a small lookup table for l up to 10. (l + m)! / (l - m)!
   may be computed as a product to avoid two large factorial overflows.

7. Painter's algorithm for the 3D sphere panel:
   For each of the ~900 surface patches, compute the patch center in 3D,
   project to 2D using the current view rotation, AND record the depth
   (signed distance from viewer; greater = farther). Sort the patch list
   by depth descending (back first, front last), then render in that
   order. The last patch drawn is on top. Without this sort, patches
   are rendered in mesh order and the orbital looks "inside out."

KNOWN FAILURE MODES to avoid:
(a) Condon-Shortley phase missing or wrong - check Y_1^1 sign.
(b) Factorial overflow for l > ~10 - cap or use log-gamma.
(c) (1 - x^2) negative due to floating-point - clamp.
(d) Forgetting normalization check at startup - the plot will look
    right in shape but wrong in absolute scale.
(e) Painter's algorithm omitted or wrong direction - orbital looks inverted.
(f) Real-combination signs wrong - p_x might point in the -x direction.
    Verify against the chemistry textbook canon (p_x maximum at +x).
(g) Y-axis labels saying "psi" instead of "|Y|^2" or "Y_{lm}" - this is
    the chapter's whole point and the label must reflect it.
```

### Part 3 — The simulation prompt

```
You are working in my directory which contains CLAUDE.md, DESIGN.md, and
PROJECT.md (with the Chapter 5 entry just added). Read all three first.

Build 05-spherical-harmonics.html: a single self-contained HTML file using
D3 v7 from a CDN, no other dependencies, that implements the Chapter 5
simulation specified in PROJECT.md following the physics rules in CLAUDE.md
and the visual constitution in DESIGN.md.

Layout: one SVG of 1100 x 650, divided as:

- Left panel (polar plot, 450 x 500 with controls below): a polar plot
  of r(theta) = |Y_{l m}(theta, phi=0)|^2 for the active (l, m). Render
  by sampling theta on a 360-point grid from 0 to 2 pi, computing
  Y_{l m}(theta, 0) (using the modulus or real part depending on mode),
  converting (r, theta) to Cartesian for SVG with the +z axis pointing
  up. Use d3.lineRadial() with d3.curveCardinalClosed for the outline.
  Fill the interior with a semi-transparent color; if Re(Y) mode is on,
  positive lobes blue and negative lobes red; if |Y|^2 mode, single
  color (e.g., teal). Draw the +z axis as a vertical reference line.
  Display the |Y|^2 magnitude scale with tick marks.

- Right panel (pseudo-3D, 500 x 500): the unit sphere with surface shading
  by |Y_{l m}|^2 at each patch. Mesh: 30 theta bands x 30 phi bands.
  For each patch, compute (theta_center, phi_center), evaluate
  Y_{l m}(theta_center, phi_center), and color the patch by:
    - magnitude (gray to bright color) if |Y|^2 mode
    - sign (blue-red diverging) if Re(Y) mode
  Project each patch corner to 2D using orthographic projection with view
  angles (alpha, beta). Sort patches by mean projected depth (painter's
  algorithm) and append in back-to-front order. Add the +z axis as a
  small arrow protruding from the sphere.

- Bottom strip (1100 x 100): eigenvalue display:
    L^2 = hbar^2 * l(l+1) = [value]   L_z = hbar * m = [value]
    Nodes in theta: [comma-separated list of nodal-cone angles in degrees]
    [m bar showing -l to +l, current m highlighted]

- Top strip (1100 x 50): controls:
  l selector (radio or stepper), m selector (constrained to -l..+l),
  convention toggle, display mode toggle, right-panel mode toggle,
  animate phi-phase toggle.

Mathematical implementation:
- Cache the patch grid (~900 entries) for the active (l, m), recompute
  on (l, m) or convention change.
- View rotation: alpha (azimuth, drag horizontally), beta (elevation, drag
  vertically). Default alpha = 20 degrees, beta = -10 degrees.
- Phi-phase animation: when enabled, replace exp(i m phi) by
  exp(i m (phi - omega t)) where omega = 1 in natural units. The shading
  of the right panel rotates at rate m. For m = 0 nothing changes.

Runtime sanity checks (write to console):
- At startup, for each (l, m) up to l = 4, integral of |Y_{l m}|^2 over
  sphere via Riemann sum must equal 1 within 0.01.
- For (l, m) = (1, 1) in physics convention, Y_1^1 at (theta=pi/2, phi=0)
  must equal -sqrt(3 / (8 pi)) within 1e-6 (real part) and 0 (imaginary
  part); the negative sign is the Condon-Shortley check.
- For chemistry-convention (l, m) = (1, 1) (the p_x orbital), the max
  of Y at theta = pi/2 should occur at phi = 0 (the +x direction).

Do NOT use any 3D library. Pure D3 with hand-rolled orthographic
projection and painter's-algorithm sorting. The decision to use pure
D3 (no three.js) is documented in PROJECT.md to keep the dependency
graph clean - one library, D3 v7 from CDN, no exceptions. Comments at
every non-trivial physics step.
```

### Part 4 — Exploration tasks and extension prompt

Run the simulation and answer the following:

1. **|Y|^2 is independent of $\phi$.** Set $(\ell, m) = (1, 1)$ in physics convention. Look at the polar cross-section (left panel) at $\phi = 0$. Now mentally rotate the view 90° about the $z$-axis — what would the cross-section at $\phi = \pi/2$ look like? Confirm by toggling the "Re(Y)" mode: the real part has a $\cos\phi$ dependence (and the cross-section at $\phi = 0$ shows the full lobe pattern), but $|Y|^2$ has the same shape at every $\phi$. The right panel makes this visible: in $|Y|^2$ mode the sphere is shaded with axial symmetry about $\hat z$, regardless of which $m$ you pick.

2. **The $p$-orbital basis swap.** Set $(\ell, m) = (1, 1)$. Toggle from "physics (complex)" to "chemistry (real)". The polar cross-section shape *changes* — from a donut-symmetric ring (the complex $|Y_1^1|^2$, which is rotationally symmetric about $z$) to a dumbbell pointing along $\hat x$ (the real $p_x$). The eigenvalue display shows that the chemistry-convention state is no longer an eigenstate of $\hat{L}_z$ — it has $\langle\hat{L}_z\rangle = 0$ but $\sigma_{L_z} = \hbar$ (you can verify by computing it). Same Hilbert subspace, different basis, different probabilities for $L_z$ measurements.

3. **$\ell(\ell+1)$, not $\ell^2$.** Set $\ell = 1$. The eigenvalue strip shows $L^2 = 2\hbar^2$ — *not* $\hbar^2$. The maximum value of $L_z$ is $1\hbar$ — *less* than $\sqrt{L^2} = \sqrt{2}\hbar$. The angular momentum vector lives on a cone, not on the $z$-axis. Compute the cone half-angle: $\arccos(1/\sqrt{2}) = 45°$. For $\ell = 2, m = 2$: $L_z = 2\hbar$, $\sqrt{L^2} = \sqrt{6}\hbar$, cone angle $\arccos(2/\sqrt{6}) \approx 35°$. As $\ell$ grows, the cone closes onto the axis — the classical limit of "angular momentum points in a definite direction."

4. **$\hat{L}_z$ generates $\phi$-rotation.** Toggle "animate phi-phase" on. For $m = 0$ (e.g., $Y_1^0$, the $p_z$), nothing happens — the wave function is real and has no $\phi$ dependence. For $m = 1$, the right panel's color pattern rotates around the $z$-axis at rate $\omega = 1$ in your units. For $m = 2$, it rotates twice as fast. For $m = -1$, it rotates the other way. Operationally: $\hat{L}_z$ is the *generator* of rotations about $\hat z$. The eigenvalue $m\hbar$ is the *rate* of phase accumulation. This is why $\hat{L}_z = -i\hbar\partial_\phi$ — it asks "how fast is the phase changing as you walk around the $z$-axis?"

5. **Nodes.** Set $\ell = 2, m = 0$. The polar cross-section of $|Y_2^0|^2$ has two nodes at the conical surfaces $\cos\theta = \pm 1/\sqrt{3}$ (about $\theta \approx 54.7°$ and $\theta \approx 125.3°$). Verify in the simulation that the eigenvalue strip lists these. Then increase $\ell$ to 4, leaving $m = 0$: there should be 4 nodes in $\theta$. As $\ell$ grows with fixed $m = 0$, the wave function develops more nodes — the angular kinetic energy increases.

**Extension prompt:**

```
Modify 05-spherical-harmonics.html to add a "central potential" panel
on the bottom right (additional 400 x 400 SVG region) that displays the
effective potential V_eff(r) = V(r) + hbar^2 l(l+1) / (2 m r^2) for a
choice of central potential V(r). Choices: 3D infinite spherical well
(V = 0 for r < 1, infinity otherwise), 3D harmonic oscillator
(V = (1/2) m omega^2 r^2), and Coulomb (V = -1/r). For each, plot the
total effective potential and the bound-state energies (computed via
matrix diagonalization on a discrete radial grid - use the Numerov
method or simple finite differences).

As l changes (the user changes l in the main simulation), the
centrifugal barrier grows, the effective potential shape changes, and
the energy levels reorganize. Highlight the connection: the angular
machinery the chapter just built is what allows the radial equation
to be one-dimensional with an l-dependent effective potential.

Update PROJECT.md to mark Chapter 05 complete and note the central-
potential panel as the bridge to Chapter 7 (hydrogen atom), where the
Coulomb-potential radial equation gets solved analytically.
```

---

*Sources consulted: Griffiths §4.1–4.3 (separation of variables, spherical harmonics, angular momentum algebra); Liboff Ch. 9 (angular momentum, pantry lines 418–423, 532), Ch. 10 (plane-wave expansion in spherical harmonics, pantry line 612); Arfken, Weber & Harris *Mathematical Methods for Physicists* (spherical harmonics and associated Legendre functions [verify chapter number]); Sakurai & Napolitano *Modern Quantum Mechanics* Ch. 3 (algebraic derivation of $\ell(\ell+1)$); Jackson *Classical Electrodynamics* Ch. 3 (spherical harmonics in potential theory); [NIST Digital Library of Mathematical Functions Ch. 14](https://dlmf.nist.gov/14) (Legendre functions, authoritative reference); Mayer & Jensen on the nuclear shell model [verify citations *Phys. Rev.* 75, 1969 (1949) and Haxel, Jensen & Suess *Phys. Rev.* 75, 1766 (1949)]; Planck Collaboration 2020 "Planck 2018 results VI: Cosmological parameters" [verify A&A 641, A6 DOI](https://www.aanda.org/articles/aa/full_html/2020/09/aa33910-18/aa33910-18.html); Karaçöp & Doymuş 2013 on chemistry students' confusion of orbitals with Bohr orbits [verify peer-reviewed publication].*

*Tags: spherical-harmonics, angular-momentum, central-potentials, centrifugal-barrier, orbitals, condon-shortley, d3-simulation*

*Status: draft for Nik's review. Voice-anchor check pending — root `style/` and `books/quantum-mechanics-with-llms/style/` not yet inspected. Flag: voice-unanchored if both empty. Several `[verify]` flags throughout — see specifically Mayer/Jensen nuclear shell model citations, Planck 2018 DOI, Karaçöp & Doymuş Turkish PER citation, Arfken section number, sign-convention difference between Griffiths 2nd and 3rd ed. for $Y_1^{\pm 1}$.*

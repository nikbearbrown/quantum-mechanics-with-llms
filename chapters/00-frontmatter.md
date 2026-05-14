# Quantum Mechanics+1: Interactive Simulations with Claude and D3

**Nik Bear Brown**

---

## Copyright

Copyright © 2026 Nik Bear Brown. All rights reserved.

Published by Bear Brown, LLC.

No part of this publication may be reproduced, distributed, or transmitted in
any form or by any means without the prior written permission of the publisher,
except in the case of brief quotations in critical reviews and certain other
noncommercial uses permitted by copyright law.

ISBN: [INSERT ISBN]

First edition: 2026

For permissions inquiries: bear@bearbrown.co

---

## Dedication

*For the junior who solved the infinite square well on paper, stared at the equations $\psi_n(x) = \sqrt{2/L} \sin(n\pi x/L)$, and still could not tell you what a wave function does. The simulations are for you. They are not a replacement for the math — they are the half of the picture the math leaves out.*

---

## Preface

There is a problem in undergraduate quantum mechanics that nobody talks about because everyone has it. The student passes the exams. The student can solve the infinite square well, the harmonic oscillator, the hydrogen atom. The student can integrate, normalize, expand in eigenstates, derive expectation values. The student can pass the second-semester midterm with a B+.

And then, in an oral exam — or in a conversation with a research advisor, or in front of their own slides at a poster session — the question comes: *what does the wave function actually do?* And the student goes quiet.

Not because they don't know the formulas. They know the formulas. They went quiet because they have no physical intuition for the object the formulas describe. They've spent two semesters manipulating something they have never seen behave. The mathematics is solid. The picture is missing.

This is the gap this book closes.

I have been teaching variants of computational physics, AI for engineering, and visualization at Northeastern for over a decade. I have watched dozens of physics majors hit this wall — students who could derive the radial equation of hydrogen on a blackboard but could not say, when asked, whether the orbital was a shape, a probability, a path, or something else entirely. The math was not the problem. The math was their solid ground. The problem was that quantum objects have no classical analogues, and a textbook full of equations does not give you intuition for an object whose behavior contradicts everything your body has learned about the world.

The solution to that problem has existed for thirty years. PhET, Visual Quantum Mechanics, Falstad's applets — these are all attempts to put quantum behavior in front of students so they can see it. The problem with those tools is that they are someone else's simulations. The student is a spectator. They click. They watch. They don't modify, can't extend, can't ask "what if I changed the potential?" and find out by changing the potential. They get a tour. They don't get the keys.

What changed in the last two years is that the keys are now available. A junior physics major, with no D3 experience, can ask Claude in plain English to produce a working interactive simulation of a wave function evolving in a finite square well — and then modify that simulation to ask the next question. The bottleneck has shifted from "I don't know how to write a simulation" to "I don't yet know what to simulate or how to verify it." That bottleneck is teachable. This book teaches it.

Why now: because Claude crossed a usability threshold for physics simulation code somewhere in 2024, and undergraduate physics curricula have not yet caught up. Why me: because I have run this experiment in my own teaching for two years and watched students who had been intuition-blind for three semesters suddenly start asking the right questions — *why does the ground state have non-zero energy? what happens to the probability current at a tunneling barrier?* — once they had a simulation they had built themselves and could change in real time.

The Brutalist system the book uses to govern simulation code (CLAUDE.md, DESIGN.md, PROJECT.md) is mine; it is what holds the boundary between physics judgment (yours) and code generation (the model's). The pedagogy is that boundary held strictly. The student decides what the simulation must show; Claude writes the SVG that shows it; the student verifies and modifies. The model never decides what the physics means.

This book does **not** teach you quantum mechanics from zero. It assumes you have had one prior semester of QM (modern physics or intro QM) and that you are comfortable with calculus through ODEs. It does not replace Griffiths or Shankar — pair this book with one of them. It does not teach you D3 from zero — it teaches you to direct Claude to write D3 for you and to verify what Claude wrote. It is not a graduate text. It is not the Brutalist system manual. It is the book I wanted to hand the student who passed the exam and still went silent when I asked them what the wave function does.

The book teaches one specific skill: how to build, modify, and verify quantum-mechanics simulations to develop the physical intuition the math by itself does not supply. After fourteen chapters, you should be able to look at a wave packet hitting a barrier, name what is about to happen and what equation governs it, and modify the simulation to ask a question your professor did not.

— Nik Bear Brown
Boston, 2026

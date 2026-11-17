# Congruent numbers

A *rational right triangle* is a triple $(a, b, c)$ of positive rational
numbers with $a^2 + b^2 = c^2$; its area is $ab/2$. Throughout, $n$ is a
positive rational number, and $E_n$ is the curve $y^2 = x^3 - n^2 x$. Its
discriminant is $64 n^6 \neq 0$, so it is an elliptic curve over $\mathbb{Q}$.

> [!milestone] Congruent numbers
> A positive rational number $n$ is *congruent* if there are positive rationals $a, b, c$ with $a^2 + b^2 = c^2$ and $ab/2 = n$. Then:
> 1. $n$ is congruent if and only if $q^2 n$ is congruent, for every nonzero rational $q$. So it is enough to decide the question for squarefree positive integers.
> 2. $5$, $6$ and $7$ are congruent, as the areas of the triangles $(3/2, 20/3, 41/6)$, $(3, 4, 5)$ and $(24/5, 35/12, 337/60)$.
>
> Sources: [@Koblitz1993, §I.1]; [@Conrad2008, §1 and the examples in §3–4].
>
> Proof routes: scale the triangle by $|q|$ for (1). For (2), check the two equations for each triangle.
>
> Formalization notes: define the predicate on `ℚ`, for example `∃ a b c : ℚ, 0 < a ∧ 0 < b ∧ 0 < c ∧ a ^ 2 + b ^ 2 = c ^ 2 ∧ a * b / 2 = n`. Statements about integers $n$ then use the cast to `ℚ`.
>
> Lean status: Mathlib —. Tau Ceti —.

> [!milestone] Right triangles and points of E_n
> Let $n$ be a positive rational. The maps
> $$(a, b, c) \mapsto \left( \frac{nb}{c - a},\ \frac{2n^2}{c - a} \right), \qquad (x, y) \mapsto \left( \frac{x^2 - n^2}{y},\ \frac{2nx}{y},\ \frac{x^2 + n^2}{y} \right)$$
> are inverse bijections between the rational solutions $(a, b, c)$ of $a^2 + b^2 = c^2$ and $ab/2 = n$, with no sign conditions, and the rational points $(x, y)$ of $E_n$ with $y \neq 0$. Consequently, $n$ is congruent if and only if $E_n(\mathbb{Q})$ has a point with $y \neq 0$.
>
> Sources: [@Conrad2008, Theorem 4.1]. Koblitz [@Koblitz1993, §I.2] relates triangles of area $n$ to points of $E_n$ whose $x$-coordinate is a rational square, and reaches the full criterion only in §I.9.
>
> Proof routes: direct computation. The denominators do not vanish: $ab = 2n \neq 0$ forces $b \neq 0$, hence $c^2 \neq a^2$ and $c \neq a$. For "consequently", replace $(a, b, c)$ by $(|a|, |b|, |c|)$, which is still a solution and is a triangle.
>
> Formalization notes: the points of $E_n$ with $y \neq 0$ are best stated as solutions of the equation, `y ^ 2 = x ^ 3 - n ^ 2 * x ∧ y ≠ 0`, and connected to Mathlib's `WeierstrassCurve.Affine.Point` for the curve $\langle 0, 0, 0, -n^2, 0 \rangle$ separately. Tau Ceti's `AlgebraicGeometry/EllipticCurve/CurveX3SubX.lean` defines the case $n = 1$ and is a template for $E_n$.
>
> Lean status: Mathlib —. Tau Ceti —.

> [!milestone] Fermat's right triangle theorem
> $1$ is not a congruent number: no right triangle with rational sides has area $1$. Equivalently, no right triangle with integer sides has an area that is a perfect square. Moreover, $2$ is not a congruent number.
>
> Sources: [@Conrad2008, Theorem 2.1] proves that $1$ is not congruent. [@Conrad2008, Appendix B, Table 5] reduces area $1$ to the equation $y^2 = x^4 - 1$ and area $2$ to $y^2 = x^4 + 1$.
>
> Proof routes:
> - For $1$, Conrad's proof is a direct infinite descent on $a^2 + b^2 = c^2$, $ab = 2d^2$ through the parametrization of primitive Pythagorean triples. It needs no quartic equation. Mathlib has the parametrization (`PythagoreanTriple`), and its descent for $x^4 + y^4 = z^2$ in `Mathlib/NumberTheory/FLT/Four.lean` is a model.
> - Alternatively, prove Fermat's theorem that $x^4 - y^4 = z^2$ has no solution in positive integers, also by descent, and deduce the case of area $1$ from it. That is a classical textbook theorem, but no source in this plan proves it.
> - For $2$: if $ab = 4$ and $a^2 + b^2 = c^2$, then multiplying by $a^2$ gives $a^4 + 2^4 = (ac)^2$. Write $a = A/D$ with integers $A, D \neq 0$. Then $(acD^2)^2 = A^4 + (2D)^4$. A rational number whose square is an integer is an integer, so $acD^2 \in \mathbb{Z}$. This gives a solution of $X^4 + Y^4 = Z^2$ with $X = A$ and $Y = 2D$ nonzero, which Mathlib's `not_fermat_42` rules out.
>
> Lean status: Mathlib —; it has `not_fermat_42`, that $x^4 + y^4 = z^2$ has no solution in nonzero integers, but not the difference $x^4 - y^4$. Tau Ceti —.

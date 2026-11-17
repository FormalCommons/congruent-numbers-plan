# Rational points

Throughout, $n$ is a positive integer and $E_n$ is the curve
$y^2 = x^3 - n^2 x$, a Weierstrass equation with integer coefficients and
discriminant $64 n^6$. So $E_n$ has good reduction at every prime $p \nmid 2n$.
Its points of order two are $(0,0)$, $(n,0)$ and $(-n,0)$, the points with
$y = 0$.

> [!milestone] Points of E_n over finite fields
> Let $p$ be a prime with $p \nmid 2n$ and $p \equiv 3 \pmod 4$. Then $E_n(\mathbb{F}_p)$ has exactly $p + 1$ points, counting the point at infinity.
>
> Sources: [@Koblitz1993, §I.9].
>
> Proof routes: let $f(x) = x^3 - n^2 x$, so that $f(-x) = -f(x)$. The three roots $0, \pm n$ of $f$ are distinct because $p \nmid 2n$, and give three points with $y = 0$. The other $p - 3$ elements of $\mathbb{F}_p$ fall into pairs $\{x, -x\}$. Since $-1$ is not a square modulo $p$, exactly one of $f(x)$ and $f(-x)$ is a nonzero square, so each pair contributes two points. That makes $3 + (p - 3) + 1 = p + 1$.
>
> Formalization notes: Tau Ceti counts the points of a Weierstrass model with `pointCount`, and `pointCount_eq_card_point` compares it with Mathlib's point type. Mathlib has `ZMod.exists_sq_eq_neg_one_iff`: $-1$ is a square modulo $p$ if and only if $p \not\equiv 3 \pmod 4$.
>
> Lean status: Mathlib —. Tau Ceti —; it counts the case $n = 1$, $p = 3$ (`pointCount_curveX3SubX`), and characterizes supersingular curves by having $p + 1$ points (`isSupersingular_iff_card_point_eq`), for $p \geq 5$, but nothing gives $p + 1$ for $E_n$.

> [!milestone] Reduction is injective on torsion
> Let $E$ be an elliptic curve over $\mathbb{Q}$ given by a Weierstrass equation with integer coefficients, and let $p$ be an odd prime that does not divide its discriminant. Then reduction modulo $p$, $E(\mathbb{Q}) \to \tilde{E}(\mathbb{F}_p)$, is injective on the torsion subgroup of $E(\mathbb{Q})$. In particular, the order of the torsion subgroup divides $\#\tilde{E}(\mathbb{F}_p)$.
>
> Sources: [@Silverman2009, Prop. VII.3.1(b)] for torsion of order prime to $p$. For the $p$-part, the kernel of reduction is the group of the formal group, which has no $p$-torsion when the ramification index is less than $p - 1$, here $1 < p - 1$ [@Silverman2009, §IV.6]. Koblitz proves what he needs for $E_n$ directly [@Koblitz1993, §I.9].
>
> Lean status: Mathlib —. Tau Ceti **full**, in a general form: `injOn_reductionHom_torsion` and `card_torsion_dvd_card_reduction` in `AlgebraicGeometry/EllipticCurve/Affine/Point/TorsionReduction.lean`. They are stated over the fraction field $F$ of a Dedekind domain $A$, at a height-one prime $u$ of $A$, for a curve that is integral at $u$ with good reduction there. They take the hypothesis `hu : ∀ q : ℕ, q.Prime → (q : A) ∉ u.asIdeal ^ (q - 1)`. Over $\mathbb{Q}$, with $A = \mathbb{Z}$ and $u = (p)$ for an odd prime $p$, this holds: a prime $q \neq p$ is not in $(p)$, and $p \notin (p)^{p-1}$ since $p - 1 \geq 2$. No lemma states this yet. Good reduction comes from `isElliptic_integralModel_baseChange`, for a curve of the form `E.baseChange ℚ` with `E : WeierstrassCurve ℤ` whose discriminant is not divisible by $p$. `card_point_reduction_baseChange` in `AlgebraicGeometry/EllipticCurve/IntegralReduction.lean` turns the count over the residue field into a count over `ZMod p`. Use these; do not reprove reduction or the formal group.

> [!milestone] Torsion of E_n
> The torsion subgroup of $E_n(\mathbb{Q})$ is $\{O, (0,0), (n,0), (-n,0)\}$, which is isomorphic to $\mathbb{Z}/2 \times \mathbb{Z}/2$.
>
> Sources: [@Koblitz1993, §I.9, Prop. 17]. [@HalbeisenHungerbuhler2018] give an elementary proof, through a theorem of Fermat, that avoids Dirichlet's theorem.
>
> Proof routes: Koblitz's proof. Let $T$ be the torsion subgroup. For every prime $p \equiv 3 \pmod 4$ with $p \nmid 2n$, the order of $T$ divides $p + 1$, by the two milestones above.
> - If an odd prime $\ell$ divided $|T|$, choose such a $p$ with also $p \equiv 1 \pmod \ell$, by Dirichlet's theorem. Then $p + 1 \equiv 2 \pmod \ell$, a contradiction.
> - If $8$ divided $|T|$, choose such a $p$ with $p \equiv 3 \pmod 8$. Then $p + 1 \equiv 4 \pmod 8$, a contradiction.
> - So $|T|$ divides $4$. The four points listed are torsion and distinct, so they are all of $T$.
>
> Formalization notes: Mathlib has Dirichlet's theorem as `Nat.forall_exists_prime_gt_and_eq_mod`, which also gives primes larger than $2n$, avoiding the primes of bad reduction. Tau Ceti's `AlgebraicGeometry/EllipticCurve/Affine/Point/InfiniteOrder.lean` has lemmas in the same spirit, and Tau Ceti's computation of the torsion of $y^2 = x^3 - x + 1$ (`torsion_curveX3SubXAddOne_eq_bot`) shows how the pieces fit together.
>
> Lean status: Mathlib —. Tau Ceti —; for $n = 1$ it has the points of order two (`neg_eq_self_iff` in `CurveX3SubX.lean`), but not the torsion subgroup.

> [!milestone] Congruent numbers and the rank of E_n
> A positive integer $n$ is congruent if and only if $E_n(\mathbb{Q})$ has a point of infinite order. Since $E_n(\mathbb{Q})$ is finitely generated, this holds if and only if $E_n(\mathbb{Q})$ is infinite, if and only if its rank is positive.
>
> Sources: [@Koblitz1993, §I.9, Prop. 18]. [@HalbeisenHungerbuhler2018, Theorem 1] proves directly, without the torsion subgroup, that the points of $E_n(\mathbb{Q})$ with $y \neq 0$ have infinite order.
>
> Proof routes: by Right triangles and points of E_n, $n$ is congruent if and only if $E_n(\mathbb{Q})$ has a point with $y \neq 0$. By Torsion of E_n, the torsion points are exactly $O$ and the points with $y = 0$. So a point with $y \neq 0$ has infinite order, and a point of infinite order has $y \neq 0$.
>
> Formalization notes: Tau Ceti proves that the rational points of an elliptic curve over a number field form a finitely generated group (`fg_point_of_numberField`, `moduleFinite_point_of_numberField`), and `finrank_point_curve37a1_pos` shows how a positive rank is stated.
>
> Lean status: Mathlib —. Tau Ceti —.

> [!milestone] E_1 and E_2 have rank zero
> $E_1(\mathbb{Q}) = \{O, (0,0), (1,0), (-1,0)\}$ and $E_2(\mathbb{Q}) = \{O, (0,0), (2,0), (-2,0)\}$. In particular both have rank zero.
>
> Sources: [@Conrad2008, §4], which states $E_1(\mathbb{Q})$ after Remark 4.2.
>
> Proof routes: $1$ and $2$ are not congruent, by Fermat's right triangle theorem. So by Right triangles and points of E_n, $E_1(\mathbb{Q})$ and $E_2(\mathbb{Q})$ have no point with $y \neq 0$. So their only points are $O$ and the points with $y = 0$, which are $(0,0)$ and $(\pm 1, 0)$ for $E_1$, and $(0,0)$ and $(\pm 2, 0)$ for $E_2$. This needs neither the torsion subgroup nor the rank.
>
> Lean status: Mathlib —. Tau Ceti —.

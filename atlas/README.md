# Congruent numbers

A positive rational number is *congruent* if it is the area of a right
triangle whose sides are rational. The congruent number problem asks which
numbers are congruent. Its classical theory turns the question into one about
the rational points of the elliptic curves
$$E_n : y^2 = x^3 - n^2 x,$$
and this plan formalizes that theory, following Chapter I of Koblitz
[@Koblitz1993] and Conrad's expository note [@Conrad2008].

## Scope

In scope: the definition and first examples; the correspondence between right
triangles of area $n$ and points of $E_n$; the number of points of $E_n$ over
$\mathbb{F}_p$ for $p \equiv 3 \pmod 4$; the torsion of $E_n(\mathbb{Q})$; the
criterion that $n$ is congruent if and only if $E_n(\mathbb{Q})$ has positive
rank; and Fermat's theorem that $1$ is not congruent, together with the fact
that $2$ is not.

Out of scope: Tunnell's theorem and anything that depends on the conjecture of
Birch and Swinnerton-Dyer; modular forms of weight $3/2$; the general theory
of elliptic curves, which Mathlib and Tau Ceti provide.

## Milestones

- [Congruent numbers](congruent-numbers.md):
  - **Congruent numbers**
  - **Right triangles and points of E_n**, which depends on Congruent numbers
  - **Fermat's right triangle theorem**, which depends on Congruent numbers
- [Rational points](rational-points.md):
  - **Points of E_n over finite fields**
  - **Reduction is injective on torsion**
  - **Torsion of E_n**, which depends on Points of E_n over finite fields and
    Reduction is injective on torsion
  - **Congruent numbers and the rank of E_n**, which depends on Right
    triangles and points of E_n, and Torsion of E_n
  - **E_1 and E_2 have rank zero**, which depends on Right triangles and points
    of E_n, and Fermat's right triangle theorem

## The libraries

As of 17 November 2026, at Tau Ceti commit `0642eae` on `main` and the Mathlib
commit it pins, `048fffa`:

- **Mathlib** has Weierstrass curves and the group of points
  (`WeierstrassCurve.Affine.Point`), base change, finite fields and quadratic
  characters, Dirichlet's theorem on primes in arithmetic progressions,
  Pythagorean triples, and Fermat's theorem that $x^4 + y^4 = z^2$ has no
  solution in nonzero integers (`not_fermat_42`).
- **Tau Ceti** has the curve $y^2 = x^3 - x$ with its points of order two;
  point counts over finite fields; integral models and reduction of rational
  points modulo a prime of good reduction, with injectivity on torsion; the
  Hasse bound; and finite generation of the group of rational points of an
  elliptic curve over a number field.

None of the milestones here is in either library, apart from Reduction is
injective on torsion, which Tau Ceti has. Nothing in this plan waits on open
pull requests.

## Sources

Koblitz [@Koblitz1993, Ch. I] is the main source; §I.9 proves the results on
torsion and rank. The numbers of Propositions 17 and 18 in §I.9 were checked
against papers that cite them, not against the book; the number of the
proposition on point counts was not checked at all, so it is cited by section.
Conrad [@Conrad2008] gives the correspondence with points of $E_n$ and the
proof that $1$ is not congruent; citations follow the numbering of the online
version of his note, which differs from the published one. Silverman
[@Silverman2009, Prop. VII.3.1] covers reduction of torsion, and Halbeisen and
Hungerbühler [@HalbeisenHungerbuhler2018] give an elementary proof that the
points of $E_n(\mathbb{Q})$ with $y \neq 0$ have infinite order.

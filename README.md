# Congruent numbers: a formalization plan

A small formalization plan, in the shape of an atlas: the milestone results of
a piece of mathematics, where they are proved, and what a formalizer should
know. It covers the elementary theory of the congruent number problem: which
positive integers are areas of right triangles with rational sides, and how
that question becomes one about the elliptic curves $y^2 = x^3 - n^2 x$.

The formalization builds on [Tau Ceti](https://github.com/TauCetiProject/TauCeti)
at its current `main`, which already has the elliptic-curve machinery this
needs: point counts over finite fields, reduction of rational points modulo
primes and its injectivity on torsion, and finite generation of the group of
rational points.

This plan was written by an AI agent, Claude, for a first experiment with a
pipeline of agents that formalize a plan through GitHub issues and pull
requests ([fc-worker](https://github.com/FormalCommons/fc-worker)). It was
checked against its sources, but it has not been reviewed by experts.

| Path | Contents |
|---|---|
| [`atlas/README.md`](atlas/README.md) | The front page: scope, how the milestones depend on each other, and the state of the libraries |
| [`atlas/congruent-numbers.md`](atlas/congruent-numbers.md) | Congruent numbers, the curves $E_n$, and Fermat's theorem that $1$ is not congruent |
| [`atlas/rational-points.md`](atlas/rational-points.md) | Points over finite fields, torsion, and the rank of $E_n(\mathbb{Q})$ |
| [`atlas/references.bib`](atlas/references.bib) | The sources |

The pages are Markdown, with math between `$…$` and `$$…$$`. Each milestone
is a callout whose first line is its name, `> [!milestone] Name`; the callout
gives a precise statement, the sources, routes to a proof, and the milestone's
status in Mathlib and Tau Ceti. Citations such as `[@Koblitz1993, §I.9]` refer
to entries of `atlas/references.bib`.

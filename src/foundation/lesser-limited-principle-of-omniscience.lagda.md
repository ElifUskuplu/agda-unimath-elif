# The lesser limited principle of omniscience

```agda
module foundation.lesser-limited-principle-of-omniscience where
```

<details><summary>Imports</summary>

```agda
open import elementary-number-theory.natural-numbers
open import elementary-number-theory.parity-natural-numbers

open import foundation.disjunction

open import foundation-core.fibers-of-maps
open import foundation-core.propositions
open import foundation-core.sets
open import foundation-core.universe-levels

open import univalent-combinatorics.standard-finite-types
```

</details>

## Idea

The lesser limited principle of omniscience asserts that for any sequence
`f : ℕ → Fin 2` containing at most one `1`, either `f n ＝ 0` for all even `n`
or `f n ＝ 0` for all odd `n`.

## Definition

```agda
LLPO : UU lzero
LLPO =
  (f : ℕ → Fin 2) → is-prop (fib f (one-Fin 1)) →
  type-disj-Prop
    ( Π-Prop ℕ
      ( λ n →
        function-Prop (is-even-ℕ n) (Id-Prop (Fin-Set 2) (f n) (zero-Fin 1))))
    ( Π-Prop ℕ
      ( λ n →
        function-Prop (is-odd-ℕ n) (Id-Prop (Fin-Set 2) (f n) (zero-Fin 1))))
```

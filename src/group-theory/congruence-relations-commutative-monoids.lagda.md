# Congruence relations on commutative monoids

```agda
module group-theory.congruence-relations-commutative-monoids where
```

<details><summary>Imports</summary>

```agda
open import foundation.binary-relations
open import foundation.contractible-types
open import foundation.dependent-pair-types
open import foundation.equivalence-relations
open import foundation.equivalences
open import foundation.identity-types
open import foundation.propositions
open import foundation.universe-levels

open import group-theory.commutative-monoids
open import group-theory.congruence-relations-monoids
```

</details>

## Idea

A congruence relation on a commutative monoid `M` is a congruence relation on
the underlying monoid of `M`.

## Definition

```agda
is-congruence-commutative-monoid-Prop :
  {l1 l2 : Level} (M : Commutative-Monoid l1) →
  Eq-Rel l2 (type-Commutative-Monoid M) → Prop (l1 ⊔ l2)
is-congruence-commutative-monoid-Prop M =
  is-congruence-monoid-Prop (monoid-Commutative-Monoid M)

is-congruence-Commutative-Monoid :
  {l1 l2 : Level} (M : Commutative-Monoid l1) →
  Eq-Rel l2 (type-Commutative-Monoid M) → UU (l1 ⊔ l2)
is-congruence-Commutative-Monoid M =
  is-congruence-Monoid (monoid-Commutative-Monoid M)

is-prop-is-congruence-Commutative-Monoid :
  {l1 l2 : Level} (M : Commutative-Monoid l1)
  (R : Eq-Rel l2 (type-Commutative-Monoid M)) →
  is-prop (is-congruence-Commutative-Monoid M R)
is-prop-is-congruence-Commutative-Monoid M =
  is-prop-is-congruence-Monoid (monoid-Commutative-Monoid M)

congruence-Commutative-Monoid :
  {l : Level} (l2 : Level) (M : Commutative-Monoid l) → UU (l ⊔ lsuc l2)
congruence-Commutative-Monoid l2 M =
  congruence-Monoid l2 (monoid-Commutative-Monoid M)

module _
  {l1 l2 : Level} (M : Commutative-Monoid l1)
  (R : congruence-Commutative-Monoid l2 M)
  where

  eq-rel-congruence-Commutative-Monoid : Eq-Rel l2 (type-Commutative-Monoid M)
  eq-rel-congruence-Commutative-Monoid =
    eq-rel-congruence-Monoid (monoid-Commutative-Monoid M) R

  prop-congruence-Commutative-Monoid : Rel-Prop l2 (type-Commutative-Monoid M)
  prop-congruence-Commutative-Monoid =
    prop-congruence-Monoid (monoid-Commutative-Monoid M) R

  sim-congruence-Commutative-Monoid : (x y : type-Commutative-Monoid M) → UU l2
  sim-congruence-Commutative-Monoid =
    sim-congruence-Monoid (monoid-Commutative-Monoid M) R

  is-prop-sim-congruence-Commutative-Monoid :
    (x y : type-Commutative-Monoid M) →
    is-prop (sim-congruence-Commutative-Monoid x y)
  is-prop-sim-congruence-Commutative-Monoid =
    is-prop-sim-congruence-Monoid (monoid-Commutative-Monoid M) R

  concatenate-sim-eq-congruence-Commutative-Monoid :
    {x y z : type-Commutative-Monoid M} →
    sim-congruence-Commutative-Monoid x y → y ＝ z →
    sim-congruence-Commutative-Monoid x z
  concatenate-sim-eq-congruence-Commutative-Monoid =
    concatenate-sim-eq-congruence-Monoid (monoid-Commutative-Monoid M) R

  concatenate-eq-sim-congruence-Commutative-Monoid :
    {x y z : type-Commutative-Monoid M} → x ＝ y →
    sim-congruence-Commutative-Monoid y z →
    sim-congruence-Commutative-Monoid x z
  concatenate-eq-sim-congruence-Commutative-Monoid =
    concatenate-eq-sim-congruence-Monoid (monoid-Commutative-Monoid M) R

  concatenate-eq-sim-eq-congruence-Commutative-Monoid :
    {x y z w : type-Commutative-Monoid M} → x ＝ y →
    sim-congruence-Commutative-Monoid y z →
    z ＝ w → sim-congruence-Commutative-Monoid x w
  concatenate-eq-sim-eq-congruence-Commutative-Monoid =
    concatenate-eq-sim-eq-congruence-Monoid (monoid-Commutative-Monoid M) R

  refl-congruence-Commutative-Monoid :
    is-reflexive-Rel-Prop prop-congruence-Commutative-Monoid
  refl-congruence-Commutative-Monoid =
    refl-congruence-Monoid (monoid-Commutative-Monoid M) R

  symm-congruence-Commutative-Monoid :
    is-symmetric-Rel-Prop prop-congruence-Commutative-Monoid
  symm-congruence-Commutative-Monoid =
    symm-congruence-Monoid (monoid-Commutative-Monoid M) R

  equiv-symm-congruence-Commutative-Monoid :
    (x y : type-Commutative-Monoid M) →
    sim-congruence-Commutative-Monoid x y ≃
    sim-congruence-Commutative-Monoid y x
  equiv-symm-congruence-Commutative-Monoid =
    equiv-symm-congruence-Monoid (monoid-Commutative-Monoid M) R

  trans-congruence-Commutative-Monoid :
    is-transitive-Rel-Prop prop-congruence-Commutative-Monoid
  trans-congruence-Commutative-Monoid =
    trans-congruence-Monoid (monoid-Commutative-Monoid M) R

  mul-congruence-Commutative-Monoid :
    is-congruence-Commutative-Monoid M eq-rel-congruence-Commutative-Monoid
  mul-congruence-Commutative-Monoid =
    mul-congruence-Monoid (monoid-Commutative-Monoid M) R
```

## Properties

### Extensionality of the type of congruence relations on a monoid

```agda
relate-same-elements-congruence-Commutative-Monoid :
  {l1 l2 l3 : Level} (M : Commutative-Monoid l1)
  (R : congruence-Commutative-Monoid l2 M)
  (S : congruence-Commutative-Monoid l3 M) → UU (l1 ⊔ l2 ⊔ l3)
relate-same-elements-congruence-Commutative-Monoid M =
  relate-same-elements-congruence-Monoid (monoid-Commutative-Monoid M)

refl-relate-same-elements-congruence-Commutative-Monoid :
  {l1 l2 : Level} (M : Commutative-Monoid l1)
  (R : congruence-Commutative-Monoid l2 M) →
  relate-same-elements-congruence-Commutative-Monoid M R R
refl-relate-same-elements-congruence-Commutative-Monoid M =
  refl-relate-same-elements-congruence-Monoid (monoid-Commutative-Monoid M)

is-contr-total-relate-same-elements-congruence-Commutative-Monoid :
  {l1 l2 : Level} (M : Commutative-Monoid l1)
  (R : congruence-Commutative-Monoid l2 M) →
  is-contr
    ( Σ ( congruence-Commutative-Monoid l2 M)
        ( relate-same-elements-congruence-Commutative-Monoid M R))
is-contr-total-relate-same-elements-congruence-Commutative-Monoid M =
  is-contr-total-relate-same-elements-congruence-Monoid
    ( monoid-Commutative-Monoid M)

relate-same-elements-eq-congruence-Commutative-Monoid :
  {l1 l2 : Level} (M : Commutative-Monoid l1)
  (R S : congruence-Commutative-Monoid l2 M) →
  R ＝ S → relate-same-elements-congruence-Commutative-Monoid M R S
relate-same-elements-eq-congruence-Commutative-Monoid M =
  relate-same-elements-eq-congruence-Monoid (monoid-Commutative-Monoid M)

is-equiv-relate-same-elements-eq-congruence-Commutative-Monoid :
  {l1 l2 : Level} (M : Commutative-Monoid l1)
  (R S : congruence-Commutative-Monoid l2 M) →
  is-equiv (relate-same-elements-eq-congruence-Commutative-Monoid M R S)
is-equiv-relate-same-elements-eq-congruence-Commutative-Monoid M =
  is-equiv-relate-same-elements-eq-congruence-Monoid
    ( monoid-Commutative-Monoid M)

extensionality-congruence-Commutative-Monoid :
  {l1 l2 : Level} (M : Commutative-Monoid l1)
  (R S : congruence-Commutative-Monoid l2 M) →
  (R ＝ S) ≃ relate-same-elements-congruence-Commutative-Monoid M R S
extensionality-congruence-Commutative-Monoid M =
  extensionality-congruence-Monoid (monoid-Commutative-Monoid M)

eq-relate-same-elements-congruence-Commutative-Monoid :
  {l1 l2 : Level} (M : Commutative-Monoid l1)
  (R S : congruence-Commutative-Monoid l2 M) →
  relate-same-elements-congruence-Commutative-Monoid M R S → R ＝ S
eq-relate-same-elements-congruence-Commutative-Monoid M =
  eq-relate-same-elements-congruence-Monoid (monoid-Commutative-Monoid M)
```

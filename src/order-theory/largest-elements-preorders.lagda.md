# Largest elements in preorders

```agda
module order-theory.largest-elements-preorders where
```

<details><summary>Imports</summary>

```agda
open import foundation.dependent-pair-types
open import foundation.propositions
open import foundation.universe-levels

open import order-theory.preorders
```

</details>

## Idea

A **largest element** in a preorder `P` is an element `t` such that `x ≤ t`
holds for every `x : P`.

## Definition

```agda
module _
  {l1 l2 : Level} (X : Preorder l1 l2)
  where

  is-largest-element-Preorder-Prop : type-Preorder X → Prop (l1 ⊔ l2)
  is-largest-element-Preorder-Prop x =
    Π-Prop (type-Preorder X) (λ y → leq-Preorder-Prop X y x)

  is-largest-element-Preorder : type-Preorder X → UU (l1 ⊔ l2)
  is-largest-element-Preorder x = type-Prop (is-largest-element-Preorder-Prop x)

  is-prop-is-largest-element-Preorder :
    (x : type-Preorder X) → is-prop (is-largest-element-Preorder x)
  is-prop-is-largest-element-Preorder x =
    is-prop-type-Prop (is-largest-element-Preorder-Prop x)

  largest-element-Preorder : UU (l1 ⊔ l2)
  largest-element-Preorder = Σ (type-Preorder X) is-largest-element-Preorder
```

# Arrays

```agda
module lists.arrays where
```

<details><summary>Imports</summary>

```agda
open import elementary-number-theory.natural-numbers

open import foundation.contractible-types
open import foundation.coproduct-types
open import foundation.dependent-pair-types
open import foundation.empty-types
open import foundation.equality-dependent-pair-types
open import foundation.equivalences
open import foundation.function-extensionality
open import foundation.functions
open import foundation.functoriality-dependent-pair-types
open import foundation.homotopies
open import foundation.identity-types
open import foundation.propositions
open import foundation.unit-type
open import foundation.universal-property-coproduct-types
open import foundation.universe-levels

open import linear-algebra.vectors

open import lists.lists

open import univalent-combinatorics.involution-standard-finite-types
open import univalent-combinatorics.standard-finite-types
```

</details>

## Idea

An array is a pair of a natural number `n`, and a function from `Fin n` to `A`.
We show that arrays and lists are equivalent.

```agda
array : {l : Level} → UU l → UU l
array A = Σ ℕ (λ n → functional-vec A n)

module _
  {l : Level} {A : UU l}
  where

  length-array : array A → ℕ
  length-array = pr1

  functional-vec-array : (t : array A) → Fin (length-array t) → A
  functional-vec-array = pr2

  empty-array : array A
  pr1 (empty-array) = zero-ℕ
  pr2 (empty-array) ()

  is-empty-array-Prop : array A → Prop lzero
  is-empty-array-Prop (zero-ℕ , t) = unit-Prop
  is-empty-array-Prop (succ-ℕ n , t) = empty-Prop

  is-empty-array : array A → UU lzero
  is-empty-array = type-Prop ∘ is-empty-array-Prop

  is-nonempty-array-Prop : array A → Prop lzero
  is-nonempty-array-Prop (zero-ℕ , t) = empty-Prop
  is-nonempty-array-Prop (succ-ℕ n , t) = unit-Prop

  is-nonempty-array : array A → UU lzero
  is-nonempty-array = type-Prop ∘ is-nonempty-array-Prop

  head-array : (t : array A) → is-nonempty-array t → A
  head-array (succ-ℕ n , f) _ = f (inr star)

  tail-array : (t : array A) → is-nonempty-array t → array A
  tail-array (succ-ℕ n , f) _ = n , f ∘ inl

  cons-array : A → array A → array A
  cons-array a t =
    ( succ-ℕ (length-array t) ,
      ind-coprod (λ _ → A) (functional-vec-array t) λ _ → a)

  revert-array : array A → array A
  revert-array (n , t) = (n , λ k → t (opposite-Fin n k))
```

## Properties

### The types of lists and arrays are equivalent

```agda
module _
  {l : Level} {A : UU l}
  where

  list-vec : (n : ℕ) → (vec A n) → list A
  list-vec zero-ℕ _ = nil
  list-vec (succ-ℕ n) (x ∷ l) = cons x (list-vec n l)

  vec-list : (l : list A) → vec A (length-list l)
  vec-list nil = empty-vec
  vec-list (cons x l) = x ∷ vec-list l

  issec-vec-list : (λ l → list-vec (length-list l) (vec-list l)) ~ id
  issec-vec-list nil = refl
  issec-vec-list (cons x l) = ap (cons x) (issec-vec-list l)

  isretr-vec-list :
    ( λ (x : Σ ℕ (λ n → vec A n)) →
      ( length-list (list-vec (pr1 x) (pr2 x)) ,
        vec-list (list-vec (pr1 x) (pr2 x)))) ~
    id
  isretr-vec-list (zero-ℕ , empty-vec) = refl
  isretr-vec-list (succ-ℕ n , (x ∷ v)) =
    ap
      ( λ v → succ-ℕ (pr1 v) , (x ∷ (pr2 v)))
      ( isretr-vec-list (n , v))

  list-array : array A → list A
  list-array (n , t) = list-vec n (listed-vec-functional-vec n t)

  array-list : list A → array A
  array-list l =
    ( length-list l , functional-vec-vec (length-list l) (vec-list l))

  issec-array-list : (list-array ∘ array-list) ~ id
  issec-array-list nil = refl
  issec-array-list (cons x l) = ap (cons x) (issec-array-list l)

  isretr-array-list : (array-list ∘ list-array) ~ id
  isretr-array-list (n , t) =
    ap
      ( λ (n , v) → (n , functional-vec-vec n v))
      ( isretr-vec-list (n , listed-vec-functional-vec n t)) ∙
    eq-pair-Σ refl (isretr-functional-vec-vec n t)

  equiv-list-array : array A ≃ list A
  pr1 equiv-list-array = list-array
  pr2 equiv-list-array =
    is-equiv-has-inverse
      array-list
      issec-array-list
      isretr-array-list

  equiv-array-list : list A ≃ array A
  pr1 equiv-array-list = array-list
  pr2 equiv-array-list =
    is-equiv-has-inverse
      list-array
      isretr-array-list
      issec-array-list
```

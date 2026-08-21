# Design

## Goal

Introduce the type parameter: writing `{T}`, using `T` inside the class,
supplying a type at the point of use, and constraining the parameter to get
more than a bare type allows.

## Learning objectives

- Declare a class with a type parameter.
- Use the parameter as a type for an attribute, an argument and a return
  value.
- Instantiate at two different types and see that they are different types.
- Constrain a parameter with `<` in order to call something on it.

## Out of scope

- Several parameters, in the concept page only. `FMAP{K,T}` has been in use
  since `field-guide`, so the idea is not new; a second one here would add
  bookkeeping and no insight.
- What the compiler does about code size when a class is used at many types.

## Note on the constraint

Task 5 exists to make the constraint necessary rather than decorative. A
student who writes `{T < $STR}` from the start will find tasks 1 to 4 work
either way, and only discover why on the last one — which is the intended
order of events.

## Concepts

- `generic-classes`

## Prerequisites

- `code-inclusion`

## Analyzer

None yet. Worth catching: task 4 assigning before keeping the old value,
which the tests catch, and a `LOST_BOX` written for `STR` alone with `T`
never used, which they also catch since the tests instantiate at `INT`.

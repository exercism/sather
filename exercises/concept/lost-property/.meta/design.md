# Design

## Goal

Introduce the type parameter: writing `{T}`, using `T` inside the class,
and supplying a type at the point of use.

## Learning objectives

- Declare a class with a type parameter.
- State what each routine leaves true with `post`.
- Use the parameter as a type for an attribute, an argument and a return
  value.
- Instantiate at two different types and see that they are different types.
- Call a routine on a `T` that every type the class is used with provides.

## Out of scope

- Several parameters, in the concept page only. `FMAP{K,T}` has been in use
  since `field-guide`, so the idea is not new; a second one here would add
  bookkeeping and no insight.
- What the compiler does about code size when a class is used at many types.
- Constraints (`{T < $STR}`), in the introduction only. The compiler checks
  each instantiation separately and does not check the body against the
  constraint, so no test can tell whether a student wrote one.

## Concepts

- `generic-classes`

## Prerequisites

- `code-inclusion`
- `contracts`
- `maps-and-sets`

## Analyzer

None yet. Worth catching: task 4 assigning before keeping the old value,
which the tests catch, and a `LOST_BOX` written for `STR` alone with `T`
never used, which they also catch since the tests instantiate at `INT`.

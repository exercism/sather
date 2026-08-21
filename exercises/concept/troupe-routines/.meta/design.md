# Design

## Goal

Introduce `include`, renaming and leaving out — and the separation of code
reuse from subtyping, which is the thing about Sather most likely to be
misread by anyone arriving from another language.

## Learning objectives

- Include another class's code.
- Rename an included routine.
- Leave one out with `-> ;` in order to replace it.
- Say why `include` and `<` are different decisions.

## Out of scope

- `private include`, in the concept page only.
- Including more than one class, and the clashes that follow. It is the
  natural next question and needs a fourth class doing real work to be worth
  posing.
- Combining `include` with `< $ACT`, which the concept page shows. Doing it
  here would put two ideas in one exercise, and the abstract class was two
  exercises ago.

## Concepts

- `code-inclusion`

## Prerequisites

- `abstract-classes`

## Analyzer

None yet. Worth catching: `FINALE::describe` recomputing `warm_up_counts * 2`
instead of calling `counts`, which passes.

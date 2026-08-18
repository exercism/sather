# Design

## Goal

Introduce the shape of a Sather program: a class, routines that return a
value, string literals, comments, and calling one routine from another.

## Learning objectives

- Recognise `class NAME is ... end;` as the container everything lives in.
- Write a routine that declares a return type and returns a value.
- Write a string literal.
- Call a routine defined in the same class, without a class prefix and
  without brackets.

## Out of scope

- Arguments. Every routine here takes none, so the student meets one new
  idea at a time; arguments arrive in `programme-notes`.
- String concatenation. The fourth task deliberately reuses a whole line
  rather than building one, so `+` is not needed until `strings`.
- `#OUT` and printing. The tests read return values, so nothing here needs
  output.

## Concepts

- `basics`

## Prerequisites

None. This is the root of the tree.

## Analyzer

None yet. A future analyzer could notice the fourth task repeating the
closing line as a literal instead of calling `closing_line`, which is the one
mistake the exercise is shaped to provoke.

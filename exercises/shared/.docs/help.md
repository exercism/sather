# Help

If your code doesn't compile, `sacomp` starts each error with the file, line and column, such as `two_fer.sa:3:20:`.
Fix the errors from the top: a later one can be caused by an earlier one.

If a run stops with a `Runtime error` such as `Violation of precondition`, a `pre`, `post`, `assert` or `invariant` check failed.
The message names the routine, and the file and line, where that happened.

To look up the language and its library, use:

- [The GNU Sather tutorial][tutorial]
- [The Sather specification][specification]
- [Built-in classes][builtin], for `INT`, `STR`, `ARRAY` and friends

To ask a question, post in the [Exercism forum][forum].

[tutorial]: https://www.gnu.org/software/sather/docs-1.2/tutorial/sather-tutorial.html
[specification]: https://www.gnu.org/software/sather/docs-1.2/specification/sather-specification.html
[builtin]: https://www.gnu.org/software/sather/docs-1.2/specification/builtinclasses.html
[forum]: https://forum.exercism.org/

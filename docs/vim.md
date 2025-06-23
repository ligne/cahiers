# Vim

## Patterns

### Nongreedy quantifiers

Quantifiers are greedy by default, as is correct.

Vim doesn't support the usual `*?`/`+?` syntax, so to get nongreedy/lazy matching you have to use a variant of the general quantifiers.
This involves appending a dash to the opening brace: instead of `\{n,m}`, the greedy form, use `\{-n,m}` to match lazily.

As usual, `n` will default to 0 and `m` to unbounded; this means `\{-}` is equivalent to `*?`, and `\{-1,}` to `+?`.

# Spelling

## pre-commit

The following tools play well with [`pre-commit`](pre-commit.md):

[`typos`](https://github.com/crate-ci/typos)

- Aimed at finding common misspellings in code rather than acting as a general-purpose spellchecker.
- Very fast.

Relatively few [configuration options](https://github.com/crate-ci/typos/blob/master/docs/reference.md).
It can use its own `.typos.toml`, but it can also be included in `pyproject.toml`.

[`cspell`](https://github.com/streetsidesoftware/cspell-cli)

- Fully-fledged spellchecker, using a much more comprehensive dictionary.
- Significantly slower.

Configure it using `.cspell.yaml`.
A [basic guide](https://cspell.org/docs/getting-started), including how to seed a local dictionary quickly, and a [detailed reference](https://cspell.org/docs/Configuration).
In addition to specifying additional project-local words, these custom dictionaries are [very flexible](https://cspell.org/docs/dictionaries/custom-dictionaries).

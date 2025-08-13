# Markdown

The markup language this is written in.

Cheat-sheets [here](https://www.markdownguide.org/basic-syntax/) and [here](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax).

## pre-commit

### Formatter

[`mdformat`](https://mdformat.readthedocs.io/en/stable/) is like `black` for Markdown files.
Probably want to use it in conjunction with `mdformat-mkdocs`.

`.pre-commit-config.yaml` snippet [here](https://github.com/KyleKing/mdformat-mkdocs?tab=readme-ov-file#pre-commit).

There are a [variety of plugins](https://mdformat.readthedocs.io/en/stable/users/plugins.html).
For the most part these either format the contents of code blocks, or add support for Markdown extensions.

### Linter

I didn't have any luck getting the Ruby `markdownlint` to work with `pre-commit`, so instead I'm using [`markdownlint-cli2`](https://github.com/DavidAnson/markdownlint-cli2#pre-commit).
This is a fairly thin wrapper around the [markdownlint](https://github.com/DavidAnson/markdownlint/) library.

The config can go in a whole plethora of files, but I prefer `.markdownlint.yaml`.
This configures `markdownlint` itself, and is therefore tool-independent.
The corollary to this is that it doesn't support tool-specific configuration, but converting just involves sticking everything in a `config:` mapping block in `.markdownlint-cli2.yaml`.

There is an index of the rules [here](https://github.com/DavidAnson/markdownlint/blob/main/doc/Rules.md).
As with other linters, they can be overridden using inline comments, in this case in HTML form; [syntax](https://github.com/DavidAnson/markdownlint/blob/main/README.md#configuration).

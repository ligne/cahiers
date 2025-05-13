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

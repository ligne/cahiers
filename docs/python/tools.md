# Tools

## isort

Sorts and formats import statements.

### Configuration

There are [various choices of file](https://pycqa.github.io/isort/docs/configuration/config_files.html) but the most convenient is to use the local `pyproject.toml`.

It's useful to have a default global config in a `.isort.cfg` file, that sets `profile = black` (to play nicely) and `float_to_top = true` (for convenience).
But it doesn't specifically look for it in `$HOME`: it just walks up the tree until it finds a suitable file.
This means that it won't be used if you're not under your home directory (such as on WSL).
It also stops when it finds a `.git/` or `.hg/` directory, so it won't work in a repository either.

## pydeps

Visualise module dependency trees using Graphviz.
Although it's primarily intended to be used as a command-line tool, it does provide an API and readable intermediate format.

[Repo](https://github.com/thebjorn/pydeps) | [Docs](https://pydeps.readthedocs.io/en/latest/)

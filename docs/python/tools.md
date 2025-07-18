# Tools

## isort

Sorts and formats import statements.

### Configuration

There are [various choices of file](https://pycqa.github.io/isort/docs/configuration/config_files.html) but the most convenient is to use the local `pyproject.toml`.

It's useful to have a default global config in a `.isort.cfg` file, that sets `profile = black` (to play nicely) and `float_to_top = true` (for convenience).
But it doesn't specifically look for it in `$HOME`: it just walks up the tree until it finds a suitable file.
This means that it won't be used if you're not under your home directory (such as on WSL).
It also stops when it finds a `.git/` or `.hg/` directory, so it won't work in a repository either.

### Modifying imports

It can also add and remove imports, which is handy for bulk operations.
Since it knows about the various ways an import statement can be organised it can do a much more precise job than `sed` realistically could.

They can be chained in the same operation, eg.: `isort --add pathlib.Path --add sys --rm "__future__.generator_stop" $(git ls-files '*.py')`.

## pydeps

Visualise module dependency trees using Graphviz.
Although it's primarily intended to be used as a command-line tool, it does provide an API and readable intermediate format.

[Repo](https://github.com/thebjorn/pydeps) | [Docs](https://pydeps.readthedocs.io/en/latest/)

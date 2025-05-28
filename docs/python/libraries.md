# Libraries

## argparse

[Docs](https://docs.python.org/3/library/argparse.html)

### Complex validation

Sometimes there's no straightforward way to express the full validation rules within the confines of `.add_argument()`.
In particular there's no guarantee that the arguments will be provided in any particular order, so Actions have to be able to work independently of each other.

In such cases it can be better to defer validation until after the parser has run.
If there are problems with the contents of the `Namespace` object, call `parser.error("...")` to exit with a tidy and consistent usage message [(source)](https://stackoverflow.com/questions/49000217/cross-argument-validation-in-argparse).

(But it might be easier [with Click](https://stackoverflow.com/a/44349292)).

## platformdirs

Determine platform-specific directories for config files and user data.
A fork of the sadly-unmaintained `appdirs`.

[Repo](https://github.com/tox-dev/platformdirs/tree/main) | [Docs](https://platformdirs.readthedocs.io/)

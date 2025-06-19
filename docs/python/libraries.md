# Libraries

## argparse

[Docs](https://docs.python.org/3/library/argparse.html)

### Complex validation

Sometimes there's no straightforward way to express the full validation rules within the confines of `.add_argument()`.
In particular there's no guarantee that the arguments will be provided in any particular order, so Actions have to be able to work independently of each other.

In such cases it can be better to defer validation until after the parser has run.
If there are problems with the contents of the `Namespace` object, call `parser.error("...")` to exit with a tidy and consistent usage message [(source)](https://stackoverflow.com/questions/49000217/cross-argument-validation-in-argparse).

(But it might be easier [with Click](https://stackoverflow.com/a/44349292)).

## lz4

Bindings for Yann Collet's [LZ4](https://lz4.github.io/lz4/) compression library.

The `frame` interface deals with both the compressed data and its container, and `lz4.frame.open()` is probably what you want to use.
The `block` interface deals with plain blocks of compressed data.

[Docs](https://python-lz4.readthedocs.io/en/stable/index.html) | [Repo](https://github.com/python-lz4/python-lz4)

### lz4json

This is a variant of LZ4 used in various Mozilla projects.
It pre-dates the full standardisation of the Frame format (hence needing special treatment), but is otherwise compliant.

It comprises a fixed eight-byte header, followed by a single Block.
Therefore to decode an `lz4json` file:

```python
with open(filename, "rb") as fh:
    if (magic := fh.read(8)) != b"mozLz40\0":
        print(f"{filename}: Unrecognised magic number '{magic}'")

    payload = lz4.block.decompress(fh.read())
```

This is basically what [`lz4jsoncat` does](https://github.com/andikleen/lz4json/blob/master/lz4jsoncat.c#L66-L72), except the bindings work out the sizes for you.

(Note that there is [a plan to (eventually) replace it with a more standard compression format](https://bugzilla.mozilla.org/show_bug.cgi?id=1209390).)

## platformdirs

Determine platform-specific directories for config files and user data.
A fork of the sadly-unmaintained `appdirs`.

[Repo](https://github.com/tox-dev/platformdirs/tree/main) | [Docs](https://platformdirs.readthedocs.io/)

## pycountry

Wraps Debian's [`iso-codes` data](https://salsa.debian.org/iso-codes-team/iso-codes) databases for ISO country, language, and script codes, along with their translations.

[Repo and docs](https://github.com/pycountry/pycountry)

## stamina

Decorator-based library for handling transient errors.
Detects exceptions and retries with exponential backoff, capping the number of retries and total time.
Basically just applies reasonable defaults to [tenacity](https://github.com/jd/tenacity).

[Repo](https://github.com/hynek/stamina) | [Docs](https://stamina.hynek.me/en/stable/)

## yarl

Parsing and modifying URLs with an immutable, `pathlib`-inspired API.
It supports query string fields with multiple values, and automatically handles IDNA- and percent-encoding.

Each part of the URL can be accessed individually, with variants for the encoded value (`raw_` prefix) and modifying/unsetting (`with_` prefix).
Additionally, it overloads the `/` operator for concatenating paths and `%` for applying a dict of parameters.

[Docs](https://yarl.aio-libs.org/en/latest/) | [Repo](https://github.com/aio-libs/yarl)

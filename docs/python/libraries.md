# Libraries

[Top PyPI packages](https://hugovk.github.io/top-pypi-packages/).

## argparse

[Docs](https://docs.python.org/3/library/argparse.html)

### Complex validation

Sometimes there's no straightforward way to express the full validation rules within the confines of `.add_argument()`.
In particular there's no guarantee that the arguments will be provided in any particular order, so Actions have to be able to work independently of each other.

In such cases it can be better to defer validation until after the parser has run.
If there are problems with the contents of the `Namespace` object, call `parser.error("...")` to exit with a tidy and consistent usage message [(source)](https://stackoverflow.com/questions/49000217/cross-argument-validation-in-argparse).

(But it might be easier [with Click](https://stackoverflow.com/a/44349292)).

## dbxs

Create a data-access layer by attaching raw SQL queries to functions at import-time.
A bit like Asterisk's `func_odbc.conf`?

It binds the function parameters to the placeholders, and automatically inflates the result(s) to (an iterator of) dataclasses.
It can help prevent SQLI and improve type-safety.

It's not stable yet, and in particular it only supports async database interfaces.
(Though *contra* the README, it does support `asyncio` as well as Twisted.)
But it could be useful as a very lightweight database layer when a full-blown ORM would be overkill.

[Docs](https://dbxs.readthedocs.io/en/latest/) | [Repo](https://github.com/glyph/dbxs)

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

## moto

Mocks for AWS services.

[Docs](https://docs.getmoto.org/en/latest/) | [Repo](https://github.com/getmoto/moto)

## msgspec

Fast serialisation and validation.
Supports JSON, MessagePack, YAML, and TOML.

[Docs](https://jcristharif.com/msgspec/) | [Repo](https://github.com/jcrist/msgspec/)

## pint

Associate quantities with physical units.
These propagate through mathematical operations and can be converted.

[Docs](https://pint.readthedocs.io/en/stable/) | [Repo](https://github.com/hgrecco/pint)

## platformdirs

Determine platform-specific directories for config files and user data.
A fork of the sadly-unmaintained `appdirs`.

[Repo](https://github.com/tox-dev/platformdirs/tree/main) | [Docs](https://platformdirs.readthedocs.io/)

## pycountry

Wraps Debian's [`iso-codes` data](https://salsa.debian.org/iso-codes-team/iso-codes) databases for ISO country, language, and script codes, along with their translations.

[Repo and docs](https://github.com/pycountry/pycountry)

## srt

Parsing and modifying SRT subtitles files, including time-shifting and combining multiple files into one.
It also provides [a command-line tool](https://github.com/cdown/srt/tree/develop/srt_tools).

An alternative is `pysrt`.

[Docs](https://srt.readthedocs.io/en/latest/quickstart.html) | [Repo](https://github.com/cdown/srt)

## stamina

Decorator-based library for handling transient errors.
Detects exceptions and retries with exponential backoff, capping the number of retries and total time.
Basically just applies reasonable defaults to [tenacity](https://github.com/jd/tenacity).

[Repo](https://github.com/hynek/stamina) | [Docs](https://stamina.hynek.me/en/stable/)

## svg.py

Simple, type-safe library for generating SVG files.
It can also be [used online](https://svg.orsinium.dev/).

[Docs and repo](https://github.com/orsinium-labs/svg.py)

## uncertainties

Calculate with automatic error propagation.

[Docs](https://pythonhosted.org/uncertainties/) | [Repo](https://github.com/lmfit/uncertainties)

## yarl

Parsing and modifying URLs with an immutable, `pathlib`-inspired API.
It supports query string fields with multiple values, and automatically handles IDNA- and percent-encoding.

Each part of the URL can be accessed individually, with variants for the encoded value (`raw_` prefix) and modifying/unsetting (`with_` prefix).
Additionally, it overloads the `/` operator for concatenating paths and `%` for applying a dict of parameters.

[Docs](https://yarl.aio-libs.org/en/latest/) | [Repo](https://github.com/aio-libs/yarl)

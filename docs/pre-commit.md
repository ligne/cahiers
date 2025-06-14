# pre-commit

[pre-commit](https://pre-commit.com/) is a tool for managing git hooks.
It runs various checks automatically on every commit, preventing syntax or formatting errors from being introduced.

## Initialising

```sh
uv tool install pre-commit  # installs it globally
pre-commit sample-config > .pre-commit-config.yaml
pre-commit install
```

## Configuring

Configuration goes in `.pre-commit-config.yaml`.
Validate it with `pre-commit validate-config .pre-commit-config.yaml`.
Documentation is [here](https://pre-commit.com/#plugins).

### Some useful hooks

- [Markdown](markdown.md#pre-commit)
- [Spell-checking](spelling.md) code and prose
- Many more [here](https://pre-commit.com/hooks.html)

### Custom hooks

It's also possible to [write your own](https://stefaniemolin.com/articles/devx/pre-commit/hook-creation-guide/).

Most of the time, [repository-local hooks](https://pre-commit.com/#repository-local-hooks) should be sufficient.
These are configured in `.pre-commit-config.yaml` using the settings [here](https://pre-commit.com/#new-hooks).

- The [`fail`](https://pre-commit.com/#fail) "language" will raise an error if it finds any matching files.
    This can be used to enforce a file naming scheme.
- Use [`pygrep`](https://pre-commit.com/#pygrep) to check file contents using regexes.
    There are some pre-canned rules [here](https://github.com/pre-commit/pygrep-hooks).
- [`script`](https://pre-commit.com/#script) and [`system`](https://pre-commit.com/#system) run local and system-level commands respectively.
    The former might be useful to wrap a custom lint command, via a script in the repository.
    The latter could be used to invoke a tool that might reasonably be assumed to exist in the dev environment.
    Either way, the command is specified with the `entry` key, including any arguments required.

## Operating

It runs automatically before every commit, on the files being committed.
If any of the hooks fail, the commit will be aborted.

Many tools can automatically fix errors they find.
For this reason it works best if the changes are added as a separate step before commit, as these changes can be reviewed with `git diff`.

You can also run it manually with `pre-commit run`.
By default this only operates on staged files; check specific files with `--files`, or select them all with `--all-files`.

Even when invoked manually it will refuse to run while there are uncommitted changes to the configuration file.
The `--files` or `--all-files` options [override this](https://github.com/pre-commit/pre-commit/issues/848#issuecomment-429991583).

Occasionally run `pre-commit autoupdate` to keep the hooks up-to-date.

### Overriding

It's still possible to force a commit that would normally be rejected.
Either `SKIP=hook1,hook2 git commit` to ignore specific hooks, or `git commit --no-verify` to ignore the whole lot.

## Troubleshooting

Solutions to [some common problems](https://stefaniemolin.com/articles/devx/pre-commit/troubleshooting-guide/).

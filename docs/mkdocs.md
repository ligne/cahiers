# MkDocs

[MkDocs](https://www.mkdocs.org/) is the static site generator used for this site.

## Initialising

In a clean directory:

```sh
uv pip install mkdocs
mkdocs new .
```

## Editing

Create [Markdown](markdown.md) files in the `docs/` directory.

Non-markdown files can go alongside them and will be copied as-is.

MkDocs comes with a test server that automatically reloads on changes:

```sh
mkdocs serve
```

### Images

* Put them in `docs/img`. Reference with the usual syntax: `![alt text](img/name_of_file.png)`.
* Custom favicon: the standard MkDocs will use `docs/img/favicon.ico` [if present](https://www.mkdocs.org/getting-started/#changing-the-favicon-icon).
  Material for MkDocs prefers `assets/images/favicon.png` but this can be overridden in the config.

## Deploying

Full documentation [here](https://www.mkdocs.org/user-guide/deploying-your-docs/).
The gist is: run `mkdocs gh-deploy` and it will soon appear on [your github site](https://ligne.github.io/cahiers/).

There is a [GitHub Action](https://squidfunk.github.io/mkdocs-material/publishing-your-site/#with-github-actions) to do this.

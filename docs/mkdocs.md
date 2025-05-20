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

- Put them in `docs/img`. Reference with the usual syntax: `![alt text](img/name_of_file.png)`.
- Custom favicon: the standard MkDocs will use `docs/img/favicon.ico` [if present](https://www.mkdocs.org/getting-started/#changing-the-favicon-icon).
    Material for MkDocs prefers `assets/images/favicon.png` but this can be overridden in the config.

## Redirects

To avoid link-rot when moving pages about, use the `mkdocs-redirects` plugin:

```yaml
plugins:
  - redirects:
      redirect_maps:
        "old-path.md": "new/path.md"
```

However redirecting anchors needs to be done within the browser.
See [uv's codebase](https://github.com/astral-sh/uv/blob/0.7.3/docs/js/extra.js#L55) for one possible implementation.

## Navigation

Material for MkDocs has [a lot of interesting options](https://squidfunk.github.io/mkdocs-material/setup/setting-up-navigation/).
If these are not enough, there's always [Awesome Nav](https://lukasgeiter.github.io/mkdocs-awesome-nav/features/nav/).

## Creation and revision dates

Add and [configure](https://timvink.github.io/mkdocs-git-revision-date-localized-plugin/index.html) the plugin:

```yaml
plugins:
  - git-revision-date-localized:
      enabled: !ENV [CI, false]
      type: timeago
      enable_creation_date: true
      timezone: Europe/London
```

The Github action will [also need tweaking](https://timvink.github.io/mkdocs-git-revision-date-localized-plugin/index.html#note-when-using-build-systems-like-github-actions).

Not all themes support this out of the box (Material for MkDocs [does](https://squidfunk.github.io/mkdocs-material/setup/adding-a-git-repository/#revisioning)).

## Deploying

Full documentation [here](https://www.mkdocs.org/user-guide/deploying-your-docs/).
The gist is: run `mkdocs gh-deploy` and it will soon appear on [your github site](https://ligne.github.io/cahiers/).

There is a [GitHub Action](https://squidfunk.github.io/mkdocs-material/publishing-your-site/#with-github-actions) to do this.

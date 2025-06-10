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

Put images in `docs/img/`.
They can then be referenced with the usual syntax: `![alt text](img/name_of_file.png)`.

Custom favicon: the standard MkDocs will use `docs/img/favicon.ico` [if present](https://www.mkdocs.org/getting-started/#changing-the-favicon-icon).
Material for MkDocs prefers `assets/images/favicon.png` but this can be overridden in the config.

### CSS and JavaScript

Like images, these [go in the document root](https://squidfunk.github.io/mkdocs-material/customization/#adding-assets), for example in `docs/{js,css}/`.
They then need to be listed in `mkdocs.yml`, using the path relative to the document root:

```yaml
extra_css:
  - css/blah.css
extra_javascript:
  - js/blah.js
```

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

### Table of contents

Each page gets a table of contents, populated with its sub-headings.
By default the Material theme puts this in a secondary sidebar on the right-hand side.

To collapse it into the main sidebar, use the [`toc.integrate`](https://squidfunk.github.io/mkdocs-material/setup/setting-up-navigation/#navigation-integration) feature.
This is not compatible with the feature that allows sections to have their own index pages, [`navigation.indexes`](https://squidfunk.github.io/mkdocs-material/setup/setting-up-navigation/#section-index-pages).

Alternatively, it's possible to move the table of contents to the left by [adding a custom CSS file](#css-and-javascript) to change the secondary sidebar's `order` property:

```css
/* TOC on the left */
.md-sidebar--secondary {
  order: 0;
}
```

This comes at the cost of having a big white space near the middle of the screen.

## Code highlighting

First of all, this relies on code blocks being annotated with the language in use.
(This is checked automatically by `markdownlint`.)
In most cases this is just the [name of the language](https://pygments.org/languages/).
There is also `console`, for a series of commands (including prompts) interspersed with their output.

A basic config looks like this:

```yaml title="mkdocs.yml"
  - pymdownx.highlight:
      anchor_linenums: true
  - pymdownx.superfences
```

As seen here, this also allows a filename (or other information) to be displayed, by adding a `title` attribute to the first line of the block.

To highlight inline code blocks, enable the `pymdownx.inlinehilite` extension and start the block with `#!` followed by the language name.

Full documentation [here](https://squidfunk.github.io/mkdocs-material/reference/code-blocks/).

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

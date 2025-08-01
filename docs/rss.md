# RSS

## Apps

A comparison of three reader apps (Feedly, NewsBlur, Inoreader) from [Zapier](https://zapier.com/blog/best-rss-feed-reader-apps/).
There's not much in it, to be honest: all of them provide a web interface and a reasonable-looking Android app that works offline, with a freemium model.

I feel [disinclined to support Feedly](https://www.citationneeded.news/feedly-launches-strikebreaking-as/).

The NewsBlur Android app is rather pleasant and ergonomic.
I can't get used to the webapp: it binds down-arrow to Next Story, so I keep finding myself on a different article whenever I try to scroll down.
This is the service Cory Doctorow says he uses in his [panegyric to RSS feeds](https://doctorow.medium.com/you-should-be-using-an-rss-reader-76aed31151f9).

The main limitations of the free tier are:

- A limited number of subscriptions.
    I'm not there yet but I think I'm getting close?
- No unified feed.
    The feeds list can be filtered to only show those with unread articles, so this just means a bit more clicking.
- Auto-expiry of unread articles after 2 weeks.
    I've not found this too much of an issue so far, not least because you can save stories for later.
    Expired stories are still available; you just can't mark them as unread.

These last two can make it hard to focus on just articles that are about to expire, however.

Saved stories are easy to browse, and are also useful for switching to a more comfortable device or deferring to a more convenient time.

But ultimately the choice doesn't matter all that much as long as it provides [OPML export](https://en.wikipedia.org/wiki/OPML).

There are also self-hosted options like [FreshRSS](https://freshrss.org/index.html).
Or [NewsBlur, apparently](https://github.com/samuelclay/NewsBlur).
Also [Selfoss](https://selfoss.aditu.de/) and [Tiny Tiny RSS](https://tt-rss.org/).

## Terminal clients

[Newsboat](https://newsboat.org/) looks pretty good and is about as intuitive as you could hope for from a complex TUI application.
It integrates with aggregator services including NewsBlur and FreshRSS, so they stay in sync.

### Configuration

First, create some directories: `mkdir -p ~/.{config,local/share}/newsboat/`.

The config goes in `~/.config/newsboat/config`.
Comments start with `#`; backslashes and double quotes need to be backslash-escaped.

To [connect it to NewsBlur](https://newsboat.org/releases/2.36/docs/newsboat.html#_newsblur):

```
urls-source "newsblur"
newsblur-login "your-newsblur-account"
newsblur-password "your-password"  # or newsblur-passwordfile/newsblur-passwordeval

cookie-cache "~/.local/share/newsboat/cookies.txt"
```

Feeds go in `~/.config/newsboat/urls`.
Again, this uses a very simple syntax: one feed per line, lines starting with `#` are comments.
Use the usual `username:password@` URL syntax for authenticated feeds, but if so remember to restrict the file permissions.
It can also use local files (as `file://` URLs), maybe created by an external script.

It's also possible to create [query-based virtual feeds](https://newsboat.org/releases/2.36/docs/newsboat.html#_query_feeds).
They'll be empty unless `prepopulate-query-feeds` is enabled in the config.

It will refuse to start unless it has at least one feed or external source configured.

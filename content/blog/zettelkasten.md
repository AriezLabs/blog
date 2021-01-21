---
title: "Note taking"
date: 2021-01-21T13:10:27+01:00
slug: ""
description: ""
keywords: []
draft: true
tags: []
math: false
toc: false
---

If you're in college, taking notes is kind of your profession. In general however, not many people seem to spend a lot of thought on how to do it well. This is outside of a few bubbles of course, which 

After trying tons of apps and whatnot, about a year ago, I converged on [Zettelkasten](https://zettelkasten.de/). I'm pretty happy with it and it's the longest I've ever stuck with a single note-taking system. And actually, it's pretty simple.


## The system

## Tooling

I'm big on Vim so using [vimwiki](https://github.com/vimwiki/vimwiki) is a no-brainer. Vimwiki is actually pretty lightweight: it kind of boils down to a set of convenient shortcuts to manage a bunch of text files (your Zettelkasten) in Vim. Its most important features are along the lines of linking and creating new pages with one keystroke, renaming pages, finding backlinks, and so on, and as it turns out that's all you really need anyway. 

Still, over time, I've supplemented vimwiki with other tools and scripts.

#### Pandoc

[Pandoc](https://pandoc.org/) is a more powerful HTML generator than vimwiki's built-in `:Vimwiki2HTML`. For example, you can add your own CSS to its HTML output, or even export to LaTeX and PDF. By virtue of offering a CLI, it also allows you to string together a more complex pipeline of commands, which I'm doing to automatically add a header and footer to each page.

And so, a random example page like this

```md
# Emulsion

See: [fat](fat)

![On a chemical level](emulsion.png)

Suspending fat and water together without them separating back.

Examples: [mayo](mayo), hollandaise, dairy (incl. chocolate), vinaigrette (which is usually only temporary)

Generally, you need an **emulsifier**: 

* egg yolk (specifically, its [lecithin](lecithin))
* mustard

Emulsions are fickle:

* some need cold, others need warm temps
* Quick temperature swings might break emulsions (e.g. heating chocolate too fast)

When creating emulsions, take care:

* if things go south, stop adding fat and potentially a splash of cold water
```

gets turned into this:

![zk_page_example png](../zk_page_example.png)

#### fzf and rg

When you have a lot of notes, navigation is going to become difficult. [fzf](https://github.com/junegunn/fzf.vim) can help - I've set it up so that `:Zk` pops up a search window where I can fuzzy search for a page and hit enter to open it. 

![zk_page_example png](../rg_example.png)

Add [rg](https://github.com/BurntSushi/ripgrep) into the mix and you can do a full-text search of your notes, not just the titles.

#### A webserver

Thanks to HTML generators, it's very easy to host your Zettelkasten on the web. I'm renting a VPS on [linode](https://www.linode.com/) for ~$5 per month on which I've set up a simple [nginx](https://www.nginx.com/) server with primitive auth. It's [basically 10 lines](https://www.digitalocean.com/community/tutorials/how-to-set-up-password-authentication-with-nginx-on-ubuntu-14-04) of config to get up and running, and being able to access your notes from anywhere is pretty nice.

#### iPad

Sketches and annotated images sometimes are the best way to explain something, but (at least for me) getting them into your Zettelkasten has to be convenient or you'll never do it. And the most convenient way I've found so far is Apple's [Continuity](https://www.apple.com/macos/continuity/). It lets you take a screenshot on your Mac (or [Hackintosh](../setups/)), instantly annotate it on your iPad, and drop it into your Zettelkasten directory with near minimal overhead. And with [Blink](https://blink.sh/), you can work with your Zettelkasten on the iPad as well.

#### Useful shortcuts

Beyond fzf and rg I've found it useful to create Python scripts for generating HTML from all edited files, and for generating HTML for the current page and immedieately opening it in the browser. I've bound those to Vim shortcuts and so it's very easy to look at what I'm writing not just in Markdown source but also in prettier HTML.


## Workflow

* "See:" line
* index pages and pages for topics


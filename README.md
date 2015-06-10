Skulpt Project Homepage
=======================

You can see [the working example site here](http://eah13.github.io/skulpt-redo/)

Current Status: Under development

Milestones on the way to shipping this:

- [x] Create skulpt.github.io
- [x] Port existing skulpt.org content
- [ ] Complete gallery, using, and contributing pages
- [ ] Pare down index.html to be Try Skulpt focused
- [ ] Ensure link continuity for eg proctest.html to avoid broken links
- [ ] alter CNAME so this site displays at skulpt.org

## Requirements

* npm & Gem. `apt-get install` or do what you do to get these fro your system.
* Jekyll.  `gem install github-pages` should get you what you need.
* grunt. For SCSS changes only. `npm install -g grunt`.

## To Hack

1. Clone the repo and cd into it
2. `npm install`
3. `bundle exec jekyll serve --watch` will start a server at http://localhost:4000
4. Hack and save and the server will serve your changes.  Exception: `_config.yaml` requires a restart of the server

*Note: `gh-pages` is the default branch in this repo.  Treat it like `master` and make all pull requests to it.  This shouldn't affect anything besides your pull requests, and Github will automatically make them to the default branch, but I thought I'd mention it.*

SCSS hacks only:

* `grunt` will start a SCSS compiler watching for changes


### Make a page

To make a new page, create a `yourpage.md` file in the root with a YAML header. A basic page would look like this:

```
---
layout: default     <- loads the _layouts/default.html template and inserts the below into {{ content }}
title: "My title here"
skulpt: true       <- optional: load the skulpt and codemirror js/css on this page
---

### This is where your markdown will go

<p>Remember, HTML is valid markdown!</p>
```

### Using foundation for responsive layout

Here's a tiny introduction to foundation: In foundation, everything's in a `<div class="row">`. Then you make columns with `<div class="small-12 columns>`.  12 is the max width of a column, and things inherit from small screens on up.  So `"small-12 columns"` means full width for all screen sizes.  `"small-12 large-6 columns"` means full width for small screens but half width for large ones, which I've used to get the code window and output side-by-side.  More on [the foundation docs site](http://foundation.zurb.com/docs), which is pretty good.  Lots of good code examples.

`default.html` sets your content in a `"small-12 columns"` so you can throw raw text at it and it'll still look decent.  In otherwords, for a basic page you should just be able to write markdown and it'll look great.

### Hacking SCSS

We'll aim for a set-and-forget style for the site.  So, after the initial hacking, this shouldn't change too much.

Make changes in `scss/_custom.scss`.  You'll want libsass running via grunt to see changes.  I sometimes forget that and needlessly debug CSS selectors >:(

Site-wide settings for foundation are accessed via `scss/_settings.scss`.  The default values are in there, commented out.  To hack, uncomment and mod them.

### Hands off the `docs` folder

The `docs` folder is generated by jsdoc.  Instead of editing it, each time one of the underlying js files or the HACKING.rst file is changed:

1. `git checkout master` if you're not already there
2. `npm install -g jsdoc` if you haven't already
3. `./skulpt.py doc` to generate the docs in `doc/ProgMan`

The generated HTML is now in a folder called `doc/ProgMan` that's in your git working tree       

4. `git checkout gh-pages` then `git checkout -b new-branch-name`.  Or checkout your pre-existing branch made from `gh-pages`
5. `rsync -r doc/ProgMan docs` then `rm -rf doc`
6. `git diff .` to see the changes, `git add .` to add them, `git commit -m "Commit message here"`

:boom: Instant docs.

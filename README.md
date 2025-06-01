# Hugo Book Theme

[![Hugo](https://img.shields.io/badge/hugo-0.147-blue.svg)](https://gohugo.io)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

### A forked version of Alex Shpak's [Hugo-book](https://github.com/alex-shpak/hugo-book/)

Main reason for forking was to update the theme for the new Hugo template structure introduced at version 0.146. You can read about it [here](https://gohugo.io/templates/new-templatesystem-overview/).

At the same time I took the liberty to make some changes (and maybe introduce some bugs):
-  Configuration parameters are grouped under the [Params.Book] section of Hugo configuration file.
-  The left (main) menu shows all pages in `content` directory by default (as opposed to `content\docs`).
-  Removed Google Analytics and Disqus integrations.



### [Hugo](https://gohugo.io) documentation theme as simple as plain book

![Screenshot](https://raw.githubusercontent.com/alex-shpak/hugo-book/master/images/screenshot.png)

- [Features](#features)
- [Requirements](#requirements)
- [Installation](#installation)
- [Menu](#menu)
- [Blog](#blog)
- [Configuration](#configuration)
- [Shortcodes](#shortcodes)
- [Versioning](#versioning)
- [Contributing](#contributing)

## Features

- Clean simple design
- Light and Mobile-Friendly
- Multi-language support
- Customizable
- Zero initial configuration
- Handy shortcodes
- Comments support
- Simple blog and taxonomy
- Primary features work without JavaScript
- Dark Mode

## Requirements

- Hugo 0.146 or higher
- Hugo extended version, [Installation Instructions](https://gohugo.io/installation/)

## Installation

### Install as git submodule
Navigate to your hugo project root and run:

```
git submodule add https://github.com/neacsum/hugo-book themes/hugo-book
```

Then run hugo (or set `theme = "hugo-book"`/`theme: hugo-book` in configuration file)

```
hugo server --minify --theme hugo-book
```

### Install as hugo module

You can also add this theme as a Hugo module instead of a git submodule.

Start with initializing hugo modules, if not done yet:
```
hugo mod init github.com/repo/path
```

Navigate to your hugo project root and add [module] section to your `hugo.toml`:

```toml
[module]
[[module.imports]]
path = 'github.com/neacsum/hugo-book'
```

Then, to load/update the theme module and run hugo:

```sh
hugo mod get -u
hugo server --minify
```

## Menu

By default, the theme will render pages from the `content`[^1] section as a menu in a tree structure.  
You can set `title` and `weight` in the front matter of pages to adjust the order and titles in the menu, as well as other parameters to hide or alter urls in the menu. You can choose which folder to use for generating menu with `Section` configuration parameter.
[^1]: The original version was using `content\docs` folder.

## Blog

A simple blog is supported in the section `posts`.  
A blog is not the primary use case of this theme, so it has only minimal features.

## Configuration

### Site Configuration

There are a few configuration options that you can add to your `hugo.toml` file.  

```toml
# (Optional) If you provide a Disqus shortname, comments will be enabled on
# all pages.
disqusShortname = "my-site"

# (Optional) Set this to true if you use capital letters in file names
disablePathToLower = true

# (Optional) Set this to true to enable 'Last Modified by' date and git author
#  information on 'doc' type pages.
enableGitInfo = true

# (Optional) Theme is intended for documentation use, therefore it doesn't render taxonomy.
# You can remove related files with config below
disableKinds = ['taxonomy', 'taxonomyTerm']

[params]
  # (Optional, default light) Sets color theme: light, dark or auto.
  # Theme 'auto' switches between dark and light modes based on browser/os preferences
  BookTheme = 'light'

  # (Optional, default true) Controls table of contents visibility on right side of pages.
  # Start and end levels can be controlled with markup.tableOfContents setting.
  # You can also specify this parameter per page in front matter.
  BookToC = true

  # (Optional, default none) Set the path to a logo for the book. If the logo is
  # /static/logo.png then the path would be 'logo.png'
  BookLogo = 'logo.png'

  # (Optional, default docs) Specify section of content to render as menu
  # You can also set value to "*" to render all sections to menu
  BookSection = 'docs'

  # Set source repository location.
  # Used for 'Last Modified' and 'Edit this page' links.
  BookRepo = 'https://github.com/alex-shpak/hugo-book'

  # Specifies commit portion of the link to the page's last modified commit hash for 'doc' page
  # type.
  # Required if 'BookRepo' param is set.
  # Value used to construct a URL consisting of BookRepo/BookCommitPath/<commit-hash>
  # Github uses 'commit', Bitbucket uses 'commits'
  BookCommitPath = 'commit'

  # Enable 'Edit this page' links for 'doc' page type.
  # Disabled by default. Uncomment to enable. Requires 'BookRepo' param.
  # Path must point to the site directory.
  BookEditPath = 'edit/master/exampleSite'

  # (Optional, default January 2, 2006) Configure the date format used on the pages
  # - In git information
  # - In blog posts
  BookDateFormat = 'Jan 2, 2006'

  # (Optional, default true) Enables search function with flexsearch,
  # Index is built on fly, therefore it might slowdown your website.
  # Configuration for indexing can be adjusted in i18n folder per language.
  BookSearch = true

  # /!\ This is an experimental feature, might be removed or changed at any time
  # (Optional, experimental, default false) Enables portable links and link checks in markdown pages.
  # Portable links meant to work with text editors and let you write markdown without {{< relref >}} shortcode
  # Theme will print warning if page referenced in markdown does not exists.
  BookPortableLinks = true

  # /!\ This is an experimental feature, might be removed or changed at any time
  # (Optional, experimental, default false) Enables service worker that caches visited pages and resources for offline use.
  BookServiceWorker = true
```

### Multi-Language Support

Theme supports Hugo's [multilingual mode](https://gohugo.io/content-management/multilingual/), just follow configuration guide there. You can also tweak search indexing configuration per language in `i18n` folder.

### Page Configuration

You can specify additional params in the front matter of individual pages:

```toml
# Set type to 'docs' if you want to render page outside of configured section or if you render section other than 'docs'
type = 'docs'

# Set page weight to re-arrange items in file-tree menu.
weight = 10

# (Optional) Set to 'true' to mark page as flat section in file-tree menu.
bookFlatSection = false

# (Optional) Set to hide nested sections or pages at that level. Works only with file-tree menu mode
bookCollapseSection = true

# (Optional) Set true to hide page or section from side menu.
bookHidden = false

# (Optional) Set 'false' to hide ToC from page
bookToC = true

# (Optional) If you have enabled BookComments for the site, you can disable it for specific pages.
bookComments = true

# (Optional) Set to 'false' to exclude page from search index.
bookSearchExclude = true

# (Optional) Set explicit href attribute for this page in a menu.
bookHref = ''
```

### Partials

There are layout partials available for you to easily override components of the theme in `layouts/partials/`.

In addition to this, there are several empty partials you can override to easily add/inject code.

| Empty Partial                                      | Placement                                   |
| -------------------------------------------------- | ------------------------------------------- |
| `layouts/partials/docs/inject/head.html`           | Before closing `<head>` tag                 |
| `layouts/partials/docs/inject/body.html`           | Before closing `<body>` tag                 |
| `layouts/partials/docs/inject/footer.html`         | After page footer content                   |
| `layouts/partials/docs/inject/menu-before.html`    | At the beginning of `<nav>` menu block      |
| `layouts/partials/docs/inject/menu-after.html`     | At the end of `<nav>` menu block            |
| `layouts/partials/docs/inject/content-before.html` | Before page content                         |
| `layouts/partials/docs/inject/content-after.html`  | After page content                          |
| `layouts/partials/docs/inject/toc-before.html`     | At the beginning of table of contents block |
| `layouts/partials/docs/inject/toc-after.html`      | At the end of table of contents block       |

### Extra Customisation

| File                     | Description                                                                           |
| ------------------------ | ------------------------------------------------------------------------------------- |
| `static/favicon.png`     | Override default favicon                                                              |
| `assets/_custom.scss`    | Customise or override scss styles                                                     |
| `assets/_variables.scss` | Override default SCSS variables                                                       |
| `assets/_fonts.scss`     | Replace default font with custom fonts (e.g. local files or remote like google fonts) |
| `assets/mermaid.json`    | Replace Mermaid initialization config                                                 |

### Plugins

There are a few features implemented as pluggable `scss` styles. Usually these are features that don't make it to the core but can still be useful.

| Plugin                            | Description                                                 |
| --------------------------------- | ----------------------------------------------------------- |
| `assets/plugins/_numbered.scss`   | Makes headings in markdown numbered, e.g. `1.1`, `1.2`      |
| `assets/plugins/_scrollbars.scss` | Overrides scrollbar styles to look similar across platforms |

To enable plugins, add `@import "plugins/{name}";` to `assets/_custom.scss` in your website root.

### Hugo Internal Templates

There are a few hugo templates inserted in `<head>`

- [Google Analytics](https://gohugo.io/templates/internal/#google-analytics)
- [Open Graph](https://gohugo.io/templates/internal/#open-graph)

To disable Open Graph inclusion you can create your own empty file `\layouts\_internal\opengraph.html`.
In fact almost empty not quite empty because an empty file looks like absent for HUGO. For example:
```
<!-- -->
```

## Shortcodes

- [Buttons](https://hugo-book-demo.netlify.app/docs/shortcodes/buttons/)
- [Columns](https://hugo-book-demo.netlify.app/docs/shortcodes/columns/)
- [Details](https://hugo-book-demo.netlify.app/docs/shortcodes/details/)
- [Hints](https://hugo-book-demo.netlify.app/docs/shortcodes/hints/)
- [KaTeX](https://hugo-book-demo.netlify.app/docs/shortcodes/katex/)
- [Mermaid](https://hugo-book-demo.netlify.app/docs/shortcodes/mermaid/)
- [Tabs](https://hugo-book-demo.netlify.app/docs/shortcodes/tabs/)

By default, Goldmark trims unsafe outputs which might prevent some shortcodes from rendering. It is recommended to set `markup.goldmark.renderer.unsafe=true` if you encounter problems.

```toml
[markup.goldmark.renderer]
  unsafe = true
```

If you are using `config.yaml` or `config.json`, consult the [configuration markup](https://gohugo.io/getting-started/configuration-markup/)

## Versioning

This theme follows a simple incremental versioning. e.g. `v1`, `v2` and so on. There might be breaking changes between versions.

If you want lower maintenance, use one of the released versions. If you want to live on the bleeding edge of changes, you can use the `master` branch and update your website when needed.

## Contributing

### [Extra credits to contributors](https://github.com/alex-shpak/hugo-book/graphs/contributors)

Contributions are welcome and I will review and consider pull requests.  
Primary goals are:

- Keep it simple.
- Keep minimal (or zero) default configuration.
- Avoid interference with user-defined layouts.
- Avoid using JS if it can be solved by CSS.

Feel free to open issues if you find missing configuration or customisation options.

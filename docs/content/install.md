---
title: Install
---

# Installation Instructions

## Download

Download Hugo Cite in the `themes/hugo-cite` directory, either by [cloning with Git](https://github.com/loup-brun/hugo-cite) (the preferred method) or by [downloading as a ZIP file](https://github.com/alex-shpak/hugo-book/archive/master.zip).

The Git way:

```bash
git submodule add https://github.com/loup-brun/hugo-cite.git themes/hugo-cite
```

Your project directory should then look like this:

```bash
# Your Hugo project directory
├── config.yml
└── themes
    └── hugo-cite
```

## Configure

Edit the `theme` parameter in your Hugo config file and add `hugo-cite` after your theme.

```yaml
# config.yml
theme:
- <your-theme>
- hugo-cite
```

## Add CSS

Reference the CSS somewhere in your HTML templates:

```html
<link rel="stylesheet" type="text/css" href="{{ "/hugo-cite.css" | relURL }}" />
```

## Next Steps

Easy enough?
Move on to the [usage guide &rarr;](/usage)

---
title: Usage
---

# Usage Guide

## CSL-JSON

You must first provide a **[CSL-JSON](https://citeproc-js.readthedocs.io/en/latest/csl-json/markup.html) bibliography file**.
(Other formats, such as BiBTeX, are _not_ supported.)
In Zotero for instance, this can be accomplished by selecting the CSL JSON format when exporting a collection.
Just include `bib` in the filename (such as `bibliography.json`,`oh-my-bib.json`, or simply `bib.json`) and save it inside your Hugo project directory.

Here is an example:

```bash
# Your Hugo project directory
├── content
│   ├── article1
│   │   ├── bib.json
│   │   └── index.md
│   ├── article2
│   │   ├── image.jpg
│   │   ├── index.md
│   │   └── mr-bib.json
│   └── article3
│       ├── index.md
│       └── oh-my-bib.json
└── path
    └── to
        └── bib.json
```

## Shortcodes

There are two shortcodes you can use in your content:

- `{{</* bibliography */>}}`: display a list of works.
- `{{</* cite */>}}`: render an in-text citation.

## Display a bibliography

### Basic Example

By default, the `{{</* bibliography */>}}` shortcode will render all entries from a `bib.json` included in a [leaf bundle](https://gohugo.io/content-management/page-bundles/#leaf-bundles). 

```markdown
<!-- Markdown -->

{{</* bibliography */>}}
```

### Cited Works

You can restrict the list only to works cited on the page (with the use of in-text citations, see below):

```markdown
<!-- Markdown -->

{{</* bibliography cited */>}}
```

### File Defined in Front Matter

You can specify the path to a JSON file located *inside* the Hugo project directory in the content page’s **front matter** using the `bibFile` parameter.
This is especially useful when working with `cited` entries:

```markdown
---
title: My Article
bibFile: path/to/bib.json # path relative to project root
---

## Bibliography

<!-- The bibliography will display works from path/to/bib.json -->
{{</* bibliography */>}}
```

### File Defined in Shortcode

Alternatively, you can specify the path to the CSL-JSON file at the shortcode level:

```markdown
<!-- Markdown -->

{{</* bibliography "path/to/bib.json" */>}}
```

### Combine Options

You can also **combine both options** (the path to the JSON file must come first):

```markdown
<!-- Markdown -->

{{</* bibliography "path/to/bib.json" cited */>}}
```

**Note**: if you are working with a `cited` bibliography, you’ll have to specify the path to the JSON file in the front matter for in-text citations to access the same file.

### Named Params

You can chose to use **named params** for clarity (the order does not matter here):

```markdown
<!-- Markdown -->

{{</* bibliography src="path/to/bib.json" cited="true" */>}}
```

### File From a URL

Thanks to Hugo’s [`getJSON`](https://gohugo.io/templates/data-templates/#data-driven-content) function, the path can also be a **URL**.  
*Note however that this method may have some drawbacks if you are [reloading often](https://gohugo.io/templates/data-templates/#livereload-with-data-files), see the Hugo docs regarding potential issues.*

```markdown
<!-- Markdown -->

{{</* bibliography "http://example.com/my/bib.json" */>}}
```

## Render in-text citations

Use the `{{</* cite */>}}` shortcode to render rich in-text citations.

Example:

```markdown
<!-- Markdown -->

{{</* cite "Lessig 2002" */>}}
```

The citation key (in the above example, `Lessig 2002`) must match the `id` field of a reference in your CSL-JSON file.
You can make it look like an author-date format, or anything else.

Here’s an excerpt of a CSL-JSON file:

```json
[
    {
        "id": "Lessig 2002",
        "author": [
            {
                "family": "Lessig",
                "given": "Lawrence"
            }
        ]
    }
]
```

Using the citation key defined in the CSL-JSON, you can reference your entry in content files:

```markdown
<!-- Markdown -->

Our generation has a philosopher.
He is not an artist, or a professional writer.
He is a programmer. {{</* cite "Lessig 2002" */>}}
```

### Suppress Author

For an abbreviated in-text citation form, you can add a **dash** (`-`) at the beginning of your citation key:

```markdown
<!-- Markdown -->

{{</* cite "-Lessig 2002" */>}}
```

The above would render `(2002)` rather than `(Lessig, 2002)`.

### Cite a Page

You can also provide a **page** as the second positional parameter:

```markdown
<!-- Markdown -->

{{</* cite "Lessig 2002" 5 */>}}
```

The example above will render `(Lessig, 2020, p. 5)` (note the `p.` was added by Hugo Cite; you need not to add it).

### Cite a Page Range

You can instead specify a **range of pages** using a **dash** `-`, which will output `pp.` before the page range (ensure there is no space between the page numbers):

```markdown
<!-- Markdown -->

{{</* cite "Lessig 2002" 5-6 */>}}
```

The example above will render `(Lessig, 2020, pp. 5-6)`.

## Cited Works

```markdown
<!-- Include the list of cited works on the page -->
{{</* bibliography cited */>}}
```

## See It In Action

Want to see a working demo?
[Check it out &rarr;](/demo)

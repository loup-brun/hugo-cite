# Hugo Cite

📝 Easily manage your bibliography and in-text citations with [Hugo](https://gohugo.io), the popular static-site generator.

---

⚠️ **Important note: APA is the only style currently available, and you must be aware that it does not match the entire APA spec.**  
More styles may be added eventually (contributions welcome!), but given that they are extremely verbose to implement, this is unlikely to happen in a near future.

---

Screenshot:

![Screenshot](https://user-images.githubusercontent.com/9596476/79055177-eddd8b00-7c18-11ea-8fe8-bad1bd8b2297.jpg)

## Install

1. Copy the partials in `layouts/partials/bibliography/` (make sure to mirror the directory structure).
2. Copy the shortcodes in `layouts/shortcodes/`.
3. Copy the CSS in your `static/` directory and reference it in your HTML.

```
# Your Hugo project directory
├── layouts
|   ├── partials
|       ├── bibliography
|           ├── apa-style.html
|           └── bibliography-list.html
|   └── shortcodes
|       ├── bibliography.html
|       └── cite.html
└── static
    └── hugo-cite.css
```

Reference the CSS in your HTML:

```html
<link rel="stylesheet" type="text/css" href="{{ "/hugo-cite.css" | relRef }}"
```

## Usage

You must first provide a **[CSL-JSON](https://citeproc-js.readthedocs.io/en/latest/csl-json/markup.html) bibliography file**.
(Other formats, such as BiBTeX, are _not_ supported.)
In Zotero for instance, this can be accomplished by selecting the CSL JSON format when exporting a collection.
Just include `bib` in the filename (such as `bibliography.json`,`oh-my-bib.json`, or simply `bib.json`) and save it inside your Hugo project directory.

Here is an example:

```
# Your Hugo project directory
├── content
|   ├── article1
|       ├── index.md
|       └── bib.json
|   ├── article2
|       ├── index.md
|       ├── image.jpg
|       └── bib.json
```

### Shortcodes

There are two shortcodes you can use in your content:

- **`{{< bibliography >}}`**: display a list of works.
- **`{{< cite >}}`**: render an in-text citation.

### Display a bibliography

#### Basic Example

By default, the `{{< bibliography >}}` shortcode will render all entries from a `bib.json` included in a [leaf bundle](https://gohugo.io/content-management/page-bundles/#leaf-bundles). 

```markdown
<!-- Markdown -->

{{< bibliography >}}
```

#### Specify a Path to the JSON File

Alternatively, you can specify the path to a JSON file located *inside* the Hugo project directory:

```markdown
<!-- Markdown -->

{{< bibliography "path/to/bib.json" >}}
```

#### Cited Works

You can restrict the list only to works cited on the page (with the use of in-text citations, see below):

```markdown
<!-- Markdown -->

{{< bibliography cited >}}
```

#### Combine Options

You can also **combine both options** (the path to the JSON file must come first):

```markdown
<!-- Markdown -->

{{< bibliography "path/to/bib.json" cited >}}
```

#### Named Params

You can chose to use **named params** for clarity (the order does not matter here):

```markdown
<!-- Markdown -->

{{< bibliography src="path/to/bib.json" cited="true" >}}
```

#### Front Matter

Instead of specifying the custom path inside your shortcode, you can specify it in the content page’s **front matter** (this is especially uesful when you want to restrict to cited entries):

```markdown
---
title: My Article
bibFile: oh/my/bib.json # path relative to project root
---

## Bibliography

<!-- The bibliography will display works from oh/my/bib.json -->
{{< bibliography >}}
```

#### File From a URL

Thanks to Hugo’s `getJSON` function, you can also provide a **URL**.  
*Note however that this method may have some drawbacks if you are [reloading often](https://gohugo.io/templates/data-templates/#livereload-with-data-files), see the Hugo docs regarding potential issues.*

```markdown
<!-- Markdown -->

{{< bibliography "https://example.com/my/bib.json" >}}
```

### Render in-text citations

Use the `{{< cite >}}` shortcode to render rich in-text citations.
The citation key must match the `id` field of a reference in your CSL-JSON file.
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
He is a programmer. {{< cite "Lessig 2002" >}}

## Cited Works

<!-- Include the list of cited works on the page -->
{{< bibliography cited >}}
```

## License

[WTFPL](LICENSE)
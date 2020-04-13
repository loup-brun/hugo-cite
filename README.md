# Hugo Cite

📝 Easily manage your bibliography and in-text citations with [Hugo](https://gohugo.io), the popular static-site generator.

[**Documentation site + demo &rarr;**](https://labs.loupbrun.ca/hugo-cite/)

---

⚠️ **Important note: APA is the only style currently available, and you must be aware that it does not match the entire APA spec.**  
More styles may be added eventually (contributions welcome!), but given that they are extremely verbose to implement, this is unlikely to happen in a near future.

---

## Install

1. Copy the partials in `layouts/partials/bibliography/` (make sure to mirror the same directory structure).
2. Copy the shortcodes in `layouts/shortcodes/`.
3. Copy the CSS in your `static/` directory and reference it in your HTML.
4. (Optional) To modify the particles or to use Hugo Cite in another language than English, copy the contents of `i18n/`.

```bash
# Your Hugo project directory
├── layouts
|   ├── partials   # 1.
|   |   └── bibliography
|   |       ├── apa-style.html
|   |       └── bibliography-list.html
|   └── shortcodes # 2.
|       ├── bibliography.html
|       └── cite.html
└── static         # 3.
    └── hugo-cite.css
```

Reference the CSS in your HTML:

```html
<link rel="stylesheet" type="text/css" href="{{ "/hugo-cite.css" | relURL }}" />
```

If you plan to use Hugo Cite in another language than English, copy the `i18n/` files:

```bash
# Your Hugo project directory
└── i18n         # 4.
    ├── en.yaml
    └── fr.yaml
```

If a language does not exist, use the `i18n/en.yaml` as a base template and create a new file with the matching language code.

## Usage

You must first provide a **[CSL-JSON](https://citeproc-js.readthedocs.io/en/latest/csl-json/markup.html) bibliography file**.
(Other formats, such as BiBTeX, are _not_ supported.)
In Zotero for instance, this can be accomplished by selecting the CSL JSON format when exporting a collection.
Just include `bib` in the filename (such as `bibliography.json`,`oh-my-bib.json`, or simply `bib.json`) and save it inside your Hugo project directory.

Here is an example:

```bash
# Your Hugo project directory
├── content
|   ├── article1
|   |   ├── bib.json
|   |   └── index.md
|   ├── article2
|   |   ├── image.jpg
|   |   ├── index.md
|   |   └── mr-bib.json
|   └── article3
|       ├── index.md
|       └── oh-my-bib.json
└── path
    └── to
        └── bib.json
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
bibFile: path/to/bib.json # path relative to project root
---

## Bibliography

<!-- The bibliography will display works from path/to/bib.json -->
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

## Demo

View a working [online demo](https://labs.loupbrun.ca/hugo-cite/demo/).

[![Screenshot featuring Hugo Cite](https://user-images.githubusercontent.com/9596476/79130193-88061600-7d74-11ea-9654-0dc8b3d5bd2d.png)](https://labs.loupbrun.ca/hugo-cite/demo/)

## License

[WTFPL](LICENSE)
---
title: FAQ
---

# Frequently Asked Questions (and troubleshooting)

---

## Can I use Hugo Cite in my Hugo project now?

**Yes! (Although still in beta.)** However, be aware that APA is currently the only style partially supported.

## Which types of publication are supported?

Hugo Cite currently supports (in beta) these types of publication:

- book
- book chapter
- article (or journal article)
- website

If the type of work (e.g. a thesis) is not supported, Hugo Cite will fall back a generic APA scheme, similar to the **book** type.

## Some APA fields are not displayed per the APA spec.

Not all types of publication are supported yet, as well as many technical variants (e.g. a republished book).
Please feel free to [open an issue](https://github.com/loup-brun/hugo-cite/issues/new) to pin-point what should be improved.

## Can I use other bibliography formats such as BiBTeX instead of CSL-JSON?

**No.** The only format supported is JSON, which must follow the [CSL-JSON spec](https://citeproc-js.readthedocs.io/en/latest/csl-json/markup.html).

## This is an open source project, where can I find the code?

The code is hosted in a [GitHub repository](https://github.com/loup-brun/hugo-cite).

## After using the `bibliography` shortcode, my Hugo build fails.

This is likely because a bibliography file was not found, or becuase you did not specify the path to a JSON file.
If you place your `bib.json` next to `index.md` in a [leaf bundle](https://gohugo.io/content-management/page-bundles/#leaf-bundles), you can omit specifying a path.

If you do not use leaf bundles, you must specify the path, either in the [front-matter](/usage/#file-defined-in-front-matter) of the page with the `bibFile` param or [directly in the shortcode](/usage/#file-defined-in-shortcode).
In both cases, the path must be relative to the Hugo **project** root (not the content root).

## I want to report a bug or request a new feature

Open a [ticket](https://github.com/loup-brun/hugo-cite/issues/new) on the GitHub repo.
Feedback welcome!

## Do I need to credit you if I use Hugo Cite in my projects?

**No.** You just [do what the fuck you want to](http://www.wtfpl.net/about/) (although it is recommended to link back to the original project, should you need to keep track of updates).

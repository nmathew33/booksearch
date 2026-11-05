# Booksearch

A fast command-line search tool that extracts readable text from EPUB files and attaches a precise source location to each text block.

# Usage

booksearch extract --input book.epub --output text.json
booksearch extract --input books/ --output text.json

If --output is not specified, booksearch will output to stdout

Accept one EPUB file or a directory of EPUB files.

For directory input, process immediate .epub files in filename order. Recursive directory traversal is optional.

Write UTF-8 JSON Lines: one complete JSON object per line.

Send diagnostics and the extraction summary to stderr.

Each record contains text and location:

{"text":"An example paragraph.","location":{"epub":"book.epub","document":"OEBPS/chapter03.xhtml","element_path":[1,1,3],"anchor":"paragraph-12"}}

| Field | Description |
| --- | --- |
| `text` | Nonempty readable text, preserving original case, punctuation, and Unicode characters. |
| `location.epub` | EPUB path relative to the input directory; for a single-file input, its filename. The caller retains the input base directory. |
| `location.document` | Content-document path relative to the EPUB archive root. |
| `location.element_path` | Array of zero-based child-element indexes locating the source element from the XHTML document root. |
| `location.anchor` | Existing ID on the source element itself, or null. This is a convenience; the structural path remains authoritative. |

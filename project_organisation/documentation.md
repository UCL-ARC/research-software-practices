# How to write effective documentation

### tl, dr

### What is effective documentation?

#### Consider your audience.

#### Self-documenting code

#### In-line comments - when to use, when to stop.

A good example:

```python
if parser == ParserLibrary.MARKER:
    rendered = converter(file)
    # right now we are discarding metadata and images.
    text, metadata, images = text_from_rendered(rendered)
    return text
# here, we could implement the other pdf parsers.
bad_parser_file_combo = f"Unsupported parser {parser} for file {file}."
raise FileParserMismatchError(bad_parser_file_combo)
```

A bad example:

### The `readme.md` file

### Github pages

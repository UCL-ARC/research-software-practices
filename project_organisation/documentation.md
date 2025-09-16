# How to write effective documentation

### tl, dr

We write documentation for our code so that it might be useable beyond its immediate purpose. There might be colleagues
working with us on our projects, there might be an intended user base (known or unknown to us) for our software, there
could be future people tasked with maintaining and building upon this code and there may also be a future version of
ourselves, much less in the weeds of our current project, who might want to work with, build upon, use and understand
the code we've written for this project.

We might assume that these folks should simply go ahead and read the code. They should. But we want to make it as easy
as possible for them, and (remember!) ourselves to do so. We achieve this through **documentation**. Documentation in
software projects can take different forms, and some of them might be more appropriate than others depending on the
nature of your project. Moreover, there are certain patterns and stylistic approaches which might be more or less useful
both in general, and given the specific nature of our project and the composition of our audience. For instance, a
project whose aim is primarily to teach/educate will have different documentation patterns than an open source library
with a broad user base.

This document aims to introduce a conceptualisation of **effective** documentation, and which patterns, both in code,
project design and prose may help achieve this for a given software project.

### What is effective documentation?

- minimise the time a typical person of your target audience requires to familiarise themselves with your code
- keep in mind the purpose & the audience.
- the typical person is important, but: keep accessibility in mind.
- don't overwhelm the reader with information, and don't re-invent the wheel. if your library uses an external library
  for http requests, you don't neeed to explain how that works. you can link to it.

#### Consider your audience.

#### Self-documenting code

- use formatters. they will help you do a lot of the heavy lifting in documenting your code while you write.

#### In-line comments - when to use, when to stop.

Ideally, your code should be self-explanatory. You might achieve this through _descriptive names for objects_ and
patterns which don't obfuscate what's going on in your code. For instance, the function `process_data()` might better be
called `quadratic_mean()`. So, descriptive names for objects can reduce the need for inline comments.

A good example:

```python
if parser == ParserLibrary.MARKER:
    rendered = converter(file)
    text, metadata, images = text_from_rendered(rendered)
    return text # don't require images and metadata, hence discarding
# here, we could implement other parsers.
bad_parser_file_combo = f"Unsupported parser {parser} for file {file}."
raise FileParserMismatchError(bad_parser_file_combo)
```

A bad example:

```python
from my_library import *
my_file_path = 'path/to/my_file.csv' # defining the file path
df = process_file(my_file_path) # processing file using function from my_library
```

### The `readme.md` file & other non-code documentation

### (Github) pages / Externally hosted documentation

### Dos and don'ts

- acronymns

# Versioning

Version numbers communicate the state and evolution of your software to users and collaborators. Good versioning
practices help others understand compatibility, track changes, and decide when to upgrade.

## Semantic Versioning

We recommend [Semantic Versioning (SemVer)](https://semver.org/) for most research software projects. A semantic version
has the format `MAJOR.MINOR.PATCH` (e.g., `2.4.1`):

- **MAJOR**: Increment when you make breaking changes that require users to update their code.
- **MINOR**: Increment when you add functionality in a backward-compatible manner
- **PATCH**: Increment when you make backward-compatible bug fixes

### Examples

- `1.0.0` → `1.0.1`: Fixed a bug, no API changes
- `1.0.1` → `1.1.0`: Added a new feature, existing code still works
- `1.1.0` → `2.0.0`: Changed function signatures, users need to update their code

### Pre-release versions

For development versions, append a pre-release identifier:

- `1.0.0-alpha.1`: Early development, unstable
- `1.0.0-beta.2`: Feature-complete, testing for bugs
- `1.0.0-rc.1`: Release candidate, potentially ready for release

Note that these are just general examples. Not every ecosystem uses the same pre-release identifiers. Always follow the
general practices used in the ecosystem you're working in!

### The 0.x.y convention

Versions starting with `0` (e.g., `0.3.2`) indicate that the software is in initial development and the API may change
at any time. Once your API stabilises, release `1.0.0`.

## Version control systems

### Git tags

Use Git tags to mark specific points in your repository's history as important (typically releases):

```sh
# Create an annotated tag
git tag -a v1.2.0 -m "Release version 1.2.0"

# Push tags to remote
git push origin v1.2.0

# Or push all tags
git push origin --tags

# List all tags
git tag -l
```

**Always use annotated tags** (`-a` flag) for releases, as they store metadata about who created the tag and when.

### Tag naming conventions

- Prefix version numbers with `v`: `v1.2.0` (recommended)
- Be consistent across your project
- Match the version in your code/package metadata exactly

## Version metadata in code

Keep your version number in a single, authoritative location to avoid inconsistencies:

### Python

Use a `__version__` attribute in your package's `__init__.py`:

```python
__version__ = "1.2.0"
```

For modern Python packages, specify the version in `pyproject.toml`:

```toml
[project]
name = "my-package"
version = "1.2.0"
```

Or use dynamic versioning with tools like [`setuptools-scm`](https://github.com/pypa/setuptools_scm), which
automatically determines the version from Git tags.

### R

Specify the version in the `DESCRIPTION` file:

```
Package: mypackage
Version: 1.2.0
```

Use [`usethis::use_version()`](https://usethis.r-lib.org/reference/use_version.html) to facilitate version bumping.

### C++

Define the version in CMake:

```cmake
project(MyProject VERSION 1.2.0)
```

## Changelog management

Maintain a `CHANGELOG.md` file to document changes between versions. Follow the
[Keep a Changelog](https://keepachangelog.com/) format:

```markdown
# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com), and this project adheres to
[Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added

- New feature X

## [1.2.0] - 2024-03-15

### Added

- Feature Y for improved performance
- Support for new data format Z

### Fixed

- Bug in calculation function

## [1.1.0] - 2024-02-01

### Changed

- Improved documentation
```

Keep in mind that changelogs are written for _humans_, not machines, so they should be clear, concise, and easy to read.

````

## Version compatibility

### Deprecation warnings

When removing features, provide deprecation warnings for at least one minor version before removal:

```python
import warnings

def old_function():
    warnings.warn(
        "old_function() is deprecated and will be removed in version 2.0.0. "
        "Use new_function() instead.",
        DeprecationWarning,
        stacklevel=2
    )
    # ... existing implementation
````

### Dependency version constraints

Specify version constraints for your dependencies to ensure compatibility:

- **Python** (`requirements.txt` or `pyproject.toml`):

  ```
  numpy>=1.20,<2.0
  pandas~=2.0.0  # Compatible with 2.0.x
  ```

- **R** (`DESCRIPTION`):
  ```
  Imports:
      dplyr (>= 1.0.0),
      ggplot2 (>= 3.3.0)
  ```

## Further reading

- [Semantic Versioning specification](https://semver.org/)
- [Keep a Changelog](https://keepachangelog.com/)
- [Git tagging documentation](https://git-scm.com/book/en/v2/Git-Basics-Tagging)

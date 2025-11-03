# Release Management

Release management is the process of preparing, packaging, and distributing your software to users. Good release
practices ensure that users can easily install and use your software, and that you can track which version they're
running.

## Why manage releases?

- 📦 **Distribution**: Make it easy for users to install and use your software
- 🔍 **Traceability**: Know which version users are running when they report issues
- 📝 **Communication**: Clearly communicate what has changed and why
- 🎯 **Stability**: Separate stable releases from ongoing development
- 🤝 **Trust**: Demonstrate that your software is maintained and reliable

## Release checklist

Before creating a release, ensure you've completed these steps:

- [ ] All tests pass
- [ ] Documentation is up to date
- [ ] `CHANGELOG.md` is updated with changes since last release
- [ ] Version number is bumped appropriately (see also [Versioning](../versioning))
- [ ] Dependencies are up to date and version constraints are specified
- [ ] Breaking changes are clearly documented in the changelog
- [ ] Examples and tutorials reflect any API changes

## GitHub Releases

[GitHub Releases](https://docs.github.com/en/repositories/releasing-projects-on-github) is our recommended platform for
distributing releases, as most of our projects are already on GitHub.

### Creating a release on GitHub

1. Navigate to your repository's main page
2. Click "Releases" in the right sidebar
3. Click "Create a new release"
4. Choose or create a tag (e.g., `v1.2.0`, see [Versioning](../versioning) for guidance on setting version numbers)
5. Write release notes (see below)
6. Optionally attach compiled binaries or other distribution files
7. Mark as pre-release if applicable
8. Click "Publish release"

### Writing good release notes

Release notes should help users understand what has changed and whether they should upgrade. It is good practice to link
to Pull Requests (PRs) for more details, where applicable. Note that noting the `#<PR-number>` is enough, GitHub will
automatically generate a link to the PR.

Below is an example of a well-written release note:

```markdown
## What's Changed

### Breaking Changes

- Renamed `process_data()` to `process_dataset()` for clarity (#123)
- Removed deprecated `old_api()` function (deprecated since v1.0.0)

### New Features

- Added support for HDF5 file format (#145)
- New `validate()` method for data verification (#156)

### Bug Fixes

- Fixed memory leak in long-running processes (#134)
- Corrected calculation error in edge cases (#142)

### Documentation

- Added tutorial for new HDF5 functionality
- Improved installation instructions for Windows

### Dependencies

- Updated numpy requirement to >=1.24.0
- Dropped support for Python 3.8 (end of life)

**Full Changelog**: https://github.com/owner/repo/compare/v1.1.0...v1.2.0
```

### Auto-generating release notes

GitHub can automatically generate release notes from pull requests:

1. When creating a release, click "Generate release notes"
2. Review and edit the generated content
3. Add any additional context or breaking changes

## Language-specific release practices

See the [coding standards](../../coding_standards) for more language-specific information:

- [Python](../../coding_standards/python)
- [R (CRAN or Bioconductor)](../../coding_standards/r)
- [C++](/coding_standards/c++)

## Automated releases on tag push with GitHub Actions

Automate your release process with GitHub Actions to ensure consistency and reduce manual work.

The following workflow will create a new release on GitHub when a tag is pushed.

```yaml
## Example with Python package
name: Release

on:
  push:
    tags:
      - "v*"

jobs:
  release:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Create Release
        uses: softprops/action-gh-release@v1
        with:
          generate_release_notes: true

      - name: Build and publish to PyPI
        if: startsWith(github.ref, 'refs/tags/')
        env:
          TWINE_USERNAME: __token__
          TWINE_PASSWORD: ${{ secrets.PYPI_API_TOKEN }}
        run: |
          pip install build twine
          python -m build
          twine upload dist/*
```

## Release cadence

Choose a release schedule that balances stability with timely updates:

### Time-based releases

- **Advantages**: Predictable, easier to plan, encourages regular maintenance
- **Disadvantages**: May release without significant changes, or delay important fixes
- **Examples**: Monthly, quarterly, or yearly releases

### Feature-based releases

- **Advantages**: Each release has clear value, no "empty" releases
- **Disadvantages**: Unpredictable timing, may delay bug fixes
- **Examples**: Release when major features are complete

### Continuous deployment

- **Advantages**: Users get fixes and features immediately
- **Disadvantages**: Requires excellent test coverage, may overwhelm users with updates
- **Examples**: Release on every merge to main branch

### Hybrid approach (recommended)

Combine multiple strategies:

- Regular minor releases (e.g., monthly) for features
- Immediate patch releases for critical bugs
- Major releases when breaking changes accumulate

## Pre-releases and release candidates

Use pre-releases to get feedback before official releases:

- **Alpha**: Early development, incomplete features, expect bugs
- **Beta**: Feature-complete, testing phase, may have bugs
- **Release Candidate (RC)**: Potentially final, last chance for testing

Mark these clearly in your version number (`1.0.0-beta.1`) and on GitHub ("Set as a pre-release").

## Long-term support (LTS)

For widely-used research software, consider maintaining LTS versions:

- Continue to fix bugs in older major versions
- Backport critical security fixes
- Clearly communicate which versions receive support
- Define an end-of-life policy

**Example support policy:**

- Latest major version: Full support (features + bugs)
- Previous major version: Bug fixes only (12 months)
- Older versions: Security fixes only (24 months)

## Deprecation policy

When removing features or dropping support for versions:

1. **Announce early**: Mention in documentation and release notes
2. **Add warnings**: Use deprecation warnings in code (at least one minor version before removal)
3. **Provide alternatives**: Document what users should use instead
4. **Follow semantic versioning**: Only remove in major version updates
5. **Update examples**: Ensure documentation doesn't use deprecated features

## Rollback plan

Prepare for problems after release:

- Keep previous releases available on GitHub
- Document how users can downgrade if needed
- Monitor issues closely after release
- Be prepared to issue a patch release quickly if critical bugs are found
- Consider a "hotfix" branch workflow for urgent fixes

## Further reading

- [GitHub Releases documentation](https://docs.github.com/en/repositories/releasing-projects-on-github)
- [Python Packaging User Guide](https://packaging.python.org/)
- [R Packages - Releasing a package](https://r-pkgs.org/release.html)
- [Keep a Changelog - Release guidelines](https://keepachangelog.com/)

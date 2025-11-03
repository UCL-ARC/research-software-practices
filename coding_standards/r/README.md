# R recommendations

## Tidyverse style guide

In general, we recommend following the [Tidyverse style guide](https://style.tidyverse.org/) as much as possible. There
are two R packages that support this style guide out of the box:

- [_styler_](http://styler.r-lib.org/) allows interactively styling selected text, files or entire projects. It includes
  a handy RStudio plugin to make your R code beautiful with one simple keyboard shortcut
- [_lintr_](https://github.com/jimhester/lintr) checks whether your code conforms to the style guide and flags potential
  problems. It can also be enabled in RStudio.

Both these tools can be customised to disable certain checks or using different values. However, we recommend sticking
to the default values as much as possible.

For VSCode users, the [vscode-R](https://code.visualstudio.com/docs/languages/r) plugin provides most of these features
in VSCode as well.

> A note on the use of the pipe (`|>` or `%>%`) operator, although
> [very useful for data analysis code](https://r4ds.hadley.nz/workflow-style.html#sec-pipes), we recommend to avoid
> their usage in **R package code**. The main reason is that pipes make code more difficult to debug, especially for
> very long sequences of pipes, as the intermediate objects are not immediately accessible. In addition, the use of
> `%>%` would incur an additional dependency.

## Package development

The [_R Packages_](https://r-pkgs.org/) book provides a comprehensive guide to R package development, which closely
follows the _Tidyverse style guide_ (as they're from the same authors). We recommend following the best practices
described in this book.

To help with adhering to these practices and make your life as an R developer much easier, there are the
[_devtools_](https://devtools.r-lib.org/) and [_usethis_](https://usethis.r-lib.org/) packages. From setting up your
package file structure with `usethis::create_package()`, running unit tests and other checks with `devtools::check()`,
to publishing your package to CRAN with `devtools::release()`, these two packages have it all covered. In fact, whenever
you need to do anything other than edit an `*.R` file, there is probably a
[_usethis_ function](https://usethis.r-lib.org/reference/index.html) function you can (and should!) use instead. And if
there is not, ask yourself whether you really need to do that thing.

And of course, both these packages play nicely together with RStudio, with several built-in features and shortcuts (see
the _R Packages_ book for tips and tricks).

### Releasing

For more general information on releasing, see the [release management guide](../../project_organisation/release).

General R packages can be submitted to [CRAN](https://cran.r-project.org/). For bioinformatics/life science related
packages, consider submitting to [Bioconductor](https://bioconductor.org/) (see below).

To release a package, follow these steps:

```r
# Check package meets CRAN standards
devtools::check()

# Build and submit to CRAN
devtools::release()
```

**Best practices:**

- Ensure your package passes `R CMD check` with no errors, warnings, or notes
- Follow [CRAN policies](https://cran.r-project.org/web/packages/policies.html)
- Respond promptly to CRAN maintainer feedback
- Consider submitting to [r-universe](https://r-universe.dev/) for faster distribution between CRAN releases
- For Bioconductor packages, follow the [Bioconductor submission process](https://contributions.bioconductor.org/)

The `usethis` package has a convenient function that will create a GitHub issue for you with a checklist of best
practices to follow when releasing your package:

```r
usethis::use_release_issue()
```

## CI with GitHub Actions

The [r-lib/actions](https://github.com/r-lib/actions) repository contains several reusable _GitHub Actions_ (GHA)
workfklows for R projects (not only packages). The [examples](https://github.com/r-lib/actions/tree/v2/examples)
directory provides complete workflows for common R project CI tasks. All of these can be easily set up using
[`usethis::use_github_action()`](https://usethis.r-lib.org/reference/use_github_action.html).

## Bioconductor

When developing an R package for the [Bioconductor project](https://bioconductor.org/), a few exceptions to the above
recommendations should be considered. Bioconductor provides
[their own list of recommendations](https://contributions.bioconductor.org/r-code.html). These are largely similar to
the _Tidyverse style guide_, with a few exceptions:

- Use of 4 spaces for indenting instead of 2
- Use of `camelCase` for function names

The reason for the latter is that Bioconductor packages make extensive use of the [S4](https://adv-r.hadley.nz/s4) OOP
framework in R. Within this framework, the convention is to use `CamelCase` for Class names and `camelCase` for method
names.

The most important of these rules are checked by
[`BiocCheck::BiocCheck()`](https://bioconductor.org/packages/release/bioc/html/BiocCheck.html) The
[_biocthis_](https://bioconductor.org/packages/release/bioc/html/biocthis.html) package provides a handy alternative to
_usethis_ for Bioconductor packages. Finally, there is a [bioc-actions](https://github.com/grimbough/bioc-actions) with
Bioconductor-specific GHA workflows.

The _biocthis_ package provides
[`biocthis::bioc_style()`](https://lcolladotor.github.io/biocthis/reference/bioc_style.html) to configure the _syler_
package with the _Bioconductor_-specific rules. You can set
`options(styler.addins_style_transformer = "biocthis::bioc_style()")` in your `~/.Rprofile` to configure these rules
globally, or in a project-specific `.Rprofile`.

### Releasing

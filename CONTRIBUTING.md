# Contributing Guide

This repository is a collection of best practices and coding standards. It has been made by [research
software engineers] at [UCL's Centre for Advanced Research Computing][UCL ARC]. Some of it is from our internal
documentation and recommendations pulled out and made public. The content is stored in [GitHub flavoured markdown], and
is rendered as a live [webpage].

Any changes should be reviewed by a member or associate member of ARC. If the additions are taken from ARC's internal
documentation, **please add the original author** as a reviewer to check that they're OK with their content being made
public under a CC-by-4.0 license. If something seems like it's broken, please go ahead and [open an issue]!

<!-- prettier-ignore -->
> [!NOTE]
> We're open for contributions from anyone but it's the UCL ARC recommended best-practices, so ulitmately it
> belongs to the software teams at ARC and we may not adopt suggestions from outside (sorry!).

## Development workflow

To contribute a change, please:

1. Create a new branch (or fork if you're not in [@UCL-ARC/collaborations]).
2. Modify an existing page, or create a new one. a. Run [pre-commit] which will lint your changes.
3. Open a _pull request_ (PR) with changes.
4. Ask someone who did not contribute to the PR from [@UCL-ARC/collaborations] to review it.
5. If approved with no comments, then the last approving reviewer should merge the PR.
6. If changes are requested, the PR author should address the comments, and then ask for review again.

<!-- links here -->

[GitHub flavoured markdown]:
  https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax
[webpage]: https://github-pages.arc.ucl.ac.uk/research-software-practices/
[UCL ARC]: https://ucl.ac.uk/arc
[open an issue]: https://github.com/UCL-ARC/coding-standards/issues/new/choose
[Research software engineers]: https://society-rse.org/about/history
[pre-commit]: https://pre-commit.com
[@UCL-ARC/collaborations]: https://github.com/orgs/UCL-ARC/teams/collaborations

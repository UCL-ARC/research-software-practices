# Python

Python code should, as a minimum, adhere to the [PEP8](http://legacy.python.org/dev/peps/pep-0008/) Python coding
standard. We also encourage compliance with modern style recommendations, such as type annotations in
[PEP484](https://peps.python.org/pep-0484/).

- As a minimum we will support the last 42 months of Python releases. This has been adopted by the wider scientific
  Python community and codified in
  [Numpy Enhancement Proposal 29](https://numpy.org/neps/nep-0029-deprecation_policy.html). If researchers require
  specific support for older versions of Python this can be offered.
- We have [separate web pages to document our Python recommendations](https://ucl-arc.github.io/python-tooling/) and we
  maintain an [ARC-recommended `cookiecutter` template](https://github.com/UCL-ARC/python-tooling), which might be a
  helpful starting point.

### Releasing

For more general information on releasing, see the [release management guide](../../project_organisation/release).

Distribute Python packages via [PyPI](https://pypi.org/) (Python Package Index):

```sh
# Install build tools
pip install build twine

# Build distribution packages
python -m build

# Upload to PyPI (requires account and API token)
python -m twine upload dist/*
```

# C++

C++ and C code should conform to [ISO C++](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines) with the
[Google style conventions](https://google.github.io/styleguide/cppguide.html) _in terms of variable and class names, and
layout_.

<details><summary>Style conflicts</summary>

We choose to follow the ISO guidelines where a Google-specific decision conflicts with the ISO.

The main example of this is the
[recommendation to throw exceptions](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Re-throw), which is
discouraged by Google. As this is recommended by ISO and not related to naming we shall throw exceptions.

</details>

We will use modern C++ features - including range-based for loops and lambda expressions - where this improves
readability. This means we prefer to work with [C++11](http://en.wikipedia.org/wiki/C++11),
[C++17](http://en.wikipedia.org/wiki/C++17), or newer.

We use the [clang-tidy](https://clang.llvm.org/extra/clang-tidy/) linter configured to obey Google style. That is:

```sh
clang-tidy  --format-style='google'
```

We also recommend using [cppcheck](https://github.com/cpplint/cpplint), a
[static analyser](https://en.wikipedia.org/wiki/Static_program_analysis). It can be helpful to improve code quality in
general.

Our preferred build system for C++ code projects is [CMake](https://cmake.org/).

## Releasing

For more general information on releasing, see the [release management guide](../../project_organisation/release).

For C++ libraries, distribution depends on your target audience:

- **Source distribution**: Tag releases on GitHub, users build from source
- **Package managers**: Submit to [vcpkg](https://vcpkg.io/), [Conan](https://conan.io/), or
  [conda-forge](https://conda-forge.org/)
- **System packages**: Create `.deb`, `.rpm`, or other system-specific packages
- **Header-only libraries**: Can be distributed as simple Git repositories

## Further reading

- More pedagogical guidance can be found in the C++ course,
  [COMP0210: Research Computing with C++](https://github-pages.ucl.ac.uk/research-computing-with-cpp).

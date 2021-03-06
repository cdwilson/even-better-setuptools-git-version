# better-setuptools-git-version

[![PackageVersion][pypi-version]][pypi-home]
[![PythonVersion][python-version]][python-home]
[![Stable][pypi-status]][pypi-home]
[![Format][pypi-format]][pypi-home]
[![License][pypi-license]](LICENSE)

[pypi-version]: https://badge.fury.io/py/better-setuptools-git-version.svg
[pypi-license]: https://img.shields.io/pypi/l/better-setuptools-git-version.svg
[pypi-status]: https://img.shields.io/pypi/status/better-setuptools-git-version.svg
[pypi-format]: https://img.shields.io/pypi/format/better-setuptools-git-version.svg
[pypi-home]: https://badge.fury.io/py/better-setuptools-git-version
[python-version]: https://img.shields.io/pypi/pyversions/better-setuptools-git-version.svg
[python-home]: https://python.org

Automatically set package version from Git. This is a re-release of
[very-good-setuptools-git-version][] with fixes and improvements, which is itself a re-release of [setuptools-git-version][]

[setuptools-git-version]: https://github.com/pyfidelity/setuptools-git-version
[very-good-setuptools-git-version]: https://github.com/Kautenja/very-good-setuptools-git-version


## Introduction

Instead of hard-coding the package version in ``setup.py`` like:

```python
setup(
    name='foobar',
    version='1.0',
    ...
)
```

this package allows to extract it from tags in the underlying Git repository:

```python
setup(
    name='foobar',
    version_config={
        "version_format": "{tag}.dev{sha}",
        "starting_version": "0.1.0"
    },
    setup_requires=['better-setuptools-git-version'],
    ...
)
```

The tool uses the semantically-latest tag as the base version. If there are no annotated tags, the version specified by `starting_version` will be used. If `HEAD` is at the tag, the version will be the tag itself. If there are commits ahead of the tag, the first 8 characters of the sha of the `HEAD` commit will be included.

In all of the above cases, if the working tree is also dirty or contains untracked files, a `+dirty` suffix will be appended to the version.

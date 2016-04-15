# Migration to Python 3 only

This document discuss some of the various possibilities to migrate Jupyter, and
its reference Kernel implementation IPython, toward a Python 3 only code base,
without breaking installation for Python 2 users.

The document is not meant to debate whether the Jupyter & IPython project should migrate
to a Python 3 only code base, but the timeline of such a migration.


# TL;DR:

  - High Priority: Fix Pip to refuse to install Python 3 only packages on Python 2. Extremely
    high priority as we want pip version to be release and propagate after
    that.
  - High Priority: Fix Setuptools to be able to express `requires-python` in `setup.py`.
  - June 2016 : Release IPython 5.0 LTS
    - Traitlets "LTS"
    - ipykernel LTS
    - ipython_genutils LTS
  - January 2017 : Release IPython 6.0 Python 3 only.
  - July 2017 : Release Notebook 6.0 Python 3 only.
  - December 2017: IPython 7.0
  - December 2017: End of active support IPython 5.x LTS
  - July 2019 : Complete end of support for IPython 5.x



# Statement of the problem

We recognize that many users of IPython and Jupyter still need to use a Python 2
environment, and will still need to do so for quite some time. However, as an open
source project, there is an overhead in maintaining Python 2 and 3 compatibility,
and this slows progress on our goals.

We also believe that Python 3 is sufficiently mature, and enough projects in
the scientific community are ready, to make the commitment to stop having new
release with active Python 2 support.

We want to provide a seamless experience to current Python 3 users, without
breaking any workflow and pipeline and installation for Python 2 users. Thus we
want in a relatively short period of time to remove the burden of supporting
Python 2 support from the core team, while preserving functionality for users
of both Python 2 and Python 3.

We also recognize that there are many companies and laboratories relying on
Python 2, and we want to offer a solution that works for them too.

# IPython 5.x LTS

IPython is the reference kernel for Jupyter. This kernel relies on
`ipykernel`, `traitlets` and `ipython_genutils`.

We propose that the next major version cycle (5.x) of IPython be the last
major version branch to support Python 2. As Python 2 is supported by the CPython core team
until 2020, we propose to make the 5.x major cycle a Long Term Support version:

  - For the 18 months following the release of IPython 5.0, the core team will
    provide critical & security bug fixes for the 5.x branch, as well as
    regular releases in the 5.x series.
    This also applies to the documentation of the 5.x branch.

  - For the 36 months following the release of IPython 5.0, the core team will
    continue to review critical & security related patches, as well as
    improvements to the documentation, and make related release if necessary. The
    core team will make sure that the 5.x version of IPython is described in
    our installation instructions.

  - The core team will fix bugs affecting IPython in the necessary versions of
    traitlets, ipykernel and ipython_genutils - IPython's first-party
    dependencies.

  - Past 36 months after the IPython 5.0 release, IPython 5.x will be considered
    unsupported.

  - These time lines are a statement of intent; they may change in the future.
    However, we do not plan to support Python 2 beyond its end of life in 2020.

  - Third parties may support IPython on Python 2 for longer, either as a
    commercial deal or in the open. IPython is BSD licensed, so anyone may
    modify and redistribute the code.

The above timeline would lead to a release of IPython 5.0 about mid 2016,
leading to active 5.x LTS support until about winter 2017, and passive LTS
support until mid 2019.

## Challenges:


### Dependencies

IPython and ipykernel rely on a few dependencies maintained by the same groups
of people, in particular: `ipykernel`, `traitlets`, and `ipython_genutils`. In
order to provide LTS support for IPython, the IPython team will provide
patches for the packages required by IPython 5.x if they
affect the behavior of IPython. Otherwise our normal conventions apply, and only
the current stable version of these packages will be supported.


### Source distribution installation.


The Python package manager (`pip`) does not respect the `requires-python`
metadata field, and `setuptools` does not provide a way to set a value of this
metadata field as far as we know. This implies that if the IPython core team release a version of
IPython that is not compatible with Python 2, a user installing IPython
by running `pip install ipython` under Python 2 will end up with a
broken installation.

There is an open issue on pip to check compatibility with Python when installing
packages:

    https://github.com/pypa/pip/issues/3182

This will not be an issue before we actually release a source version
of a package which is not Python 2 compatible, but we likely want to have
this fixed in pip as soon as possible, so that users have a chance to upgrade to
this version **before** upgrading IPython.

There are alternative ways around that, like making `ipython` a metapackage which
expresses a dependency on (say) `ipython_real`

#### Multiple source distributions

Alternatively, we could use a hidden feature of `pip`. Source distributions whose
base name ends in `-pyX.Y` are considered for installation only on a matching
Python version. Thus instead of publishing a single `.tar.gz`, we
could publish multiple identical source distribution with various names.

For supported python versions:

  - ipython-6.x-py3.4.tar.gz
  - ipython-6.x-py3.5.tar.gz

For future python versions:

  - ipython-6.x-py3.6.tar.gz
  - ipython-6.x-py3.7.tar.gz


It may be possible to patch pip to handle a more general form like
`ipython-6.x-py3.tar.gz`, so we only need to publish a single sdist.

# Notebook & Python 3 support.

The Jupyter Protocol is designed to be language agnostic, so the language the
Notebook server (or any frontend) is written in does not have to match the
language of code within a notebook.

For the next+1 version of the Notebook server (6.0), we propose to require Python 3.

The rationale being that the notebook application is one of those that can
benefit the most from recent Python improvement, such as asyncio or function annotations.

Unlike for IPython, we do not believe a LTS support is necessary, as a Python 3
only version of the notebook application can perfectly run a Python 2 kernel.

In order to allow a progressive transition to Python 3 for users and downstream
integrators, we propose to release the first Python 3 only version of the
notebook 6 months after the first release of the Python 3 only version of IPython.

We propose to clearly communicate on the next release of the notebook (5.0), that
one of the next versions will require a Python 3 environment.

Timelines:
    - Notebook 5.0 – Python 2 compatible – Summer/Fall 2016
    - IPython 6.0 – Python 3 Only – Early 2017
    - Notebook 6.0 (or 7.0) – Python 3 only – Mid 2017


## Challenges

As for IPython above; the notebook package need to be able to express that it
requires Python 3. This is mitigated by people installing `jupyter`: we can
make that conditionally depend on different version of `notebook`, depending on
the version of Python.

In particular for Anaconda, one path forward would be to bundle the
notebook with its own Python 3 interpreter. This can lead to some
inconsistency for notebook server extensions, as on Python 2 Anaconda, the
notebook server will be in a separate environment, and the notebook extensions
and optional dependencies need to be installed in this environment as well. We
are thus speaking of `nbconvert`, custom exporters, custom handler and server
side extension.

This is not a problem for most Linux package managers, where the norm is to
treat Python 2 and 3 as distinct packages. In this context, the notebook will
have a dependency on `python3`.

# Not in this roadmap:


- `nbconvert` CLI: Can likely be migrated to Python 3 only in roughly same schedule than notebook.
- `nbformat` : suggest to keep Python 2 support as long as we support IPython 5.x, maybe later, to allow people to "upgrade" their notebook and read newer version on "old" notebook.
- `jupyter_client` : Suggest keeping some Python 2 compatibility as this might be helpful for some downstream project.
- `ipyparallel`: Decision is on ipyparallel users/devs.
- `ipywidgets`
- `nbgrader`
- `jupyterhub` is already Py3 only
- `jupyter_console`


# Alternatives not discussed:

- keep Python 2 support: unless an external entity comes with sufficient
  contributions for a longer enough amount of time to IPython/Jupyter and offer
  to support Python 2, Python 2 support will be discontinued.

- Is there a way to develop using Python 3 only and have a 3to2 conversion
  process to generate Python 2 compatible versions.


# Misc

We propose to move forward with signing something similar to "no more legacy python pledge"

https://gist.github.com/brettcannon/2f6926dc6a7874478ccd

Which text should be refined and get feedback from both Python 2 and 3 supporters.


Scikit-bio rfc to drop Python 2 support:

https://github.com/biocore/scikit-bio-rfcs/blob/master/active/002-py3-only.md


 - Make it explicit on website, PyPI, GitHub, and documentations that 5.x is LTS for Python 2.
 - Make it explicit on IPython 5.x install that it is LTS, and that IPython 6.0 is/will be Python 3 only.

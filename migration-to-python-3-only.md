# Migration to Python 3 only

This document discuss some of the various possibility to migrate Jupyter, and
its reference Kernel implementation IPython toward a Python 3 only code base. 

The document is not meant to debate the Jupyter & IPython project should migrate
to a Python 3 only code base.

# TL;DR: 

  - ASAP: Fix Pip to refuse to install Python 3 only packages on Python 2. Extremely
    high priority as we want pip version to be release and propagate after
    that.
  - ASAP: Fix Setuptools to be able to express `requires-python` in `setup.py`.
  - June 2016 : Release IPython 5.0 LTS
    - Traitlets "LTS"
    - ipykernel LTS
    - ipython_genutils LTS
  - January 2017 : Release IPython 6.0 Python 3 only. 
  - July 2017 : Release Notebook 6.0 Python 3 only.
  - December 2017: IPython 7.0 
  - December 2017: End of active support IPython 5.x LTS
  - July 2019 : Complete end of support for IPython 5.x



# Exposition of the problem

We recognize that many user of IPython and Jupyter still need to use a Python 2
environment, and will still need to do so for quite some time. Though as an open
source project, the overhead in maintaining both Python 2 and 3 compatibility at
the same time is significant, and slow the Jupyter and IPython open-source teams
to achieve many of our goals.

We also believe that the maturity of Python 3 is sufficient enough, and a
sufficient number of project in the scientific community are ready to make the
commitment to drop Python 2 support.

We want to provide a seamless experience to current Python 3 users without
breaking any workflow and pipeline for Python 2 users. Thus we want in a
relatively short period of time to remove the burden of support ting Python 2
support from the core team, while preserving functionality for users. 

We also recognize that companies and laboratories may rely on Python 2, and
want to offer solution for these too, whether they directly use, or sell
product relying on Jupyter and IPython.

# IPython 5.x LTS

This part concern the reference kernel implementation of Jupyter, also know as
IPython. This specific kernel implementation also rely on `ipykernel`, `traitlets`
and `ipython_genutils`.

We propose that the next major version cycle (5.x) of IPython be the last
version to support Python 2. As we recognize that Python 2 is supported by the
CPython core team until 2020, we propose to make the 5.x major cycle a Long
Term Support version under the following intent:

  - For the 18 month following the release of IPython 5.0, the core team will
    engage in critical & security bug fix for the 5.x branch, as well as
    regular release (both of minor and patch revision) of IPython 5.x branch.
    This apply also to the documentation of the 5.x branch. THe core team will
    also accept to provide reasonable support requests for the IPython 5.x
    branch.


  - For the 36 month following the release of IPython 5.x, the core team will
    continue to review critical & security releated patches, as well as
    improvment to the documentation, and make related release if necessary. The
    core team will make sure that the 5.x Version of IPython stay visible
    various web pages mentionning how to get IPython. The core team reserve the
    right to ignore and or close any support request, request for patch
    integration or other communication that oes not go into the previous
    category.

  - The IPython/Jupyter team will do a best effort to provide fixes in the
    realm of reasonable requests, and will actively try to provide upstream
    patches if IPython missbehavior is due dependedncies, unless otherwise
    specified. I.E, we will backport and release fix to traitlets, and
    ipykernel only if it dirrectly affect IPython

  - pass 36 month after IPython 5.0 release, IPython 5.x will be considers
    unsupported.

  - The above time lines are intent, and the IPython core team reserve the
    right to modify them in the future.

  - regardless of above statement, Python 2 support in the 5.x branch will not
    exceed support of CPython 2.7, and be likely much shorter.

  - The above statements do not apply to third party who are welcome to provide
    open or commercial support for IPython.

The above timeline would lead to a release of IPython 5.0 about mid 2016,
leading to active 5.x LTS support until about winter 2017, and passive LTS
support until Mid 2019.

## Challenges:


### Dependencies

IPython and ipykernel rely on a few dependencies maintained by the same groups
of people, in particular: `ipykernel`, `traitlets`, and `ipython_genutils`. In
order to provide LTS support for IPython, the IPython team, will provide
patches for the packages requires by IPython 5.x at the condition that they
affect the behavior of IPython. Otherwise the normal rules apply, where only
the stable version of these software is supported, without guaranties of timeline.


### Source distribution installation.


The Python package manager (`pip`) does not respect the `requires-python`
metadata field, and `setuptools` does not provide a way to set a value of this
metadata field as far as we know. This implies that if the IPython core team release a version of
IPython that is not compatible with IPython, the end use installing ipython
through `pip install ipython` or equivalent under python 2, will end up with a
broken installation.

The we need to to fix at least the following issues for this to work:

    https://github.com/pypa/pip/issues/3182

Note that this will not be an issue before we actually release a source version
of a package which is not Python 2 compatible, but that we likely want to have
this fixed in pip as soon as possible so that users have a chance to upgrade to
this version **before** upgrading IPython.

There are alternative ways around that, like have IPython being only a meta package, 





# Notebook & Python 3 support. 

The way the Jupyter Protocol is designed, it is language agnostic, thus it is
perfectly possible to imagine that the notebook server (in particular), could
be written in a non-python language. 

For the next+1 version of the Notebook (6.0), we propose to require a Python 3 environment. 

The rational being that the notebook application is one of those that can
benefit the most from recent Python improvement, being asyncio, `yiield from`, etc. 

Unlike for IPython, we do not believe a LTS support is necessary, as a Python 3
only version of the notebook application can perfectly run a Python 2 kernel.
Thus a Python 3 only version of the notebook is technically not really dropping Python 2.

In order to allow progressive transition to Python 3 for users and downstream
integrators, we propose to release the first Python 3 only version of the
notebook 6 month after the first release of the Python 3 only version of IPython. 

We propose to strongly communicate for next release of the notebook (5.0), that
one of the next version will require a Python 3 environment. 

Timelines:
    - Notebook 5.0 – Python 2 compatible – Summer/Fall 2016
    - IPython 6.0 – Python 3 Only – Early 2017
    – Notebook 6.0 (or 7.0) – Python 3 only – Mid 2017.




## Challenges

As for IPython above; the notebook package need to be able to express that it
requires Python 3. This is mitigated by people installing `jupyter` that we can
make conditionally depend on different version of the notebook depending on the
version of Python. 

In particular for Anaconda, one of the path forward would be to bundle the
notebook with its own python 3 interpreter. This can lead to small
inconsistency for notebook server extensions, as on Python 2 Anaconda, the
notebook server will be in a separate environment, and the notebook extensions
and optional dependencies need to be installed in this environment as well. We
are thus speaking of `nbconvert`, custom exporters, custom handler and server
side extension.

The anaconda crew told us that dropping support for Python 2 will lead them to
unbundle Jupyter from Anaconda instead of using the 2 environment trick.

This is not a problem on linux and unix-like system where notebook will "just" requires Python 3. 

# Not in this roadmap:


- `nbconvert` CLI: Can likely be migrated to Python 3 only in roughly same schedule than notebook. 
- `nbformat` : suggest to keep Python 2 support as long as we support IPython 5.x, maybe later, to allow people to "upgrade" their notebook and read newer version on "old" notebook. 
- `jupyter_client` : Suggest keeping some Python 2 compatibility as this might be helpful for some downstream project. 
- `ipyparallel`: Decision is on ipyparallel users/devs.
- `ipywidgets`
- `nbgrader`
- `jupyterhub` is already Py3 only
- `jupyter_console`


# Misc

We propose to move forward with signing the "no more legacy python pledge"

https://gist.github.com/brettcannon/2f6926dc6a7874478ccd





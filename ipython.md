## IPython

IPython is comparatively mature, and there are consequently fewer major changes
planned. However, we plan to:

### IPython 5.0

Released planned mid 2016.

#### Switch to prompt toolkit.

Switch from readline to prompt_toolkit for terminal interaction; this should
simplify installation and provide a richer experience in the terminal.
The switch to `prompt_toolkit` will also imply dropping the readline interface.

#### Last IPython version compatible with Python 2 and LTS

See [Migration to Python 3 only document](accepted/migration-to-python-3-only.md),

IPython 5.0 would be the last version to work on Python 2. Active long term support
is planned until Fall/Winter 2017, and passive support until mid 2019.


### IPython 6.0


#### Refactor tab completion:

  Refactor the completion machinery, and investigate using
  [Jedi](https://jedi.readthedocs.org/en/latest/) for completing in regular
  Python code (separate completion machinery is still needed for our special
  syntax).

#### Drop Python 2

 - Deletion and removal of various Python 2 shims  and code path.
 - Make sure upgrade process does not upgrade on Python 2.

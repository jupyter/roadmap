## Jupyter Qt Console

- The functionality of the Qt Console is being implemented inside JupyterLab.
- The goal of the initial version of the JupyterLab console is feature parity
  with the Qt Console application.
- The JupyterLab console will also support any cells that a notebook can render.

### Next
- There is currently no "save session" functionality. There are several ways the
  mechanics of saving the content of a console session might be implemented. A
  discussion of its semantics may be fruitful and may lead to an interesting
  "save" feature for the next version.
- A full replacement of the Qt Console application may require wrapping the web
  version in a native application in the next version.

# Project Jupyter Roadmap

The following is a very rough outline of the roadmap for Project Jupyter and IPython.
Historically, we have published major releases every 6-9 months. With our project now
split across many subprojects, we expect to release subprojects separately and more
often.

This roadmap only includes mainline subproject under the Jupyter
(https://github.com/jupyter) and IPython (https://github.com/ipython) GitHub orgs. We
also have a number of newer, experimental subprojects in the Jupyter Incubator
(https://github.com/jupyter-incubator) organization.

## Notebook

### Next (4.1)

* Multi-cell selection and actions.
* Notebook wide find and replace.
* Command palette.
* Restart kernel and run all.

### Next+1 (5.0)

* Prototype of the *Jupyter Workbench*:
  - Initially, a new page in the existing notebook web-app that allows multiple
    components on the same browser tab.
  - Flexible, custimizable tabbed and paneled layout system.
  - File browser.
  - Text editor.
  - Terminal.
* All new frontend work is being done as small, loosely coupled npm packages.
* The entire Jupyter Workbench will be a set of plugins (again just npm packages)
  that exchange runtime APIs.
* Application infrastucture (keyboard shortcuts, commands, menus, layout), view
  layer, and other utilities (signals, properties, messages) provided by phosphorjs
  (http://phosphorjs.github.io/).
* Models and views that can be used on any web page in the following repos:
  - https://github.com/jupyter/jupyter-js-services
  - https://github.com/jupyter/jupyter-js-terminal
  - https://github.com/jupyter/jupyter-js-editor
  - https://github.com/jupyter/jupyter-js-filebrowser
  - https://github.com/jupyter/jupyter-js-input-area
  - https://github.com/jupyter/jupyter-js-output-area
  - https://github.com/jupyter/jupyter-js-cells
  - https://github.com/jupyter/jupyter-js-notebook
* Wrapping of those models and views as plugins for the Jupyter Workbench
  - https://github.com/jupyter/jupyter-js-services-plugin
  - https://github.com/jupyter/jupyter-js-metaservice-plugin
  - https://github.com/jupyter/jupyter-js-output-area-plugin
  - https://github.com/jupyter/jupyter-js-notebook-plugin
  - https://github.com/jupyter/jupyter-js-terminal-plugin
  - https://github.com/jupyter/jupyter-js-editor-plugin
  - https://github.com/jupyter/jupyter-js-filebrowser-plugin
* Movement towards having stable, documented JavaScript APIs.
* Ability to hide/show code and entire cells based on query syntax.

### Next+2

* New plugins for the Jupyter Workbench:
  - Standalone output area.
  - Ability to hook kernels up to text editors and output areas.
  - Themes.

### Future

* New plugins for the Jupyter Workbench:
  - Notebook.
  - Variable inspector.
  - UI for managing plugins.
* Dashboarding of output areas and interactive widgets.
* Replace existing pages in the notebook web-application by the Jupyter Workbench.
* Interactive debugger.
* Real-time collaboration on notebooks, text-editors and other plugins.
* Perform and publish accesibility audit by running an automated tool.
* Bring our core plugins up to the level of the Web Accessibility Standards
  (http://www.w3.org/standards/webdesign/accessibility)

## ipywidgets

### Next (4.1)

* Improved and consistent visual style of built-in widgets.
* Better abstractions for styling widgets using CSS and doing layout with flexbox.
* Ability to run ipywidgets outside of the notebook.
* Initial refactoring to start to use npm for packaging the JavaScript code.

### Future

* Further decoupling of the JavaScript and Python kernel backend.
* Replace views based on backbone.js with phosphorjs widgets.
* Wrap backbone models into standardized interfaces.
* Transition to ES6/TypeScript.
* Ability to pop-out widgets to the top-level of the Jupyter Workbench UI.

## traitlets

### Next (4.1)

* Much nicer, decorator based APIs for observing (`@observe`), validating
  (`@validate) and providing defaults (`@default) for traits.
* Looking forward to its usage in Matplotlib.

## nbconvert

### Future

* Implementations in either node.js or Pandoc.
* Exporter for EPUB.

## JupyterHub

## Deployment

## IPython kernel

## nbgrader

## nbviewer

## Notebook document

## Message specification

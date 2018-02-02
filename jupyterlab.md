## JupyterLab

## Beta Release
* Flexible, customizable tabbed and paneled layout system.
* All of JupyterLab will be a set of plugins that exchange runtime APIs.
* Initial plugins:
  - Menu bar.
  - Overall page layout.
  - File browser.
  - Text editor.
  - Terminal.
  - Notebook.
  - Console.
* Application infrastucture (keyboard shortcuts, commands, menus, layout), view
  layer, and other utilities (signals, properties, messages) provided by phosphorjs
  (http://phosphorjs.github.io/).
* JupyterLab now has its own GitHub organization: https://github.com/jupyterlab
* Movement towards having stable, documented JavaScript APIs.
* Usability and UX User survey to help us guide the design process of JupyterLab.
* Draggable standalone output area.
* Ability to hook kernels up to text editors.
* Cell drag and drop


## 1.0 Release
* Feature parity with the classic notebook. We are tracking notebook feature parity issues with a combination of [labels](https://github.com/jupyterlab/jupyterlab/issues?q=is:open+is:issue+label:"tag:Feature+Parity"+label:pkg:Notebook).
* Settings system.
* Work on porting nbextensions to JupyterLab and building the bridge layers.
* Theme switching.
* Ability to hook kernels up to output areas.


## Future
* Variable inspector.
* UI for managing plugins.
* Real-time collaboration on the notebook, text editor, and other plugins.
* Perform and publish accesibility audit by running an automated tool.
* Bring our core plugins up to the level of the Web Accessibility Standards
  (http://www.w3.org/standards/webdesign/accessibility)
* Address the [2015 UX survey findings](https://github.com/jupyter/design/blob/master/surveys/2015-notebook-ux/analysis/report_dashboard.ipynb)
    * Version control (via git in particular)
    * Robust text and code editing (like in Emacs, Vim, Sublime, PyCharm)
    * Advanced code development tools (debugging, profiling, variable watching, code modularization)
    * Simpler export and deployment options (one-click transformations to slides, scripts, reports)
    * Improved installation guides, usage tutorials, and within-tool help

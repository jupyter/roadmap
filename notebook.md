## Notebook

### Next (4.1)

* Multi-cell selection and actions.
* Notebook wide find and replace.
* Command palette.
* Restart kernel and run all.

### Next+1 (5.0)

* Prototype of *JupyterLab*:
  - Initially, a new page in the existing notebook web-app that allows multiple
    plugins in the same browser tab.
  - Flexible, customizable tabbed and paneled layout system.
  - Initial plugins:
    - Menu bar.
    - Overall page layout.
    - File browser.
    - Text editor.
    - Terminal.
* All new frontend work is being done as small, loosely coupled npm packages.
* All of JupyterLab will be a set of plugins (again just npm packages)
  that exchange runtime APIs.
* Application infrastucture (keyboard shortcuts, commands, menus, layout), view
  layer, and other utilities (signals, properties, messages) provided by phosphorjs
  (http://phosphorjs.github.io/).
* Here is a list of all the repositories in which we are developing JupyterLab:
  - https://github.com/jupyter?utf8=%E2%9C%93&query=jupyter-js
* Movement towards having stable, documented JavaScript APIs.
* Usability and UX User survey to help us guide the design process of JupyterLab.
* Ability to hide/show code and entire cells based on query syntax.
* Plan for Phased JupyterLab releases:
	* Phase 1:
	  * A series of major releases starting with 5.0 that will have the existing notebook pages as the main UI with a JupyterLab button that takes people to the new JupyterLab page
	  * These releases may have new features in the existing notebook pages, some API changes, focus on transitioning to JupyerLab.
	  * These releases will have bug fixes and new features in JupyterLab designed to get JupyterLab to  Phase 2.
	  * During this phase, we will continue to work on porting nbextensions to JupyterLab and building the bridge layers.
	  * Explicit that people can request help for porting extensions.
	  * *Criteria for transition to phase 2:*
		1. Jupyter Lab has all the primary functionality of the classic notebook interface.
		1. Jupyter Lab offers some interesting features beyond the classic interface.
		1. At least some important, popular extensions are ported / bridged to Jupyter Lab.
		1. Documentation and examples exist for creating Jupyter Lab plug-ins.
	* Phase 2:
	  * A series of major releases that will have JupyterLab as the main UI and the old notebook is available as a button
	  * At this point, we start to discourage the development of new features in the existing notebook.
	  * *Criteria for transition to phase 3:*
		1. No major development or use of the classic UI.
	* Phase 3:
	  * Starting with the z.0 major release. will remove the existing notebook pages.
	  * Maybe offer the existing notebook as a server extension.

### Next+2

* New plugins for JupyterLab:
  - Standalone output area.
  - Ability to hook kernels up to text editors and output areas.
  - Themes.

### Future

* New plugins for JupyterLab:
  - Notebook.
  - Variable inspector.
  - UI for managing plugins.
* If, and only if, JupyterLab becomes a full replacement, deprecate existing pages in the notebook
  web-application.
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

## Notebook

### Next (4.1)

* Multi-cell selection and actions.
* Notebook wide find and replace.
* Command palette.
* Restart kernel and run all.

### Next+1 (5.0)
* Ability to hide/show code and entire cells based on query syntax.
* Plan for Phased Notebook/JupyterLab releases:
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

* If, and only if, JupyterLab becomes a full replacement, deprecate existing pages in the notebook web-application.

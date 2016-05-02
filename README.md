# Project Jupyter Roadmap

The following is a very rough outline of the roadmap for Project Jupyter and IPython.
Historically, we have published major releases every 6-9 months. With our project now
split across many subprojects, we expect to release subprojects separately and more
often.

This roadmap only includes mainline subprojects under the Jupyter
(https://github.com/jupyter) and IPython (https://github.com/ipython) GitHub orgs. We
also have a number of newer, experimental subprojects in the Jupyter Incubator
(https://github.com/jupyter-incubator) organization.

In this roadmap, we refer to the future major releases as follows:

* Next (the next major release)
* Next+1 (the major release after that)
* Future (any release beyond the Next+1)

This reflects the inherent uncertainty in releases that are more than about 1 year away. In
some cases, if progress is made more quickly, features may be moved to earlier releases.

## Documentation

We list documentation as a top-level section in our roadmap to acknowledge the importance
of it for developer communication, scaling and maintenance of deployments, and early user
adoption of new releases. The state of the existing documentation has not kept pace with
the rapid development in our projects, and effort will be focused on improving it. Because
our documentation spans all subprojects, each of which have their own release cycles and
versioning, the documentation roadmap doesn't have concrete version numbers associated with
each milestone.

### Next

* Hire full time and part time staff who will focus on improving our documentation.
* Research existing tools for writing documentation (Readthedocs, Sphinx, Notebooks, etc.)
  and evaluate which tools we use to write documentation.
* Develop a project wide outline of our existing and proposed documentation.
* Perform observational and survey based user studies of our documentation to guide its
  design and development.
* Explore and research the questions around how to maintain documentation across multiple
  subprojects. Do we centralize all or some of our documentation? Do we keep it in separate
  subproject repos?
* Build publicly accessible API documentation on all commits for all JavaScript and
  TypeScript repositories.
* Encode documentation in our project principles and community process as a core activity
  that is part of the everyday process of development, and adopt this in an integral
  fashion throughout the project for all project members.

### Next+1

* Integrate Jupyter Notebooks more closely into our documentation tools.
* Develop a formal documentation process and standard that includes technical review,
  organizational review, design, usability testing and copy-editing.* Where needed, develop
  additional tools for writing our documentation.
* Work with each subproject to integrate our documentation tools and process into their
  workflow and roadmap.

### Future

* Begin to block releases of subprojects until documentation meets our standards.
* Using our new JavaScript packages and live kernels hosted in the cloud, enable
  documentation to be runnable in place.
* Build documentation indexing and search into JupyterLab.
* Build tools that make it easier for downstream projects to distribute notebook based
  documentation to users.

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
      
## ipywidgets

### Next (5.0)

* Improved and consistent visual style of built-in widgets.
* Hands off approach to styling.  ipywidgets only provides an API for
  adding/removing CSS classes and the Style API.  The Style API provides the
  ability to set layout CSS traits in a mutable fashion. All other styling APIs
  are deprecated.
* Include a new interact API that behaves like Sage's equivalent.
* Use npm for packaging the JavaScript code as `jupyter-js-widgets`.
* Use the new notebook nbextension mechanism, introduced in Jupyter notebook 4.2
  for the widgetsnbextension package, which will contain all of the notebook
  specific widget Javascript.
* Include two mechanisms for exporting widgets to static formats, rasterized
  screencaptures of the widgets and an embed widget manager which is capable of
  rendering widgets outside of the notebook.
* Add examples for using the widgets outside of the notebook.
* Add narrative docs describing the widgets basic usage and low level widget
  spec information.

### Next+1 (6.0)

* Unit tests for jupyter-js-widgets individual widgets
* Unit tests for widgetsnbextension, especially manager.js
* Enable a modern transpiler, either ES6 or TypeScript.  Gradually transition
  the code as we make changes elsewhere.
* Evaluate and possibly transition the codebase to use modern Javascript
  standards.  Linting tools (i.e. eslint) should be used to assist developers
  into complying to said standard.
* Integrate framework/foundation classes of the Declaritive Widget incubator
  directly into jupyter-js-widgets and ipywidgets.
* Shrink the jupyter-js-widgets codebase using well adopted Javascript libraries
  installed via npm.
* Treat widgets as regular output, and not have to have a separate widget area
  in the DOM.
* Remove dependency on jQuery, jQuery UI, and bootstrap.
* Integrate existing widgets with JupyterLab.
* Explore mechanisms to allow Phosphor views to be used directly with
  jupyter-js-widget models.
* Allow widgets to be used at the top-level of the JupyterLab UI to create dashboards.
* Give the widgets a facelift.  Maybe material-ui?  Home spun design?
* Add more synchronized events.  In the process, investigate slicker ways to do
  cross context event synchronization.
* Investigate making the model layer of widgets more symmetric, allowing
  widgets to be created, with traits, entirely in the front-end.

### Future

* Extract the widget module synchronization layer into it's own generic project,
  maybe renaming to "XObject" or something similar along the way.  The existing
  widgets will remain as-is, but will connect to this layer instead of to comms
  directly.

* Regarding embeddable widgets, enable a mechanism for it to work with custom widget models and views to without having to manually put more with script tags on the page. We discussed multiple approaches during our meeting on the integration of a module version number so that we could compose npmcdn urls for custom models.

* Datetime and Date traits with serialization + Date picker and date time picker. The date traits should work with the time-zone issues between browser and backend as discussed earlier.

* Use jupyter-js-outputarea for the ouput widget.


## Declarative widgets

### Next

* Decide where to draw the line between Web Components specific functionality and generic code that should live closer to ipywidgets / jupyter-js-widgets to prevent future breakage.
* Migrate generic, JS modules to jupyter-js-widgets (may be a no-op).
* Graduate the declarativewidgets from the incubator.  Specifically the move jupyter-incubator/declarativewidgets code to jupyter/jupyter-web-components or another appropriately named repo.
* Investigate with the jupyter/notebook team about upstreaming a generic bower/npm restful API.
* Determine the best location for kernel specific code. A possible options it to move Python bits under ipywidgets, move the R code into the IRkernel and the Scala code into Apache Toree or related project.

## traitlets

### Next (4.1)

* Much nicer, decorator based APIs for observing (`@observe`), validating
  (`@validate) and providing defaults (`@default) for traits.
* Looking forward to its usage in Matplotlib.

## nbconvert

### Next (4.2)

* Bring examples of nbconvert functionality that exists in locations like @takluyver's
  demos from last summer's Southampton workshop into the official docs.

### Future

* Explore implementing nbconvert using Pandoc extensions.
* Explore implementing the html output of nbconvert using node.js and the various npm packages we are creating to avoid reimplementing all of the HTML logic.
* Implement an exporter for EPUB.

## JupyterHub

### Not tied to releases

JupyterHub constellation of repos may move to top-level jupyterhub org on GitHub.

- jupyterhub itself
- spawners
- authenticators
- reference deployments
- configurable-http-proxy

#### Reference Deployments

Start with two reference deployments:

- common best practices
    - letsencrypt
    - nginx out front
    - postgres for db
- single machine nbgrader, no docker
    - ansible
    - local users, optionally GitHub auth
    - based on Brian's https://github.com/calpolydatascience/jupyterhub-deploy-data301
- docker, no nbgrader
    - docker-compose
    - GitHub OAuth


### Next (0.7)

The main feature of 0.7 will be the addition of Services.

- A Service is a process that interacts with JupyterHub and is managed by the Hub process.
- A service MAY:
   - use the Hub REST API with an authentication token
   - run an HTTP server that is added to the Hub proxy
   - authenticate HTTP requests with GitHub users in a manner similar to the single-user server
- Enhancements will include:
   - The ability to launch services, provided an auth token for the REST API as a specified user
   - An importable implementation of authentication with the Hub
- Examples:
   - `cull_idle_servers` example script which shuts down servers that have been idle for a period of time
    - uses Hub REST API as an administrator for starting
   - nbgrader formgrader
     - uses Hub auth to specify graders
  - Hub statistics (compmodels/stats)


### Next + 1 (0.8)

The main feature of 0.8 will be the addition of a sharing service.

Users should be able to:

- Push a project to other users.
- Get a checkout of a project from other users.
- Push updates to a published project.
- Pull updates from a published project.
- Manage conflicts/merges by simply picking a version (our/theirs)
- Get a checkout of a project from the internet. These steps are completely different from saving notebooks/files.
- Have directories that are managed by git completely separately from our stuff.
- Look at pushed content that they have access to without an explicit pull.
- Define and manage teams of users.
  - Adding/removing a user to/from a team gives/removes them access to all projects that team has access to.
- Build other services, such as static HTML publishing and dashboarding on top of these things.
- Enter into real-time collaboration mode for a project that starts a shared execution context.

### Future

- Once the single-user notebook package supports realtime collaboration,
  implement sharing mechanism integrated into the Hub.

## Deployment

- provide reference "best practice" deployment of JuptyerHub, via Ansible scripts or otherwise

## IPython

IPython is comparatively mature, and there are consequently fewer major changes
planned. However, we plan to:

* Switch from readline to prompt_toolkit for terminal interaction; this should
  simplify installation and provide a richer experience in the terminal.
* Refactor the completion machinery, and investigate using
  [Jedi](https://jedi.readthedocs.org/en/latest/) for completing in regular
  Python code (separate completion machinery is still needed for our special
  syntax).

## Dashboarding

### jupyter/enhancement-proposals (now)

* Create an enhancement proposal to define an extensible layout metadata schema within the Jupyter notebook document format.
    * Use the jupyter-incubator/dashboards and Anaconda-server/nbpresent metadata as a guide for what needs to be supported.

### jupyter-incubator/dashboards (0.6.0)

* Update the incubator extension to work with the new schema and deprecate support for the older `urth.layout` schema.
* Submit an enhancement proposal to graduate the project from incubator as a "classic" Jupyter Notebook extension.

### jupyter-js-plugins (>0.16.0)

* Implement a dashboard layout editor/viewer in Jupyter Lab compatible with the layout metadata schema and jupyter-incubator/dashboards use of that schema to layout dashboards.
* Improve upon the layout authoring experience afforded in the "classic" Notebook by taking advantage of the multi-view capabilities of the Jupyter Lab interface.

### jupyter/notebook (>4.2)

* Add a URL in the single user notebook server that shows a rendered dashboard given a notebook that follows the layout metadata schema.
    * TBD what renderer implementation does the rendering at the URL (e.g., new Jupyter Lab code?)
* Possibly bundle the `jupyter/dashboards` extension in a Jupyter Notebook release.

### jupyter-incubator/dashboards_bundlers, jupyter-incubator/dashboards_server

* For now, continue to explore the bundling and external deployment of notebooks as dashboards in incubator (e.g., security beyond trusted users).

## nbgrader

## nbviewer

## Notebook document

## Kernel specification

Implement a way for static resources (js, css, images, etc.) to be fetched based on the kernel for use by frontends (notebook, thebe, etc.).

## Message specification

## Community Pipeline

### Next

- Metrics: looking at contributions (e.g. percent from non-maintainers,
  distribution of number of contributions)
- Create a basic "overview of Jupyter" page with at least a listing of all the
  projects in the Jupyter repo plus a short description of each
- Create the common development guide for all Jupyter projects
- Create the repo maintainer checklist and identify which repos need to add
  which things from the checklist. Carol will take a first pass at this.
- Come up with a checklist/cheatsheet for developers. This should include things
  like the repo maintainer checklist as well as a guidelines for how to respond
  to issues and PRs, conduct, etc. This should be linked to from the Jupyter
  incubation instructions and from the development guide.
- Create thoughtful replies for common reasons that a PR might be closed (e.g.
  pep8 changes). We can't actually use the GitHub saved replies for this because
  those are per-person rather per repo, but we can write a template for people
  to use at least.

### Next + 1

- Continue fleshing out the "overview of Jupyter" page and include things like:
  * a dependency tree
  * better descriptions of how the projects relate to each other
  * status indicators
- All projects should link to the common development guide and should satisfy
  all of the maintainer checklist requirements.
- Grant access to 1 or 2 people who are not maintainers to be issue triagers --
  this will just involve labeling issues as they come in and going back through
  old PRs/issues periodically.
- Include in the newsletter both a "maintainer of the month" (someone with
  commit bits) and a "contributor of the month" (someone without commit bits)
- Include in the newsletter a list of new contributors since the last newsletter

### Future

- Create a bot to take actions on issues based on labels (e.g. "duplicate" gets
  closed automatically).
- Create a mentorship mailing list (based on the Python Core Mentorship mailing
  list) for new contributors to ask questions

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

* Regarding embeddable widgets, enable a mechanism for it to work with custom widget models and views to without having to manually put more with script tags on the page. We discussed multiple approaches during our meeting on the integration of a module version number so that we could compose unpkg urls for custom models.

* Datetime and Date traits with serialization + Date picker and date time picker. The date traits should work with the time-zone issues between browser and backend as discussed earlier.

* Use jupyter-js-outputarea for the ouput widget.


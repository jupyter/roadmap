## Declarative widgets

### Next

* Decide where to draw the line between Web Components specific functionality and generic code that should live closer to ipywidgets / jupyter-js-widgets to prevent future breakage.
* Migrate generic, JS modules to jupyter-js-widgets (may be a no-op).
* Graduate the declarativewidgets from the incubator.  Specifically the move jupyter-incubator/declarativewidgets code to jupyter/jupyter-web-components or another appropriately named repo.
* Investigate with the jupyter/notebook team about upstreaming a generic bower/npm restful API.
* Determine the best location for kernel specific code. A possible options it to move Python bits under ipywidgets, move the R code into the IRkernel and the Scala code into Apache Toree or related project.

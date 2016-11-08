## Dashboarding

Discussed during the Spring 2016 dev meeting.

### Graduate jupyter/dashboards from Incubator

The [dashboards wiki](https://github.com/jupyter-incubator/dashboards/wiki) summarizes the current scope of the dashboarding effort in jupyter incubator. We discussed graduation of these assets and agreed on the following rough steps.

1. Create an enhancement proposal to define an extensible layout metadata schema within the Jupyter notebook document format.
    * Use the jupyter-incubator/dashboards and Anaconda-server/nbpresent metadata as a guide for what needs to be supported.
    * https://github.com/jupyter/enhancement-proposals/pull/15
2. Update the incubator projects to work with the new schema and deprecate support for the older `urth.layout` schema.
    * https://github.com/jupyter-incubator/dashboards/wiki/Dashboard-Metadata-and-Rendering
    * https://github.com/jupyter-incubator/dashboards/issues/243
3. Submit an enhancement proposal to graduate the jupyter-incubator/dashboards project from incubator as a "classic" Jupyter Notebook extension.
    * Will be submitted when [v0.6.0 is released](https://github.com/jupyter-incubator/dashboards/milestones/0.6.0)
4. For now, keep the other two dashboard projects ([jupyter-incubator/dashboards_bunders](https://github.com/jupyter-incubator/dashboards_bundlers) and [jupyter-incubator/dashboards_server](https://github.com/jupyter-incubator/dashboards_server)) in incubator to continue exploration of the bundling and external deployment of notebooks as dashboards in incubator (e.g., security beyond trusted users).

### Dashboarding Support in Jupyter Lab

We also discussed actions to be taken post-graduation, primarily with respect to dashboarding support in Jupyter Lab. We agreed on the following rough steps.

1. Implement a dashboard layout editor/viewer in Jupyter Lab compatible with the layout metadata schema and jupyter-incubator/dashboards use of that schema to layout dashboards.
2. Improve upon the layout authoring experience afforded in the "classic" Notebook by taking advantage of the multi-view capabilities of the Jupyter Lab interface.
3. Add a URL in the single user notebook server that shows a rendered dashboard given a notebook that follows the layout metadata schema.
    * TBD what renderer implementation does the rendering at the URL (e.g., new Jupyter Lab code?)
4. Possibly bundle the `jupyter/dashboards` extension in a Jupyter Notebook release.

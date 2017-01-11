# Improving Jupyter for Spark

Exploring where Jupyter protocols, formats, and UI need to adapt to make it so that “integration with Spark” is seamless. The word “Spark” could likely be replaced with “TensorFlow” or “Dask” throughout all of this issue.

This is a culmination of feedback, in progress initiatives, and further R&D that needs to be done to improve how Jupyter provides a wonderful ecosystem for Spark, Hadoop, and other cluster tooling.

## Asynchronous/Background Outputs ✅

For environments like Spark and Dask, when a job or multiple jobs are submitted, they provide a progress bar for the jobs with a way to cancel the overall job. They also provide links to external UI (Spark UI or Dask UI). When finished, you’re able to see the resulting table view.

There’s a similar use case for Hive Jobs, Presto Jobs, etc.

As far as Jupyter is concerned, there are things we can do to make updating a display like this easier without having to use widgets:
- Routing background outputs: https://github.com/ipython/ipython/issues/9969
- Ability to update prior displays: https://github.com/jupyter/jupyter_client/issues/209

Progress:

* [Outputs can now be updated by named display](https://github.com/jupyter/jupyter_client/issues/209)

## Progress Bar Primitives

As discussed above in the Async Outputs section, we should seek to provide simple clean-cut library tooling for creating progress bars in the frontend. This is not to seek a replacement of e.g. [tqdm](https://github.com/noamraph/tqdm), but to provide the necessary additions to the messaging spec (whether an actual message or a specific versioned mimetype).

The nested structure for Spark Jobs is something we can likely represent with a clean format for nested content with progress bars and external links.

Approaches:

- https://github.com/mozilla/jupyter-spark
- [Progress monitor](https://github.com/jupyter/jupyter_client/issues/209#issuecomment-260789525)

## Cluster/computational Context

Users need a way to get context about their running spark setup, because you’re dealing with an extra remote resource beyond the kernels. They tend to want to know:
- What cluster am I attached to?
- What resources do I have (memory, CPU, Spark version, Hadoop version)?
- How do I access the UI/logs for that cluster?

Many users want to think in terms of “clusters” and a notebook that is attached to that cluster. The real distinction is

notebook ← → kernel ← → cluster (or other background resources)

This can be a cognitive burden for the user. One way of solving this is to have “kernels” that are assumed to be attached to clusters.

## Kernel Startup and Background Resources

Stages a spark user cares about when opening a notebook and running first cell:

- Runtime started (kernel)
- Preparing driver/Attaching to cluster $NAME/preparing Spark Context
- Libraries uploading
- Attached to cluster $NAME/Spark ready

This seems to me like additional startup messages from the kernel (yes, new message spec) about driver context.

We do have a banner for kernel_info, perhaps we can do banner updates with links to:

- Cluster/driver logs
- Spark UI/Dask UI

## Uploading libraries

For a user of Spark, they need a way to upload JARs to the current spark cluster (and, many times, they need to restart the spark cluster).

This is out of scope for the Jupyter protocols, would need to be implemented on the outside of the notebook. We need to be able to provide more context, likely through the kernel, about the operating environment and how the cluster is initialized for each kernel.

Unsure of what/how we can handle this, needs exploration.

## Timing Data

The transient information for how long a command took (as well as the user) are available in the message spec, but not persisted to the notebook document. We can certainly show this in the UI, but there is another reason for keeping this output consistent in serialized state:

- Lifecycle management of notebooks -- need to be able to know if execution results are stale relative to data, APIs, etc.
- In multi-user collaboration, this must be shared amongst all clients

This is super useful, and part of why it’s in the message spec. An earlier implementation of IPython notebooks (2006) included and displayed all of this information. We found the information useful enough to keep it in the current protocol implementation, but not enough to put it in the UI or persist it to disk.

Downsides of storing it in the document:

- 100% chance of every re-run causing git changes, merge conflicts

Options: opt-in ‘provenance mode’, where we persist a whole bunch of extra metadata. Super unpleasant for version control, but useful in notebooks that run as jobs, especially for analysts.

## Tables and Simple Charts

For many people, being able to plot simple results before getting to deeper visualization frameworks is pretty important: e.g. in pandas we can use the `df.plot()`, `.hist()`, `.bar()`, etc. methods for quick and easy vis.

There are a couple approaches to this right now, including mime types for plotly and vega being available and easy to use in both nteract and jupyterlab. For tables, there is an open discussion on Pandas: https://github.com/pandas-dev/pandas/issues/14386

There's also the [spark magics incubation project](https://github.com/jupyter-incubator/sparkmagic).

## Scala Kernel

Massive effort needs to be put into making the Scala kernel(s) for Jupyter first class citizens. Competitive angle: It should be so good that Zeppelin or Beaker would adopt it (or create it) and contribute to it. Current contenders:
- https://github.com/alexarchambault/jupyter-scala
- https://toree.incubator.apache.org/documentation/user/quick-start

## Style of error reporting

If you’ve ever worked with PySpark, you know the joys of having python tracebacks embedded in JVM tracebacks. In order to make development easier, we need to bring attention to the right lines to go straight to in a traceback. Spark centric notebooks do this, showing exactly the error text the user needs and a collapsible area for tracebacks. Jupyter has some open issues and discussion about improving error semantics - it’s really important for kernels and the libraries building on them - to be able to expose more useful context to users.

At a minimum, we should expose links and/or popups to the spark driver’s stdout/stderr, Spark UI, and YARN application master where relevant. Without these essentials, a notebook user can’t debug issues that aren’t returned in the notebook output cell.

## POC ➡️  Production

This part is more JVM centric and not language agnostic - people need a way to turn code segments into a Scala class, compile it, and generate a JAR. My knowledge of how this can be done is fairly old/outdated.

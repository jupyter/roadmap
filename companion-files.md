## Companion files

Discussed Spring 2016, will require new versions of notebook and ?nbformat.

We want to store more volatile information such as widget existence and state
when saving notebooks. However, putting this kind of data in `.ipynb` files
would make storing them in version control really inconvenient. We know that
version controlling notebooks is already somewhat painful, and we don't want to
make it worse.

*Companion files* are how we intend to solve this. On save, if there is any data
to store in it, a companion file will be written next to the `.ipynb` file.
On load, if a companion file exists, its data will be recombined with the
notebook file as far as possible. Where they do not match up, the `.ipynb` is
considered canonical, and data from the companion file may be discarded.

* The companion file will be used by ipywidgets to store widget state, but is
  also available to use for other data.
* We may introduce an option to store large/binary(/all?) outputs in the
  companion file rather than base64 encoded in the `.ipynb` file.
* Companion files are designed to be excluded from version control; if checked
  in, they should be treated as a blob of binary data, and not subject to
  line-based diffing and merging.
* Each notebook has a single companion file. We discussed storing a directory
  of companion files: that may be better in some ways for version control, but
  directories can't be conveniently sent as email attachments. This is a
  compromise between the two use cases.
* Companion files will be zip files: this provides a namespace to store
  different pieces of data, and easy access for other tools. We chose a binary
  format deliberately, so that tools like git do not try to diff or merge it as
  a text file. At the same time, it's possible that e.g. Github could offer a
  nicer UI showing the contents of the zip file.

An alternate option could be to have the companion file be essentially the ipynb itself with the widget state in the metadata. On save, you would get something like:

`foobar.ipynb` (no widget state)
`foobar.full.ipynb` (contains widget state etc)

To avoid the churn, we could also decide to remove anything that is output from the first one. A default `.gitignore` would ignore the full version, but you could still send it by email to someone with the inline figures an all.

The widget state in the full file could be encoded in base64...

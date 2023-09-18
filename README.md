# Overview

**quartodoc** lets you quickly generate Python package API reference
documentation using Markdown and [Quarto](https://quarto.org). quartodoc
is designed as an alternative to
[Sphinx](https://www.sphinx-doc.org/en/master/).

Check out the below screencast for a walkthrough of creating a
documentation site, or read on for instructions.

<div>

[![](https://cdn.loom.com/sessions/thumbnails/fb4eb736848e470b8409ba46b514e2ed-00001.gif)](https://www.loom.com/share/fb4eb736848e470b8409ba46b514e2ed)

</div>

## Installation

``` bash
python -m pip install quartodoc
```

or from GitHub

``` bash
python -m pip install git+https://github.com/machow/quartodoc.git
```

<div>

> **Install Quarto**
>
> If you haven’t already, you’ll need to [install
> Quarto](https://quarto.org/docs/get-started/) before you can use
> quartodoc.

</div>

## Basic use

Getting started with quartodoc takes two steps: configuring quartodoc,
then generating documentation pages for your library.

You can configure quartodoc alongside the rest of your Quarto site in
the
[`_quarto.yml`](https://quarto.org/docs/projects/quarto-projects.html)
file you are already using for Quarto. To [configure
quartodoc](basic-docs.qmd#site-configuration), you need to add a
`quartodoc` section to the top level your `_quarto.yml` file. Below is a
minimal example of a configuration that documents the `quartodoc`
package:

``` yaml
project:
  type: website

# tell quarto to read the generated sidebar
metadata-files:
  - _sidebar.yml


quartodoc:
  # the name used to import the package you want to create reference docs for
  package: quartodoc

  # write sidebar data to this file
  sidebar: _sidebar.yml

  sections:
    - title: Some functions
      desc: Functions to inspect docstrings.
      contents:
        # the functions being documented in the package.
        # you can refer to anything: class methods, modules, etc..
        - get_object
        - preview
```

Now that you have configured quartodoc, you can generate the reference
API docs with the following command:

``` bash
quartodoc build
```

This will create a `reference/` directory with an `index.qmd` and
documentation pages for listed functions, like `get_object` and
`preview`.

Finally, preview your website with quarto:

``` bash
quarto preview
```

## Rebuilding site

You can preview your `quartodoc` site using the following commands:

First, watch for changes to the library you are documenting so that your
docs will automatically re-generate:

``` bash
quartodoc build --watch
```

Second, preview your site:

``` bash
quarto preview
```

## Looking up objects

Generating API reference docs for Python objects involves two pieces of
configuration:

1.  the package name.
2.  a list of objects for content.

quartodoc can look up a wide variety of objects, including functions,
modules, classes, attributes, and methods:

``` yaml
quartodoc:
  package: quartodoc
  sections:
    - title: Some section
      desc: ""
      contents:
        - get_object        # function: quartodoc.get_object
        - ast.preview       # submodule func: quartodoc.ast.preview
        - MdRenderer        # class: quartodoc.MdRenderer
        - MdRenderer.render # method: quartodoc.MDRenderer.render
        - renderers         # module: quartodoc.renderers
```

The functions listed in `contents` are assumed to be imported from the
package.

## Learning more

Go [to the next page](basic-docs.qmd) to learn how to configure
quartodoc sites, or check out these handy pages:

- [Examples page](../examples/index.qmd): sites using quartodoc.
- [Tutorials page](../tutorials/index.qmd): screencasts of building a
  quartodoc site.
- [Docstring issues and examples](docstring-examples.qmd): common issues
  when formatting docstrings.
- [Programming, the big picture](dev-big-picture.qmd): the nitty gritty
  of how quartodoc works, and how to extend it.

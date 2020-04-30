# User Documentation Proof of Concept with Read the Docs

This is a proof of concept for using Read the Docs to setup a user documentation site backed by GitHub source control with versioning and template rendering. 

[Read the Docs](https://readthedocs.org/) is a set of software documentation tools for building, rendering, hosting, and managing documentation, all for free. It provides many of the features we need out of the box, such as versioning and template rendering. 

Read the Docs works natively with two underlying documentation generation engines, [Sphinx](https://docs.readthedocs.io/en/stable/intro/getting-started-with-sphinx.html) and [MkDocs](https://docs.readthedocs.io/en/stable/intro/getting-started-with-mkdocs.html). Both engines have pros and cons, but this proof of concept uses MkDocs, as it is more geared toward markdown content than Sphinx. 

## GitHub Setup

To begin, we created a new GitHub repository to host our documentation. The repository contains the following top level files and directories:

* `docs/` - This directory hosts the documentation content. It must be a distinct directory from the directory which contains the configuration files (the top level, in this case), though they can be nested. 
* `README` - A standard GitHub repo README with information about the repository contents. Not used by Read the Docs in this proof of concept. 
* `.readthedocs.yml` - A [configuration file](https://docs.readthedocs.io/en/stable/config-file/index.html) for Read the Docs. It specifies the documentation generation engine to be used. It can further configure Read the Docs, but it's pretty barebones for the proof of concept. 
* `mkdocs.yml` - A [configuration file](https://www.mkdocs.org/user-guide/configuration/) for MkDocs. Specifies the theme, the navigation layout, and other metadata for the documentation in our proof of concept. 

The `docs/` directory is also populated with markdown files for the documentation content. 

## Read the Docs Setup

With the GitHub repository ready, we set up an account on Read the Docs and imported our documentation from GitHub. For the proof of concept, the account was set up with a personal GitHub account. For a full implementation, a more robust authorization system should be considered. Read the Docs provides organization management through their [For Business](https://docs.readthedocs.io/en/stable/commercial/organizations.html) offering, which currently costs $50/mo. for the basic plan. 

While signed in with a new Read the Docs account, we clicked Import Project on the projects page and selected the GitHub repository created earlier from the list of available repositories. Read the Docs automatically imported our documentation and set up our documentation site (though it took some fiddling with configuration and formatting to get it completely correct; the end product can be seen in the repository and Read the Docs admin panel). 

## Versioning

By default, Read the Docs builds a latest version from the `master` branch in GitHub. To test versioning, we created a couple of GitHub releases based on different commits in the repository. Then, in the Read the Docs administration dashboard, we activated new versions based on the GitHub releases, `v0.0.1` and `v.0.0.2`. We also changed the default version to point to `v0.0.2` via the Admin > Advanced Settings panel. Unforuntately, it does not seem like versioning can be configured using configuration files. 

## Interactivity

One of our major goals for documentation is that it provide an interactive learning experience. We have identified [Jupyter](https://jupyter.org/) as a possible tool for providing interactivity. Although Read the Docs does not provide Jupyter integration out of the box, there are other options for integration. A few promising solutions are [Jupyter Widgets](https://github.com/jupyter-widgets/ipywidgets), which are able to [embed in static web pages](https://ipywidgets.readthedocs.io/en/latest/embedding.html), and [a guide using multiple technologies](https://elc.github.io/posts/embed-interactive-notebooks/), which seems more complicated by may be more flexible. These approaches will need to be considered as part of the full interactive documentation architecture. 

## Future Work

This proof of concept is just a start. It demonstrates a bare bones Read the Docs setup with basic configuration and versioning. The following additional work is necessary to get a fully featured user documentation site up and running:

* Setup a [custom domain name](https://docs.readthedocs.io/en/stable/custom_domains.html). 
* Create a [custom theme](https://www.mkdocs.org/user-guide/styling-your-docs/). 
* Determine proper administration of the documentation. 
  * Whose [GitHub account](https://docs.readthedocs.io/en/stable/connected-accounts.html) owns it? 
  * Do we need the additional management features of [Read the Docs for Business](https://docs.readthedocs.io/en/stable/commercial/index.html)?
* Add interactive components, per the above section. 
* Write documentation content. 

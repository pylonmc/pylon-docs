# Contributing to documentation

We use [MkDocs](https://www.mkdocs.org/) and [Github pages](https://pages.github.com/) for the documentation site you're reading right now.

## Prerequisites

Before you begin, ensure you have the following installed on your system:

- **Python 3** - Required for MkDocs
- **pip** - Python package installer (usually comes with Python)

Check [MkDocs' installation guide](https://www.mkdocs.org/user-guide/installation/) on how to install these dependencies.

## How to get started

1. Clone the `pylon-docs` repository: `git clone https://github.com/pylonmc/pylon-docs`
2. Install all required dependencies: `pip install -r requirements.txt`
3. Run the documentation website locally using `mkdocs serve`

## Deploying

Only core members can deploy the website.

1. Clone the `pylonmc.github.io` repository: `git clone https://github.com/pylonmc/pylonmc.github.io`
2. Deploy the site by running **in the pylonmc.github.io repository** `mkdocs gh-deploy --config-file ../pylon-docs/mkdocs.yml --remote-branch master`

[comment]: <> (TODO add more detailed explanation like Slimefun has (https://github.com/Slimefun/Slimefun4/wiki/Expanding-the-Wiki))


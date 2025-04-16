# Getting started
We use [MkDocs](https://www.mkdocs.org/) for documentation. Documentation is hosted using [Github pages](https://pages.github.com/).

## Local development
- Clone the `pylon-docs` repository: `git clone https://github.com/pylonmc/pylon-docs`
- Install MkDocs using pip: `pip install mkdocs`
- Install the MkDocs material theme: `pip install mkdocs-material`
- Run the documentation website locally using `mkdocs serve`

## Deploying
- Clone the `pylonmc.github.io` repository: `git clone https://github.com/pylonmc/pylonmc.github.io`
- Deploy the site with `mkdocs gh-deploy --config-file ../pylon-docs/mkdocs.yml --remote-branch master`


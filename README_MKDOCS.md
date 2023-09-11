# mkdocs Overview

## How to add and edit documentation

Documentation uses `mkdocs` with Github Pages. All pages are editable as markdown. The file structure of the `docs` folder is cloned into the URL structure or the documentation.
For info on how to use `mkdocs` see: `https://www.mkdocs.org/getting-started/`

## Installing mkdocs

```shell
python3 -m pip install mkdocs
```

## Live preview server

You can view your changes before deploying them using

```shell
python3 -m mkdocs serve
```

And navigating to `http://127.0.0.1:8000/` in your browser.

## Deploying documentation

Documentation should be developed and maintained using the normal version control process.

Only deploy documentation from the main branch (`main`).

**Warning: the following command will push changes to the `gh-pages` branch on Github! Don't use it until you are sure you are ready.**

```shell
git checkout main
git pull origin main

mkdocs gh-deploy
```
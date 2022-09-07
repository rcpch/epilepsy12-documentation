---
title: Documentation development
reviewers:
---

## Introduction

The RCPCH Audit Engine / Epilepsy 12 documentation is made with [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/), which is a framework, separate from Django, which takes Markdown source files from `docs` and compiles them into a static HTML site. These static files are then served from our hosting resources.

## Setup Python and Pyenv

See LINK for a guide on how to set up a Pyenv virtual environment containing the correct version of Python.

The documentation repository contains a `.python-version` file which will automatically select the correct Pyenv for you when you navigate to the repository, as long as you have called your virtualenv `mkdocs`.

You need to have Material for MkDocs installed (this installs MkDocs as well for you)

In most circumstances this is simply `pip install mkdocs-material`, but if you hit issues then there is more information at https://squidfunk.github.io/mkdocs-material/getting-started/

## `mkdocs serve`

`mkdocs serve` starts up a development server which will auto-reload after changes to the source files, and will serve the documentation on [`localhost:8001`](http://localhost:8001).

## How to edit content

- Check out a **new local branch** on which to make the changes, with a **descriptive name**.
- Make changes to the Markdown files in the `docs` folder in the project root.
- Ensure any new or renamed files are listed in the `nav` element within `mkdocs.yml` or they won't show up.
- Save and the changes.
- The auto-reloaded site will show the changes.
- Commit the changes. Try to keep commits tidy and 'atomic' - in that ideally a single commit should be one new or edited piece of content, not a whole raft of changes. This allows us to easily select which commits to include.
- Push the changes and create a pull request to have them included in the main project.

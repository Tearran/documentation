# Armbian Documentation

[![Create offline documentation to release](https://github.com/armbian/documentation/actions/workflows/release.yaml/badge.svg)](https://github.com/armbian/documentation/actions/workflows/release.yaml)

<p align="center">
  <a target="_blank" href="https://docs.armbian.com">
    <img alt="logo" src="./docs/images/logo.png">
  </a>
</p>

## Overview

Documentation is written in [markdown](https://www.markdownguide.org/basic-syntax/) and stored in the `docs/` subfolder.  Images go in `docs/images`.

This repo is meant for storing and quick glances.  Official output is [https://docs.armbian.com](https://docs.armbian.com).

Armbian Documentation is available in the following formats:

* [Official document website](https://docs.armbian.com),
* [PDF document](https://github.com/armbian/documentation/releases/latest)

## Contributing

This site is built with [mkdocs](https://github.com/mkdocs/mkdocs/) and depends on [mkdocs-material](https://github.com/squidfunk/mkdocs-material).

Armbian Documentation naming of document files follows this rules:

`[Parent-Topic-Example]_[Child-Topic]-example.md`

`Parent-Topic-Name` and `Child-Topic-Name` are separated by an underscore `_`.  Hyphens `-` are automatically converted to space.

Please try to avoid creating new parent topics unless absolutely necessary.

Current Parent Topics:

* User Guide
* Hardware notes
* Developer Guide
* Contributor Process
* Release management
* Community

See the [document template](.github/DOCUMENT_TEMPLATE.md) before you writing any content.

---
## Working on the content
### Prerequisites

**Ensure Python and the necessary development packages are installed**. For Debian-based systems:

```bash
sudo apt-get update
sudo apt-get install python3 python3-pip python3-venv python3.11-dev
```

### Environment Setup and Repository Cloning

**Set up a Python virtual environment** to isolate project dependencies. This example uses a directory within the current user's home directory, but you can adjust the path as needed:

```bash
python3 -m venv ~/armbian-docs-env
source ~/armbian-docs-env/bin/activate
```

Alternatively, for a project-specific environment, replace `~/armbian-docs-env` with `./env` or another directory within your project's folder.

**Clone the Armbian documentation** repository and navigate into it:

```bash
git clone https://github.com/armbian/documentation
cd documentation
```

**Install the required Python packages** from the `requirements.txt` file:

```bash
pip install -r requirements.txt
```

## Building and Serving the Documentation

To build and serve the documentation locally, allowing you to make edits and observe the results in real time, use:

```bash
mkdocs build --clean && mkdocs serve
```

This command builds the documentation and starts a local server. You can view the documentation by visiting `http://127.0.0.1:8000` in your web browser.

- **For editing existing files:** After making changes, the `mkdocs serve` command automatically rebuilds the documentation. Simply refresh your browser to see the updates.
- **For adding new files:** Ensure the new files are referenced in the `mkdocs.yml` configuration file under the `nav` section. The server automatically incorporates changes, so just refresh your browser to view them.

After adding a new file, either hand-edit `mkdocs.yml`, or re-run `tools/mkArmbianDocs.py` **unless making changes to the structure of the `docs/` folder**. (See below)

## Generate tools

### mkArmbianDocs.py
Generate `mkdocs.yml` based on the contents of `docs/` folder

* Command-line options for input and output directories
* Requires install requirement
* You don't need to run it every time unless making changes to the structure of the `docs/` folder
* See `mkArmbianDocs.py -h` for help

From the parent folder of the repo, run:

`python3 tools/mkArmbianDocs.py && mkdocs build`

This will generate the `mkdocs.yml` and publish built HTML to the `site/` folder.

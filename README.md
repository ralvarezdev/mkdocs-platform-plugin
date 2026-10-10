# mkdocs-platform-plugin

A [MkDocs](https://www.mkdocs.org/) plugin that lets one Markdown file serve both GitHub and a MkDocs site: content in special HTML comments is either removed from the MkDocs site (GitHub-only) or shown only there (MkDocs-only).

PyPI package `mkdocs-platform-plugin` (0.1.2, <https://pypi.org/project/mkdocs-platform-plugin>). Python `>=3.8`, `mkdocs>=1.5`. Plugin entry point: `platform-content`.

## Installation

```bash
pip install mkdocs-platform-plugin
```

```yaml
# mkdocs.yml
plugins:
  - platform-content
```

## Usage

The plugin processes each page's Markdown (`on_page_markdown`).

GitHub-only content is removed from the MkDocs build:

```markdown
<!-- github-only-start -->
Shown on GitHub, stripped from the MkDocs site.
<!-- github-only-end -->
```

MkDocs-only content is a comment on GitHub and uncommented on the MkDocs site, in a multi-line or inline form:

```markdown
<!-- mkdocs-only-start
Comment on GitHub, rendered by MkDocs.
mkdocs-only-end -->

<!-- mkdocs-only-start Inline MkDocs-only text mkdocs-only-end -->
```

After substitution, runs of three or more newlines collapse to a blank line.

## Project structure

```
src/mkdocs_platform_plugin/__init__.py   PlatformContentPlugin
pyproject.toml                           packaging (setuptools), entry point
.github/workflows/publish.yml            publish to PyPI on v* tags
```

The publish workflow checks that the `pyproject.toml` version matches the `v*` tag, builds with `python -m build`, runs `twine check` and publishes via PyPI Trusted Publishing. There are no tests.

## License

GNU General Public License v3.0. `pyproject.toml` declares `GPL-3.0-only`, matching the `LICENSE` file.

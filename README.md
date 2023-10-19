# Documentation Setup using Sphinx

This README guides you through setting up [Sphinx](https://www.sphinx-doc.org/) for documentation of our software.

## Prerequisites

- Python (3.6 or newer is recommended)
- pip

## Step-by-step Guide for A New Project

#### 1. Install Sphinx

First, install Sphinx and the RTD theme:

```bash
pip install sphinx sphinx_rtd_theme
```

#### 2. Setup the Documentation Directory

Navigate to your project directory and run:

```bash
mkdir docs
cd docs
sphinx-quickstart
```

Follow the prompts. For most options, the default is fine. Ensure that you select "yes" for the "autodoc" option, as it will allow Sphinx to automatically generate docs from docstrings in your code.

#### 3. Choose a Theme

By default, Sphinx uses the "alabaster" theme. If you want to use the Read the Docs theme (which is quite popular), open `conf.py` in the `docs` directory (or whatever name you gave your documentation directory) and modify the `html_theme` line to:

```python
import sphinx_rtd_theme

html_theme = "sphinx_rtd_theme"
html_theme_path = [sphinx_rtd_theme.get_html_theme_path()]
```

#### 4. Write Your Documentation

Within the `docs` directory, you'll see an `index.rst` file. This is the main entry point for your documentation. You can edit this file to add more content, or link to other `.rst` files you create.

#### 5. Generate the Documentation

To generate the docs, run:

```bash
make html
```

This will generate a `_build` directory within `docs`, with your rendered HTML documentation inside.

#### 6. Hosting Your Documentation (optional)

If you wish to host your documentation for public viewing, consider using a service like [Read the Docs](https://readthedocs.org/). They provide free hosting for Sphinx-generated documentation and integrate well with GitHub.

## Tips

- Remember to regularly regenerate the documentation with `make html` whenever you update the `.rst` files.
- If you update your code and want those changes reflected in the auto-generated documentation, ensure your modules are on the Python path (or adjust the Python path in `conf.py`) and run:

```bash
sphinx-apidoc -o <output_directory> <module_directory>
```

Then rebuild your documentation.


## Deploying Sphinx documentation to GitHub Pages

**Objectives:**
- Create a basic workflow which you can take home and adapt for your project.

## [GitHub Pages](https://pages.github.com/)
- Serve websites from a GitHub repository.
- It is no problem to serve using your own URL `https://myproject.org` instead of `https://myuser.github.io/myproject`.

## [GitHub Actions](https://github.com/features/actions/)
- Automatically runs code when your repository changes.
- We will let it run `sphinx-build` and make the result available to GitHub Pages.

## Our goal: putting it all together
- Host source code with documentation sources on a public Git repository.
- Each time we `git push` to the repository, a GitHub action triggers to rebuild the documentation.
- The documentation is pushed to a separate branch called 'gh-pages'.

---

## Exercise - Deploy Sphinx documentation to GitHub Pages

**GH-Pages-1: Deploy Sphinx documentation to GitHub Pages**

In this exercise we will create an example repository on GitHub and deploy it to GitHub Pages.

**Step 1**: Go to the [documentation-example](https://github.com/coderefinery/documentation-example/generate) project template on GitHub and create a copy to your namespace.
- Give it a name, for instance "documentation-example".
- You don't need to "Include all branches"
- Click on "Create a repository".

**Step 2**: Browse the new repository.
- It will look very familiar to the previous episode.
- However, we have moved the documentation part under `doc/` (many projects do it this way). But it is still a Sphinx documentation project.
- The source code for your project could then go under `src/`.

**Step 3**: Add the GitHub Action to your new Git repository.
- Add a new file at `.github/workflows/documentation.yml` (either through terminal or web interface), containing:

```yaml
name: documentation

on: [push, pull_request, workflow_dispatch]

permissions:
  contents: write

jobs:
  docs:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-python@v3
      - name: Install dependencies
        run: |
          pip install sphinx sphinx_rtd_theme myst_parser
      - name: Sphinx build
        run: |
          sphinx-build doc _build
      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        if: ${{ github.event_name == 'push' && github.ref == 'refs/heads/main' }}
        with:
          publish_branch: gh-pages
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: _build/
          force_orphan: true
```

**Step 4**: Enable GitHub Pages
- On GitHub go to "Settings" -> "Pages".
- In the "Source" section, choose "Deploy form a branch" in the dropdown menu.
- In the "Branch" section choose "gh-pages" and "/root" in the dropdown menus and click save.
- You should now be able to verify the pages deployment in the Actions list).

**Step 5**: Verify the result
- Your site should now be live on `https://USER.github.io/documentation-example/` (replace USER).

**Step 6**: Verify refreshing the documentation
- Commit some changes to your documentation
- Verify that the documentation website refreshes after your changes (can take few seconds or a minute)

---

## Alternatives to GitHub Pages
- [GitLab Pages](https://docs.gitlab.com/ee/user/project/pages/) and [GitLab CI](https://docs.gitlab.com/ee/ci/) can create a very similar workflow.
- [Read the Docs](https://readthedocs.org) is the most common alternative to hosting in GitHub Pages.
- Sphinx builds HTML files (this is what static site generators do), and you can host them anywhere, for example your university's web space or own web server.

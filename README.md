# Doxygen GitHub Pages Deploy Action

GitHub Action for making and deploying Doxygen documentation to a GitHub pages branch

## Basic Usage

To deploy docs on every push to the `main` branch, create a new file in the `.github/workflows/` directory called `doxygen-gh-pages.yml` with the following contents:

```yml
name: Doxygen GitHub Pages Deploy Action

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: DenverCoder1/doxygen-github-pages-action@v1.1.0
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
```

## Options

- `github_token` (required): GitHub token for pushing to repo. See the [docs](https://git.io/passing-token) for more info.
- `branch` (optional): Branch to deploy to. Defaults to `gh-pages`.
- `folder` (optional): Folder where the docs are built. Defaults to `docs/html`.
- `config_file` (optional): Path of the Doxygen configuration file. Defaults to `Doxyfile`.

## Advanced Usage

Here is an example of a `.github/workflows/doxygen-gh-pages.yml` file with more advanced configuration:

```yml
name: Doxygen GitHub Pages Deploy Action

on:
  push:
    branches:
      - main
  workflow_dispatch:

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: DenverCoder1/doxygen-github-pages-action@v1.1.0
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          branch: gh-pages
          folder: docs/html
          config_file: Doxyfile
```

## About this Action

This action is a composite action containing the following steps:

### 1. Checkout repository

The [actions/checkout](https://github.com/actions/checkout) step is used to checkout the repository with any submodules.

### 2. Install Doxygen

Doxygen is installed by running the following command:

```bash
sudo apt-get install doxygen -y
```

### 3. Generate Doxygen Documentation

Doxygen documentation is generated by running the following command.

Set the `config_file` input option to change `Doxyfile` to a different filename.

```bash
doxygen Doxyfile
```

### 4. Create .nojekyll

Creating a .nojekyll file ensures pages with underscores work on GitHub Pages.

Set the `folder` input option to change `docs/html` to a different folder.

```bash
touch docs/html/.nojekyll
```

### 5. Deploy to GitHub Pages

The [JamesIves/github-pages-deploy-action](https://github.com/JamesIves/github-pages-deploy-action) action is used to deploy the documentation to GitHub Pages.

The `folder` option determines which folder to deploy. By default, it is `docs/html`.

The `branch` option determines which branch to deploy to. By default, it is `gh-pages`.

## License

This work is under an [MIT license](LICENSE)

## Support

If you like this project, give it a ⭐ and share it with friends!

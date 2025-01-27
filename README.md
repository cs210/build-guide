# CS 210 Build Guide

This guide is intended to be a collection of resources for current and future CS 210 students. In particular, we want the guide to evolve as trends and technologies change.

## To Run

This website uses the [Hugo Book](https://github.com/alex-shpak/hugo-book) Hugo theme. To run locally, first add the theme as a submodule:

```bash
git submodule add https://github.com/alex-shpak/hugo-book themes/hugo-book
```

You my also need to update the submodule:

```bash
git submodule update --init --recursive
```

Since the config file has already been updated, you can then run the server:

```bash
hugo server --minify --theme hugo-book
```

## Contribution

All the documents are in the `content/docs` folder. In particular, you can follow the folder structure of `ml/` to add a new section. From there, you can then follow the deployment instructions below.

## Deployment

The website publishes to this [link](https://cs210.github.io/build-guide/) on every push to `main`.
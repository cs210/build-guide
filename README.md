# CS 210 Build Guide

This guide is intended to be a collection of resources for current and future CS 210 students. In particular, we want the guide to evolve as trends and technologies change.

## To Run

This website uses the [Hugo Book](https://github.com/alex-shpak/hugo-book) Hugo theme. To run locally, first add the theme as a submodule:

```bash
git submodule add https://github.com/alex-shpak/hugo-book themes/hugo-book
```

Since the config file has already been updated, you can then run the server:

```bash
hugo server --minify --theme hugo-book
```

## Deployment

To deploy, first, we can generate the static `public` folder:

```bash
hugo -D
```

We currently use GitHub Pages to host our site, so we can then push the `public` folder to the `gh-pages` branch as below:

```bash
git init
git remote add origin https://github.com/cs210/build-guide.git
git branch -M gh-pages
git add .
git commit -m "Deploy Hugo site"
git push -f origin gh-pages
```

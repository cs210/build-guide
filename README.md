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

```
hugo -D
cd public
git init
git remote add origin https://github.com/cpondoc/test-hugo-blog.git
git branch -M gh-pages
git add .
git commit -m "Deploy Hugo site"
git push -f origin gh-pages
```
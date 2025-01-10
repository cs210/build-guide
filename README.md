# Test Hugo Blog

For potential use in other applications.

## To Run

```
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
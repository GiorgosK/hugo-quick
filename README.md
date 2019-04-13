# Hugo deploying to github project pages 

https://[username].github.io/[project-name]/
https://giorgosk.github.io/hugo-quick/


## Deployment of Project Pages From Your gh-pages branch

This setup utilizes the automatic deployment to github pages by pushing to the `gh-pages` branch

## Initial preparation for gh-pages Branch as described on [hugo documentation](https://gohugo.io/hosting-and-deployment/hosting-on-github/#preparations-for-gh-pages-branch) 

Ignore `public` folder in `master` branch
```
echo "public" >> .gitignore
git commit -am "Ignoring public folder in master branch"
```

Initialize your `gh-pages` branch as an empty [orphan branch](https://git-scm.com/docs/git-checkout/#git-checkout---orphanltnewbranchgt)

```
# initialize branch
git checkout --orphan gh-pages
git reset --hard

# commit and puth to github
git commit --allow-empty -m "Initializing gh-pages branch"
git push origin gh-pages

# return to master
git checkout master
```

## Build and Deployment

Setup [git worktree](https://git-scm.com/docs/git-worktree) (one time setup, kept until removed)

```
git worktree add -B gh-pages public origin/gh-pages
```


Clean public directory (optional)
```
rm -rf public
```

build the site (publishDir = "public" assumed)
```
hugo
```

Start server and make sure all works by visiting the url created
```
hugo serve 
```

Commit to `gh-pages` branch
```
cd public && git add --all && git commit -m "Publishing to gh-pages" && cd ..
```

Push to github
```
git push origin gh-pages
```
Github will see the `gh-pages` branch has changed and will automatically deploy the new version of the site
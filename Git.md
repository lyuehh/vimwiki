## Git

### change url
`git remote set-url origin git@github.com:lyuehh/dotfiles.git`

### tag

`git pull --tags`

### gh-pages

```
rm -rf _site
git clone git@github.com:lyuehh/html5_demo.git _site
cd _site
git checkout --orphan gh-pages
rm -rf *
cd ..
jekyll build
cd _site
git add .
git commit -a -m 'init gh-pages'
git commit --amend --reset-author
git push origin gh-pages

```

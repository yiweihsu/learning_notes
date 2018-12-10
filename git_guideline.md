```git

$ git stash
$ git checkout unstable
$ git pull

$ git checkout -b api2
$ git reset --hard
$ yarn install

/*
check out to another branch, so we can delete the branch we were at before.
*/

$ git checkout 78a6d6c4b7195c20f4a2ce0c938c8e076d3903f1
$ git branch -d public-api-module
$ git log
$ git checkout -b public-api-module
$ git push origin public-api-module -f

$ git stash pop
$ git status

```


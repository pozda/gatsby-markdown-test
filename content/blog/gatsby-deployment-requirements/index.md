---
title: Gatsby Deployment Requirements!
date: '2019-01-23T21:47:32.169Z'
---

## Gatsby MArkdown Heroku Deploy via Github pushes to master branch

![Garden by the Bay in Singapore](./gardenByTheBay.png)

after installing gatsby-cli ``npm i -g gatsby-cli`` install gatsby blog starter

````
npm gatsby new my-blog-starter https://github.com/gatsbyjs/gatsby-starter-blog
````
and push it to new github repo.

make new file ``app.json`` in the root folder and paste this code:

```
{
  "buildpacks": [
    {
      "url": "heroku/nodejs"
    },
    {
      "url": "https://github.com/heroku/heroku-buildpack-static"
    }
  ]
}
```

in the scripts section of ```package.json``` add heroku-postbuild line:

```
{
 
  // ...
  "scripts": {
    // ...
    "heroku-postbuild": "gatsby build"
    // ...
  }
  // ...
}
```

make ```static.json``` in root folder and paste this code:

```
{
  "root": "public/",
  "headers": {
    "/**.js": {
      "Cache-Control": "public, max-age=0, must-revalidate"
    }
  }
}
```
Last step is to make ```Procfile``` in root folder and to add this line: 
````
web: gatsby serve --port ${PORT}
````

setup app on heroku and link it to the master branch, set autodeploy when pushing to master.

every time you add new content in markdown, it will build new static site.
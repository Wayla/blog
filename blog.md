Our blog is focused on the technical and UX topics relevant to mobile web development. The posts are inspired by the work our team has performed building Wayla's mobile web app.

## Contributors
- Brett Shwom
- Judd Morgenstern
- Jak Horner
- Zach Smith

## Friends
- Francis Gulotta
- Sara Robinson

## Our heros
- Rich Harris
- Francis Gulotta (heros can be friends too!)
- Rob DiMarco

## Keywords:

- mobile web
- javascript
- HTML5
- ractive.js
- backbone.js
- firebase
- Newer CSS3 features such as
  - flexbox
  - position: sticky
- Single page apps
- performance optimication for mobile
- Add to homescreen apps
- iOS

## Stack

Our stack consists of:
- firebase
  - backend api
  - nosql hierarchical datastore
- backbone.js
  - backbone models and collections
- oauth.io
- ractive
- stylus
- grunt
- component
- typography
- nginx

## Collaboration between designers and me (the sole engineer)

## Architecture

We use a single codebase to support our mobile app and desktop site. We rely heavily on CSS media queries to pull this off. We also

The only actual production server we maintain ourselves is an AWS server that serves all of our environments. That server:
- runs an instance of nginx
- has a bare git repo with a post recieve hook that copies the `/dist` folder of the pushed git tag/branch to ngnix's root directory
- nginx is configured such requests to `[subdomain].wayla-development-environment.com` will serve up files from `[ngnix-root]/[subdomain]`
- So we can create a branch locally, then push it to our AWS server via a bash deploy script we wrote, and then access the deployed code at `[branchname].wayla-development-environment.com` - super useful for demoing and sharing

which is doing a few fancy things:

- gzip compression is enabled
- w

## Scale

### Concurrent Users

According to the firebase analytics dashboard, the peak number of concurrent connections over the last 30 days (02/22/2014 - 02/22/2014) is 21.

### Data load per user

Our event feed...

## Environments

We maintain 3 environments:

- Production
- Local development
- Remote development

Momentum Paging
---------------

<i>Momentum paging</i> is a concept that we stumbled upon when R&Ding a paging interaction for our app. We liked the paging interaction in <a href=https://itunes.apple.com/us/app/feedly-reader/id396069556?mt=8>Feedly's</a> iOS app and wanted to create a variation of it. One day, we tried combining `position:-webkit-sticky` with `-webkit-overflow-scrolling:touch` and discoved this interaction:

```
<style>
    .sticky-is-not-supported:after {
        content: "sticky is not supported by your browser";
        color:red;
        position:fixed;
        top:0;
        left:0;
    }

    .sticky-is-supported:after {
        content: "sticky is supported by your browser";
        color:green;
        position:fixed;
        top:0;
        left:0;
    }

    .post {
        position: -webkit-sticky;
        height:500px;
        width:500px;
        background-image:url(http://placehold.it/500x500);
    }

</style>

<body>

<script>

    //feature detection

    function isStickySupported() {

        var testElement = document.createElement('div')
        testElement.style.position = 'sticky'

        //if sticky isn't supported, testElement.style.position will be equal to something other than sticky

        if (testElement.style.position === 'sticky') {
            return true
        }

        //try the prefixed version

        testElement.style.position = '-webkit-sticky'

        if (testElement.style.position === '-webkit-sticky') {
            return true
        }

        return false
    }

    if (isStickySupported()) {
        document.body.classList.add('sticky-is-supported')
    }
    else {
        document.body.classList.add('sticky-is-not-supported')
    }



</script>


<article class='post'></article>
<article class='post'></article>
<article class='post'></article>
<article class='post'></article>
<article class='post'></article>

</body>

```

A word about `position:-webkit-sticky`. Its presence seemed to be causing our app to randomly crash on iPad. It's also only supported in Safari : http://caniuse.com/#search=sticky .


keywords: sticky, momentum scrolling, momentum paging, feedly, paging

Flexbox Ordering
-----------------

Transition Router
-----------------

Touch Menu
-----------------

Browser Detection
-----------------

Media Query Detection
---------------------

Placehold.it
---------------------

Visit <a href=http://placehold.it>placehold.it</a> for placeholder images. It's Lorem Ipsum for your images!

Multiple Models Per View
---------------------

```

new Ractive({
    ...,
    data {
        Model1 : model1,
        Model2 : model2,
        ...
    }
})

```

This idiom is great for things like:
- a view which needs to show both posts from a particular user, as well as information about the user him/herself.

```
new Ractive({
    ...,
    data {
        BlogPost : post,
        User : user,
        ...
    }
})

```


Image Uploading
---------------------

- Ractive template
- Local preview with tempDataUrl || actualImage
- Creating an edit page from the same create-event page

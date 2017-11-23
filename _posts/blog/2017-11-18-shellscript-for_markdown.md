---
layout: post
title: 'Generating a markdown template for new blogposts'
featured_image: 'logo-knutbehrends-square-circle.72x72.jpg'
comments: false
tags: post, code, scipting, 
summary: 'How to use a shell script to generate a template for a markdown page'
---

## How to generate a template for a _jekyll_ blog post

Put his code into a shell function, perhaps into file `~/.bash_functions`:

```sh
function new_post() {
  # use within a dir containing a jekyll project
  #knb 20171118
  cd _posts
  SLUGIFIED="$(echo -n "$1" | sed -e 's/[^[:alnum:]]/-/g' | tr -s '-'| tr 'A-Z' 'a-z')"
  SLUG=$(date +"%Y-%m-%d"-$SLUGIFIED.md)
  HEADER=$(cat <<END
---
layout: post
title: '$1'
featured_image: 'logo-knutbehrends-square-circle.72x72.jpg'
comments: false
tags:
summary: 'Summary here'

---

## Some heading


END
)
  echo -e "$HEADER" > $SLUG
  echo $SLUG
  cd ../
}
```

Executing `new_post "exciting News!"` on the bash command line will then create
a new file in the subdirectory `_posts/`. It will be named
`_posts/2017-11-18-exciting-news-.md` and contain this markdown:

```
---
layout: post
title: 'Exciting news!'
featured_image: 'logo-knutbehrends-square-circle.72x72.jpg'
comments: false
tags:
summary: 'Summary here'
---

## Some heading
```

which you can further customize.

I've seen this script in a training video in the course
[_"Serverless Web Applications"_](https://www.pluralsight.com/courses/web-applications-without-server/)
( by Rob Conery), and then I modified the script.

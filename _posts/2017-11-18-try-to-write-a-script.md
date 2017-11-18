---
layout: default
title: 'Generating a template for a new blogpost'
featured_image: ''
comments: false
tags: post, code, scipting, 
summary: 'How to use a shell script to generate a template for a markdown page'
---
  
## How to generate a template for a *jekyll* blog post  
  

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
featured_image: ''
comments: false
ntags: 
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
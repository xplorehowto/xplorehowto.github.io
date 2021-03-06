## Explore How-to

Compilation of findings in the form of how-to.

Powered by: [Jekyll](https://jekyllrb.com/) static site-generator

## Setup development environment

- See [Jekyll Quickstart](https://jekyllrb.com/docs/).

- [Template documentation](https://idratherbewriting.com/documentation-theme-jekyll/index.html)

## Adding contents

### Setup

- Clone this repo to laptop
- Edit the content in `pages` folder
- To run the site locally, you need to setup [Ruby development environment](https://jekyllrb.com/docs/installation/)
- Build the site and make it available on a local server
```
bundle exec jekyll serve
```
- Next, browse to http://localhost:4000

## Add New Page

- Add new page to the `pages` folder, organized by the topics
- Prepare the front matter, for example
  - Tags should be one word, or use underscore; add a new tag to the 
    `_data/tags.yml` to allow entrance into the page
  - Permalink reflects filename
```
---
title: Software Coding
keywords: software, development, coding
tags: [software_development, coding]
sidebar: coding_sidebar
permalink: /coding
folder: coding
---
```
 
## Manage Sidebar 

See `_data/sidebars` folder and `_config.yml`.

## Add New Folder

- Create new folder under `pages`
- Add New Page, see instructions above
- Add Topic entry in the top navigation, `_data/topnav.yml`
- Add Topic entry in the home sidebar, `_data/home_sidebar.yml`


### Jekyll debugging
```
<pre>
    site: {{ site | jsonify | escape }}
    page: {{ page | jsonify | escape }}
    layout: {{ layout | jsonify | escape }}
    content: {{ content | jsonify | escape }}
    paginator: {{ paginator | jsonify | escape }}
</pre>
```

### Markdown

Referencess:
* [Github markdown basics](https://help.github.com/articles/markdown-basics/)
* [Github flavored markdown](https://help.github.com/articles/github-flavored-markdown/)
* [Original markdown spec: Syntax](http://daringfireball.net/projects/markdown/syntax)
* [Original markdown spec: Basics](http://daringfireball.net/projects/markdown/basics)
* [marked.js library used by Colaboratory](https://github.com/chjj/marked)
* [LaTex mathematics for equations](https://en.wikibooks.org/wiki/LaTeX/Mathematics)
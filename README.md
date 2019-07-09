## Explore How-to

Compilation of findings in the form of how-to.

Powered by: [Jekyll](https://jekyllrb.com/) static site-generator

## Setup development environment

See [Jekyll Quickstart](https://jekyllrb.com/docs/).

### Adding contents

- Clone this repo to laptop
- Edit the content in `pages` folder
- To run the site locally, you need to setup [Ruby development environment](https://jekyllrb.com/docs/installation/)
- Build the site and make it available on a local server
```
bundle exec jekyll serve
```
- Next, browse to http://localhost:4000


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
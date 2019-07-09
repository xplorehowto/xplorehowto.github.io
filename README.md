## Explore How-to

Compilation of all findings in the form of how-to.

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
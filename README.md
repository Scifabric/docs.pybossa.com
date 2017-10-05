# PYBOSSA Docs in Markdown (BETA)

Needs `pandoc` and install requirements.txt with pip.

## preview docs locally

```bash
# preview mkdocs
mkdocs serve
```

## publish to gh-pages

Instructions for [deploying in GitHub](http://www.mkdocs.org/user-guide/deploying-your-docs/):

```bash
mkdocs gh-deploy
```

Result is visible on  
<https://scifabric.github.io/docs.pybossa.com/>

## TODO

* [ ] remove HTML
* [ ] write admonition (like info) like described here <https://pythonhosted.org/Markdown/extensions/admonition.html>
* [ ] Theming (maybe the sphinx theme can be reused?)
* [ ] automatic gh pages publishing
* [ ] replace existing docs

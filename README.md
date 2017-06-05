# Test PYBOSSA docs in Markdown

Needs `pandoc`.

## To generate Markdown files out of PYBOSSA rst files
```bash
# first copy all PYBOSSA rst files into ./original_rst

# delete docs directory
rm -rf docs
# run conversion (files from ./original_rst to ./docs)
./convertall
```

## preview mkdocs

```bash
# install mkdocs and plugins in a virtualenv
pip install -r requirements.txt

# preview mkdocs
mkdocs serve
```

## publish to gh-pages

Instructions for [deploying in GitHub](http://www.mkdocs.org/user-guide/deploying-your-docs/):

```bash
mkdocs gh-deploy
```


## TODO

* [ ] - remove HTML
* [ ] - write admonition (like info) like described here <https://pythonhosted.org/Markdown/extensions/admonition.html>
* [ ] - Theming (maybe the sphinx theme can be reused?)
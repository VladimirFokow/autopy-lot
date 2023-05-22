# Warning

**Currently doesn't work fully.**

**It converts the file(s) inside the docker image, but doesn't commit them to the repository, so the result is discarded.**


---

![autopy-lot](https://socialify.git.ci/deep5050/autopy-lot/image?description=1&descriptionEditable=github%20action%20to%20convert%20jupyter%20notebooks%20to%20various%20formats&font=Source%20Code%20Pro&forks=1&issues=1&logo=https%3A%2F%2Fi.imgur.com%2FWZSNO5m.png&pattern=Signal&pulls=1&stargazers=1&theme=Light)

![test-markdown](https://github.com/VladimirFokow/autopy-lot/workflows/test-markdown/badge.svg)
![test-py](https://github.com/VladimirFokow/autopy-lot/workflows/test-py/badge.svg)
![vistors](http://hits.dwyl.com/VladimirFokow/autopy-lot.svg)


## conversions:
1. .ipynb -> .md
2. .ipynb -> .py   <b>(DEFAULT)</b>
3. .py -> .ipynb

### NOTE
``R`` is not supported. Please don't try to convert R files for now.

## USAGE

Create a ``autopy-lot.yml`` file under ``.github/workflows`` with the following contents:

```yaml
name: autopy-lot

on: [push]

jobs:
  build:
    name: autopy-lot
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: autopy-lot 
        uses: VladimirFokow/autopy-lot@master
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          output_dir: './autopy-lot/'
          # Optional configuration:
          check: latest
          input_type: ipynb
          comment_magics: true
          split_at_heading: true
          output_type: markdown
          # ... more to come
```

- `build` keyword itself can be anything (not necessarily `build`)
- names can be arbitrary(`name: anything`)
- can specify the autopy-lot options under the `with:` keyword (see below


### Input options

``check``  : ``all`` to convert all specified files (based on file type) on every run. ``latest`` to convert only the files changed on last commit.

``input_types`` : ``py`` ``ipynb`` ``r``

``comment_magics`` : ``true`` see jupytext documentation for further details.

``split_at_heading`` : ``true`` see jupytext documentation for further details.


``output_type`` : ``py`` ``markdown`` ``r`` ``ipynb``


``output_dir``: give a output directory name where all the converted outputs will be stored. default is ``./autopy-lot/``. when provide custom path name, make sure the to put the initial ``.`` and ``/`` at the end. please note that it is a mandatory input argument.

# **# TODO:**
- select whether to apply option `--update-metadata '{"jupytext": {"notebook_metadata_filter": "-all"}}'`
- provide file names
- add all formats supported by jupytext (essentially, make a full wrapper around jupytext, that additionally just *selects the files to convert* and *commits the results to the provided path*)


## Note

This action can handle only one **type** of conversion per workflow setup (i.e., `md`, or `py`).
If you need to convert input files to different file types, you need to create several ``.yml`` files under ``.github/workflows``.

Example :

``autopy-lot-markdown.yml`` , ``autopy-lot-py.yml``.

<br />

## License

This project is based on [deep5050/autopy-lot](https://github.com/deep5050/autopy-lot) by Dipankar Pal. 

All code is licensed under the MIT License. See the [licenses](licenses/) folder for detailed information.

Thanks: icons made by <a href="https://www.flaticon.com/authors/freepik" title="Freepik">Freepik</a> from <a href="https://www.flaticon.com/" title="Flaticon"> www.flaticon.com</a>

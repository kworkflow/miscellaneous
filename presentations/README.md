# About

This folder compress all presentation used by kw.

## What do we use for creating kw presentation

We use Sphinx and Revealjs to generate kw presentations; this is possible
thanks to an extension named sphinx-revealjs. If you want to know more about
this, take a look at the following links:

* https://github.com/attakei/sphinx-revealjs
* https://dev.to/attakei/sphinx-extension-to-generate-revealjs-presentation-from-plain-rest-58ip

# How to build kw presentations

You need Sphinx and pip installed in your system; for example, if you are using
Debian based system, just use:

```
apt install python3-docutils sphinx-doc python3-pip
```

Next, install the sphinx-revealjs extension:

```
pip install sphinx-revealjs
```

Finally, use the following command to build the documentation:

```
cd TARGET_PRESENTATION/
make revealjs
```

# How to create a new presentation

First of all, create a specific folder for the target presentation:

```
mkdir presentations/NAME
cd presentations/NAME
```

Create a simple Sphinx documentation structure:

```
sphinx-quickstart
```

Open the `config.py` file, and add the `sphinx_revealjs` extension as described
below:

```
extensions = [
    'sphinx_revealjs',
]
```

# Others

If you want to create gif, we recommed: peek.

If you want to compress your gifs from terminal screen shot, use:

```
gifsicle -i full-kw-install.gif -O3 --colors 256 --lossy=170 -o full-kw-install-reduced.gif
```

The following website is really good for edit gif:

 https://ezgif.com/crop

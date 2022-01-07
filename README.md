# papermill-altair-pdf

How to build a PDF from a notebook with `altair` graphics via `papermill`.

## Install homebrew

    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

### Install pyenv

    brew install pyenv

### Build recent version of python, set global

    pyenv install 3.10.0
    # set as global
    pyenv global 3.10.0

## Install deps

    python3 -m pip install papermill jupyterlab altair altair_saver papermill

## Setup `selenium`

First, update your Chrome installation.
Next, download the chrome driver into downloads folder from https://chromedriver.chromium.org/downloads.
Move it to a directory you have permissions in, that's in your PATH:

    mv ~/Downloads/chromedriver /usr/local/bin

Trust it:

    xattr -d com.apple.quarantine /usr/local/bin/chromedriver

## Run `papermill`

Test that it has the parameter cell:

    papermill --help-notebook altair-example.ipynb

Now run:

    papermill altair-example.ipynb altair-example-papermill.ipynb

## Convert to HTML

    jupyter-nbconvert altair-example-papermill.ipynb --to html

## Setup for PDF

### Install tinytex

    curl -sL "https://yihui.org/tinytex/install-bin-unix.sh" | sh

Put it on the `PATH`:

    export PATH=$HOME/Library/TinyTeX/bin/universal-darwin:$PATH

Get the things we need, knock them out 1-by-1 via https://yihui.org/tinytex/#maintenance:

    tlmgr update --all --self
    tlmgr install tcolorbox
    tlmgr install pgf
    tlmgr install xcolor
    tlmgr install environ
    tlmgr install palatino
    tlmgr install courier
    tlmgr install mathpazo
    tlmgr install collection-fontsrecommended
    tlmgr install pdfcol
    tlmgr install lwarp
    tlmgr install oberdiek
    tlmgr install parskip
    tlmgr install caption
    tlmgr install upquote
    tlmgr install ucs
    tlmgr install adjustbox
    tlmgr install collectbox
    tlmgr install titling
    tlmgr install enumitem
    tlmgr install ulem
    tlmgr install jknapltx

## Inkscape

First, download inkscape dmg.
Copy it to `~/.local/` rather than `Applications` folder if you don't have admin.
Manually link it, if necessary:

    ln -s $HOME/.local/Inkscape.app/Contents/MacOS/inkscape /usr/local/bin/inkscape

# Make the pdf!

    jupyter-nbconvert altair-example-papermill.ipynb --to pdf
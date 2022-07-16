# How to combine wsl-pdflatex with TeXstudio

The idea here is use texlive distribution installed in ubuntu on wsl from TeXstudio intalled on windows 11.

Remark that there is some information about this fact in

https://marcus.handte.org/2017/11/18/using-texstudio-with-texlive-from-ubuntu-on-wsl/

and some discusion about this in

https://github.com/texstudio-org/texstudio/issues/698

The approach here is a little bit different.

## Installing wsl-alias

First, install wsl-alias from

https://github.com/leongrdic/wsl-alias

Do not forget to include the installation path into your user environment variable on Windows, which should be something like:

``C:\Users\YOUR_USER_NAME\wsl-alias;``

## Preparing wsl-alias

Use the command wsl-alias inside WSL to create an alias for pdflatex:

``wsl-alias add pdflatex pdflatex`` 

This will create a file `pdflatex.bat` inside the folder ``C:\Users\YOUR_USER_NAME\wsl-alias;``

You may want to add any environmental variables you use inside WSL. For instance, inside WSL I have edited `$HOME/.wsl-alias/env.sh` to add

.. code-block:: bash
  export BIBINPUTS=.:$HOME/Documents/Bibtex:$HOME/.bib:$BIBINPUTS
  
  export TEXINPUTS=.:$HOME/.TeX:$TEXINPUTS


This is a normal text paragraph. The next paragraph is a code sample::

   It is not processed in any way, except
   that the indentation is removed.

   It can span multiple lines.

This is a normal text paragraph again.


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

where `YOUR_USER_NAME` is your user path in windows

## Preparing wsl-alias

Use the command wsl-alias inside WSL to create an alias for pdflatex:

``wsl-alias add pdflatex pdflatex`` 

This will create a file `pdflatex.bat` inside the folder ``C:\Users\YOUR_USER_NAME\wsl-alias``

This part is optional, but you may want to add any environmental variables you use inside WSL. For instance, inside WSL I have edited `$HOME/.wsl-alias/env.sh` to add


```bash
export BIBINPUTS=.:$HOME/Documents/Bibtex:$HOME/.bib:$BIBINPUTS
export TEXINPUTS=.:$HOME/.TeX:$TEXINPUTS
```

## Configure TeXstudio

Now, you have everything prepared to configure TeXstudio on Windows. Just go to Configure and in commands, add to pdflatex something similar to 

``"C:/Users/YOUR_USER_NAME/wsl-alias/pdflatex.bat"  -synctex=1 -interaction=nonstopmode %.tex``

and you can now test if everything is working

## Configuring synctex

synctex will not work directly and you cannot go to source from the pdf or viceversa because synctex will refer to the linux path and TeXstudio will be on windows.

To fix this, edit ``C:\Users\YOUR_USER_NAME\wsl-alias\pdflatex.bat`` and after the line ``wsl ~/.wsl-alias/wrapper.sh '%pwd%' pdflatex %cmd%`` add the following

``wsl ~/.wsl-alias/wrapper.sh '%pwd%' ~/bin/synctex2win %cmd%``

Now, in WSL add the file  ``synctex2win`` located in this repository to a folder included in the PATH of WSL. 
It could be something lik ``$HOME/.local/bin``

You have to install perl as well in WSL as it will be needed by the script

That is, with that, everything should work now

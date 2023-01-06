====================
sphinx documentation
====================


Steps for creating sphinx doc
=============================

Links
-----

Please read the documentation online. Below are  reference links, you can checkout.

**Install sphinx in local**: https://www.sphinx-doc.org/en/master/usage/installation.html#linux

**Tutorial sphinx**:

https://www.sphinx-doc.org/en/master/usage/quickstart.html

https://docs.readthedocs.io/en/stable/intro/getting-started-with-sphinx.html


**readthedocs tutorial**: https://docs.readthedocs.io/en/latest/tutorial/index.html#


**reStructuredText-Documentation-Reference** : https://github.com/DevDungeon/reStructuredText-Documentation-Reference


**.rst demo source code**: https://github.com/DevDungeon/NanoLifePy#readme


**Youtube demo video**: 
    *Live Coding: Documentation w/ ReadTheDocs.org (RTFD)*
    **Reference link**: https://www.youtube.com/watch?v=UFYPLhhIDSg&list=LL&index=1

GitHub repo setup in local
--------------------------

1. Create a public repository on GitHub

2. Setup in local::

    cd /var/www/html/GitRepo/dipakp-docs
    git init
    git remote add origin https://github.com/dipakp-logicrays/dipakp-docs.git
    git fetch


**Source Code**: https://github.com/dipakp-logicrays/dipakp-docs

Configure sphinx
-----------------
- Run this command for creating the necessary files:: 

    sphinx-quickstart


- **Screenshots:**

    .. image:: images/configure-sphinx-1.png
        :alt: Configure sphinx


    .. image:: images/configure-sphinx-2.png
        :alt: Configure sphinx
    

- Check files and directories on the docs directory
    
    .. image:: images/directories.png
        :alt: File list



Install the extensions in vscode
---------------------------------
- Python
    .. image:: images/python-vscode.png
        :alt: Python vscode extension


- Makefile Tools
    .. image:: images/makefile-tool-vscode.png
        :alt: Makefile Tools vscode extension


Build sphinx
------------

	**make html**
		- It will build in ``/var/www/html/GitRepo/dipakp-docs/docs/_build/html``

        .. image:: images/build-html.png
            :alt: build html

	| **make man**
		- It will build in ``/var/www/html/GitRepo/dipakp-docs/docs/_build/man``
        
        .. image:: images/build-man.png
            :alt: build man
	
    | **make epub**
		- It will build in ``/var/www/html/GitRepo/dipakp-docs/docs/_build/epub``
        
        .. image:: images/build-epub.png
            :alt: build epub

Check html of the doc
---------------------
- Go to ``/var/www/html/GitRepo/dipakp-docs/docs/_build/html``

- Open ``index.html`` in a browser

-  **Screenshot**:
    .. image:: images/html-result.png
        :alt: html Result


Create .gitignore to root path:
-------------------------------
- **File**: ``/var/www/html/GitRepo/dipakp-docs/.gitignore`` 

-  **Example**: https://github.com/DevDungeon/Cathy

- Add the below code to this file::

    # Sphinx documentation
    docs/_build/

Create subpage in left sidebar
------------------------------
- **Screenshot**: 
    .. image:: images/sidebar-subpage.png
        :alt: html Result

-  Add the below code to ``/var/www/html/GitRepo/dipakp-docs/docs/index.rst``::

    pages/inviting-the-doc

- **Screenshot**:
    .. image:: images/sidebar-subpage-content.png
        :alt: html Result

- **Create pages directory**: ``/var/www/html/GitRepo/dipakp-docs/docs/pages``

- Create file same as title ``inviting-the-doc.rst``

- Add content as you want::


    =============================
    Inviting Dipak to your server
    =============================

    This will cover how to invite to your server.


- Execute the below command to build html and check in the browser::

    make html


**Push the all files on git**::

    git add .
    git config user.name "dipakp-logicrays"
    git config user.email "dipakp@logicrays.com"
    git commit -m "reStructuredText documentation"
    git push --set-upstream origin master

**Screenshots**:
	
    .. image:: images/github-command-list-1.png
        :alt: GitHub command list

    .. image:: images/github-command-list-2.png
        :alt: GitHub command list

    .. image:: images/github-directory-tree.png
        :alt: GitHub directories tree

Import project and configure on readthedocs
-------------------------------------------

**Sign up on readthedocs**: https://readthedocs.org/accounts/signup/

**Login  on readthedocs** : https://readthedocs.org/accounts/login/

Use the blue theme in the documentation:
----------------------------------------
- Open ``/var/www/html/GitRepo/dipakp-docs/docs/conf.py``

- comment on the below line::
	
    # html_theme = 'alabaster'

- git add, commit and push 

- After some time it will affect the blue theme

Install pip in linux
--------------------

#. Updating package info::

    sudo apt-get update

#. Downloading all upgrades::

    sudo apt-get upgrade

#. Reinstalling pip::

    sudo apt-get install python3-pip

#. Check ``pip`` installed

    .. image:: images/pip-installed.png
        :alt: pip installed

Change blue theme to readthedoc
-------------------------------

This theme is distributed on PyPI and can be installed with pip::

    pip install sphinx-rtd-theme

To use the theme in your Sphinx project, you will need to edit your ``conf.py`` file's html_theme setting::

    html_theme = "sphinx_rtd_theme"

Go to ``docs`` directory and run below command to apply theme::

    make html


Sphinx Documentation Steps
==========================

Reference Links
---------------

Please read the documentation online. Below are  reference links, you can checkout.

**Sphinx Tutorial**:

:Live Coding Documentation youtube video: https://www.youtube.com/watch?v=UFYPLhhIDSg&list=LL&index=1

:readthedocs tutorial: https://docs.readthedocs.io/en/latest/tutorial/index.html

:sphinx-doc official: https://www.sphinx-doc.org/en/master/usage/quickstart.html

:sphinx-doc readthedocs: https://docs.readthedocs.io/en/stable/intro/getting-started-with-sphinx.html

:reStructuredText-Documentation-Reference: https://github.com/DevDungeon/reStructuredText-Documentation-Reference

:.rst demo source code: https://github.com/DevDungeon/NanoLifePy#readme


Install sphinx
--------------  
    
    **Debian/Ubuntu**

    Install either python3-sphinx using apt-get::

        apt-get install python3-sphinx

    :Reference link: https://www.sphinx-doc.org/en/master/usage/installation.html#linux


Quick start
-----------

#. Create a public repository on GitHub

#. Setup in local::

    cd /var/www/html/GitRepo/dipakp-docs
    git init
    git remote add origin <your_public_github_repo_url>
    git fetch

#. Create a directory inside your project to hold your docs:

    .. prompt:: bash $

        mkdir docs

#. Run ``sphinx-quickstart`` in there:

    .. prompt:: bash $

        cd docs
        sphinx-quickstart

#. **Screenshots:**

    .. figure:: images/configure-sphinx-1.png
        :alt: Configure sphinx
        :align: center
        
        Configure sphinx

    .. figure:: images/configure-sphinx-2.png
        :alt: Configure sphinx
        :align: center

        Configure sphinx
    
#. Check files and directories on the docs directory
    
    .. image:: images/directories.png
        :alt: File list


Build Sphinx
------------
You can build html by executing ``make html`` command into ``docs`` directory.

	Run command : ``make html``
		- It will build in ``/var/www/html/GitRepo/dipakp-docs/docs/_build/html``

        .. image:: images/build-html.png
            :alt: build html

Check HTML Of The Doc
---------------------
- Go to ``/var/www/html/GitRepo/dipakp-docs/docs/_build/html``

- Open ``index.html`` in a browser

-  **Screenshot**:
    .. image:: images/html-result.png
        :alt: html Result


Install pip In Linux
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

Install ``sphinx_rtd_theme`` theme Locally
------------------------------------------

This theme is distributed on PyPI and can be installed with pip::

    pip install sphinx-rtd-theme

To use the theme in your Sphinx project, you will need to edit your ``conf.py`` file's html_theme setting::

    html_theme = "sphinx_rtd_theme"

Go to ``docs`` directory and run below command to apply theme::

    make html


Create Subpage In Left Sidebar
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


Install VS Code Extensions
--------------------------

- Python
    .. image:: images/python-vscode.png
        :alt: Python vscode extension


- Makefile Tools
    .. image:: images/makefile-tool-vscode.png
        :alt: Makefile Tools vscode extension

Install Sphinx Extensions
-------------------------

Following are require extension, install by below commands::

    pip install sphinx-hoverxref
    pip install sphinxcontrib.video
    pip install sphinx-prompt
    pip install readthedocs-sphinx-search
    pip install sphinx-notfound-page
    pip install sphinxemoji
    pip install sphinx_design
    pip install myst-parser

Install sphinx-code-tabs
------------------------

You can check how to install sphinx-code-tabs online at: https://pypi.org/project/sphinx-code-tabs/

**Installation**

.. code-block:: bash

    pip install sphinx_code_tabs

**Configure**

To enable the extension in sphinx, simply add the package name in your ``conf.py`` to the list of ``extensions``:

.. code-block:: bash

    extensions = [
        ...
        'sphinx_code_tabs',
    ]

**Usage**

By enabling the extension you get access to the ``tabs`` directive that declares a notebook of code block alternatives.

The individual tabs are created with the ``tab`` or ``code-tab`` directives. A ``tab`` can contain arbitrary restructuredText, while a ``code-tab`` acts like a ``code-block`` and accepts all corresponding arguments. Both types of tabs can appear in the same notebook.

The ``:selected:`` option allows to switch to a specified tab at start. By default, the first tab is used.

For example, this is the source of above example:

.. code-block:: bash

    .. tabs::

        .. code-tab:: bash

            echo "Hello, *World*!"

        .. code-tab:: c
            :caption: C/C++
            :emphasize-lines: 2

            #include <stdio.h>
            int main() { printf("Hello, *World*!\n"); }

        .. code-tab:: python

            print("Hello, *World*!")

        .. tab:: Output
            :selected:

            Hello, *World*!

**Grouped tabs**

The ``tabs`` directive takes an optional argument that identifies its *tab group*. Within a given tab group, all notebooks will automatically be switched to the same tab number if the tab is switched in one member of the group. It is your responsibility to make sure that each member of the group has the same number and ordering of tabs. Example:

.. code-block:: bash

    .. tabs:: lang

        .. code-tab:: bash

            echo "Hello, group!"

        .. code-tab:: python

            print("Hello, group!")


    .. tabs:: lang

        .. code-tab:: bash

            echo "Goodbye, group!"

        .. code-tab:: python

            print("Goodbye, group!")


sphinx doc configurations
-------------------------

You can use sphinx extensions and change default theme by below Steps

#. Change default theme in ``conf.py`` file
    
    .. code-block:: python
        
        html_theme = 'sphinx_rtd_theme'

#. Add sphinx extensions to ``conf.py`` file
    
    .. code-block:: python
        
        extensions = [
            "sphinx.ext.autodoc",
            "sphinxcontrib.video",
            "sphinx_tabs.tabs",
            "sphinx-prompt",
            "notfound.extension",
            "hoverxref.extension",
            "sphinxemoji.sphinxemoji",
            "sphinx_design",
        ]

#. Add below code bottom of line in ``conf.py`` file

    .. code-block:: python

        # If true, links to the reST sources are added to the pages.
        html_show_sourcelink = False

        # If true, "Created using Sphinx" is shown in the HTML footer. Default is True.
        html_show_sphinx = False

        myst_enable_extensions = [
            "deflist",
        ]
        hoverxref_intersphinx = [
            "sphinx",
            "pip",
            "nbsphinx",
            "myst-nb",
            "ipywidgets",
            "jupytext",
        ]

        hoverxref_auto_ref = True
        hoverxref_domains = ["py"]
        hoverxref_roles = [
            "option",
            "doc",  # Documentation pages
            "term",  # Glossary terms
        ]
        hoverxref_role_types = {
            "mod": "modal",  # for Python Sphinx Domain
            "doc": "modal",  # for whole docs
            "class": "tooltip",  # for Python Sphinx Domain
            "ref": "tooltip",  # for hoverxref_auto_ref config
            "confval": "tooltip",  # for custom object
            "term": "tooltip",  # for glossaries
        }
        hoverxref_ignore_refs = [
        ]
            


How to create reproducible builds 
---------------------------------

:Reference link: https://docs.readthedocs.io/en/stable/guides/reproducible-builds.html

#. Add ``.readthedocs.yml`` to project root

    .. code-block:: yaml
       :caption: readthedocs.yml

        version: 2

        formats:
        - pdf

        sphinx:
        configuration: docs/conf.py
        fail_on_warning: true

        python:
        install:
            - requirements: requirements/pip.txt
            - requirements: requirements/docs.txt

        build:
        os: ubuntu-22.04
        tools:
            python: "3.10"

#. Create below require files ``<project_root>/requirements/`` directory

    **Example**

    .. tabs::

        .. tab:: docs.in

            .. code-block:: bash

                # Packages required to build docs, independent of application dependencies

                -r pip.txt

                sphinx_rtd_theme==1.2.0rc1
                # Note: Version 3.4.1 of sphinx-tabs requires docutils 0.18 which is yet to be supported by sphinx-rtd-theme
                # Version 3.4.0 has an incompatible Jinja2 version which also blocks sphinx-rtd-theme
                # All-together, we cannot upgrade to Sphinx 5.x before either sphinx-tabs or sphinx-rtd-theme fixes these
                # issues.
                sphinx-tabs==3.3.1
                sphinx-intl==2.0.1
                sphinx-design==0.2.0
                sphinx-multiproject==1.0.0rc1
                readthedocs-sphinx-search==0.1.2

                # Test out hoverxref
                git+https://github.com/readthedocs/sphinx-hoverxref

                # Docs
                sphinxemoji==0.2.0
                sphinxcontrib-httpdomain==1.8.1
                sphinx-prompt==1.4.0
                sphinx-notfound-page==0.8
                sphinx-autobuild==2021.3.14

                # Markdown
                myst_parser==0.17.2

                # spinxcontrib-video
                git+https://github.com/readthedocs/sphinxcontrib-video/



        .. tab:: docs.txt
            
            .. code-block:: bash

                #
                # This file is autogenerated by pip-compile with Python 3.10
                # by the following command:
                #
                #    pip-compile --output-file=requirements/docs.txt --resolver=backtracking requirements/docs.in
                #

                docker==6.0.1
                    # via -r requirements/pip.txt
                docutils==0.17.1
                    # via
                    #   -r requirements/pip.txt
                    #   myst-parser
                    #   sphinx
                    #   sphinx-rtd-theme
                    #   sphinx-tabs

                sphinx==4.5.0
                    # via
                    #   -r requirements/pip.txt
                    #   myst-parser
                    #   sphinx-autobuild
                    #   sphinx-design
                    #   sphinx-hoverxref
                    #   sphinx-intl
                    #   sphinx-prompt
                    #   sphinx-rtd-theme
                    #   sphinx-tabs
                    #   sphinxcontrib-httpdomain
                    #   sphinxemoji
                sphinx-autobuild==2021.3.14
                    # via -r requirements/docs.in
                sphinx-design==0.2.0
                    # via -r requirements/docs.in
                sphinx-hoverxref @ git+https://github.com/readthedocs/sphinx-hoverxref
                    # via -r requirements/docs.in
                sphinx-intl==2.0.1
                    # via -r requirements/docs.in
                sphinx-multiproject==1.0.0rc1
                    # via -r requirements/docs.in
                sphinx-notfound-page==0.8
                    # via -r requirements/docs.in
                sphinx-prompt==1.4.0
                    # via -r requirements/docs.in
                sphinx-rtd-theme==1.2.0rc1
                    # via -r requirements/docs.in
                sphinx-tabs==3.3.1
                    # via -r requirements/docs.in
                sphinxcontrib-applehelp==1.0.2
                    # via
                    #   -r requirements/pip.txt
                    #   sphinx
                sphinxcontrib-devhelp==1.0.2
                    # via
                    #   -r requirements/pip.txt
                    #   sphinx
                sphinxcontrib-htmlhelp==2.0.0
                    # via
                    #   -r requirements/pip.txt
                    #   sphinx
                sphinxcontrib-httpdomain==1.8.1
                    # via -r requirements/docs.in
                sphinxcontrib-jquery==3.0.0
                    # via sphinx-hoverxref
                sphinxcontrib-jsmath==1.0.1
                    # via
                    #   -r requirements/pip.txt
                    #   sphinx
                sphinxcontrib-qthelp==1.0.3
                    # via
                    #   -r requirements/pip.txt
                    #   sphinx
                sphinxcontrib-serializinghtml==1.1.5
                    # via
                    #   -r requirements/pip.txt
                    #   sphinx
                sphinxcontrib-video @ git+https://github.com/readthedocs/sphinxcontrib-video/
                    # via -r requirements/docs.in
                sphinxemoji==0.2.0
                    # via -r requirements/docs.in
                wcwidth==0.2.5
                    # via
                    #   -r requirements/pip.txt
                    #   prompt-toolkit
                websocket-client==1.4.2
                    # via
                    #   -r requirements/pip.txt
                    #   docker

                # The following packages are considered to be unsafe in a requirements file:
                # setuptools
                myst_parser==0.17.2

        .. tab:: pip.in

            .. code-block:: bash

                # Base packages
                pip
                virtualenv

                # For intersphinx during builds
                # We need these pinned to build the docs properly
                Sphinx==4.5.0
                docutils==0.17.1

                docker

        .. tab:: pip.txt
        
            .. code-block:: bash

                #
                # This file is autogenerated by pip-compile with Python 3.10
                # by the following command:
                #
                #    pip-compile --output-file=requirements/pip.txt --resolver=backtracking requirements/pip.in
                #
                docker==6.0.1
                    # via -r requirements/pip.in
                docutils==0.17.1
                    # via
                    #   -r requirements/pip.in
                    #   sphinx
                wcwidth==0.2.5
                    # via prompt-toolkit
                websocket-client==1.4.2
                    # via docker

                # The following packages are considered to be unsafe in a requirements file:
                # pip


Create .gitignore To Root Path:
-------------------------------
- **File**: ``/var/www/html/GitRepo/dipakp-docs/.gitignore`` 

-  **Example**: https://github.com/DevDungeon/Cathy

- Add the below code to this file::

    # Sphinx documentation
    docs/_build/

**Push the all files on git**::

    git add .
    git config user.name "dipakp-logicrays"
    git config user.email "dipakp@logicrays.com"
    git commit -m "reStructuredText documentation"
    git push --set-upstream origin master

.. important::
    Please change your username and email

**Screenshots**:
	
    .. image:: images/github-command-list-1.png
        :alt: GitHub command list

    .. image:: images/github-command-list-2.png
        :alt: GitHub command list

    .. image:: images/github-directory-tree.png
        :alt: GitHub directories tree

Import Project And Configure On readthedocs
-------------------------------------------

**Sign up on readthedocs**: https://readthedocs.org/accounts/signup/

**Login  on readthedocs** : https://readthedocs.org/accounts/login/

After successfully logged in, You can import your github project.

Read more information: https://docs.readthedocs.io/en/stable/intro/import-guide.html
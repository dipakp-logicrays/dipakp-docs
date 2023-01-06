vscode configuration
====================

Download vscode
---------------

`Download Visual Studio Code`_
Free and built on open source. Integrated Git, debugging and extensions.

.. _Download Visual Studio Code: https://code.visualstudio.com/download


Adding ``Code Sniffer`` In vscode For Magento2:
-----------------------------------------------

Reference link: `Webkul code sniffer`_

.. _Webkul code sniffer: https://webkul.com/blog/adding-code-sniffer-in-visual-studio-code-for-magento2/


The code sniffer that Magento uses is Sqiz Lab/s code sniffer,
which checks the code on some PHP code standards check such as `PEAR coding standard`_ or `PSR`_,
by default it uses PEAR coding standard or you can switch to any other standard by simply using this command:


.. _PEAR coding standard: https://pear.php.net/manual/en/standards.php

.. _PSR: https://www.php-fig.org/psr/

**Magento uses its own code standard, which you can find on git**: https://github.com/magento/magento-coding-standard

Configuration Steps
~~~~~~~~~~~~~~~~~~~

#. Go to your ``/var/www/html/`` directory

#. Run below command::
    
    composer create-project magento/magento-coding-standard --stability=dev InstallationDir

#. Open vscode

#. Open setting.json by pressing ``ctrl+shift+p`` and select settings.json

    .. image:: images/settings-json.png
        :alt: Configure sphinx

#. Add below code to ``settings.json`` ::

    {
        "phpcs.executablePath": "/var/www/html/InstallationDir/vendor/bin/phpcs",
        "phpcs.standard": "/var/www/html/InstallationDir/Magento2/ruleset.xml",
    }

#. Check below Screenshot   

    .. image:: images/vscode-settings.png
        :alt: Configure sphinx

#. Now restart your editor and it will start showing code standard issues against Magento2 Code Standard on the fly, like below:

    .. image:: images/issue.png
       :alt: Configure sphinx

Extensions for Visual Studio Code
---------------------------------

These are useful extensions for developer:

* Apache Conf
* Auto Close TagAuto
* Auto Rename Tag
* AutoMageDev
* Better Comments
* change-case
* Color Picker
* Email
* Excel Viewer
* GraphQL:Syntax Highlighting
* HTML Snippets
* jQuery Code Snippets
* jQuery Snippets
* Live Server
* Magento 2 Snippets
* Magento DevSearch
* Magento Snippets
* Markdown All in One
* markdownlint
* Material Icon Theme
* Mithril Emmet
* phpcs
* PHP DocBlocker
* PHP Intelephense
* PHPStan
* Remote - SSH
* Thunder Client

Check following Screenshots

    .. figure:: images/vscode-ext1.png
        :align: center
        :alt: Visual Studio Extensions

        Visual Studio Extensions

    .. figure:: images/vscode-ext2.png
        :align: center
        :alt: Visual Studio Extensions

        Visual Studio Extensions
    
    .. figure:: images/vscode-ext3.png
        :align: center
        :alt: Visual Studio Extensions

        Visual Studio Extensions

vscode completely freeze or Hang
--------------------------------

Here, There are some settings that you need to change in vscode.

#. To fix this for a ``vscode`` you have to update the ``.vscode/settings.json`` to look something like this::

    {
        "files.exclude": {
            "**/.git": true,
            "**/.svn": true,
            "**/.hg": true,
            "**/CVS": true,
            "**/.DS_Store": true,
            "**/node_modules": true,
            "**/.firebase": true
        },
        "files.watcherExclude": {
            "**/.git/objects/**": true,
            "**/.git/subtree-cache/**": true,
            "**/node_modules/**": true
        }
    }

#. Switch off ``git.autorefresh`` in the Settings, then it works flawlessly and smoothly

    .. figure:: images/git-autorefresh.png
        :align: center
        :alt: Switch off git-autorefresh

        Switch off git-autorefresh

#. Press ``ctrl+shift+p``, Go to `Configure Runtime Arguments`, and add below line end of the file before closing the curly bracket::

    "disable-hardware-acceleration": true

#. Check below screenshot for above step:

    .. figure:: images/disable-hardware-acceleration.png
        :align: center
        :alt: disable hardware acceleration

        disable hardware acceleration

setting.json file example
-------------------------

This is the ``vscode settings.json`` file content, You can compare your ``settings.json`` file to the below content::

    {   
        // Magento Coding Standard
        "phpcs.executablePath": "/var/www/html/InstallationDir/vendor/bin/phpcs",
        "phpcs.standard": "/var/www/html/InstallationDir/Magento2/ruleset.xml",
        "workbench.iconTheme": "material-icon-theme",
        "security.workspace.trust.emptyWindow": false,
        "security.workspace.trust.startupPrompt": "never",
        "security.workspace.trust.untrustedFiles": "open",
        "security.workspace.trust.enabled": false,
        "git.autorefresh": false,
        "files.exclude": {
            "**/.git": true,
            "**/.svn": true,
            "**/.hg": true,
            "**/CVS": true,
            "**/.DS_Store": true,
            "**/node_modules": true,
            "**/.firebase": true
        },
        "files.watcherExclude": {
            "**/.git/objects/**": true,
            "**/.git/subtree-cache/**": true,
            "**/node_modules/**": true
        },
        "editor.linkedEditing": true,
        "bracketPairColorizer.depreciation-notice": false,
        "workbench.editorAssociations": {
            "*.gz": "default",
            "*.php": "default"
        },
        "workbench.startupEditor": "none",
        "intelephense.diagnostics.undefinedTypes": false,
        "intelephense.diagnostics.undefinedMethods": false,
        "intelephense.diagnostics.undefinedFunctions": false,
        "intelephense.diagnostics.undefinedConstants": false,
        "intelephense.diagnostics.undefinedProperties": false,
        "intelephense.diagnostics.undefinedSymbols": false,
        "intelephense.diagnostics.undefinedClassConstants": false,
        "intelephense.diagnostics.typeErrors": false,
        "intelephense.diagnostics.deprecated": false,
        "intelephense.diagnostics.implementationErrors": false,
        "intelephense.diagnostics.undefinedVariables": false,
        "intelephense.diagnostics.unexpectedTokens": false,
        "intelephense.diagnostics.unusedSymbols": false,
        "intelephense.diagnostics.duplicateSymbols": false,
        "intelephense.diagnostics.embeddedLanguages": false,
        "intelephense.diagnostics.enable": false,
        "intelephense.diagnostics.languageConstraints": false,
        "intelephense.phpdoc.returnVoid": false,
        "intelephense.completion.fullyQualifyGlobalConstantsAndFunctions": true,
        "workbench.editor.untitled.hint": "hidden",
        "better-comments.highlightPlainText": true,
        "editor.guides.bracketPairs": true,
        "workbench.editor.enablePreview": false,
        "editor.stickyScroll.enabled": true,
        "workbench.list.horizontalScrolling": true,
        "intelephense.format.enable": false,
    }
VS Code Configuration
=====================

Download VS Code
----------------

`Download Visual Studio Code`_
Free and built on open source. Integrated Git, debugging and extensions.

.. _Download Visual Studio Code: https://code.visualstudio.com/download


Adding ``Code Sniffer`` In VS Code For Magento 2
------------------------------------------------

Reference link: `Webkul code sniffer`_

.. _Webkul code sniffer: https://webkul.com/blog/adding-code-sniffer-in-visual-studio-code-for-magento2/


The code sniffer that Magento uses is Sqiz Lab/s code sniffer,
which checks the code on some PHP code standards check such as `PEAR coding standard`_ or `PSR`_,
by default it uses PEAR coding standard or you can switch to any other standard by simply using this command:


.. _PEAR coding standard: https://pear.php.net/manual/en/standards.php

.. _PSR: https://www.php-fig.org/psr/

**Magento uses its own code standard, which you can find on git**: https://github.com/magento/magento-coding-standard

**Configuration Steps**

#. Go to your ``/var/www/html/`` directory

#. Run below command::
    
    composer create-project magento/magento-coding-standard --stability=dev InstallationDir

#. Open VS Code 

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

Extensions For Visual Studio Code
---------------------------------

These are useful extensions for developer:

* Apache Conf
* Auto Close Tag
* Auto Complete Tag
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
* MagentoWizard
* Markdown All in One
* markdownlint
* Material Icon Theme
* Material Theme
* Material Theme Icons
* Mithril Emmet
* PHP Awesome Snippets
* PHP Constructor
* PHP Debug
* PHP DocBlocker
* PHP Getters & Setters
* PHP Intelephense
* PHP Support Utils
* phpcs
* PHPUnit Snippets
* PHPStan
* Remote - SSH
* Thunder Client
* ToDo+
* GitLens


Check following Screenshots

    .. figure:: images/vscode-ext-1.png
        :align: center
        :alt: Visual Studio Extensions

        Visual Studio Extensions

    .. figure:: images/vscode-ext-2.png
        :align: center
        :alt: Visual Studio Extensions

        Visual Studio Extensions
    
    .. figure:: images/vscode-ext-3.png
        :align: center
        :alt: Visual Studio Extensions

        Visual Studio Extensions
    
    .. figure:: images/vscode-ext-4.png
        :align: center
        :alt: Visual Studio Extensions

        Visual Studio Extensions

VS Code Freeze Or Hang
----------------------

Here, There are some settings that you need to change in VS Code.

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

setting.json File Example
-------------------------

This is the ``vscode settings.json`` file content, You can compare your ``settings.json`` file to the below content::

    {
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
        "intelephense.diagnostics.implementationErrors": false,
        "intelephense.diagnostics.undefinedVariables": false,
        "intelephense.diagnostics.unexpectedTokens": false,
        "intelephense.diagnostics.unusedSymbols": false,
        "intelephense.diagnostics.duplicateSymbols": false,
        "intelephense.diagnostics.embeddedLanguages": false,
        "intelephense.diagnostics.languageConstraints": false,
        "intelephense.completion.fullyQualifyGlobalConstantsAndFunctions": true,
        "workbench.editor.untitled.hint": "hidden",
        "better-comments.highlightPlainText": true,
        "editor.guides.bracketPairs": true,
        "workbench.editor.enablePreview": false,
        "editor.stickyScroll.enabled": true,
        "workbench.list.horizontalScrolling": true,
        "intelephense.format.enable": false,
        "editor.formatOnType": true,
        "editor.mouseWheelZoom": true,
        "editor.quickSuggestions": {
            "other": "on",
            "comments": "on",
            "strings": "on"
        },
        "editor.minimap.scale": 2,
        "editor.minimap.showSlider": "always",
        "editor.cursorBlinking": "phase",
        "editor.cursorStyle": "line",
        "editor.suggest.snippetsPreventQuickSuggestions": false,
        "php.suggest.basic": false,
        "intelephense.diagnostics.argumentCount": false,
        "intelephense.diagnostics.typeErrors": false,
        "files.associations": {
            "*.module": "php"
        },
        "intelephense.phpdoc.useFullyQualifiedNames": true,
        "editor.showFoldingControls": "always",
        "notebook.showFoldingControls": "always",
        "files.eol": "\r\n",
        "[python]": {
            "editor.formatOnType": true
        },
        "git.openRepositoryInParentFolders": "never",
        "terminal.integrated.shellIntegration.history": 10000,
        "intelephense.diagnostics.enable": false,
        "intelephense.diagnostics.deprecated": false,
        // "editor.foldingStrategy": "indentation"
        "editor.wordWrap": "on",
        "php.validate.run": "onType",
        "phpcs.showWarnings": false
    }

VS Code Snippet
---------------

#. Open Visual Studio Code

#. Click on the setting icon bottom left

#. Configure user settings

#. php.json

#. Add below code in snippet

    .. code-block:: bash

        {
            // Place your snippets for php here. Each snippet is defined under a snippet name and has a prefix, body and 
            // description. The prefix is what is used to trigger the snippet and the body will be expanded and inserted. Possible variables are:
            // $1, $2 for tab stops, $0 for the final cursor position, and ${1:label}, ${2:another} for placeholders. Placeholders with the 
            // same ids are connected.
            // Example:
            "PrintR and exit": {
                "prefix": "ep",
                "body": [
                    "echo '<pre>';",
                    "print_r($1);",
                    "exit();"
                ],
                "description": "echo print_r exit"
            },
            "PrintCustomLogger": {
                "prefix": "cLog",
                "body": [
                    "$writer = new \Zend_Log_Writer_Stream(BP . '/var/log/custom.log');"
                    "$logger = new \Zend_Log();"
                    "$logger->addWriter($writer);"
                    "$logger->info(print_r($1));"
                ],
                "description": "print custom logger"
                }
        }

#. You can use above snippet by ``ep`` for print_r and exit and ``cLog`` for print custom logger.
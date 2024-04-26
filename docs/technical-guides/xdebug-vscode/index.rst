Xdebug in vscode for PHP
========================

Xdebug is a PHP extension that provides debugging and profiling capabilities.
This article shows how you can enable and use Xdebug in the VSCode code editor.

Official Docs
-------------

**Official doc for Xdebug 3 — Documentation**: https://xdebug.org/docs/

**Install xdebug**:https://xdebug.org/docs/install


How to know the xdebug version I have installed?
------------------------------------------------

``php -v`` command output includes information about installed XDebug version:

.. figure:: images/if-xdebug-not-installed.png
    :align: center

.. note::
    This image captured when I was testing the ``Magento 2.4.3`` with ``php7.4``.

Install Xdebug
--------------

**For PHP8.1**
    .. code-block:: bash

        sudo apt-get install php8.1-xdebug

.. note::
    We will use php8.1 for debugging, You can change accoring to your php version.

**Restart apache**
    .. code-block:: bash

        sudo systemctl restart apache2

**Run command** ``php -v`` **to check xdebug installed**

    .. figure:: images/xdebug-installed.png
        :align: center

.. note::
    This image captured when I was debugging the ``Magento 2.4.3`` with ``php7.4``.


Install PHP Debug extension in vscode
-------------------------------------

#. Open VSCode editor.

#. Install the extension ``PHP Debug`` by Xdebug.

    .. figure:: images/php-debug-extension-vscode.png
        :align: center


Configure Xdebug
----------------

- Find Xdebug ini file by creating file `xdebuginfo.php` and put below content

    .. code-block:: php

        <?php echo xdebug_info(); ?>


- Find **Additional .ini files parsed** file path: `20-xdebug.ini`

- You will see like this:

    .. figure:: images/php-xdebug-ini-file-path.jpg
        :align: center

- Here, we will use ``php8.1``

- Open the file ``/etc/php/8.1/apache2/conf.d/20-xdebug.ini`` and add the following code to enable Xdebug:

    .. code-block:: ini

        zend_extension=xdebug.so
        xdebug.mode=develop,debug
        ; Use `trigger` when debug is not need, when you debug change it with `yes` for below line
        xdebug.start_with_request = trigger

**Restart apache**

    .. code-block:: bash

        sudo systemctl restart apache2

Create launch.json file
-----------------------

#. Open your project in VSCode.

#. In the left sidebar where you have the folder, extension, search, etc. icons, now you will also see the ``Debugger`` icon. or press ``ctrl + shift + D``

    .. figure:: images/run-debug.png
        :align: center

#. Click on the ``Debugger`` icon.

#. Click on create a ``launch.json``

    .. figure:: images/create-launch-json.png
        :align: center


#. It will show a popup to select the environment. Select ``PHP`` as the environment.

#. This will create a file ``.vscode/launch.json`` with the required configuration settings auto-loaded. Add below content after ``"port":9003`` in ``configuration`` section

    .. code-block:: json

        "pathMappings": {
            "/var/www/html/<your_project_directory_name>": "${workspaceFolder}"
        }


    The pathMappings in the above launch.json file indicates a mapping of server paths to local paths.

    **pathMappings**: A list of server paths mapping to the local source paths on your machine.

    Path mapping is used to make VS Code map the files on the server to the right files on your local machine.

    - My ``vscode/launch.json`` file example:

        .. code-block:: json

            {
                "version": "0.2.0",
                "configurations": [
                    {
                        "name": "Listen for Xdebug",
                        "type": "php",
                        "request": "launch",
                        "port": 9003,
                        "pathMappings": {
                            "/var/www/html/ci244p2": "${workspaceFolder}"
                        },
                    },
                    {
                        "name": "Launch currently open script",
                        "type": "php",
                        "request": "launch",
                        "program": "${file}",
                        "cwd": "${fileDirname}",
                        "port": 0,
                        "runtimeArgs": [
                            "-dxdebug.start_with_request=yes"
                        ],
                        "env": {
                            "XDEBUG_MODE": "debug,develop",
                            "XDEBUG_CONFIG": "remote_port=${port}"
                        }
                    }
                ]
            }


    .. note::

        If ${workspaceFolder} doesn’t work then you can try writing the absolute path to your project folder, like /var/www/html/your-project.

#. All settings are done now


Start/Stop Debugging in VSCode
------------------------------

:Reference link: https://blog.chapagain.com.np/enable-xdebug-in-vscode-for-php/

#. Let's debug customer login process

#. Open VSCode editor

#. Open a file. Typically, the ``vendor/magento/module-customer/Controller/Account/LoginPost.php`` file.

#. Set a breakpoint in the file around line 191

    .. code-block:: bash

	    $customer = $this->customerAccountManagement->authenticate($login['username'], $login['password']);

#. Click on the menu: ``Run > Start Debugging`` or Press ``F5`` to start debugging

#. Browse your site, go to customer login page , e.g. https://localhost/customer/account/login/

#. You should be able to see the variables section populated in the Debug section of your VSCode editor.

#. An icon set will appear in the code editor from where you can **Continue (F5)**, **Step Over (F10)**, **Step Into (F11)**, **Step Out (Shift+F11)**, **Restart (Shift+CMD+F5)**, or **Stop (Shift+F5)** the debugger.

#. You can debug with step in , step out and step over


Difference between step into, step over and step out
----------------------------------------------------

Step Into
    - In the debugging process, you reached a function call.
    - You clicked on the ``Step Into`` button.
    - The **debugger will go inside that function** and you can see how the **function is executing line by line** till it returns.
    - After it returns, the debugger takes you back to the next line right after your initial function call.

Step Over
    - In the debugging process, you reached a function call.
    - You clicked on the ``Step Over`` button.
    - The debugger just executes it like a black box, **returns the result, and goes to the next line**.
    - You cannot see how the function was executed.

Step Out
    - In the debugging process, you reached a function call.
    - You clicked on the “Step Into” button.
    - The debugger will go inside that function and you can see how the function is executing line by line till it returns.
    - Now, **if you don’t want to see the line-by-line execution of this function and want to return back early to the previous function, then you can click** “Step Out”.
    - The debugger will go back to the next line of your previous function call.

Demo video
----------

:Reference video: https://jumpshare.com/v/9n0Atl1NnLrLNrZWvGJw

YouTube Reference
-----------------
**Xdebug 3: Setting up Apache, PHP, VS Code, and Xdebug in 10 minutes** : https://www.youtube.com/watch?v=MmyxWy8jl7U&ab_channel=DerickRethans

**Magento 2 Debugging Tricks - xDebug by Matheus Gontijo**
    - Debug with ``setData`` , ``DataObject.php`` methods : https://youtu.be/eo8N7e9eEPI
    - ``MySQL Query``, ``fetchAll``, ``fetchRow``, ``Data Hydrate`` & PHP xDebug: https://youtu.be/xLf3OwpAFhQ

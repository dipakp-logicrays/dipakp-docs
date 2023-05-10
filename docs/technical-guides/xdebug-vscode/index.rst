Enable Xdebug in VSCode for PHP
===============================

Xdebug is a PHP extension that provides debugging and profiling capabilities.
This article shows how you can enable and use Xdebug in the VSCode code editor.

**Official doc for Xdebug 3 — Documentation**: https://xdebug.org/docs/

How to know the xdebug version I have installed?
------------------------------------------------

``php -v`` command output includes information about installed XDebug version:

.. figure:: images/if-xdebug-not-installed.png
    :align: center
	
Install Xdebug 
--------------

**Reference link**: https://xdebug.org/docs/install

**For PHP7.3**
    .. code-block:: bash

        sudo apt-get install php7.3-xdebug
    
**For PHP7.4**
    .. code-block:: bash

        sudo apt-get install php7.4-xdebug
    
**Restart apache**
    .. code-block:: bash

        sudo systemctl restart apache2

**Run command** ``php -v`` **to check xdebug installed**

    .. figure:: images/xdebug-installed.png
        :align: center

Install PHP Debug extension in vscode
-------------------------------------

#. Open VSCode editor.

#. Install the extension ``PHP Debug`` by Xdebug.

    .. figure:: images/php-debug-extension-vscode.png
        :align: center

	
Configure PHP to use Xdebug
---------------------------

**For php7.3:**

open the file ``/etc/php/7.3/mods-available/xdebug.ini`` and add the following code to enable Xdebug:

**For php7.4**

open the file ``/etc/php/7.4/mods-available/xdebug.ini`` and add the following code to enable Xdebug:

**Add Below content for Xdeubg 3**

    .. code-block:: bash

        zend_extension=xdebug.so
        xdebug.remote_enable=1
        xdebug.remote_autostart=1
        xdebug.remote_port=9003
        xdebug.remote_host=127.0.0.1
        xdebug.start_with_request = yes
        xdebug.mode = debug

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

#. This will create a file ``.vscode/launch.json`` with the required configuration settings auto-loaded. Add below content after ``"port":9003``
	
    Please change your project path and save the file

    .. code-block:: bash

        "pathMappings": {
            "/var/www/html/m243": "${workspaceFolder}"
        }

    .. figure:: images/launch-json.png
        :align: center
    

    The pathMappings in the above launch.json file indicates a mapping of server paths to local paths.

    **pathMappings**: A list of server paths mapping to the local source paths on your machine.

    Path mapping is used to make VS Code map the files on the server to the right files on your local machine.

    
    .. note::
        
        If ${workspaceFolder} doesn’t work then you can try writing the absolute path to your project folder, like /Users/mukeshchapagain/Sites/your-project.

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
    - The debugger will go inside that function and you can see how the function is executing line by line till it returns.
    - After it returns, the debugger takes you back to the next line right after your initial function call.

Step Over 
    - In the debugging process, you reached a function call.
    - You clicked on the ``Step Over`` button.
    - The debugger just executes it like a black box, returns the result, and goes to the next line.
    - You cannot see how the function was executed.

Step Out
    - In the debugging process, you reached a function call.
    - You clicked on the “Step Into” button.
    - The debugger will go inside that function and you can see how the function is executing line by line till it returns.
    - Now, if you don’t want to see the line-by-line execution of this function and want to return back early to the previous function, then you can click “Step Out”.
    - The debugger will go back to the next line of your previous function call.

Demo video
----------

:Reference video: https://jumpshare.com/v/9n0Atl1NnLrLNrZWvGJw

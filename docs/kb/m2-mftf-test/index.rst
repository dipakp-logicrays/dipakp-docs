Magento Functional Testing Framework (MFTF)
===========================================

Introduction
-------------
This tutorial will provide basic information of the `MFTF`_ test.

.. _MFTF: https://developer.adobe.com/commerce/testing/functional-testing-framework/

The Magento Functional Testing Framework (MFTF) is a framework used to perform automated end-to-end functional testing.

You have to follow the below **steps for the running MFTF test** and configure it in your system which I mentioned here,

Those steps, I collect from the official MFTF test document.

MFTF Tests Location
-------------------

MFTF supports two different locations for storing the tests and test artifacts (Just for knowledge where MFTF tests are available in Magento):

* ``<magento_root>/app/code/<vendor_name>/<module_name>/Test/Mftf/`` is the location of local, customized tests.
* ``<magento_root>/vendor/<vendor_name>/<module_name>/Test/Mftf/``  is the location of tests provided by Magento and vendors.

If you installed Magento with Composer, please refer to ``vendor/magento/<module_dir>/Test/Mftf/`` for examples.

Directory Structure
-------------------
Following are MFTF test directory structures

    .. figure:: images/directory-structure.png
        :align: left
        :alt: Directory Structure

        Directory Structure

.. important:: 
    Please follow the MFTF test steps for configuring and running the MFTF test in your local magento project setup. 
    I prepared this document and successfully worked and tested on the **Magento2.4.3-p1** version.

Prepare Environment
-------------------

Make sure that you have the following software installed and configured on your development environment:

- PHP version supported by the Adobe Commerce or Magento Open Source instance under test
- `Composer`_ 1.3 or later
- Java 1.8 or later (`Install JAVA and JRE`_)
- Selenium Server Standalone 3.1 or later 
- `ChromeDriver`_ 2.33 or later or other webdriver in the same directory

.. _Composer: https://getcomposer.org/download/
.. _Install JAVA and JRE: https://getcomposer.org/download/
.. _ChromeDriver: https://sites.google.com/a/chromium.org/chromedriver/downloads

Install Composer
~~~~~~~~~~~~~~~~

You can download composer here: https://getcomposer.org/download/

    .. figure:: images/install-composer.png
        :align: center
        :alt: Install composer

        Install composer

Install Java
~~~~~~~~~~~~

You can download here: https://www.oracle.com/java/technologies/downloads/

    .. figure:: images/install-java.png
        :align: center
        :alt: Install java

        Install java

You can **check version**: ``java --version``

    .. figure:: images/check-java-version.png
        :align: center
        :alt: Check Java version

Install ChromeDriver
~~~~~~~~~~~~~~~~~~~~

Install ChromeDriver 2.33 or later version

#. Go to the site and `download`_

#. Select ChromeDriver version

    .. figure:: images/select-chrome-driver.png
        :align: center
        :alt: Select ChromeDriver version

        Select  ChromeDriver version

#. Download zip file according to your system

#. Extract the zip file on magento root

    .. figure:: images/extract-chrome-driver-zip.png
        :align: center
        :alt: Select ChromeDriver version

        Select  ChromeDriver version

.. _download:  https://sites.google.com/a/chromium.org/chromedriver/downloads

Download Selenium Server
~~~~~~~~~~~~~~~~~~~~~~~~

#. Go to /var/www/html/<magento_root>

#. Run below command to download

    .. code-block:: bash
        
        curl -O http://selenium-release.storage.googleapis.com/3.14/selenium-server-standalone-3.14.0.jar


    .. figure:: images/download-selenium-server.png
        :align: left
        :width: 1400px
        :alt: download-selenium-server


Directory Structure After Installation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

After executing above all commands, it will show below files on magento root which is
highlighted on below screenshot.

    .. figure:: images/after-installation-directory-structure.png
        :align: center
        :alt: download-selenium-server



Find your MFTF Version
----------------------
You can check MFTF version by two ways

Using MFTF CLI
~~~~~~~~~~~~~~
    .. code-block:: bash
        
        vendor/bin/mftf --version
    
Using Composer CLI
~~~~~~~~~~~~~~~~~~
    .. code-block:: bash
    
        composer show magento/magento2-functional-testing-framework

WYSIWYG Admin Configuration
---------------------------

A Selenium web driver cannot enter data to fields with WYSIWYG.
To disable the WYSIWYG and enable the web driver to process these fields as simple text
areas:
#. Log in to the Magento Admin as an administrator.

#. Navigate to :guilabel:`Stores` > :guilabel:`Settings` > :guilabel:`Configuration` > :guilabel:`General` > :guilabel:`Content Management`.

#. In the WYSIWYG Options section set the **Enable WYSIWYG Editor** option to ``Disabled`` Completely.

#. Click Save Config.

#. Clear the cache

Change Security Settings
------------------------

You have to change security settings from admin configuration
To enable the **Admin Account Sharing setting**, to avoid unpredictable logout during a
testing session, and disable the Add Secret Key in URLs setting, to open pages using direct
URLs:

#. Navigate to :guilabel:`Stores` > :guilabel:`Settings` > :guilabel:`Configuration` >  :guilabel:`Advanced` > :guilabel:`Admin` > :guilabel:`Security`.

#. Set **Admin Account Sharing** to ``Yes``.

#. Set **Add Secret Key to URLs** to ``No``.

    .. figure:: images/system-config.png
        :align: center
        :alt: system-config

#. Click Save Config.

#. Clear the cache



.. note:: 
    If system config value not updated, you can fix by installing this module.
    Download and install this module: `Click here`_

.. _Click here: https://drive.google.com/file/d/17GojfOZ6_8ZfVaQJ5UWs8hx_bV_EQDWY/view

Check MFTF Health
-----------------

#. Open new terminal window and go to ``/var/www/html/<magento_root>``

#. Start your selenium-server by this command: ``java -jar selenium-server-standalone-3.14.0.jar``

#. You can check MFTF health by using this command: ``vendor/bin/mftf doctor``


Steps For The Running MFTF Test
-------------------------------

#. Go to your Magento root path
    .. code-block::bash

        cd /var/www/html/imgix-m243p1

#. Check MFTF version before running MFTF test
    .. code-block::bash

        cd /var/www/html/imgix-m243p1

    .. error::
        If you getting the below error::
        
            PHP Warning: require_once(/var/www/html/imgix-m243p1): failed to open stream:
            No such file or directory in /var/www/html/imgix-m243p1/vendor/bin/mftf on
            line 21


    **Fixed by modified this file**::
        
        <magento_root>/vendor/bin/mftf

    **Comment the below line**::

        // $autoloadPath = realpath(__DIR__ . '/../../../autoload.php');

    **Add a new line and set full path**::
    
        $autoloadPath = "/var/www/html/imgix-m243p1/app/autoload.php";

    **After update above the line, execute mftf version command**::
        
        vendor/bin/mftf --version
    
    .. figure:: images/mftf-doctor.png
        :align: center
        :alt: successfully run mftf doctor command
        
        Successfully run mftf doctor command

#. Build the project
    **Run this command**::

        vendor/bin/mftf build:project

    .. error::
        If you getting the below error::
        
            The codecept build command failed unexpectedly. Please see the above output for more details.


    **Fixed by modified this file**::
        
        <magento_root>/vendor/bin/codecept

    **Comment the below line**::

        // require __DIR__ . '/app.php';

    **Add a new line and set full path**::
    
        require "/var/www/html/imgix-m243p1/vendor/codeception/codeception/app.php"; // Set Full path manually
    
    **Execute again build project command**::

        vendor/bin/mftf build:project

#. Edit environmental settings
    In the ``<magento_root>/dev/tests/acceptance/`` directory, edit the ``.env`` file to match your system.

    - Open .env file::

        vim dev/tests/acceptance/.env

    - In the ``.env`` file replace the below code and save the file::

        MAGENTO_BASE_URL=http://127.0.0.1/imgix-m243p1/pub #Here imgix-m243p1 is base
        project directory
        MAGENTO_BACKEND_NAME=admin #Your magento admin name
        MAGENTO_ADMIN_USERNAME=admin #Your Magento admin username
        MAGENTO_ADMIN_PASSWORD=admin@123 #Your Magento admin password
        SELENIUM_CLOSE_ALL_SESSIONS=true
        BROWSER=chrome
        MODULE_ALLOWLIST=Magento_Framework,ConfigurableProductWishlist,ConfigurablePro
        ductCatalogSearch
        BROWSER_LOG_BLOCKLIST=other
        ELASTICSEARCH_VERSION=7
        SELENIUM_HOST=127.0.0.1
        SELENIUM_PORT=4444
        SELENIUM_PROTOCOL=http
        SELENIUM_PATH=/wd/hub
    
    .. important::
        Please configure your Magento admin credentials.

#. Enable the Magento CLI commands
    Run the below command::

        cp dev/tests/acceptance/.htaccess.sample dev/tests/acceptance/.htaccess

#. Generate and run tests 
    Executing the below command::
        
        vendor/bin/mftf generate:tests

    .. note:: 
        Sometimes, It will take some time to complete the execution.

    .. figure:: images/mftf-generate-test.png
        :align: center
        :width: 1400px
        :alt: Generate MFTF test
        
        Generate MFTF test

#. Start the Selenium server in new terminal window and Go to ``<magento_root>`` path
    Executing the below command::

        java -jar selenium-server-standalone-3.14.0.jar

    .. figure:: images/started-selenium-server.png
        :align: center
        :width: 1400px
        :alt: Started selenium server 
        
        Started selenium server 

#. Run a simple test (Admin Login Test)
    - Open a new tab on the terminal and go Magento root directory::

        cd /var/www/html/imgix-m243p1
    
    - Admin login mftf test::

        vendor/bin/mftf run:test AdminLoginSuccessfulTest

    - Result
        
        .. figure:: images/admin-login-mftf-test.png
            :align: center
            :width: 1400px
            :alt: Admin Login MFTF test 
            
            Admin Login MFTF test

Workflow MFTF
-------------

How MFTF test work

Test
~~~~

    - You should put one test in each file and the file name and test name must be the same and the name should follow camel casing.
        
    - For e.g **StorefrontSellerCreateTest**

Page
~~~~

    - We can define pages that will be visited during test case execution.
        
    - The naming convention of the file name and page name must be the same, and the name will follow camel casing and all the names must end with the “Page” suffix.
    
    - For e.g **StorefrontSellerCreatePage**

Section
~~~~~~~

    - A <section> is a reusable part of a <page> and is the standard file for defining UI elements on a page used in a test.

ActionGroup
~~~~~~~~~~~

    - An action group is a group of actions (like clicking on the button, page load, etc.).
        
    - It is very useful to create a group of actions for better reusability.
    
    - For e.g **LoginToStorefrontActionGroup**

Data
~~~~

    - Any test case will need some dummy data for completing the test case,
      like dummy data for a product to test product create flow,
      dummy data for the customer to test registration, and login feature.

    - All the data XML files must end with a data suffix.

MetaData
~~~~~~~~

    - While executing test cases sometimes the tester might need some data entities to be created at runtime and used in the test or delete all the created data after the test is complete.
        
    - This can be done using metadata.
    
    - You can create operations like create, delete, update, and get.

    - After creating, our own MFTF test cases for a custom module, we need to run generate command so that Magento will consider our test cases as well with their own default cases.

        
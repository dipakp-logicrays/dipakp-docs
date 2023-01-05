==========================
Install Magento Extensions
==========================

How to Install Magento 2 Extension
==================================

There are two ways of installing an extension in Magento 2. Let's consider them both.

Do you have a new Magento 2 store? Check out the Starter Pack with must-have plugins

.. important::
    Warning: Before installing any 3rd-party extension on your Magento, make sure to back up the root folder of the Magento website and of the database.

---------------------------------------
1. Method 1. Via Composer (recommended)
---------------------------------------

- The first option on how to install Magento 2 extension manually is via Composer.
- You can freely install, update, and remove Magento 2 extensions using Composer.
- Execute composer command to download and install magento extension::

    composer require logicrays/module-core

-----------------------------------------------
2. Method 2. Using Magento 2 extension zip file
-----------------------------------------------

- For the installation, please prepare Magento admin panel and SSH access details.

Follow the steps:
-----------------

 
2.1 upload and unpack the .zip file you've downloaded to ``<magento_root>/app/code/<Vendor_Name>/<Module_Name>``.

     .. image:: images/unzip-module.png
        :alt: Unzip module

2.2 connect to the server where the website source folder is located with FTP/SFTP client (WinSCP, Filezilla, etc).

2.3 run the following commands::

    php bin/magento setup:upgrade
    php bin/magento setup:di:compile
    php bin/magento setup:static-content:deploy


If you use the default or developer mode, you can skip the last 2 commands. 

That's it! These were all the options for how to install our module in Magento 2.
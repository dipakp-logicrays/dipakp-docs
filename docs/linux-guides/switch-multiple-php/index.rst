Switch Multiple PHP
===================

Basic Information
-----------------
    This tutorial walks you through the steps to **switch between multiple PHP versions** in Ubuntu Linux.
    
Reference Link
--------------
	This is `reference link`_ for switch multiple php.
    
.. _reference link: https://ostechnix.com/how-to-switch-between-multiple-php-versions-in-ubuntu/

Steps for Switch PHP Version
----------------------------

Switch From PHP 7.4 to PHP 8.1
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

    **Enable php8.1**::
        
        sudo a2enmod php8.1

    **Disable php7.4**::
        
        sudo a2dismod php7.4

    **Set Default php**::
        
        sudo update-alternatives --set php /usr/bin/php8.1

    **Show installed php**::

        sudo update-alternatives --config php

    **Restart apache 2**::

        sudo systemctl restart apache2


Switch From PHP 8.1 to PHP 7.4
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

    **Enable php7.4**::
        
        sudo a2enmod php7.4

    **Disable php8.1**::
        
        sudo a2dismod php8.1

    **Set Default php**::
        
        sudo update-alternatives --set php /usr/bin/php7.4

    **Show installed php**::

        sudo update-alternatives --config php

    **Restart apache 2**::

        sudo systemctl restart apache2

.. note::

        If you getting an error: ``ERROR: Module php8.1 does not exist!``,

        Just execute this command: ``sudo apt-get install libapache2-mod-php8.1``
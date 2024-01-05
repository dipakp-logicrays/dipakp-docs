Install Magento 2
=================

Here, We will install magento v2.4.4 in local environment in linux systetm.

Before you start installation, check `system requirements`_

.. _system requirements: https://devdocs.magento.com/guides/v2.3/install-gde/system-requirements.html

Magento Links
-------------
* `Magento installation guide`_
* `Magento Marketplace`_
* `Adobe Commerce 2.4 Developer Guide`_

.. _Magento installation guide: https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/composer.html?lang=en
.. _Magento Marketplace: https://marketplace.magento.com/
.. _Adobe Commerce 2.4 Developer Guide: https://devdocs.magento.com/

Switch PHP Version
------------------

**Enable php 8.1 and disbaled other php versions, here I'm disabling php7.3**

#. Disable php7.3::

	sudo a2dismod php7.3

#. Enable php8.1::

	sudo a2enmod php8.1

#. Set Default php::

	sudo update-alternatives --set php /usr/bin/php8.1

#. Show installed php::

	sudo update-alternatives --config php

#. Restart apache 2::

	sudo systemctl restart apache2


Steps For Install Magento 2
---------------------------

#. Enable php8.1 and disable other php::

    sudo a2enmod php8.1
    sudo a2dismod php7.4
    sudo update-alternatives --set php /usr/bin/php8.1
    sudo update-alternatives --config php
    sudo systemctl restart apache2


#. Install php8.1 extensions::

    sudo apt-get install php8.1-dom
    sudo apt-get install php8.1-xml
    sudo apt-get install php8.1-bcmath
    sudo apt-get install php8.1-curl
    sudo apt-get install php8.1-gd
    sudo apt-get install php8.1-intl
    sudo apt-get install php8.1-mbstring
    sudo apt-get install php8.1-mcrypt
    sudo apt-get install php8.1-zip
    sudo apt-get install php8.1-soap
    sudo apt-get install php8.1-mysql

#. Go to ``/var/www/html`` directory

#. Execute composer command to download magento

    **Using composer Magento community version** ::

        composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition=2.4.4 m244

    **Using composer Magento Enterprise** ::

        composer create-project --repository-url=https://repo.magento.com/ magento/project-enterprise-edition=2.4.4 m244 

#. Create DB using CLI::

    mysql -uroot -p
    pass: secret

    CREATE DATABASE m244;
    GRANT ALL PRIVILEGES ON m244.* TO 'root'@'localhost';
    FLUSH PRIVILEGES;


#. Change composer version 1 to 2 if needed::
    
    sudo composer self-update --2
    
#. Set file permissions::

    cd /var/www/html/m244
    find var generated vendor pub/static pub/media app/etc -type f -exec chmod g+w {} +
    find var generated vendor pub/static pub/media app/etc -type d -exec chmod g+ws {} +
    chown -R :www-data . # Ubuntu
    chmod u+x bin/magento

    # or

    find . -type f -exec chmod 644 {} \;            
    find . -type d -exec chmod 755 {} \;        
    chmod -Rf 777 var
    chmod -Rf 777 pub/static
    chmod -Rf 777 pub/media
    chmod 777 ./app/etc
    chmod 644 ./app/etc/*.xml
    chmod -Rf 775 bin

#. Install Magento using CLI::

    php bin/magento setup:install \
    --base-url=http://127.0.0.1/m244/pub \
    --db-host=localhost \
    --db-name=m244 \
    --db-user=root \
    --db-password=secret \
    --admin-firstname=admin \
    --admin-lastname=admin \
    --admin-email=dipakp@logicrays.com \
    --admin-user=admin \
    --admin-password=admin@123 \
    --language=en_US \
    --currency=USD \
    --timezone=America/Chicago \
    --use-rewrites=1 \
    --search-engine=elasticsearch7 \
    --elasticsearch-port=9200 \
    --elasticsearch-index-prefix=magento2 \
    --elasticsearch-timeout=15	


    [SUCCESS]: Magento installation complete.
    [SUCCESS]: Magento Admin URI: /admin_1ojk54
    Nothing to import.

#. Change admin url : /admin_1ojk54 to admin in ``app/etc/env.php``

#. Disable TwoFactorAuth Module:: 

    php bin/magento module:disable Magento_TwoFactorAuth

#. Run all Magento commands::

    php bin/magento deploy:mode:set developer
    php bin/magento s:up
    php bin/magento s:d:c
    php bin/magento s:s:d -f
    php bin/magento i:rei
    php bin/magento c:c
    php bin/magento c:f
    sudo chmod -R 777 generated/ pub/ var/

#. Check your frontend and admin are working properly.

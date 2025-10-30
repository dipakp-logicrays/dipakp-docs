Magento 2: Installation Guide
==============================

Complete guide for installing Magento 2 (Open Source and Adobe Commerce) on Ubuntu/Debian Linux systems.

.. contents:: Table of Contents
   :local:
   :depth: 2

Overview
--------

This guide covers:

- System requirements and prerequisites
- Installation via Composer (recommended)
- Installation via Archive
- Post-installation configuration
- Common installation issues and solutions

System Requirements
-------------------

Minimum Requirements
~~~~~~~~~~~~~~~~~~~~

**Operating System**
- Linux x86-64 (Ubuntu 20.04/22.04, Debian 10/11)

**Web Server**
- Apache 2.4.x with mod_rewrite
- Nginx 1.x

**Database**
- MySQL 8.0
- MariaDB 10.4, 10.5, 10.6

**PHP**
- PHP 8.1, 8.2, 8.3 (for Magento 2.4.6+)
- PHP 8.1, 8.2 (for Magento 2.4.4-2.4.5)

**Composer**
- Composer 2.x

**Search Engine**
- Elasticsearch 7.17, 8.x
- OpenSearch 1.x, 2.x

**Optional**
- Redis 6.x or later (for cache and session storage)
- Varnish 7.x (for page caching)
- RabbitMQ 3.11 (for message queues)

Hardware Recommendations
~~~~~~~~~~~~~~~~~~~~~~~~

.. list-table::
   :header-rows: 1
   :widths: 30 35 35

   * - Component
     - Minimum
     - Recommended
   * - RAM
     - 2 GB
     - 4 GB+
   * - CPU
     - 2 cores
     - 4+ cores
   * - Disk Space
     - 2 GB
     - 10 GB+ (SSD)

Prerequisites Installation
--------------------------

Before installing Magento 2, you need to have a LAMP stack (Linux, Apache, MySQL, PHP) configured on your system.

For detailed installation instructions, please refer to:

- :doc:`../../linux-guides/lamp-stack/index` - Complete LAMP stack installation guide including Apache, MySQL, PHP, Elasticsearch, and Composer installation
- :doc:`../../linux-guides/switch-multiple-php/index` - Guide for switching between multiple PHP versions

Quick Summary
~~~~~~~~~~~~~

If you already have LAMP stack installed, ensure you have:

- **PHP 8.1 or 8.2** (for Magento 2.4.4-2.4.5)
- **PHP 8.1, 8.2, or 8.3** (for Magento 2.4.6+)
- **All required PHP extensions** (see list below)
- **Composer 2.x**
- **MySQL 8.0** or **MariaDB 10.4+**
- **Elasticsearch 7.17, 8.x** or **OpenSearch 1.x, 2.x**

Required PHP Extensions
~~~~~~~~~~~~~~~~~~~~~~~

Ensure the following PHP extensions are installed:

.. code-block:: text

    bcmath, ctype, curl, dom, fileinfo, gd, hash, iconv, intl,
    json, libxml, mbstring, openssl, pcre, pdo_mysql, simplexml,
    soap, sodium, spl, xsl, zip, zlib

To check installed extensions:

.. code-block:: bash

    php -m | grep -E 'bcmath|ctype|curl|dom|fileinfo|gd|hash|iconv|intl|json|libxml|mbstring|openssl|pcre|pdo_mysql|simplexml|soap|sodium|spl|xsl|zip|zlib'

Configure PHP for Magento
~~~~~~~~~~~~~~~~~~~~~~~~~~

Edit PHP configuration file:

.. code-block:: bash

    sudo nano /etc/php/8.2/apache2/php.ini

Update the following settings:

.. code-block:: ini

    memory_limit = 2G
    max_execution_time = 1800
    zlib.output_compression = On
    upload_max_filesize = 64M
    post_max_size = 64M

Restart Apache:

.. code-block:: bash

    sudo systemctl restart apache2

Create Database
~~~~~~~~~~~~~~~

Create a database for Magento:

.. code-block:: bash

    sudo mysql -u root -p

.. code-block:: sql

    CREATE DATABASE magento2;
    CREATE USER 'magento2user'@'localhost' IDENTIFIED BY 'strong_password';
    GRANT ALL PRIVILEGES ON magento2.* TO 'magento2user'@'localhost';
    FLUSH PRIVILEGES;
    EXIT;

Installation Methods
--------------------

Method 1: Install via Composer (Recommended)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Step 1: Get Authentication Keys**

1. Go to https://marketplace.magento.com/
2. Navigate to My Profile > Marketplace > My Products > Access Keys
3. Generate new keys or use existing ones
   - Public Key = Username
   - Private Key = Password

**Step 2: Create Project Directory**

.. code-block:: bash

    cd /var/www/html
    sudo mkdir magento2
    sudo chown -R $USER:$USER magento2
    cd magento2

**Step 3: Install Magento**

.. code-block:: bash

    # For Magento Open Source
    composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition .

    # For Adobe Commerce
    composer create-project --repository-url=https://repo.magento.com/ magento/project-enterprise-edition .

When prompted, enter your authentication keys.

**Step 4: Set Permissions**

.. code-block:: bash

    cd /var/www/html/magento2
    find var generated vendor pub/static pub/media app/etc -type f -exec chmod g+w {} +
    find var generated vendor pub/static pub/media app/etc -type d -exec chmod g+ws {} +
    chown -R :www-data .
    chmod u+x bin/magento

**Step 5: Run Installation**

.. code-block:: bash

    php bin/magento setup:install \
    --base-url=http://magento2.local/ \
    --db-host=localhost \
    --db-name=magento2 \
    --db-user=magento2user \
    --db-password=strong_password \
    --admin-firstname=Admin \
    --admin-lastname=User \
    --admin-email=admin@example.com \
    --admin-user=admin \
    --admin-password=Admin@123 \
    --language=en_US \
    --currency=USD \
    --timezone=America/Chicago \
    --use-rewrites=1 \
    --search-engine=elasticsearch8 \
    --elasticsearch-host=localhost \
    --elasticsearch-port=9200 \
    --elasticsearch-index-prefix=magento2 \
    --elasticsearch-timeout=15

Method 2: Install from Archive
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Step 1: Download Magento**

.. code-block:: bash

    cd /var/www/html
    wget https://github.com/magento/magento2/archive/2.4.6.tar.gz
    tar -xzvf 2.4.6.tar.gz
    mv magento2-2.4.6 magento2

**Step 2: Install Dependencies**

.. code-block:: bash

    cd /var/www/html/magento2
    composer install

**Step 3: Set Permissions and Install**

Follow steps 4-5 from Method 1.

Configure Apache Virtual Host
------------------------------

For detailed Apache virtual host configuration, refer to:

- :doc:`../../linux-guides/virtual-host/index` - Complete guide for creating and configuring Apache virtual hosts

Create Virtual Host Configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Create a virtual host configuration for your Magento installation:

.. code-block:: bash

    sudo nano /etc/apache2/sites-available/magento2.conf

Add the following configuration:

.. code-block:: apache

    <VirtualHost *:80>
        ServerName magento2.local
        ServerAdmin admin@example.com
        DocumentRoot /var/www/html/magento2/pub

        <Directory /var/www/html/magento2/pub>
            Options Indexes FollowSymLinks MultiViews
            AllowOverride All
            Require all granted
        </Directory>

        ErrorLog ${APACHE_LOG_DIR}/magento2_error.log
        CustomLog ${APACHE_LOG_DIR}/magento2_access.log combined
    </VirtualHost>

Enable Site and Modules
~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

    # Enable rewrite module
    sudo a2enmod rewrite

    # Enable site
    sudo a2ensite magento2.conf

    # Disable default site
    sudo a2dissite 000-default.conf

    # Restart Apache
    sudo systemctl restart apache2

Update Hosts File
~~~~~~~~~~~~~~~~~

.. code-block:: bash

    sudo nano /etc/hosts

Add:

.. code-block:: text

    127.0.0.1   magento2.local

Post-Installation Configuration
--------------------------------

Common Post-Installation Steps
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

After installation, you may need to perform these common steps:

#. Change admin URL (if needed):

   Edit ``app/etc/env.php`` to change the admin URL from generated path (e.g., ``/admin_1ojk54``) to ``admin``.

#. Disable Two-Factor Authentication Module (for local development):

   .. code-block:: bash

       php bin/magento module:disable Magento_TwoFactorAuth

#. Run common Magento commands:

   .. code-block:: bash

       php bin/magento deploy:mode:set developer
       php bin/magento setup:upgrade
       php bin/magento setup:di:compile
       php bin/magento setup:static-content:deploy -f
       php bin/magento indexer:reindex
       php bin/magento cache:clean
       php bin/magento cache:flush
       sudo chmod -R 777 generated/ pub/ var/

   Or use shortcut commands:

   .. code-block:: bash

       php bin/magento deploy:mode:set developer
       php bin/magento s:up
       php bin/magento s:d:c
       php bin/magento s:s:d -f
       php bin/magento i:rei
       php bin/magento c:c
       php bin/magento c:f
       sudo chmod -R 777 generated/ pub/ var/

   Where:
   
   - ``s:up`` = ``setup:upgrade``
   - ``s:d:c`` = ``setup:di:compile``
   - ``s:s:d -f`` = ``setup:static-content:deploy -f``
   - ``i:rei`` = ``indexer:reindex``
   - ``c:c`` = ``cache:clean``
   - ``c:f`` = ``cache:flush``

#. Check your frontend and admin are working properly.

Deploy Static Content
~~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

    php bin/magento setup:static-content:deploy -f

Set Magento Mode
~~~~~~~~~~~~~~~~

.. code-block:: bash

    # For development
    php bin/magento deploy:mode:set developer

    # For production
    php bin/magento deploy:mode:set production

Configure Cron
~~~~~~~~~~~~~~

.. code-block:: bash

    # Install cron
    php bin/magento cron:install

    # Verify cron is running
    crontab -l

Configure Redis (Optional)
~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Install Redis**

.. code-block:: bash

    sudo apt install redis-server -y
    sudo systemctl enable redis-server
    sudo systemctl start redis-server

**Configure Magento to use Redis**

Edit ``app/etc/env.php``:

.. code-block:: php

    'cache' => [
        'frontend' => [
            'default' => [
                'backend' => 'Cm_Cache_Backend_Redis',
                'backend_options' => [
                    'server' => '127.0.0.1',
                    'port' => '6379',
                    'database' => '0',
                    'compress_data' => '1'
                ]
            ],
            'page_cache' => [
                'backend' => 'Cm_Cache_Backend_Redis',
                'backend_options' => [
                    'server' => '127.0.0.1',
                    'port' => '6379',
                    'database' => '1',
                    'compress_data' => '1'
                ]
            ]
        ]
    ],

Configure Two-Factor Authentication
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Disable for local development:

.. code-block:: bash

    php bin/magento module:disable Magento_TwoFactorAuth
    php bin/magento cache:flush

Verification
------------

Check Installation
~~~~~~~~~~~~~~~~~~

**1. Access Frontend**

Open browser: http://magento2.local/

**2. Access Admin Panel**

URL: http://magento2.local/admin

**3. Run System Check**

.. code-block:: bash

    php bin/magento sys:check

**4. Check Module Status**

.. code-block:: bash

    php bin/magento module:status

**5. Verify Cron**

.. code-block:: bash

    php bin/magento cron:run
    tail -f var/log/system.log

Performance Optimization
------------------------

Enable Flat Catalog
~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

    # Enable flat catalog
    php bin/magento config:set catalog/frontend/flat_catalog_category 1
    php bin/magento config:set catalog/frontend/flat_catalog_product 1

    # Reindex
    php bin/magento indexer:reindex

Configure Full Page Cache
~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

    # Enable full page cache
    php bin/magento cache:enable full_page

Production Mode Optimization
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

    # Compile DI
    php bin/magento setup:di:compile

    # Deploy static content
    php bin/magento setup:static-content:deploy -f

    # Set production mode
    php bin/magento deploy:mode:set production

Troubleshooting
---------------

Common Issues
~~~~~~~~~~~~~

**Issue 1: Permission Errors**

.. code-block:: bash

    cd /var/www/html/magento2
    find var generated vendor pub/static pub/media app/etc -type f -exec chmod g+w {} +
    find var generated vendor pub/static pub/media app/etc -type d -exec chmod g+ws {} +
    chown -R :www-data .
    chmod u+x bin/magento

**Issue 2: 404 Error on Admin**

.. code-block:: bash

    php bin/magento cache:flush
    php bin/magento setup:upgrade

**Issue 3: Blank Pages**

Check PHP error logs:

.. code-block:: bash

    tail -f /var/log/apache2/magento2_error.log
    tail -f var/log/system.log
    tail -f var/log/exception.log

Enable display errors in ``pub/index.php``:

.. code-block:: php

    ini_set('display_errors', 1);
    ini_set('display_startup_errors', 1);
    error_reporting(E_ALL);

**Issue 4: Elasticsearch Connection Failed**

.. code-block:: bash

    # Check Elasticsearch status
    sudo systemctl status elasticsearch

    # Test connection
    curl -X GET 'http://localhost:9200'

    # Restart Elasticsearch
    sudo systemctl restart elasticsearch

**Issue 5: Composer Authentication**

.. code-block:: bash

    # Clear composer cache
    composer clear-cache

    # Re-add credentials
    composer config --global http-basic.repo.magento.com <public_key> <private_key>

**Issue 6: Out of Memory**

Increase PHP memory limit:

.. code-block:: bash

    sudo nano /etc/php/8.2/apache2/php.ini
    # Set: memory_limit = 4G

    sudo systemctl restart apache2

Maintenance Commands
--------------------

Update Magento
~~~~~~~~~~~~~~

.. code-block:: bash

    # Enable maintenance mode
    php bin/magento maintenance:enable

    # Backup
    php bin/magento setup:backup --code --media --db

    # Update via composer
    composer update

    # Upgrade
    php bin/magento setup:upgrade
    php bin/magento setup:di:compile
    php bin/magento setup:static-content:deploy -f
    php bin/magento indexer:reindex
    php bin/magento cache:flush

    # Disable maintenance
    php bin/magento maintenance:disable

Backup Database
~~~~~~~~~~~~~~~

.. code-block:: bash

    # Create backup
    php bin/magento setup:backup --db

    # Manual backup
    mysqldump -u magento2user -p magento2 > magento2_backup_$(date +%Y%m%d).sql

Clear Cache
~~~~~~~~~~~

.. code-block:: bash

    # Clear all cache
    php bin/magento cache:flush

    # Clear specific cache
    php bin/magento cache:clean config full_page

    # Manually clear cache
    rm -rf var/cache/* var/page_cache/* var/view_preprocessed/*

Reindex Data
~~~~~~~~~~~~

.. code-block:: bash

    # Reindex all
    php bin/magento indexer:reindex

    # Reindex specific indexer
    php bin/magento indexer:reindex catalog_product_price

    # Check indexer status
    php bin/magento indexer:status

Security Best Practices
-----------------------

1. **Change Admin URL**

   .. code-block:: bash

       php bin/magento setup:config:set --backend-frontname="custom_admin"

2. **Use Strong Passwords**
   - Admin password minimum 12 characters
   - Database password should be complex

3. **Disable Developer Mode in Production**

   .. code-block:: bash

       php bin/magento deploy:mode:set production

4. **Enable Two-Factor Authentication**

   .. code-block:: bash

       php bin/magento module:enable Magento_TwoFactorAuth

5. **Regular Updates**
   - Keep Magento updated
   - Update PHP, MySQL, and server software

6. **Set Proper File Permissions**
   - Follow Magento's permission guidelines
   - Don't use 777 permissions

7. **Use HTTPS**
   - Install SSL certificate
   - Force HTTPS in Magento admin

Quick Reference
---------------

Essential Commands
~~~~~~~~~~~~~~~~~~

.. list-table::
   :header-rows: 1
   :widths: 50 50

   * - Command
     - Description
   * - ``setup:install``
     - Install Magento
   * - ``setup:upgrade``
     - Update database schema
   * - ``setup:di:compile``
     - Compile dependencies
   * - ``setup:static-content:deploy``
     - Deploy static files
   * - ``cache:flush``
     - Clear cache
   * - ``indexer:reindex``
     - Reindex data
   * - ``deploy:mode:set``
     - Set Magento mode
   * - ``maintenance:enable/disable``
     - Toggle maintenance mode
   * - ``cron:install``
     - Install cron jobs
   * - ``module:status``
     - List module status

Installation Checklist
~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: text

    ☐ System requirements met
    ☐ Apache/Nginx installed
    ☐ MySQL/MariaDB installed
    ☐ PHP 8.x with all extensions
    ☐ Composer installed
    ☐ Elasticsearch installed
    ☐ Database created
    ☐ Authentication keys obtained
    ☐ Magento installed
    ☐ Virtual host configured
    ☐ Permissions set
    ☐ Cron configured
    ☐ Admin accessible
    ☐ Frontend working

See Also
--------

Prerequisites
~~~~~~~~~~~~~

- :doc:`../../linux-guides/lamp-stack/index` - Complete LAMP stack installation guide (Apache, MySQL, PHP, Elasticsearch, Composer)
- :doc:`../../linux-guides/switch-multiple-php/index` - Guide for switching between multiple PHP versions
- :doc:`../../linux-guides/virtual-host/index` - Apache virtual host configuration guide

Magento Related
~~~~~~~~~~~~~~~

- :doc:`../module-installation/index` - Module installation guide
- :doc:`../mftf-testing/index` - MFTF testing framework guide
- :doc:`../n98-magerun2/index` - n98-magerun2 CLI tool

External References
~~~~~~~~~~~~~~~~~~~

- `Magento DevDocs <https://devdocs.magento.com/>`_
- `Magento Installation Guide <https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/overview.html>`_

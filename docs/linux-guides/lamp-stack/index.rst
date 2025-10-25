LAMP Stack Installation Guide
==============================

Complete guide for installing and configuring Linux, Apache, MySQL, PHP (LAMP) stack along with Elasticsearch and Composer on Linux systems.

.. contents:: Table of Contents
   :local:
   :depth: 3

Introduction
------------

What is LAMP Stack?
~~~~~~~~~~~~~~~~~~~

LAMP is an acronym for a popular open-source web development platform consisting of:

- **L**\ inux: Operating System
- **A**\ pache: Web Server
- **M**\ ySQL: Database Server
- **P**\ HP: Server-side Scripting Language

This guide also covers installation of Elasticsearch (search engine) and Composer (PHP dependency manager) to create a complete development environment.

**Benefits of LAMP Stack:**

- Open-source and free
- Cross-platform compatibility
- Mature and stable technology
- Large community support
- Extensive documentation
- Wide range of applications support

Prerequisites
-------------

Before starting the installation, ensure you have:

- A Linux system (Ubuntu/Linux Mint/Debian-based distribution)
- Root or sudo access
- Internet connection
- At least 2GB of RAM (4GB recommended)
- At least 20GB of free disk space

.. warning::
   Always backup your system before making major configuration changes. Some commands in this guide require root privileges.

Apache Web Server Installation
-------------------------------

Update System Packages
~~~~~~~~~~~~~~~~~~~~~~~

First, update your system to ensure all packages are current:

.. code-block:: bash

   sudo apt-get update && sudo apt-get upgrade

.. note::
   The ``&&`` operator ensures the upgrade only runs if the update succeeds.

Install Apache
~~~~~~~~~~~~~~

Install the Apache2 web server package:

.. code-block:: bash

   sudo apt install apache2

The system will prompt you to continue. Type ``y`` and press Enter to proceed.

Verify Apache Installation
~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Check Apache Version:**

.. code-block:: bash

   sudo apache2ctl -v

**Test Apache in Browser:**

Open your web browser and navigate to:

- ``http://localhost/``
- or ``http://127.0.0.1``

If you see the Apache default page, the installation was successful.

.. tip::
   The Apache default page indicates Apache is running correctly. You can now replace it with your own content.

Configure UFW Firewall (Remote Servers)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If you're setting up a remote server, configure the UFW firewall to allow web traffic:

.. code-block:: bash
   :caption: UFW Firewall Configuration

   # Check UFW status
   sudo ufw status

   # Enable UFW
   sudo ufw enable

   # List available applications
   sudo ufw app list

   # Allow OpenSSH (important for remote access)
   sudo ufw allow OpenSSH

   # Allow SSH on port 22
   sudo ufw allow 22

   # Allow Apache Full (ports 80 and 443)
   sudo ufw allow 'Apache Full'

   # Verify rules
   sudo ufw show added

.. danger::
   Never run ``sudo ufw disable`` or ``sudo ufw reset`` on a remote server without ensuring you have alternative access. This could lock you out of your server.

**UFW Profile Options:**

- ``Apache Full``: Opens both port 80 (HTTP) and 443 (HTTPS)
- ``Apache``: Opens only port 80 (HTTP)
- ``Apache Secure``: Opens only port 443 (HTTPS)

Enable Apache Modules
~~~~~~~~~~~~~~~~~~~~~~

Enable the rewrite module for URL rewriting:

.. code-block:: bash

   sudo a2enmod rewrite

Restart Apache to apply changes:

.. code-block:: bash

   sudo systemctl restart apache2

Manage Apache Service
~~~~~~~~~~~~~~~~~~~~~~

**For Systemd Systems:**

.. code-block:: bash

   # Start Apache
   sudo systemctl start apache2

   # Enable Apache on boot
   sudo systemctl enable apache2

   # Check Apache status
   sudo systemctl status apache2

   # Reload Apache configuration
   sudo systemctl reload apache2

   # Restart Apache
   sudo systemctl restart apache2

**For SysVinit Systems:**

.. code-block:: bash

   # Start Apache
   sudo service apache2 start

   # Enable on boot
   sudo chkconfig httpd on

   # Check status
   sudo service apache2 status

Set Directory Permissions
~~~~~~~~~~~~~~~~~~~~~~~~~~

Set appropriate permissions for the web root directory:

.. code-block:: bash

   cd /var/www/
   sudo chmod -R 777 html/

.. warning::
   Setting permissions to 777 gives full access to all users. This is convenient for development but **NOT recommended for production environments**. Use more restrictive permissions (755 or 644) in production.

Troubleshooting Apache
-----------------------

Configuration Test
~~~~~~~~~~~~~~~~~~

If Apache is not working, test the configuration:

.. code-block:: bash

   apache2ctl configtest

This command will identify syntax errors in the ``apache2.conf`` file.

Fix 404 Not Found Errors
~~~~~~~~~~~~~~~~~~~~~~~~~

**Problem:** Pages return 404 errors even though files exist.

**Solution:**

1. Enable the rewrite module:

.. code-block:: bash

   sudo a2enmod rewrite

2. Edit Apache configuration:

.. code-block:: bash

   sudo nano /etc/apache2/apache2.conf

3. Find the ``<Directory /var/www/>`` section and modify:

.. code-block:: apache
   :caption: /etc/apache2/apache2.conf - Before

   <Directory /var/www/>
       Options Indexes FollowSymLinks
       AllowOverride None
       Require all granted
   </Directory>

.. code-block:: apache
   :caption: /etc/apache2/apache2.conf - After

   <Directory /var/www/>
       Options Indexes FollowSymLinks
       AllowOverride All
       Require all granted
   </Directory>

4. Restart Apache:

.. code-block:: bash

   sudo service apache2 restart
   # or
   sudo /etc/init.d/apache2 restart

Fix 403 Forbidden Errors
~~~~~~~~~~~~~~~~~~~~~~~~~

**Problem:** Access to pages results in 403 Forbidden errors.

**Solution:**

Open the Apache configuration file:

.. code-block:: bash

   sudo nano /etc/apache2/apache2.conf

Update the ``<Directory /var/www/>`` section:

.. code-block:: apache
   :caption: /etc/apache2/apache2.conf

   <Directory /var/www/>
       Options Indexes FollowSymLinks MultiViews
       AllowOverride All
       Order allow,deny
       Allow from all
   </Directory>

Configure ServerName
~~~~~~~~~~~~~~~~~~~~

To eliminate the "Could not reliably determine the server's fully qualified domain name" warning:

1. Open Apache configuration:

.. code-block:: bash

   sudo nano /etc/apache2/apache2.conf

2. Add the following line at the bottom:

.. code-block:: apache

   ServerName 127.0.0.1

3. Save and restart Apache:

.. code-block:: bash

   sudo systemctl restart apache2

MySQL Database Installation
----------------------------

Install MySQL Server
~~~~~~~~~~~~~~~~~~~~

Install MySQL using the apt package manager:

.. code-block:: bash

   sudo apt install mysql-server

When prompted, type ``Y`` to confirm installation and press Enter.

Verify MySQL Installation
~~~~~~~~~~~~~~~~~~~~~~~~~~

Check the installed MySQL version:

.. code-block:: bash

   mysql -V

Configure MySQL Root Password
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

MySQL 8.0+ requires secure password configuration for the root user.

**Step 1: Login to MySQL as root:**

.. code-block:: bash

   sudo mysql

**Step 2: Check current authentication methods:**

.. code-block:: sql

   SELECT user, authentication_string, plugin, host FROM mysql.user;

**Step 3: Set a secure password for root:**

.. code-block:: sql
   :caption: MySQL Root Password Configuration

   -- Replace 'your_secure_password' with your actual password
   ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'your_secure_password';

.. important::
   Choose a strong password with a mix of uppercase, lowercase, numbers, and special characters. Store it securely.

**Step 4: Exit MySQL:**

.. code-block:: sql

   EXIT;

**Step 5: Login with the new password:**

.. code-block:: bash

   mysql -u root -p

Enter your password when prompted.

Create Database
~~~~~~~~~~~~~~~

Create a database for your application:

.. code-block:: sql
   :caption: Example: Creating a Database

   CREATE DATABASE magento2;

List all databases:

.. code-block:: sql

   SHOW DATABASES;

Exit MySQL:

.. code-block:: sql

   EXIT;

.. note::
   Database names are case-sensitive on Linux systems. Use consistent naming conventions.

MySQL Security Configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Run the MySQL security script to improve security:

.. code-block:: bash

   sudo mysql_secure_installation

This interactive script will prompt you to:

1. **Set password validation policy** - Choose password strength requirements
2. **Remove anonymous users** - Recommended: Yes
3. **Disallow root login remotely** - Recommended: Yes (for production)
4. **Remove test database** - Recommended: Yes
5. **Reload privilege tables** - Recommended: Yes

.. warning::
   For production servers, always:

   - Use strong passwords for all MySQL users
   - Disable remote root access
   - Create separate database users with minimal required privileges
   - Keep MySQL updated with security patches

Create Database User with Privileges
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Instead of using root for applications, create dedicated users:

.. code-block:: sql
   :caption: Creating a Database User

   -- Create a new user
   CREATE USER 'appuser'@'localhost' IDENTIFIED BY 'secure_password';

   -- Grant privileges to specific database
   GRANT ALL PRIVILEGES ON magento2.* TO 'appuser'@'localhost';

   -- Grant specific privileges only
   GRANT SELECT, INSERT, UPDATE, DELETE ON magento2.* TO 'appuser'@'localhost';

   -- Apply changes
   FLUSH PRIVILEGES;

   -- Verify user privileges
   SHOW GRANTS FOR 'appuser'@'localhost';

Manage MySQL Service
~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

   # Start MySQL
   sudo systemctl start mysql

   # Stop MySQL
   sudo systemctl stop mysql

   # Restart MySQL
   sudo systemctl restart mysql

   # Check MySQL status
   sudo systemctl status mysql

   # Enable MySQL on boot
   sudo systemctl enable mysql

   # View MySQL error logs
   sudo tail -f /var/log/mysql/error.log

Useful MySQL Commands
~~~~~~~~~~~~~~~~~~~~~

.. code-block:: sql
   :caption: Common MySQL Operations

   -- List all databases
   SHOW DATABASES;

   -- Select a database
   USE database_name;

   -- List all tables in current database
   SHOW TABLES;

   -- Show table structure
   DESCRIBE table_name;

   -- Export database (run from terminal)
   -- mysqldump -u root -p database_name > backup.sql

   -- Import database (run from terminal)
   -- mysql -u root -p database_name < backup.sql

   -- Drop database (be careful!)
   DROP DATABASE database_name;

   -- Create database with character set
   CREATE DATABASE mydb CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;

PHP Installation and Configuration
-----------------------------------

Update System Packages
~~~~~~~~~~~~~~~~~~~~~~~

Update the package manager:

.. code-block:: bash

   sudo apt update && sudo apt upgrade

Install Required Dependencies
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Install dependencies required for PHP installation:

.. code-block:: bash

   sudo apt install software-properties-common ca-certificates lsb-release apt-transport-https

Add Ondrej PPA Repository
~~~~~~~~~~~~~~~~~~~~~~~~~~

Add the Ondrej repository, which provides multiple PHP versions:

.. code-block:: bash

   LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php

Update package cache:

.. code-block:: bash

   sudo apt update

Install PHP
~~~~~~~~~~~

The Ondrej repository provides PHP versions 5.6, 7.0, 7.1, 7.2, 7.3, 7.4, 8.0, 8.1, 8.2, 8.3, and 8.4.

**Install your preferred version:**

.. code-block:: bash

   # PHP 8.4 (Latest)
   sudo apt install php8.4

   # PHP 8.3
   sudo apt install php8.3

   # PHP 8.2
   sudo apt install php8.2

   # PHP 8.1
   sudo apt install php8.1

   # PHP 8.0
   sudo apt install php8.0

   # PHP 7.4
   sudo apt install php7.4

   # PHP 7.3
   sudo apt install php7.3

   # PHP 7.2
   sudo apt install php7.2

   # PHP 5.6 (Legacy)
   sudo apt install php5.6

.. tip::
   You can install multiple PHP versions side by side and switch between them as needed.

.. note::
   PHP 8.4 is the latest version with improved performance, new features, and security enhancements. Always check your application compatibility before upgrading.

Install PHP Extensions
~~~~~~~~~~~~~~~~~~~~~~

**For PHP 7.4:**

.. code-block:: bash
   :caption: PHP 7.4 Extensions

   sudo apt install php7.4-bcmath php7.4-common php7.4-json php7.4-xml \
   php7.4-xmlrpc php7.4-curl php7.4-gd php7.4-imagick php7.4-cli \
   php7.4-dev php7.4-imap php7.4-mbstring php7.4-opcache php7.4-soap \
   php7.4-zip php7.4-intl php7.4-gettext -y

**For PHP 8.1:**

.. code-block:: bash
   :caption: PHP 8.1 Extensions

   sudo apt-get install php8.1-dom php8.1-xml php8.1-bcmath php8.1-curl \
   php8.1-gd php8.1-intl php8.1-mbstring php8.1-mcrypt php8.1-zip \
   php8.1-soap php8.1-mysql php8.1-common

**For PHP 8.2:**

.. code-block:: bash
   :caption: PHP 8.2 Extensions

   sudo apt install php8.2-mysql php8.2-mbstring php8.2-mcrypt php8.2-dom \
   php8.2-bcmath php8.2-intl php8.2-soap php8.2-zip php8.2-gd php8.2-curl \
   php8.2-cli php8.2-xml php8.2-xmlrpc php8.2-gmp php8.2-common

**For PHP 8.3:**

.. code-block:: bash
   :caption: PHP 8.3 Extensions

   sudo apt install php8.3-mysql php8.3-mbstring php8.3-dom php8.3-bcmath \
   php8.3-intl php8.3-soap php8.3-zip php8.3-gd php8.3-curl php8.3-cli \
   php8.3-xml php8.3-xmlrpc php8.3-gmp php8.3-common php8.3-opcache \
   php8.3-readline php8.3-imagick

**For PHP 8.4:**

.. code-block:: bash
   :caption: PHP 8.4 Extensions

   sudo apt install php8.4-common php8.4-mysql php8.4-cli php8.4-fpm \
   php8.4-mbstring php8.4-xml php8.4-bcmath php8.4-curl php8.4-gd \
   php8.4-intl php8.4-soap php8.4-zip php8.4-opcache php8.4-dom \
   php8.4-xmlrpc php8.4-gmp php8.4-readline php8.4-imagick php8.4-pdo \
   php8.4-pgsql php8.4-sqlite3 php8.4-ldap

.. important::
   PHP 8.4 introduces several new features and improvements:

   - Property hooks for cleaner getter/setter syntax
   - Enhanced array functions with ``array_find()`` and ``array_find_key()``
   - ``new`` without parentheses in chained expressions
   - Improved performance and JIT compiler optimizations
   - PDO driver-specific SQL parsers for better prepared statement support

.. note::
   Some extensions like ``mcrypt`` are deprecated in PHP 8.x. Use modern alternatives like ``openssl`` or ``sodium`` for encryption.

Reload Apache after installing extensions:

.. code-block:: bash

   sudo systemctl reload apache2

Configure PHP Settings
~~~~~~~~~~~~~~~~~~~~~~

**Step 1: Locate php.ini file:**

.. code-block:: bash

   php -i | grep "Configuration File"

This command shows the path to your active ``php.ini`` file.

**Step 2: Edit php.ini:**

.. code-block:: bash

   sudo nano <path_of_php.ini_file>

**Step 3: Modify these settings:**

.. code-block:: ini
   :caption: Recommended PHP Configuration

   max_execution_time = 18000
   max_input_time = 1800
   memory_limit = 4G

.. note::
   These values are suitable for development environments and applications like Magento. Adjust based on your specific requirements.

**Step 4: Save and reload Apache:**

.. code-block:: bash

   sudo systemctl reload apache2

Switch Between PHP Versions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You can switch between installed PHP versions easily:

**Disable Current Version (e.g., PHP 7.4):**

.. code-block:: bash

   sudo a2dismod php7.4

**Enable New Version (e.g., PHP 8.4):**

.. code-block:: bash

   sudo a2enmod php8.4

**Set Default PHP CLI Version:**

.. code-block:: bash

   # Switch to PHP 8.4
   sudo update-alternatives --set php /usr/bin/php8.4

   # Or use interactive mode to select from all installed versions
   sudo update-alternatives --config php

**View All Installed PHP Versions:**

.. code-block:: bash

   sudo update-alternatives --config php

**Restart Apache:**

.. code-block:: bash

   sudo systemctl restart apache2

**Common PHP Version Switching Examples:**

.. code-block:: bash
   :caption: Switching Between Different PHP Versions

   # Switch from PHP 7.4 to PHP 8.1
   sudo a2dismod php7.4
   sudo a2enmod php8.1
   sudo update-alternatives --set php /usr/bin/php8.1
   sudo systemctl restart apache2

   # Switch from PHP 8.1 to PHP 8.4
   sudo a2dismod php8.1
   sudo a2enmod php8.4
   sudo update-alternatives --set php /usr/bin/php8.4
   sudo systemctl restart apache2

   # Switch from PHP 8.3 to PHP 8.4
   sudo a2dismod php8.3
   sudo a2enmod php8.4
   sudo update-alternatives --set php /usr/bin/php8.4
   sudo systemctl restart apache2

.. tip::
   Always verify the active PHP version after switching:

   .. code-block:: bash

      # Check CLI version
      php -v

      # Check Apache module version
      php -v
      apache2ctl -M | grep php

Verify PHP Installation
~~~~~~~~~~~~~~~~~~~~~~~~

Check the active PHP version:

.. code-block:: bash

   php -v

PHP-FPM Configuration (Optional)
---------------------------------

PHP-FPM (FastCGI Process Manager) is the modern FastCGI implementation for PHP.

Understanding PHP Execution Methods
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

There are two main ways to run PHP with Apache:

**1. mod_php (Apache Module)** - Default method used in this guide

- PHP runs as an Apache module
- Simpler to configure
- **Perfect for most use cases**
- Suitable for shared hosting and small-to-medium sites
- Lower complexity

**2. PHP-FPM (FastCGI Process Manager)** - Advanced option

- PHP runs as a separate process
- Better resource management for high-traffic sites
- Can run different PHP versions per virtual host
- More configuration options
- Recommended for large-scale production environments

.. note::
   **For most users, mod_php (default) is sufficient and recommended.** Only consider PHP-FPM if you:

   - Run high-traffic websites (10,000+ requests/day)
   - Need multiple PHP versions running simultaneously
   - Want fine-grained process control
   - Have specific performance requirements

What is PHP-FPM?
~~~~~~~~~~~~~~~~

PHP-FPM is the official FastCGI implementation for PHP with advanced features:

- Independent process pool management
- Ability to run different PHP versions per site
- Better resource isolation
- Adaptive process spawning
- Graceful stop/start processes
- Detailed logging and monitoring

Install and Configure PHP-FPM
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Step 1: Install PHP-FPM** (already included in extensions if you installed php8.4-fpm)

.. code-block:: bash

   # Install PHP-FPM for your PHP version
   sudo apt install php8.4-fpm

**Step 2: Enable required Apache modules:**

.. code-block:: bash

   # Enable proxy modules
   sudo a2enmod proxy_fcgi setenvif

   # Enable PHP-FPM configuration
   sudo a2enconf php8.4-fpm

   # Disable mod_php if it's enabled
   sudo a2dismod php8.4

**Step 3: Restart services:**

.. code-block:: bash

   sudo systemctl restart php8.4-fpm
   sudo systemctl restart apache2

Manage PHP-FPM Service
~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

   # Start PHP-FPM
   sudo systemctl start php8.4-fpm

   # Stop PHP-FPM
   sudo systemctl stop php8.4-fpm

   # Restart PHP-FPM
   sudo systemctl restart php8.4-fpm

   # Check status
   sudo systemctl status php8.4-fpm

   # Enable on boot
   sudo systemctl enable php8.4-fpm

   # View PHP-FPM logs
   sudo tail -f /var/log/php8.4-fpm.log

Configure PHP-FPM Pool
~~~~~~~~~~~~~~~~~~~~~~

Edit the PHP-FPM pool configuration:

.. code-block:: bash

   sudo nano /etc/php/8.4/fpm/pool.d/www.conf

**Key settings to adjust:**

.. code-block:: ini
   :caption: /etc/php/8.4/fpm/pool.d/www.conf

   ; Process manager type (static, dynamic, ondemand)
   pm = dynamic

   ; Maximum number of child processes
   pm.max_children = 50

   ; Number of child processes created on startup
   pm.start_servers = 5

   ; Minimum number of idle processes
   pm.min_spare_servers = 5

   ; Maximum number of idle processes
   pm.max_spare_servers = 35

   ; Maximum requests per child process before respawning
   pm.max_requests = 500

.. note::
   Adjust these values based on your server's RAM and expected traffic. For a server with 4GB RAM, the above values are a good starting point.

Virtual Host Configuration for PHP-FPM
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Configure Apache virtual host to use PHP-FPM:

.. code-block:: apache
   :caption: /etc/apache2/sites-available/example.conf

   <VirtualHost *:80>
       ServerName example.com
       DocumentRoot /var/www/html

       <Directory /var/www/html>
           Options -Indexes +FollowSymLinks
           AllowOverride All
           Require all granted
       </Directory>

       # PHP-FPM Configuration
       <FilesMatch \.php$>
           SetHandler "proxy:unix:/run/php/php8.4-fpm.sock|fcgi://localhost"
       </FilesMatch>

       ErrorLog ${APACHE_LOG_DIR}/error.log
       CustomLog ${APACHE_LOG_DIR}/access.log combined
   </VirtualHost>

Run Multiple PHP Versions with PHP-FPM
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

PHP-FPM allows running different PHP versions for different websites:

.. code-block:: apache
   :caption: Site 1 with PHP 8.4

   <VirtualHost *:80>
       ServerName site1.com
       DocumentRoot /var/www/site1

       <FilesMatch \.php$>
           SetHandler "proxy:unix:/run/php/php8.4-fpm.sock|fcgi://localhost"
       </FilesMatch>
   </VirtualHost>

.. code-block:: apache
   :caption: Site 2 with PHP 7.4

   <VirtualHost *:80>
       ServerName site2.com
       DocumentRoot /var/www/site2

       <FilesMatch \.php$>
           SetHandler "proxy:unix:/run/php/php7.4-fpm.sock|fcgi://localhost"
       </FilesMatch>
   </VirtualHost>

.. tip::
   This is particularly useful when migrating applications between PHP versions or maintaining legacy applications.

Troubleshooting PHP
-------------------

Module Does Not Exist Error
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Error:** ``Module php7.4 does not exist!`` or ``Module php8.4 does not exist!``

**Solution:** Install the Apache PHP module:

.. code-block:: bash

   # For PHP 7.4
   sudo apt-get install libapache2-mod-php7.4

   # For PHP 8.1
   sudo apt-get install libapache2-mod-php8.1

   # For PHP 8.2
   sudo apt-get install libapache2-mod-php8.2

   # For PHP 8.3
   sudo apt-get install libapache2-mod-php8.3

   # For PHP 8.4
   sudo apt-get install libapache2-mod-php8.4

.. note::
   Replace the version number with your installed PHP version.

Apache Not Executing PHP Files
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If Apache serves PHP files as downloads instead of executing them:

1. Verify PHP module is enabled:

.. code-block:: bash

   sudo a2enmod php8.1

2. Check Apache configuration for PHP handler
3. Restart Apache:

.. code-block:: bash

   sudo systemctl restart apache2

For detailed troubleshooting, refer to: `TechRepublic Guide <https://www.techrepublic.com/article/how-to-fix-apache-2-not-executing-php-files/>`_

Elasticsearch Installation
---------------------------

Install Java (OpenJDK)
~~~~~~~~~~~~~~~~~~~~~~

Elasticsearch requires Java. Install OpenJDK 17:

.. code-block:: bash

   sudo apt install openjdk-17-jdk

Verify Java installation:

.. code-block:: bash

   java -version

Install cURL
~~~~~~~~~~~~

.. code-block:: bash

   sudo apt install curl

Import Elasticsearch GPG Key
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Import the GPG key for package verification:

.. code-block:: bash

   sudo curl -sSfL https://artifacts.elastic.co/GPG-KEY-elasticsearch | \
   sudo gpg --no-default-keyring \
   --keyring=gnupg-ring:/etc/apt/trusted.gpg.d/magento.gpg --import

Add Elasticsearch Repository
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Add the Elasticsearch 7.x repository:

.. code-block:: bash

   sudo sh -c 'echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" > /etc/apt/sources.list.d/elastic-7.x.list'

   sudo chmod 666 /etc/apt/trusted.gpg.d/magento.gpg

Install Elasticsearch
~~~~~~~~~~~~~~~~~~~~~

Update package cache and install:

.. code-block:: bash

   sudo apt update
   sudo apt install elasticsearch

Enable and Start Elasticsearch
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

   sudo systemctl daemon-reload
   sudo systemctl enable elasticsearch.service
   sudo systemctl start elasticsearch.service

.. important::
   Elasticsearch may take several minutes to start. Be patient before testing the service.

Configure Elasticsearch
-----------------------

Configuration Files Location
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Elasticsearch configuration files are located in ``/etc/elasticsearch/``:

- ``elasticsearch.yml`` - Main configuration file
- ``jvm.options`` - JVM settings (memory, etc.)

Edit Main Configuration
~~~~~~~~~~~~~~~~~~~~~~~

Open the configuration file:

.. code-block:: bash

   sudo nano /etc/elasticsearch/elasticsearch.yml

**Configure Basic Settings:**

.. code-block:: yaml
   :caption: /etc/elasticsearch/elasticsearch.yml

   # Cluster and node names
   node.name: "My First Node"
   cluster.name: my-application

   # Network settings
   network.host: 127.0.0.1
   http.port: 9200

.. warning::
   Setting ``network.host: 0.0.0.0`` makes Elasticsearch publicly accessible. Only use this in secure, controlled environments. For local development, use ``127.0.0.1``.

Configure JVM Memory Settings
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

For systems with limited RAM (< 2GB), adjust JVM heap size:

.. code-block:: bash

   sudo nano /etc/elasticsearch/jvm.options

Modify the heap size values:

.. code-block:: text
   :caption: /etc/elasticsearch/jvm.options

   -Xms256m
   -Xmx256m

.. note::
   The heap size should be set to about 50% of available RAM, but not more than 32GB. For production, 1-2GB is recommended minimum.

Increase Startup Timeout
~~~~~~~~~~~~~~~~~~~~~~~~~

If Elasticsearch fails to start within the default timeout:

.. code-block:: bash

   sudo nano /usr/lib/systemd/system/elasticsearch.service

Find and modify:

.. code-block:: ini

   TimeoutStartSec=900

Reload and restart:

.. code-block:: bash

   sudo systemctl daemon-reload
   sudo systemctl start elasticsearch.service

Verify Elasticsearch
~~~~~~~~~~~~~~~~~~~~

**Check Version:**

.. code-block:: bash

   curl -X GET 'http://localhost:9200'

**Check Cluster Health:**

.. code-block:: bash

   curl http://localhost:9200/_cluster/health?pretty

Expected response should show cluster status as ``green`` or ``yellow``.

Manage Elasticsearch Service
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

   # Start Elasticsearch
   sudo systemctl start elasticsearch

   # Restart Elasticsearch
   sudo systemctl restart elasticsearch

   # Check status
   sudo systemctl status elasticsearch

   # View logs
   sudo journalctl -u elasticsearch

Composer Installation
---------------------

Composer is a dependency management tool for PHP.

Download Composer Installer
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Navigate to your home directory:

.. code-block:: bash

   cd ~

Download the Composer installer:

.. code-block:: bash

   curl -sS https://getcomposer.org/installer -o composer-setup.php

Install Composer Globally
~~~~~~~~~~~~~~~~~~~~~~~~~~

Install Composer to make it available system-wide:

.. code-block:: bash

   sudo php composer-setup.php --install-dir=/usr/bin --filename=composer

Verify Composer Installation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Check Composer version and available commands:

.. code-block:: bash

   composer

You should see the Composer version and a list of available commands.

Manage Composer Versions
~~~~~~~~~~~~~~~~~~~~~~~~~

**Switch to Composer Version 1:**

.. code-block:: bash

   composer self-update --1

**Switch to Composer Version 2:**

.. code-block:: bash

   composer self-update --2

**Install Specific Version:**

.. code-block:: bash

   composer self-update 1.10.12
   composer self-update 2.0.7

Clear Composer Cache
~~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

   cd ~
   composer clear-cache
   # or
   composer clear cache

Health Check
~~~~~~~~~~~~

Verify Composer installation integrity:

.. code-block:: bash

   curl -sS https://getcomposer.org/installer | php -- --check

Complete Stack Verification
----------------------------

After installing all components, verify your LAMP stack:

Apache Status
~~~~~~~~~~~~~

.. code-block:: bash

   sudo systemctl status apache2

Expected: ``active (running)``

MySQL Status
~~~~~~~~~~~~

.. code-block:: bash

   sudo systemctl status mysql

Expected: ``active (running)``

PHP Version
~~~~~~~~~~~

.. code-block:: bash

   php -v

Expected: Your installed PHP version

Elasticsearch Status
~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

   curl http://localhost:9200

Expected: JSON response with Elasticsearch version

Composer Version
~~~~~~~~~~~~~~~~

.. code-block:: bash

   composer --version

Expected: Composer version number

Create PHP Info Page
~~~~~~~~~~~~~~~~~~~~

Create a test file to verify PHP is working with Apache:

.. code-block:: bash

   sudo nano /var/www/html/info.php

Add the following content:

.. code-block:: php
   :caption: /var/www/html/info.php

   <?php
   phpinfo();
   ?>

Visit ``http://localhost/info.php`` in your browser. You should see PHP configuration information.

.. danger::
   Remove the ``info.php`` file after testing, as it exposes sensitive system information:

   .. code-block:: bash

      sudo rm /var/www/html/info.php

Performance Optimization
------------------------

Apache Optimization
~~~~~~~~~~~~~~~~~~~

**Enable caching modules:**

.. code-block:: bash

   sudo a2enmod expires
   sudo a2enmod headers
   sudo a2enmod deflate
   sudo systemctl restart apache2

**Optimize Apache MPM settings** in ``/etc/apache2/mods-available/mpm_prefork.conf`` based on available RAM.

MySQL Optimization
~~~~~~~~~~~~~~~~~~

**Configure my.cnf:**

.. code-block:: bash

   sudo nano /etc/mysql/my.cnf

Add performance tuning based on your system resources and workload.

PHP Optimization
~~~~~~~~~~~~~~~~

**Enable OPcache** in php.ini:

.. code-block:: ini

   opcache.enable=1
   opcache.memory_consumption=128
   opcache.interned_strings_buffer=8
   opcache.max_accelerated_files=4000

Security Best Practices
------------------------

Apache Security
~~~~~~~~~~~~~~~

1. **Disable directory listing:**

.. code-block:: apache

   <Directory /var/www/html>
       Options -Indexes
   </Directory>

2. **Hide Apache version:**

.. code-block:: apache

   ServerTokens Prod
   ServerSignature Off

3. **Enable SSL/TLS** with Let's Encrypt or self-signed certificates

MySQL Security
~~~~~~~~~~~~~~

1. **Run security script:**

.. code-block:: bash

   sudo mysql_secure_installation

2. **Create separate database users** with limited privileges
3. **Use strong passwords** for all database users
4. **Disable remote root login**

PHP Security
~~~~~~~~~~~~

1. **Disable dangerous functions** in php.ini:

.. code-block:: ini

   disable_functions = exec,passthru,shell_exec,system

2. **Hide PHP version:**

.. code-block:: ini

   expose_php = Off

3. **Enable open_basedir restriction**

Elasticsearch Security
~~~~~~~~~~~~~~~~~~~~~~

1. **Keep Elasticsearch private** (network.host = 127.0.0.1)
2. **Enable authentication** with X-Pack Security
3. **Regular updates** to latest security patches
4. **Monitor access logs**

Additional Resources
--------------------

Official Documentation
~~~~~~~~~~~~~~~~~~~~~~

- `Apache HTTP Server Documentation <https://httpd.apache.org/docs/>`_
- `MySQL Documentation <https://dev.mysql.com/doc/>`_
- `PHP Manual <https://www.php.net/manual/en/>`_
- `Elasticsearch Guide <https://www.elastic.co/guide/en/elasticsearch/reference/current/index.html>`_
- `Composer Documentation <https://getcomposer.org/doc/>`_

Tutorial References
~~~~~~~~~~~~~~~~~~~

- `DigitalOcean - LAMP Stack Installation <https://www.digitalocean.com/community/tutorials/how-to-install-linux-apache-mysql-php-lamp-stack-on-ubuntu-20-04>`_
- `DigitalOcean - UFW Firewall Setup <https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-with-ufw-on-ubuntu>`_
- `DigitalOcean - Apache Installation <https://www.digitalocean.com/community/tutorials/how-to-install-the-apache-web-server-on-ubuntu-22-04>`_
- `TecAdmin - PHP Installation <https://tecadmin.net/install-php-ubuntu-20-04/>`_
- `The Coach SMB - Magento Installation Guide <https://www.thecoachsmb.com/install-magento-2-4-5-on-ubuntu-22-04-complete-guide/>`_

Community Support
~~~~~~~~~~~~~~~~~

- `Stack Overflow <https://stackoverflow.com/>`_
- `Server Fault <https://serverfault.com/>`_
- `Ask Ubuntu <https://askubuntu.com/>`_

Quick Command Reference
------------------------

Apache Commands
~~~~~~~~~~~~~~~

.. code-block:: bash
   :caption: Essential Apache Commands

   # Service management
   sudo systemctl start apache2
   sudo systemctl stop apache2
   sudo systemctl restart apache2
   sudo systemctl reload apache2
   sudo systemctl status apache2

   # Enable/disable sites
   sudo a2ensite sitename.conf
   sudo a2dissite sitename.conf

   # Enable/disable modules
   sudo a2enmod rewrite
   sudo a2dismod php7.4

   # Test configuration
   sudo apache2ctl configtest
   sudo apache2ctl -t

   # View loaded modules
   apache2ctl -M

   # Check version
   apache2 -v

MySQL Commands
~~~~~~~~~~~~~~

.. code-block:: bash
   :caption: Essential MySQL Commands

   # Service management
   sudo systemctl start mysql
   sudo systemctl stop mysql
   sudo systemctl restart mysql
   sudo systemctl status mysql

   # Access MySQL
   mysql -u root -p
   sudo mysql

   # Check version
   mysql -V

   # Backup database
   mysqldump -u root -p database_name > backup.sql

   # Restore database
   mysql -u root -p database_name < backup.sql

   # Backup all databases
   mysqldump -u root -p --all-databases > all_databases.sql

PHP Commands
~~~~~~~~~~~~

.. code-block:: bash
   :caption: Essential PHP Commands

   # Check version
   php -v
   php -i

   # Find php.ini location
   php -i | grep "Configuration File"
   php --ini

   # Check installed modules
   php -m

   # Test PHP syntax
   php -l file.php

   # Run PHP built-in server (development only)
   php -S localhost:8000

   # Switch PHP versions
   sudo update-alternatives --config php
   sudo update-alternatives --set php /usr/bin/php8.4

PHP-FPM Commands
~~~~~~~~~~~~~~~~

.. code-block:: bash
   :caption: Essential PHP-FPM Commands

   # Service management
   sudo systemctl start php8.4-fpm
   sudo systemctl stop php8.4-fpm
   sudo systemctl restart php8.4-fpm
   sudo systemctl status php8.4-fpm

   # Reload configuration
   sudo systemctl reload php8.4-fpm

   # Test configuration
   sudo php-fpm8.4 -t

   # View PHP-FPM pool status
   sudo systemctl status php8.4-fpm

Elasticsearch Commands
~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash
   :caption: Essential Elasticsearch Commands

   # Service management
   sudo systemctl start elasticsearch
   sudo systemctl stop elasticsearch
   sudo systemctl restart elasticsearch
   sudo systemctl status elasticsearch

   # Health check
   curl http://localhost:9200
   curl http://localhost:9200/_cluster/health?pretty

   # List indices
   curl http://localhost:9200/_cat/indices?v

   # Delete index
   curl -X DELETE http://localhost:9200/index_name

Composer Commands
~~~~~~~~~~~~~~~~~

.. code-block:: bash
   :caption: Essential Composer Commands

   # Check version
   composer --version

   # Install dependencies
   composer install

   # Update dependencies
   composer update

   # Require a package
   composer require vendor/package

   # Remove a package
   composer remove vendor/package

   # Clear cache
   composer clear-cache

   # Self-update Composer
   composer self-update

   # Switch Composer versions
   composer self-update --1
   composer self-update --2

   # Validate composer.json
   composer validate

File Permissions
~~~~~~~~~~~~~~~~

.. code-block:: bash
   :caption: Common Permission Commands

   # Set web directory permissions
   sudo chown -R www-data:www-data /var/www/html
   sudo chmod -R 755 /var/www/html

   # Set file permissions
   sudo find /var/www/html -type f -exec chmod 644 {} \;

   # Set directory permissions
   sudo find /var/www/html -type d -exec chmod 755 {} \;

   # Make storage writable (Laravel/Magento)
   sudo chmod -R 775 storage
   sudo chmod -R 775 bootstrap/cache

Log File Locations
~~~~~~~~~~~~~~~~~~

.. code-block:: bash
   :caption: Important Log Files

   # Apache logs
   /var/log/apache2/error.log
   /var/log/apache2/access.log

   # MySQL logs
   /var/log/mysql/error.log

   # PHP logs (check php.ini for location)
   /var/log/php8.4-fpm.log

   # Elasticsearch logs
   /var/log/elasticsearch/

   # View logs in real-time
   sudo tail -f /var/log/apache2/error.log
   sudo tail -f /var/log/mysql/error.log

   # View last 100 lines
   sudo tail -n 100 /var/log/apache2/error.log

System Monitoring
~~~~~~~~~~~~~~~~~

.. code-block:: bash
   :caption: System Monitoring Commands

   # Check disk usage
   df -h

   # Check memory usage
   free -m

   # Check CPU and memory usage
   htop
   top

   # Check running processes
   ps aux | grep apache2
   ps aux | grep mysql
   ps aux | grep php-fpm

   # Check open ports
   sudo netstat -tulpn
   sudo ss -tulpn

   # Check listening services
   sudo lsof -i :80
   sudo lsof -i :3306
   sudo lsof -i :9200

Backup and Maintenance
-----------------------

Database Backup
~~~~~~~~~~~~~~~

Create automated MySQL backup script:

.. code-block:: bash
   :caption: /usr/local/bin/mysql-backup.sh

   #!/bin/bash
   # MySQL Backup Script

   BACKUP_DIR="/backup/mysql"
   DATE=$(date +%Y%m%d_%H%M%S)
   DB_USER="root"
   DB_PASS="your_password"

   # Create backup directory
   mkdir -p $BACKUP_DIR

   # Backup all databases
   mysqldump -u $DB_USER -p$DB_PASS --all-databases > $BACKUP_DIR/all_databases_$DATE.sql

   # Compress backup
   gzip $BACKUP_DIR/all_databases_$DATE.sql

   # Delete backups older than 7 days
   find $BACKUP_DIR -name "*.sql.gz" -mtime +7 -delete

   echo "Backup completed: $BACKUP_DIR/all_databases_$DATE.sql.gz"

Make the script executable:

.. code-block:: bash

   sudo chmod +x /usr/local/bin/mysql-backup.sh

Website Backup
~~~~~~~~~~~~~~

.. code-block:: bash
   :caption: Backup Website Files

   # Create backup directory
   sudo mkdir -p /backup/websites

   # Backup website files
   sudo tar -czf /backup/websites/website_$(date +%Y%m%d).tar.gz /var/www/html

   # Backup specific site
   sudo tar -czf /backup/websites/mysite_$(date +%Y%m%d).tar.gz /var/www/html/mysite

Automated Backups with Cron
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Schedule automatic backups:

.. code-block:: bash

   # Edit crontab
   sudo crontab -e

   # Add these lines:
   # Daily MySQL backup at 2 AM
   0 2 * * * /usr/local/bin/mysql-backup.sh

   # Weekly website backup on Sunday at 3 AM
   0 3 * * 0 tar -czf /backup/websites/full_backup_$(date +\%Y\%m\%d).tar.gz /var/www/html

System Updates
~~~~~~~~~~~~~~

Keep your system updated:

.. code-block:: bash

   # Update package list
   sudo apt update

   # Upgrade all packages
   sudo apt upgrade

   # Upgrade distribution
   sudo apt dist-upgrade

   # Remove unused packages
   sudo apt autoremove

   # Clean package cache
   sudo apt clean

.. warning::
   Always test updates in a development environment before applying to production servers. Create backups before major updates.

Restore from Backup
~~~~~~~~~~~~~~~~~~~

**Restore MySQL Database:**

.. code-block:: bash

   # Decompress backup
   gunzip /backup/mysql/all_databases_20250125.sql.gz

   # Restore all databases
   mysql -u root -p < /backup/mysql/all_databases_20250125.sql

   # Restore specific database
   mysql -u root -p database_name < /backup/mysql/database_backup.sql

**Restore Website Files:**

.. code-block:: bash

   # Extract backup
   sudo tar -xzf /backup/websites/website_20250125.tar.gz -C /

   # Restore to specific location
   sudo tar -xzf /backup/websites/mysite_20250125.tar.gz -C /var/www/html/

   # Set proper permissions after restore
   sudo chown -R www-data:www-data /var/www/html
   sudo chmod -R 755 /var/www/html

Conclusion
----------

You now have a complete LAMP stack installed with Elasticsearch and Composer. This environment is suitable for:

- Web application development
- Content Management Systems (WordPress, Drupal, Joomla)
- E-commerce platforms (Magento, PrestaShop, WooCommerce)
- Custom PHP applications
- Search-enabled applications

**Next Steps:**

1. Configure virtual hosts for multiple websites
2. Set up SSL certificates for HTTPS
3. Install and configure your web application
4. Set up regular backups
5. Implement monitoring and logging

.. tip::
   Keep your system and all components regularly updated for security and performance improvements.

For specific application requirements, refer to the application's documentation for additional dependencies and configuration.
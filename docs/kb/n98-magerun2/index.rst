n98-magerun2 Tool for Magento 2
================================

n98-magerun2 is a powerful command-line tool that extends Magento 2's native CLI (bin/magento) with many developer-friendly commands to speed up development, debugging, and administration.

.. contents:: Table of Contents

Overview
--------

What is n98-magerun2.phar?
~~~~~~~~~~~~~~~~~~~~~~~~~~

n98-magerun2 is:

- A powerful command-line tool that extends Magento 2's native CLI (bin/magento) with many developer-friendly commands to speed up development, debugging, and administration
- The Magento 2 version of the popular n98-magerun for Magento 1
- The n98 magerun CLI Tools provides some handy tools to work with Magento / Mage-OS / Adobe Commerce from command line

Source & Documentation
~~~~~~~~~~~~~~~~~~~~~~

- **GitHub**: https://github.com/netz98/n98-magerun2
- **Atwix**: https://www.atwix.com/magento-2/n98-magerun2-tool-overview/
- **Built-in Docs**: Use ``n98-magerun2.phar list`` and ``n98-magerun2.phar help <command>`` for built-in help

Installation
------------

Follow these steps to install n98-magerun2:

#. Download n98-magerun2 using one of the following methods:

   **Using wget**::

       wget https://files.magerun.net/n98-magerun2.phar

   **Using curl**::

       curl -O https://files.magerun.net/n98-magerun2.phar

#. Make the downloaded file executable::

       chmod +x n98-magerun2.phar

#. Move it to ``/usr/local/bin`` (recommended):

   This allows you to run n98-magerun2.phar from any location::

       sudo mv n98-magerun2.phar /usr/local/bin/mage2run

#. Verify the installation::

       mage2run --version

Create Alias (Optional)
-----------------------

If you prefer not to create the global alias, you can create a shell alias instead.

.. note::
   If you created the global alias above (``/usr/local/bin/mage2run``), you can skip this section. This is only if you want a different alias name.

#. Open the shell configuration file::

       code ~/.bashrc

#. Add the following line at the end of the file::

       alias n98mage='/usr/local/bin/n98-magerun2.phar'

#. Save the file and exit the editor

#. Apply the changes to the current shell session::

       source ~/.bashrc

#. Test the alias::

       n98mage list

Available Commands
------------------

n98-magerun2 provides all the default Magento commands from ``bin/magento`` plus additional commands listed below.

Core Commands
~~~~~~~~~~~~~

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Command
     - Description
   * - ``_complete``
     - Internal command to provide shell completion suggestions
   * - ``install``
     - Install Magento
   * - ``open-browser``
     - Open the current project in the browser
   * - ``script``
     - Runs multiple n98-magerun commands
   * - ``self-update`` / ``selfupdate``
     - Updates n98-magerun2.phar to the latest or a specified version

Admin Commands
~~~~~~~~~~~~~~

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Command
     - Description
   * - ``admin:notifications``
     - Toggles admin notifications
   * - ``admin:token:create``
     - Create a new token for an admin user
   * - ``admin:user:change-password``
     - Changes the password of an adminhtml user
   * - ``admin:user:change-status``
     - Set/toggle the status of an admin user
   * - ``admin:user:delete``
     - Delete the account of an adminhtml user
   * - ``admin:user:list``
     - List admin users

Cache Commands
~~~~~~~~~~~~~~

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Command
     - Description
   * - ``cache:catalog:image:flush``
     - Flush catalog image cache
   * - ``cache:list``
     - Lists all magento caches
   * - ``cache:remove:id``
     - Remove cache entry by id
   * - ``cache:view``
     - Prints a cache entry

CMS Commands
~~~~~~~~~~~~

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Command
     - Description
   * - ``cms:block:toggle``
     - Toggle Cms Block status

Configuration Commands
~~~~~~~~~~~~~~~~~~~~~~

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Command
     - Description
   * - ``config:data:acl``
     - Prints acl.xml data as a table
   * - ``config:data:di``
     - Dump dependency injection config
   * - ``config:data:indexer``
     - Dump the merged data of indexer.xml files
   * - ``config:data:mview``
     - Dump merged data of mview.xml files
   * - ``config:env:create``
     - Create an env file interactively
   * - ``config:env:delete``
     - Delete the entry from env.php
   * - ``config:env:set``
     - Set value in env.php
   * - ``config:env:show``
     - List env.php file
   * - ``config:search``
     - Search system configuration descriptions
   * - ``config:store:delete``
     - Deletes a store config item
   * - ``config:store:get``
     - Get a store config item
   * - ``config:store:set``
     - Set a store config item

Customer Commands
~~~~~~~~~~~~~~~~~

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Command
     - Description
   * - ``customer:add-address``
     - Adds an address to a customer
   * - ``customer:change-password``
     - Changes the password of a customer
   * - ``customer:create``
     - Creates a new customer/user for the shop frontend
   * - ``customer:delete``
     - Deletes a customer/user by matching or fuzzy search and/or range
   * - ``customer:info``
     - Loads basic customer info by email address
   * - ``customer:list``
     - Lists all magento customers
   * - ``customer:token:create``
     - Create a new token for a customer

Database Commands
~~~~~~~~~~~~~~~~~

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Command
     - Description
   * - ``db:add-default-authorization-entries``
     - Add default entry to authorization_role and authorization_rule tables
   * - ``db:console`` / ``mysql-client``
     - Opens mysql client by database config from env.php
   * - ``db:create``
     - Create currently configured database
   * - ``db:drop``
     - Drop current database
   * - ``db:dump``
     - Dumps database with mysqldump cli client
   * - ``db:import``
     - Imports database with mysql cli client according to database defined in env.php
   * - ``db:info``
     - Dumps database informations
   * - ``db:maintain:check-tables``
     - Check database tables
   * - ``db:query``
     - Executes an SQL query on the database defined in env.php
   * - ``db:status``
     - Shows important server status information or custom selected status values
   * - ``db:variables``
     - Shows important variables or custom selected

Design Commands
~~~~~~~~~~~~~~~

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Command
     - Description
   * - ``design:demo-notice``
     - Toggles demo store notice for a store view

Development Commands
~~~~~~~~~~~~~~~~~~~~

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Command
     - Description
   * - ``dev:asset:clear``
     - Clear static assets
   * - ``dev:console``
     - Opens PHP interactive shell with a initialized Magento application
   * - ``dev:decrypt``
     - Decrypt the given value using magento's crypt key
   * - ``dev:di:preferences:list``
     - Lists all registered preferences
   * - ``dev:encrypt``
     - Encrypt the given value using magento's crypt key
   * - ``dev:module:create``
     - Create and register a new magento module
   * - ``dev:module:detect-composer-dependencies``
     - Search for soft and hard dependencies for Magento 2 modules
   * - ``dev:module:list``
     - List all installed modules
   * - ``dev:module:observer:list``
     - Lists all registered observers
   * - ``dev:report:count``
     - Get count of report files
   * - ``dev:symlinks``
     - Toggle allow symlinks setting
   * - ``dev:template-hints``
     - Toggles template hints
   * - ``dev:template-hints-blocks``
     - Toggles template hints block names
   * - ``dev:theme:build-hyva``
     - Build Hyvä theme CSS
   * - ``dev:theme:list``
     - Lists all available themes
   * - ``dev:translate:admin``
     - Toggle the inline translation tool for the admin
   * - ``dev:translate:export``
     - Export inline translations
   * - ``dev:translate:set``
     - Adds a translation to the core_translate table globally for locale
   * - ``dev:translate:shop``
     - Toggle the inline translation tool for the shop

EAV Commands
~~~~~~~~~~~~

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Command
     - Description
   * - ``eav:attribute:list``
     - List EAV attributes
   * - ``eav:attribute:remove``
     - Remove attribute for a given attribute code
   * - ``eav:attribute:view``
     - View information about an EAV attribute

Generation Commands
~~~~~~~~~~~~~~~~~~~

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Command
     - Description
   * - ``generation:flush``
     - Flushes generated code like factories and proxies

GitHub Commands
~~~~~~~~~~~~~~~

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Command
     - Description
   * - ``github:pr``
     - Download patch from github merge request (experimental)

Index Commands
~~~~~~~~~~~~~~

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Command
     - Description
   * - ``index:list``
     - Lists all magento indexes
   * - ``index:trigger:recreate``
     - ReCreate all triggers

Integration Commands
~~~~~~~~~~~~~~~~~~~~

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Command
     - Description
   * - ``integration:create``
     - Create a new integration
   * - ``integration:delete``
     - Delete an existing integration
   * - ``integration:list``
     - List all existing integrations
   * - ``integration:show``
     - Show details of an existing integration

Media Commands
~~~~~~~~~~~~~~

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Command
     - Description
   * - ``media:dump``
     - Creates an archive with content of media folder

Route Commands
~~~~~~~~~~~~~~

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Command
     - Description
   * - ``route:list``
     - Lists all registered routes

Sales Commands
~~~~~~~~~~~~~~

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Command
     - Description
   * - ``sales:sequence:add``
     - Add the sequence tables and metadata for given store or all stores
   * - ``sales:sequence:remove``
     - Remove sequence tables and metadata for given store or all stores

Script Commands
~~~~~~~~~~~~~~~

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Command
     - Description
   * - ``script:repo:list``
     - Lists all scripts in repository
   * - ``script:repo:run``
     - Run script from repository

Search Commands
~~~~~~~~~~~~~~~

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Command
     - Description
   * - ``search:engine:list``
     - Lists all registered search engines

System Commands
~~~~~~~~~~~~~~~

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Command
     - Description
   * - ``sys:check``
     - Checks Magento System
   * - ``sys:cron:history``
     - Last executed cronjobs with status
   * - ``sys:cron:kill``
     - Kill cron jobs by code
   * - ``sys:cron:list``
     - Lists all cronjobs
   * - ``sys:cron:run``
     - Runs a cronjob by job code
   * - ``sys:cron:schedule``
     - Schedule a cronjob for execution right now, by job code
   * - ``sys:info``
     - Prints info about the current magento system
   * - ``sys:maintenance``
     - Toggles maintenance mode if --on or --off preferences are not set
   * - ``sys:setup:change-version``
     - Change module resource version
   * - ``sys:setup:compare-versions``
     - Compare the module version with the setup_module table
   * - ``sys:setup:downgrade-versions``
     - Automatically downgrade schema and module versions
   * - ``sys:store:config:base-url:list``
     - Lists all base urls
   * - ``sys:store:list``
     - Lists all installed store-views
   * - ``sys:url:list``
     - Get all urls
   * - ``sys:website:list``
     - Lists all websites

Common Usage Examples
---------------------

Here are some commonly used commands and examples:

Admin User Management
~~~~~~~~~~~~~~~~~~~~~

**List all admin users**::

    mage2run admin:user:list

**Create admin token**::

    mage2run admin:token:create admin_username

**Change admin password**::

    mage2run admin:user:change-password admin_username

Database Operations
~~~~~~~~~~~~~~~~~~~

**Open MySQL console**::

    mage2run db:console

**Dump database**::

    mage2run db:dump filename.sql

**Import database**::

    mage2run db:import filename.sql

**Execute SQL query**::

    mage2run db:query "SELECT * FROM admin_user"

Cache Management
~~~~~~~~~~~~~~~~

**List all caches**::

    mage2run cache:list

**Flush image cache**::

    mage2run cache:catalog:image:flush

Configuration
~~~~~~~~~~~~~

**Show env.php contents**::

    mage2run config:env:show

**Set configuration value**::

    mage2run config:store:set web/unsecure/base_url http://example.com/

**Get configuration value**::

    mage2run config:store:get web/unsecure/base_url

Customer Management
~~~~~~~~~~~~~~~~~~~

**List all customers**::

    mage2run customer:list

**Get customer info**::

    mage2run customer:info customer@example.com

**Create customer token**::

    mage2run customer:token:create customer@example.com

Development Tools
~~~~~~~~~~~~~~~~~

**List all modules**::

    mage2run dev:module:list

**List observers**::

    mage2run dev:module:observer:list

**Open PHP console**::

    mage2run dev:console

**Toggle template hints**::

    mage2run dev:template-hints

System Information
~~~~~~~~~~~~~~~~~~

**System info**::

    mage2run sys:info

**List stores**::

    mage2run sys:store:list

**List all URLs**::

    mage2run sys:url:list

**Cron history**::

    mage2run sys:cron:history

**Run specific cron**::

    mage2run sys:cron:run job_code

Best Practices
--------------

#. **Use in Development**: n98-magerun2 is primarily designed for development and debugging environments
#. **Regular Updates**: Keep n98-magerun2 updated with ``mage2run self-update``
#. **Backup Before Database Operations**: Always backup before running database modification commands
#. **Test Commands**: Test commands in development before running in production
#. **Read Help**: Use ``mage2run help <command>`` to understand command options and arguments

.. tip::
   You can chain multiple commands using the ``script`` command to automate repetitive tasks.

.. warning::
   Be cautious when using database modification commands, especially in production environments. Always create backups first.

See Also
--------

- `n98-magerun2 GitHub Repository <https://github.com/netz98/n98-magerun2>`_
- `Atwix n98-magerun2 Overview <https://www.atwix.com/magento-2/n98-magerun2-tool-overview/>`_
- :doc:`../m2-npm-package/index`

Configure Virtual Host
======================

You can configure virtual host by following commands in your linux enviroment with apache2.

Steps
-----

#. Create ``proxy-le-ssl.conf`` on magento root path

#. Add below content to ``/var/www/html/<magento_root>/proxy-le-ssl.conf``::

    <VirtualHost *:80>
        # The ServerName directive sets the request scheme, hostname and port that
        # the server uses to identify itself. This is used when creating
        # redirection URLs. In the context of virtual hosts, the ServerName
        # specifies what hostname must appear in the request's Host: header to
        # match this virtual host. For the default virtual host (this file) this
        # value is not decisive as it is used as a last resort host regardless.
        # However, you must set it for any further virtual host explicitly.
        ServerName alpha.oneagrix.com
        ServerAlias alpha.oneagrix.com
        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/html/magento/pub
        # Available loglevels: trace8, ..., trace1, debug, info, notice, warn,
        # error, crit, alert, emerg.
        # It is also possible to configure the loglevel for particular
        # modules, e.g.
        #LogLevel info ssl:warn
        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
        # For most configuration files from conf-available/, which are
        # enabled or disabled at a global level, it is possible to
        # include a line for only one particular virtual host. For example the
        # following line enables the CGI configuration for this host only
        # after it has been globally disabled with "a2disconf".
        #Include conf-available/serve-cgi-bin.conf
    </VirtualHost>


#. Open file: ``/etc/apache2/sites-available/000-default.conf``

#. Add below line at bottom to ``000-default.conf`` file::

    Include /var/www/html/magento/proxy-le-ssl.conf


#. Check admin and front-end are working or not.
	
    If the magento admin not working, please run this sql query to phpmyadmin::

	SELECT * FROM `core_config_data` WHERE `path` LIKE '%web/secure%';

    .. figure:: images/sql-query.png
        :align: center
        :alt: SQL query

        SQL query

#. set 0 to 1 in path ``web/secure/use_in_frontend`` and ``web/secure/use_in_adminhtml``.
    
    You can check `Reference link`_
    
.. _Reference link : https://magento.stackexchange.com/questions/162392/https-not-working-on-magento2-backend/201830#201830

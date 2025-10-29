Mailpit: Email Testing Tool for Developers (Linux)
===================================================

Mailpit is a comprehensive email testing tool designed for developers. It acts as an SMTP server and provides a modern web interface to view and test intercepted emails, along with an API for automated integration testing.

.. note::
   This guide is specifically written for **Linux** systems. While Mailpit supports multiple platforms (Linux, macOS, Windows), the installation and configuration steps in this document are tailored for Linux environments, particularly Ubuntu/Debian-based distributions.

.. contents:: Table of Contents
   :local:
   :depth: 2

Overview
--------

What is Mailpit?
~~~~~~~~~~~~~~~~

Mailpit is a feature-rich email testing solution that helps developers test SMTP functionality and email delivery without sending actual emails to real recipients. It captures all outgoing emails and displays them in a user-friendly web interface.

Key Features
~~~~~~~~~~~~

**Core Functionality**

- Runs entirely from a single static binary or multi-architecture Docker images
- Modern web UI with advanced mail search capabilities
- View emails in multiple formats: formatted HTML, highlighted HTML source, text, headers, raw source, and MIME attachments
- Image thumbnails for attachments
- Optional HTTPS and authentication support

**SMTP Server**

- Full-featured SMTP server with optional STARTTLS or SSL/TLS
- Authentication support including "accept any" mode
- SMTP relaying (message release) to relay messages via different SMTP servers
- SMTP forwarding to automatically forward messages to predefined email addresses
- Configurable SMTP errors for testing application resilience (Chaos feature)

**Advanced Features**

- REST API for integration testing
- Real-time web UI updates using WebSockets for new mail
- Optional browser notifications when new mail is received
- Optional POP3 server to download captured messages into email clients
- HTML check to test and score mail client compatibility
- Link check to test message links (HTML and text) and linked images
- Spam check to test message "spamminess" using SpamAssassin
- Create screenshots of HTML messages via the web UI
- Mobile and tablet HTML preview toggle in desktop mode
- Message tagging (manual or automated using filtering and "plus addressing")
- List-Unsubscribe syntax validation
- Optional webhook for received messages

**Performance**

- Fast message storing and processing
- Ingest 100-200 emails per second over SMTP (depending on CPU, network speed, and email size)
- Easily handle tens of thousands of emails
- Automatic email pruning (default: keeps the most recent 500 emails)

Installation
------------

Prerequisites
~~~~~~~~~~~~~

- Linux or macOS operating system
- curl installed
- Sudo privileges
- PHP installed (for PHP integration)

Install Mailpit Binary
~~~~~~~~~~~~~~~~~~~~~~~

**Step 1: Download and Install**

Install Mailpit directly to ``/usr/local/bin/mailpit``::

    sudo bash < <(curl -sL https://raw.githubusercontent.com/axllent/mailpit/develop/install.sh)

This script automatically downloads the latest version and installs it to the system path.

**Step 2: Verify Installation**

Check that Mailpit is installed correctly::

    mailpit version

You should see the version number displayed.

.. tip::
   The installation script automatically detects your system architecture and downloads the appropriate binary.

PHP Configuration
-----------------

To enable PHP to send emails through Mailpit, you need to configure the ``sendmail_path`` in your PHP configuration files.

Configure php.ini Files
~~~~~~~~~~~~~~~~~~~~~~~

**Step 1: Locate php.ini Files**

Depending on your PHP version and setup, you may need to configure multiple php.ini files:

- **CLI**: ``/etc/php/8.1/cli/php.ini``
- **Apache**: ``/etc/php/8.1/apache2/php.ini``
- **FPM**: ``/etc/php/8.1/fpm/php.ini``

.. note::
   Replace ``8.1`` with your PHP version (e.g., ``7.4``, ``8.2``, ``8.3``, ``8.4``).

**Step 2: Edit php.ini Files**

Open each php.ini file and find the ``sendmail_path`` directive::

    # For CLI
    sudo nano /etc/php/8.1/cli/php.ini

    # For Apache
    sudo nano /etc/php/8.1/apache2/php.ini

    # For PHP-FPM
    sudo nano /etc/php/8.1/fpm/php.ini

**Step 3: Set sendmail_path**

Add or modify the ``sendmail_path`` directive::

    sendmail_path = /usr/local/bin/mailpit sendmail -t -i

**Step 4: Save and Exit**

- In nano: Press ``Ctrl+X``, then ``Y``, then ``Enter``

**Step 5: Restart Web Server**

Restart Apache or PHP-FPM to apply changes:

**For Apache**::

    sudo systemctl restart apache2

**For Nginx with PHP-FPM**::

    sudo systemctl restart php8.1-fpm
    sudo systemctl restart nginx

.. important::
   You must restart your web server or PHP-FPM service for the changes to take effect.

Creating Mailpit Service
-------------------------

To run Mailpit as a system service that starts automatically on boot, follow these steps.

Prepare Service Configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Step 1: Check Current User**

Identify your current username::

    whoami

**Step 2: Check Primary Group**

Identify your user's primary group::

    id -gn

**Step 3: Create Data Directory**

Create a directory to store Mailpit's database file:

.. important::
   **Why create a data directory?**

   By default, if you run Mailpit without specifying a database file location, all captured emails are stored in memory only. This means that whenever you restart the Mailpit service or reboot your system, **all your test emails will be lost**.

   Creating a persistent data directory and configuring Mailpit to use a database file ensures that:

   - All captured emails are saved to disk
   - Emails persist across service restarts
   - Emails remain available after system reboots
   - You can review historical test emails anytime

Create the directory::

    mkdir -p /home/logicrays/mailpit_data

.. note::
   Replace ``/home/logicrays`` with your actual home directory path. You can use ``$HOME/mailpit_data`` or any preferred location.

Create Mailpit Systemd Service
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. important::
   **Why create a systemd service?**

   Creating a systemd service file for Mailpit provides several important benefits:

   - **Auto-start on boot**: Mailpit automatically starts when your system boots up
   - **Background operation**: Runs Mailpit in the background without needing a terminal session
   - **Automatic restart**: If Mailpit crashes, systemd automatically restarts it
   - **Easy management**: Use standard systemctl commands to start, stop, and monitor Mailpit
   - **Persistent email storage**: When configured with ``--db-file``, ensures emails are saved to disk and preserved across restarts

   Without a service file, you would need to manually start Mailpit every time you boot your system, and it would stop when you close your terminal.

**Step 1: Create Service File**

Create a new systemd service file::

    sudo nano /etc/systemd/system/mailpit.service

**Step 2: Add Service Configuration**

Add the following content to the file:

.. code-block:: ini
   :caption: /etc/systemd/system/mailpit.service

   [Unit]
   Description=Mailpit email testing service
   After=network.target

   [Service]
   ExecStart=/usr/local/bin/mailpit --db-file=/home/logicrays/mailpit_data/mailpit.db
   Restart=always
   RestartSec=5

   User=logicrays
   Group=logicrays

   [Install]
   WantedBy=multi-user.target

.. important::
   **Customize the following values:**

   - Replace ``logicrays`` in ``User=`` with your username (from ``whoami``)
   - Replace ``logicrays`` in ``Group=`` with your group (from ``id -gn``)
   - Replace ``/home/logicrays/mailpit_data/`` with your chosen data directory path

**Step 3: Save and Exit**

Save the file and exit the editor.

Service Management
------------------

Managing Mailpit Service
~~~~~~~~~~~~~~~~~~~~~~~~~

**Reload Systemd Daemon**

After creating or modifying the service file, reload systemd::

    sudo systemctl daemon-reload

**Enable Mailpit Service**

Enable Mailpit to start automatically on boot::

    sudo systemctl enable mailpit

**Start Mailpit Service**::

    sudo systemctl start mailpit

**Stop Mailpit Service**::

    sudo systemctl stop mailpit

**Restart Mailpit Service**::

    sudo systemctl restart mailpit

**Check Mailpit Status**::

    sudo systemctl status mailpit

**Verify Auto-Start Configuration**::

    systemctl is-enabled mailpit

This should return ``enabled`` if configured correctly.

Service Status Commands
~~~~~~~~~~~~~~~~~~~~~~~

.. list-table::
   :header-rows: 1
   :widths: 40 60

   * - Command
     - Description
   * - ``sudo systemctl daemon-reload``
     - Reload systemd manager configuration
   * - ``sudo systemctl enable mailpit``
     - Enable service to start on boot
   * - ``sudo systemctl disable mailpit``
     - Disable service from starting on boot
   * - ``sudo systemctl start mailpit``
     - Start the Mailpit service
   * - ``sudo systemctl stop mailpit``
     - Stop the Mailpit service
   * - ``sudo systemctl restart mailpit``
     - Restart the Mailpit service
   * - ``sudo systemctl status mailpit``
     - View service status and recent logs
   * - ``systemctl is-enabled mailpit``
     - Check if service is enabled
   * - ``systemctl is-active mailpit``
     - Check if service is running
   * - ``journalctl -u mailpit``
     - View full service logs
   * - ``journalctl -u mailpit -f``
     - Follow (tail) service logs in real-time

Using Mailpit
-------------

Accessing the Web Interface
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Once Mailpit is running, access the web interface using one of these URLs:

- http://localhost:8025/
- http://127.0.0.1:8025/

.. figure:: images/mailpit-web-interface.png
   :align: center
   :alt: Mailpit Web Interface

   Mailpit Web Interface

The web interface provides:

- Email inbox view
- Email preview in multiple formats
- Search functionality
- Message details and headers
- Attachment viewer

Testing Email with PHP
~~~~~~~~~~~~~~~~~~~~~~

**Create a Test PHP Script**

Create a simple PHP script to test email sending:

.. code-block:: php
   :caption: test_email.php

   <?php
   $to = "test@example.com";
   $subject = "Test Email from Mailpit";
   $message = "This is a test email sent through Mailpit!";
   $headers = "From: sender@example.com\r\n";
   $headers .= "Reply-To: sender@example.com\r\n";
   $headers .= "Content-Type: text/html; charset=UTF-8\r\n";

   if (mail($to, $subject, $message, $headers)) {
       echo "Email sent successfully!";
   } else {
       echo "Email sending failed!";
   }
   ?>

**Run the Script**::

    php test_email.php

**View the Email**

Open http://localhost:8025/ in your browser to see the captured email.

Testing with Magento 2
~~~~~~~~~~~~~~~~~~~~~~

.. important::
   If you are using any SMTP extension or plugin in Magento 2 (such as Mageplaza SMTP, Magepal SMTP, or similar), you must disable it first. These plugins override the default PHP mail configuration and will prevent emails from being captured by Mailpit. Disable the SMTP module via command line or admin panel before testing.

For Magento 2, emails are automatically sent through Mailpit once the PHP configuration is set up correctly::

    # Trigger a test email
    cd /path/to/magento
    php bin/magento setup:config:set --enable-debug-logging=true

    # Or test via admin panel
    # Stores > Configuration > General > Store Email Addresses
    # Send a test order confirmation email

Viewing Captured Emails
~~~~~~~~~~~~~~~~~~~~~~~~

The Mailpit web interface allows you to:

#. **Browse all captured emails** in the inbox view
#. **Search emails** using advanced search filters
#. **View email content** in multiple formats (HTML, text, source)
#. **Download attachments** from emails
#. **Test links** in the email
#. **Check spam score** if SpamAssassin is configured
#. **Take screenshots** of HTML emails
#. **Tag messages** for organization


Updating Mailpit
----------------

Keeping Mailpit Up to Date
~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Step 1: Check Current Version**::

    mailpit version

**Step 2: Download Latest Version**

Run the installation script again to update::

    sudo bash < <(curl -sL https://raw.githubusercontent.com/axllent/mailpit/develop/install.sh)

**Step 3: Restart Service**::

    sudo systemctl restart mailpit

**Step 4: Verify New Version**::

    mailpit version

Handling Update Errors
~~~~~~~~~~~~~~~~~~~~~~

If you encounter a permission denied error during update::

    cp: cannot create regular file '/usr/local/bin/mailpit': Permission denied

**Solution 1: Remove Existing Binary**::

    sudo rm /usr/local/bin/mailpit

Then run the installation script again::

    sudo bash < <(curl -sL https://raw.githubusercontent.com/axllent/mailpit/develop/install.sh)

**Solution 2: Rename Existing Binary**::

    sudo mv /usr/local/bin/mailpit /usr/local/bin/mailpit.old

Then run the installation script::

    sudo bash < <(curl -sL https://raw.githubusercontent.com/axllent/mailpit/develop/install.sh)

**Step 3: Restart Service**::

    sudo systemctl restart mailpit

Troubleshooting
---------------

Common Issues
~~~~~~~~~~~~~

**Mailpit Service Not Starting**

Check the service status and logs::

    sudo systemctl status mailpit
    journalctl -u mailpit -n 50

**Port Already in Use**

If port 8025 or 1025 is already in use, modify the service file to use different ports::

    ExecStart=/usr/local/bin/mailpit --smtp=2025 --listen=9025

**Emails Not Being Captured**

#. Verify PHP configuration::

       php -i | grep sendmail_path

#. Ensure it shows::

       sendmail_path => /usr/local/bin/mailpit sendmail -t -i

#. Restart your web server::

       sudo systemctl restart apache2
       # or
       sudo systemctl restart php8.1-fpm

**Permission Issues**

Ensure the data directory has correct permissions::

    chmod 755 /home/logicrays/mailpit_data
    chown logicrays:logicrays /home/logicrays/mailpit_data

**Web Interface Not Accessible**

#. Check if Mailpit is running::

       systemctl is-active mailpit

#. Check firewall rules (if applicable)::

       sudo ufw allow 8025/tcp

#. Verify listening ports::

       ss -tulpn | grep mailpit


Best Practices
--------------

Development Environment
~~~~~~~~~~~~~~~~~~~~~~~

#. **Use Mailpit Only in Development**: Never use Mailpit in production environments
#. **Regular Updates**: Keep Mailpit updated to get the latest features and security fixes
#. **Secure Access**: If exposing Mailpit over a network, enable authentication
#. **Resource Limits**: Configure automatic email pruning to manage disk space

Testing Workflow
~~~~~~~~~~~~~~~~

#. **Test Email Templates**: Use Mailpit to verify email templates render correctly
#. **Check Responsive Design**: Use the mobile/tablet preview feature
#. **Validate Links**: Use the link checker to ensure all links work
#. **Spam Testing**: If using SpamAssassin, check spam scores before sending to real users
#. **Screenshot Emails**: Capture screenshots for documentation or review

Integration Testing
~~~~~~~~~~~~~~~~~~~

#. **Use the API**: Leverage Mailpit's REST API for automated testing
#. **Webhook Integration**: Configure webhooks for CI/CD pipelines
#. **Search Filters**: Use advanced search filters to find specific test emails

Security Considerations
~~~~~~~~~~~~~~~~~~~~~~~

#. **Network Access**: Limit access to localhost in development
#. **Authentication**: Enable UI authentication if accessible over network
#. **HTTPS**: Use HTTPS for production-like testing environments
#. **Clean Up**: Regularly clear old test emails

.. warning::
   Mailpit stores emails in plain text. Never use it with sensitive production data.

Search Filters
--------------

Mailpit supports advanced search filters to find specific emails quickly.

Common Search Filters
~~~~~~~~~~~~~~~~~~~~~

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Filter
     - Description
   * - ``from:user@example.com``
     - Emails from specific sender
   * - ``to:user@example.com``
     - Emails to specific recipient
   * - ``subject:test``
     - Emails with "test" in subject
   * - ``has:attachment``
     - Emails with attachments
   * - ``is:unread``
     - Unread emails
   * - ``is:read``
     - Read emails
   * - ``tag:important``
     - Emails tagged as "important"

**Example Searches**::

    from:noreply@example.com
    to:customer@test.com subject:order
    has:attachment from:admin@shop.com

For more search filter options, visit: https://mailpit.axllent.org/docs/usage/search-filters/


Resources
---------

Official Documentation
~~~~~~~~~~~~~~~~~~~~~~

- **Official Website**: https://mailpit.axllent.org/
- **GitHub Repository**: https://github.com/axllent/mailpit
- **Search Filters Guide**: https://mailpit.axllent.org/docs/usage/search-filters/
- **API Documentation**: https://mailpit.axllent.org/docs/api-v1/

Related Guides
~~~~~~~~~~~~~~

- :doc:`../linux-commands/index` - General Linux command reference
- :doc:`../lamp-stack/index` - LAMP stack setup guide
- :doc:`../package-management/index` - Linux package management

Quick Reference
---------------

**Installation**::

    # Install Mailpit
    sudo bash < <(curl -sL https://raw.githubusercontent.com/axllent/mailpit/develop/install.sh)

    # Configure PHP
    echo "sendmail_path = /usr/local/bin/mailpit sendmail -t -i" | sudo tee -a /etc/php/8.1/apache2/php.ini

    # Restart Apache
    sudo systemctl restart apache2

**Service Management**::

    sudo systemctl start mailpit      # Start service
    sudo systemctl stop mailpit       # Stop service
    sudo systemctl restart mailpit    # Restart service
    sudo systemctl status mailpit     # Check status
    sudo systemctl enable mailpit     # Enable on boot

**Common URLs**::

    http://localhost:8025/            # Web interface
    smtp://localhost:1025             # SMTP server

**Useful Commands**::

    mailpit version                   # Check version
    journalctl -u mailpit -f          # View logs
    systemctl is-enabled mailpit      # Check if enabled

**Update Mailpit**::

    sudo bash < <(curl -sL https://raw.githubusercontent.com/axllent/mailpit/develop/install.sh)
    sudo systemctl restart mailpit

Conclusion
----------

Mailpit is an essential tool for modern web development, providing a safe and efficient way to test email functionality without sending real emails. Its rich feature set, including the web interface, API, and advanced testing capabilities, makes it invaluable for developers working with email-enabled applications.

Key takeaways:

- Easy to install and configure
- Works seamlessly with PHP and other languages
- Provides comprehensive email testing features
- Runs as a system service for convenience
- Includes powerful search and filtering capabilities
- Offers an API for automated testing

By following this guide, you should have Mailpit up and running on your development machine, ready to capture and test all your application's emails.

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

    **Disable php7.4**::

        sudo a2dismod php7.4

    **Enable php8.1**::

        sudo a2enmod php8.1

    **Set Default php**::

        sudo update-alternatives --set php /usr/bin/php8.1

    **Show installed php**::

        sudo update-alternatives --config php

    **Restart apache 2**::

        sudo systemctl restart apache2


Switch From PHP 8.1 to PHP 7.4
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

    **Disable php8.1**::

        sudo a2dismod php8.1

    **Enable php7.4**::

        sudo a2enmod php7.4

    **Set Default php**::

        sudo update-alternatives --set php /usr/bin/php7.4

    **Show installed php**::

        sudo update-alternatives --config php

    **Restart apache 2**::

        sudo systemctl restart apache2

.. note::

        If you getting an error: ``ERROR: Module php8.1 does not exist!``,

        Just execute this command: ``sudo apt-get install libapache2-mod-php8.1``

Switch PHP using shell script
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

:Reference: https://github.com/vinugawade/s-php/blob/master/s-php

#. Create ``switch.sh`` file anywhere. Here, I am creating this file to ``/var/www/html`` path.

#. Add below content to this file and save it
    
    .. code-block:: bash

        #!/bin/bash
        # This is a bash script that allows you to switch between different versions of PHP.
        # Reference: https://github.com/vinugawade/s-php/blob/master/s-php

        # s-php script version.
        VERSION="1.0.0"

        # Function to display error/help messages.
        function show_msg() {
        [[ $1 == "invalid" ]] && echo -e "sphp: Invalid argument"
        [[ $1 == "help" ]] && echo "Usage:
        s-php <version> | [options]
        Easily switch PHP versions on Linux.
        Options:
        -h, --help                 display this help and exit
        -v, --version              display s-php script version"

        # Display versions separated by `,`.
        echo -e "\nPHP Versions :-"
        versions=$(printf '%s, ' ${php_ver[*]})
        echo "  ${versions::-2}"
        exit 1
        }

        # Define available PHP versions.
        php_ver=("5.6" "7.0" "7.1" "7.2" "7.3" "7.4" "8.0" "8.1" "8.2")
        # php_ver=("7.1" "7.2" "7.3" "7.4" "8.0" "8.1" "8.2")


        # Check input value.
        if [ -z "$1" ]; then
        show_msg invalid # Show invalid input message.
        elif [ $# -gt 1 ]; then
        echo -e "Too many arguments:- $*"
        exit 1
        else
        # Check input and show help message.
        if [[ ($* == "--help") || ($* == "-h") ]]; then
            show_msg help
        fi

        # Check input and script version.
        if [[ ($* == "--version") || ($* == "-v") ]]; then
            echo -e "s-php v${VERSION} \nVisit :- https://vinugawade.github.io/s-php"
            exit 1
        fi

        # Check valid PHP version input.
        if [[ ${php_ver[*]} =~ (^|[[:space:]])"${*}"($|[[:space:]]) ]]; then
            php="php${*}"
            phar="phar${*}"
            echo -e "Disabling PHP versions."
            echo "---------------------------"
            # Disable active PHP of apache.
            for i in "${php_ver[@]}"; do
            sudo a2dismod "php${i}" > /dev/null
            printf 'php%s x \n' "${i}"
            done
        else
            show_msg invalid # Show invalid input message.
        fi

        echo -e "\nActivating PHP version. \u2714"
        echo "---------------------------"
        # Change PHP version of system.
        sudo update-alternatives --set php /usr/bin/"${php}" > /dev/null
        sudo update-alternatives --set phar /usr/bin/"${phar}" > /dev/null
        sudo update-alternatives --set phar.phar /usr/bin/phar."${phar}" > /dev/null
        printf '%s \u2714 \n' "${php}"

        # Check apache server is active or not.
        if pgrep -x apache2 > /dev/null; then
            # Enable PHP version for apache.
            echo -e "\nSwitch apache PHP version \u2714"
            echo "---------------------------"
            sudo a2enmod "${php}" > /dev/null

            # Restart apache server.
            echo -e "\nRestart apache server \u2714"
            echo "---------------------------"
            sudo systemctl restart apache2 > /dev/null
            sudo service apache2 restart > /dev/null
        else
            echo -e "\nApache server not running x"
        fi

        # Print new PHP cli version.
        echo -e "\nCurrent PHP version :-"
        echo "---------------------------"
        php -v
        exit 1
        fi

#. Give permission to ``switch.sh`` file::
    
    sudo chmod u+x switch.sh 

#. Move script file for accessing globally by run below command::

    sudo mv switch.sh /usr/bin/switch

#. Run below command to switch php version, like if you want to switch PHP version 8.1::

    switch 8.1

#. See result

    .. figure:: images/swith-php.png
        :align: center

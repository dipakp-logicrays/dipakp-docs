Project Setup Using GIT
=======================

You can setup git project using cli.

.. note:: 
    ``veritaspress`` is our project name that will setup in locally

Let's get started.

Steps
-----

#. Go to ``/var/www/html``

#. Create directory: ``mkdir veritaspress``

#. Execute following commands::

    cd veritaspress
    git init
    git remote add origin <git_url>
    git fetch
    git checkout master

#. Go to github, select the project and copy the github repository url:

    .. figure:: images/git-url.png
        :align: center
        :alt: git project url

        git project url

    .. important::
        Please change your url.

#. Change composer version 2 to 1 : if require::

    sudo composer self-update --1

#. Run command::

    composer install

#. Add ``env.php`` file to ``app/etc/env.php``

#. DB import

    - Remove definer::
        
        grep "DEFINER" your_database_file.sql -rsn
        find your_database_file.sql -type f -exec sed -i 's/DEFINER=`root`@`localhost`/ /g' {} +

    - Create DB : ``veritaspress``

    - Login mysql using cli. Here, ``root`` is **username** and ``secret`` is **password**::
        
        mysql -uroot -p 
        Enter password : secret
    
    - Import db using SOURCE command::

        SET FOREIGN_KEY_CHECKS=0;
        use veritaspress;
        SOURCE cw_m2_LIVE_2022-06-09_09-27-25.sql;
        SET FOREIGN_KEY_CHECKS=1;

#. Update base_url in ``core_config_data`` table

#. Run all magento commands  and check functionality

#. Add pub/media directories

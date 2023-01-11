Linux Commands
==============

You can use the linux commands using cli.

.. contents::
    
Create Database 
---------------
    **Syntax**:
    GRANT ALL PRIVILEGES ON <database_name>.* TO '<mysql_username>'@'localhost';

    **Example**:
    Here, ``root`` is **username** of ``mysql``::

        mysql -uroot -p
        CREATE DATABASE m2demo;
        GRANT ALL PRIVILEGES ON m2demo.* TO 'root'@'localhost';
        FLUSH PRIVILEGES;
   

Import Database 
---------------

    **Example**::

        mysql -u <username> -p <your_database_name> < database_file_name.sql
   

Export Database 
---------------

    **Example**::

        mysqldump -u <username> -p <your_database_name> > database_file_name.sql
       
Remove Definer
--------------

     **Example**::

        grep "DEFINER" db_bkp_01042022.sql -rsn
        find your_database_name.sql -type f -exec sed -i 's/DEFINER=`root`@`localhost`/ /g' {} +

SCP Commands
------------

    #. Create tar files in ``Server A``::
        
        cd /var/www/html/
        tar -cvzf mage245.tar.gz mage245/

    #. Transfer file Server A to B
    
        .. important:: Login Sever B using SSH.
    
    #. Go to root path (**Example**: ``cd /home/plugincardknox/public_html``) where you want to copied file paste in Sever B

    #. Execute below command in ``Server B.``::  
            
        scp root@197.280.111.178:/var/www/html/mage245.tar.gz
            

Create .tar File
----------------

    **Example**::

        tar -cvzf code.tar.gz app/code/


Extract .tar File
-----------------

    **Example**::

        tar -xvzf code.tar.gz

Extract .zip File
-----------------

    **Example**::

        unzip file_name.zip

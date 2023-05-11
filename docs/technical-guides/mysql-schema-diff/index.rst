Compare MySQL database schema
=============================

This article show you how can we compare MySQL database schemas free in linux or ubuntu environment.


Basic Information
-----------------

* ``mysql-schema-diff`` compares the data structures (i.e. schema / table definitions) of two MySQL databases, and returns the differences as a sequence of MySQL commands suitable for piping into mysql which will transform the structure of the first database to be identical to that of the second (c.f. diff and patch)

* Database structures can be compared whether they are files containing table definitions or existing databases, local or remote.

Install
-------

You can install ``mysql-schema-diff`` tool using below command:

.. code-block:: bash
    
    sudo apt install libmysql-diff-perl

Options
-------

More details to come; for now run ``mysql-schema-diff --help``.

How to use
----------

Run below command to compare 2 database and save it to new file. I used this command locally.

**Syntax**

    .. code-block:: bash
        
        mysql-schema-diff --host=<your_mysql_host> --user=<your_mysql_username> --password=<your_mysql_password> <database1_before_upgrade> <database2_after_upgrade> > <file_name>

**Examples**

    .. code-block:: bash

        # compare table definitions in two databases on a remote or local machine
        mysql-schema-diff --host=127.0.0.1 --user=root --password=secret cellisrael-prod cellisrael-prod-test-new-code > diff-db.sql

        # compare table definitions in two files
        mysql-schema-diff db1.mysql db2.mysql

        # compare table definitions in a file 'db1.mysql' with a database 'db2'
        db1.mysql db2

        # interactively upgrade schema of database 'db1' to be like the
        # schema described in the file 'db2.mysql'
        mysql-schema-diff -A db1 db2.mysql

        # compare table definitions in a local database 'foo' with a
        # database 'bar' on a remote machine, when a file foo already
        # exists in the current directory
        mysql-schema-diff --host2=remote.host.com --password=secret db:foo bar

:See output: https://gist.github.com/dipakp-logicrays/beaa94187d290d4b9dff36600784f298

:Reference:  https://manpages.ubuntu.com/manpages/xenial/man1/mysql-schema-diff.1p.html


Internals
---------
How it is work in background. For both of the database structures being compared, the following happens:

* If the argument is a valid filename, the file is used to create a temporary database which ``mysqldump -d`` is run on to obtain the table definitions in canonicalised form. The temporary database is then dropped.(The temporary database is named ``test_mysqldiff_temp_something`` because default MySQL permissions allow anyone to create databases beginning with the prefix ``test_``.)

* If the argument is a database, ``mysqldump -d`` is run directly on it.

* Where authentication is required, the hostname, username, and password given by the corresponding options are used (type ``mysql-schema-diff --help`` for more information).

* Each set of table definitions is now parsed into tables, and fields and index keys within those tables; these are compared, and the differences outputted in the form of MySQL statements.

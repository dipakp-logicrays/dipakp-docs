Compare MySQL Database Schema
==============================

This guide shows you how to compare MySQL database schemas for free in Linux or Ubuntu environments using the ``mysql-schema-diff`` tool.

Overview
--------

What is mysql-schema-diff?
~~~~~~~~~~~~~~~~~~~~~~~~~~~

``mysql-schema-diff`` is a powerful tool that compares the data structures (schema and table definitions) of two MySQL databases and returns the differences as a sequence of MySQL commands. These commands can be piped into MySQL to transform the structure of the first database to match the second database (similar to ``diff`` and ``patch`` for files).

Key Features
~~~~~~~~~~~~

- **Compare database structures** from files containing table definitions or existing databases
- **Works with local or remote** databases
- **Generates SQL statements** to synchronize schemas
- **Supports multiple comparison** scenarios

Installation
------------

Install the ``mysql-schema-diff`` tool using the following command:

.. code-block:: bash

    sudo apt install libmysql-diff-perl

.. note::
    This tool is part of the ``libmysql-diff-perl`` package and works on Debian-based systems (Ubuntu, Debian, etc.).

Command Options
---------------

Usage Syntax
~~~~~~~~~~~~

.. code-block:: bash

    mysql-schema-diff [ options ] <database1> <database2>

General Options
~~~~~~~~~~~~~~~

``-?``, ``--help``
    Show help information

``-A``, ``--apply``
    Interactively patch database1 to match database2

``-B``, ``--batch-apply``
    Non-interactively patch database1 to match database2

``-d``, ``--debug[=N]``
    Enable debugging [level N, default 1]

``-l``, ``--list-tables``
    Output the list of all used tables

``-o``, ``--only-both``
    Only output changes for tables in both databases

``-k``, ``--keep-old-tables``
    Don't output DROP TABLE commands

``-c``, ``--keep-old-columns``
    Don't output DROP COLUMN commands

``-n``, ``--no-old-defs``
    Suppress comments describing old definitions

``-t``, ``--table-re=REGEXP``
    Restrict comparisons to tables matching REGEXP

``-i``, ``--tolerant``
    Ignore DEFAULT, AUTO_INCREMENT, COLLATE, and formatting changes

``-S``, ``--single-transaction``
    Perform DB dump in transaction

Connection Options
~~~~~~~~~~~~~~~~~~

``-h``, ``--host=...``
    Connect to host

``-P``, ``--port=...``
    Use this port for connection

``-u``, ``--user=...``
    User for login if not current user

``-p``, ``--password[=...]``
    Password to use when connecting to server

``-s``, ``--socket=...``
    Socket to use when connecting to server

Database-Specific Connection Options
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

For database-specific connections (where N == 1 or 2), use:

``--hostN=...``
    Connect to host for databaseN

``--portN=...``
    Use this port for connection to databaseN

``--userN=...``
    User for login for databaseN

``--passwordN[=...]``
    Password to use when connecting to databaseN

``--socketN=...``
    Socket to use when connecting to databaseN

.. note::
    Databases can be either files or database names. If there is an ambiguity, the file will be preferred. To prevent this, prefix the database argument with ``db:``.

Usage
-----

Basic Syntax
~~~~~~~~~~~~

Run the following command to compare two databases and save the differences to a file:

.. code-block:: bash

    mysql-schema-diff --host=<your_mysql_host> --user=<your_mysql_username> --password=<your_mysql_password> <database1_before_upgrade> <database2_after_upgrade> > <file_name>

Usage Examples
~~~~~~~~~~~~~~

**Example 1: Compare Two Databases on a Local or Remote Machine**

.. code-block:: bash

    mysql-schema-diff --host=127.0.0.1 --user=root --password=secret cellisrael-prod cellisrael-prod-test-new-code > diff-db.sql

This compares table definitions in two databases and saves the SQL diff to ``diff-db.sql``.

**Example 2: Compare Two SQL Files**

.. code-block:: bash

    mysql-schema-diff db1.mysql db2.mysql

Compares table definitions in two SQL dump files.

**Example 3: Compare SQL File with Database**

.. code-block:: bash

    mysql-schema-diff db1.mysql db2

Compares table definitions in a file ``db1.mysql`` with a database ``db2``.

**Example 4: Interactive Schema Upgrade**

.. code-block:: bash

    mysql-schema-diff -A db1 db2.mysql

Interactively upgrades the schema of database ``db1`` to match the schema in ``db2.mysql``.

**Example 5: Compare Local and Remote Databases**

.. code-block:: bash

    mysql-schema-diff --host2=remote.host.com --password=secret db:foo bar

Compares a local database ``foo`` with a database ``bar`` on a remote machine. The ``db:`` prefix is used when a file with the same name exists in the current directory.

Output Example
~~~~~~~~~~~~~~

View a sample output: https://gist.github.com/dipakp-logicrays/beaa94187d290d4b9dff36600784f298

**Reference Documentation**: https://manpages.ubuntu.com/manpages/xenial/man1/mysql-schema-diff.1p.html


How It Works (Internals)
-------------------------

Understanding what happens behind the scenes when comparing database structures:

Process Flow
~~~~~~~~~~~~

For both database structures being compared, the following process occurs:

**1. File-Based Comparison**
   If the argument is a valid filename:

   - The file is used to create a temporary database
   - ``mysqldump -d`` is run on the temporary database to obtain table definitions in canonicalized form
   - The temporary database is then dropped

   .. note::
       The temporary database is named ``test_mysqldiff_temp_something`` because default MySQL permissions allow anyone to create databases with the ``test_`` prefix.

**2. Database-Based Comparison**
   If the argument is a database:

   - ``mysqldump -d`` is run directly on the database

**3. Authentication**
   Where authentication is required:

   - The hostname, username, and password from the command options are used
   - Type ``mysql-schema-diff --help`` for more information on authentication options

**4. Comparison and Output**

   - Each set of table definitions is parsed into tables, fields, and index keys
   - These structures are compared
   - The differences are output as MySQL statements that can be executed to synchronize the schemas

Use Cases
---------

Common scenarios where ``mysql-schema-diff`` is useful:

- **Before/After Upgrades**: Compare database schema before and after application upgrades
- **Development vs Production**: Ensure development and production schemas are synchronized
- **Migration Planning**: Identify schema changes needed for database migrations
- **Code Review**: Verify that schema changes match expected modifications
- **Disaster Recovery**: Validate database structure after recovery operations

.. tip::
    Always review the generated SQL statements before applying them to production databases. Use the ``-A`` flag for interactive mode to review changes step-by-step.

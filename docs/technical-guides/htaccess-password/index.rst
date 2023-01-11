htaccess Password Protect URL
=============================
To add password protection to your website you need to create a file to store usernames/passwords and add some code into a ``.htaccess`` file.

Let's get started…

Creating Hash Password
----------------------

You can generate Hash password online at: https://www.lcn.com/support/articles/how-to-password-protect-a-folder-on-your-website-with-htaccess/


Steps to creating Hash password:

    .. figure:: images/hash-password.png
        :align: center
        :alt: Creating Hash password

        Creating Hash password

#. Create a file using a text editor such as Notepad or TextEdit.

#. Save the file as: ``.htpasswd``

#. Copy and paste the username/password string generated using our tool into the document.

#. Upload the .htpasswd file to your website using FTP.

#. Add below code to ``.htpasswd`` file::

    test-admin:{SHA}NJ3oRBPNcAGuHUiMm39Ukzii9Zc=

#. Below are Login credentials
    
    | **Username** : test-admin
    | **Password** : test-admin@123

#. Add below code into ``.htaccess`` file of website root: ``/var/www/html/<magento_root>/.htaccess``::

    AuthType Basic
    AuthName "restricted area"
    AuthUserFile /var/www/html/magento/.htpasswd
    require valid-user

#. Let's take a look above step in detail

    **Line 1**:
    *AuthType Basic*

        Defines the type of authentication the web server will use, ‘Basic’ is perfectly adequate for what we need.

    **Line 2**:
    *AuthName "restricted area"*

        Sets the title of the username/password box that will popup when someone tries to view your protected page.

    **Line 3**:
    *AuthUserFile /var/www/html/magento/.htpasswd*

        Tells the web server where to find the username/password file. 
        You will need to update ``.htpasswd`` with a relative path to the location of your ``.htpasswd`` file.
        The ``.htpasswd`` path indicates the file is located two folders above the current directory, to point to a file within the same directory for example, you could use: ./.htpasswd

    **Line 4**:
    *require valid-user*
    
        Tells the web server who in your .htpasswd file can access your folder, by using valid-user everyone in the file can view the folder.
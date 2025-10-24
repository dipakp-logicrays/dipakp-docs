Linux Alias Configuration
=========================

Linux aliases are shortcuts for frequently used commands. They help you save time and increase productivity by reducing the amount of typing required for common tasks.

What is an Alias?
-----------------

An alias is a custom shortcut that replaces a longer command or series of commands. Once created, you can use the alias name instead of typing the full command.

For example::

    alias ll='ls -la'

Now typing ``ll`` will execute ``ls -la``.

Setting Up Aliases
------------------

Configuration Steps
~~~~~~~~~~~~~~~~~~~

Follow these steps to set up permanent aliases in your Linux system:

**Step 1: Open Bash Configuration File**

Open the ``.bashrc`` file in your terminal::

    code ~/.bashrc

Or use any text editor::

    nano ~/.bashrc
    # or
    vim ~/.bashrc

**Step 2: Add Alias Definitions**

Add your alias definitions at the bottom of the file (see sections below for specific aliases).

**Step 3: Save and Close the File**

Save the file and close the editor.

**Step 4: Apply the Changes**

Reload the bash configuration to apply changes::

    source ~/.bashrc

.. note::
    Aliases added to ``~/.bashrc`` will be available every time you open a new terminal session.

System Management Aliases
--------------------------

Update System
~~~~~~~~~~~~~

Update, upgrade, and clean up the system in one command::

    alias updateall='sudo apt-get autoremove -y && sudo apt-get update && sudo apt-get upgrade -y'

**Usage**::

    updateall

This alias will:

1. Remove unnecessary packages (``apt-get autoremove``)
2. Update the package list (``apt-get update``)
3. Upgrade all installed packages (``apt-get upgrade``)

Clean System
~~~~~~~~~~~~

Remove unused packages and clean cache::

    alias cleanup='sudo apt-get autoclean && sudo apt-get autoremove'

Install DEB Package
~~~~~~~~~~~~~~~~~~~

Easily install any ``.deb`` package::

    alias install-deb='sudo dpkg -i'

**Usage**::

    install-deb package-name.deb

Magento Development Aliases
----------------------------

Magento Command Shortcut
~~~~~~~~~~~~~~~~~~~~~~~~~

Create a one-letter shortcut for Magento CLI::

    alias m='bin/magento'

**Usage**::

    m cache:flush
    m setup:upgrade
    m indexer:reindex

Instead of typing ``bin/magento`` every time.

Basic Magento Cleanup
~~~~~~~~~~~~~~~~~~~~~

Remove generated code and cache directories::

    alias mageclean='rm -rf generated/code/* var/cache/* var/di/* var/page_cache/*'

**Usage**::

    mageclean

This cleans:

- ``generated/code/*`` - Generated code files
- ``var/cache/*`` - Cache files
- ``var/di/*`` - Dependency injection cache
- ``var/page_cache/*`` - Full page cache

Full Magento Cleanup
~~~~~~~~~~~~~~~~~~~~

Complete cleanup including preprocessed views::

    alias magecleanall='rm -rf generated/code/* var/cache/* var/di/* var/page_cache/* var/view_preprocessed/*'

**Usage**::

    magecleanall

This includes everything from ``mageclean`` plus:

- ``var/view_preprocessed/*`` - Preprocessed view files (CSS, JS, etc.)

.. important::
    After running ``magecleanall``, you need to run::

        m setup:upgrade
        m setup:di:compile
        m setup:static-content:deploy

Check Magento Versions
~~~~~~~~~~~~~~~~~~~~~~

View available Magento 2.4.x versions::

    alias mageversions="composer show magento/product-community-edition 2.4.* --available | grep -m 1 versions"

**Usage**::

    mageversions

**Output example**::

    versions : * 2.4.0, 2.4.1, 2.4.2, 2.4.3, 2.4.4, 2.4.5, 2.4.6

n98-magerun2 Tool
~~~~~~~~~~~~~~~~~

Shortcut for n98-magerun2.phar development tool::

    alias n98mage='/usr/local/bin/n98-magerun2.phar'

**Usage**::

    n98mage sys:info
    n98mage cache:clean

Git Aliases
-----------

Count Git Commits
~~~~~~~~~~~~~~~~~

Quickly count the number of commits in the current branch::

    alias git_commit_count='git rev-list --count HEAD'

**Usage**::

    git_commit_count

**Output example**::

    42

This shows the total number of commits in the current branch.

Common Useful Aliases
---------------------

Navigation Shortcuts
~~~~~~~~~~~~~~~~~~~~

Quick directory navigation::

    alias ..='cd ..'
    alias ...='cd ../..'
    alias ....='cd ../../..'
    alias ~='cd ~'
    alias -- -='cd -'

List Files with Details
~~~~~~~~~~~~~~~~~~~~~~~

::

    alias ll='ls -la'
    alias la='ls -A'
    alias l='ls -CF'
    alias lt='ls -ltr'

- ``ll`` - Long format with all files
- ``la`` - List all files except . and ..
- ``l`` - List in column format
- ``lt`` - List sorted by modification time (oldest first)

Disk Usage
~~~~~~~~~~

Check disk usage in human-readable format::

    alias df='df -h'
    alias du='du -h'

Search History
~~~~~~~~~~~~~~

Grep through command history::

    alias histgrep='history | grep'

**Usage**::

    histgrep docker

Process Management
~~~~~~~~~~~~~~~~~~

::

    alias psg='ps aux | grep -v grep | grep -i -e VSZ -e'
    alias ports='netstat -tulanp'

Safety Aliases
~~~~~~~~~~~~~~

Confirm before overwriting or deleting::

    alias cp='cp -i'
    alias mv='mv -i'
    alias rm='rm -i'

Web Development Aliases
-----------------------

Apache Management
~~~~~~~~~~~~~~~~~

::

    alias apache-start='sudo systemctl start apache2'
    alias apache-stop='sudo systemctl stop apache2'
    alias apache-restart='sudo systemctl restart apache2'
    alias apache-status='sudo systemctl status apache2'

MySQL Management
~~~~~~~~~~~~~~~~

::

    alias mysql-start='sudo systemctl start mysql'
    alias mysql-stop='sudo systemctl stop mysql'
    alias mysql-restart='sudo systemctl restart mysql'
    alias mysql-status='sudo systemctl status mysql'

Docker Aliases
~~~~~~~~~~~~~~

::

    alias dps='docker ps'
    alias dpsa='docker ps -a'
    alias di='docker images'
    alias drm='docker rm'
    alias drmi='docker rmi'
    alias dstop='docker stop'
    alias dstart='docker start'

Network Aliases
---------------

Check Public IP
~~~~~~~~~~~~~~~

::

    alias myip='curl ifconfig.me'
    alias localip='hostname -I'

Ping Google
~~~~~~~~~~~

::

    alias ping='ping -c 5'
    alias fastping='ping -c 100 -i 0.2'

Network Connections
~~~~~~~~~~~~~~~~~~~

::

    alias listening='sudo lsof -i -P | grep LISTEN'

Complete Alias Setup Script
----------------------------

Here's a complete script with all recommended aliases for Magento/PHP development:

.. code-block:: bash

    # System Management
    alias updateall='sudo apt-get autoremove -y && sudo apt-get update && sudo apt-get upgrade -y'
    alias cleanup='sudo apt-get autoclean && sudo apt-get autoremove'
    alias install-deb='sudo dpkg -i'

    # Magento Development
    alias m='bin/magento'
    alias mageclean='rm -rf generated/code/* var/cache/* var/di/* var/page_cache/*'
    alias magecleanall='rm -rf generated/code/* var/cache/* var/di/* var/page_cache/* var/view_preprocessed/*'
    alias mageversions="composer show magento/product-community-edition 2.4.* --available | grep -m 1 versions"
    alias n98mage='/usr/local/bin/n98-magerun2.phar'

    # Git
    alias git_commit_count='git rev-list --count HEAD'

    # Navigation
    alias ..='cd ..'
    alias ...='cd ../..'
    alias ....='cd ../../..'
    alias ~='cd ~'

    # List Files
    alias ll='ls -la'
    alias la='ls -A'
    alias l='ls -CF'
    alias lt='ls -ltr'

    # Disk Usage
    alias df='df -h'
    alias du='du -h'

    # History
    alias histgrep='history | grep'

    # Safety
    alias cp='cp -i'
    alias mv='mv -i'
    alias rm='rm -i'

    # Apache
    alias apache-start='sudo systemctl start apache2'
    alias apache-stop='sudo systemctl stop apache2'
    alias apache-restart='sudo systemctl restart apache2'
    alias apache-status='sudo systemctl status apache2'

    # MySQL
    alias mysql-start='sudo systemctl start mysql'
    alias mysql-stop='sudo systemctl stop mysql'
    alias mysql-restart='sudo systemctl restart mysql'
    alias mysql-status='sudo systemctl status mysql'

    # Docker
    alias dps='docker ps'
    alias dpsa='docker ps -a'
    alias di='docker images'
    alias drm='docker rm'
    alias drmi='docker rmi'
    alias dstop='docker stop'
    alias dstart='docker start'

    # Network
    alias myip='curl ifconfig.me'
    alias localip='hostname -I'
    alias listening='sudo lsof -i -P | grep LISTEN'

Managing Aliases
----------------

List All Aliases
~~~~~~~~~~~~~~~~

View all currently defined aliases::

    alias

View Specific Alias
~~~~~~~~~~~~~~~~~~~

::

    alias alias_name

Example::

    alias ll

Remove Temporary Alias
~~~~~~~~~~~~~~~~~~~~~~

Remove an alias for the current session only::

    unalias alias_name

Example::

    unalias ll

Remove Permanent Alias
~~~~~~~~~~~~~~~~~~~~~~

1. Open ``~/.bashrc``::

    nano ~/.bashrc

2. Delete or comment out the alias line

3. Save and reload::

    source ~/.bashrc

Alias Best Practices
--------------------

1. **Use Descriptive Names**
   Choose alias names that are easy to remember and indicate what they do.

2. **Don't Override System Commands**
   Avoid creating aliases with names of existing commands unless intentional.

3. **Group Related Aliases**
   Organize aliases by category in your ``.bashrc`` file with comments.

4. **Add Comments**
   Document what each alias does, especially for complex commands.

5. **Test Before Making Permanent**
   Test aliases in the terminal before adding them to ``.bashrc``.

6. **Use Safety Aliases**
   Consider adding ``-i`` flag to ``rm``, ``cp``, and ``mv`` for confirmation prompts.

7. **Keep It Simple**
   Avoid overly complex aliases. For complex tasks, create shell functions instead.

Advanced: Creating Functions
-----------------------------

For more complex operations, use functions instead of aliases:

Extract Archives
~~~~~~~~~~~~~~~~

Add to ``~/.bashrc``::

    extract() {
        if [ -f $1 ]; then
            case $1 in
                *.tar.bz2)   tar xjf $1     ;;
                *.tar.gz)    tar xzf $1     ;;
                *.bz2)       bunzip2 $1     ;;
                *.rar)       unrar e $1     ;;
                *.gz)        gunzip $1      ;;
                *.tar)       tar xf $1      ;;
                *.tbz2)      tar xjf $1     ;;
                *.tgz)       tar xzf $1     ;;
                *.zip)       unzip $1       ;;
                *.Z)         uncompress $1  ;;
                *.7z)        7z x $1        ;;
                *)           echo "'$1' cannot be extracted" ;;
            esac
        else
            echo "'$1' is not a valid file"
        fi
    }

**Usage**::

    extract archive.tar.gz

Make Directory and Navigate
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    mkcd() {
        mkdir -p "$1" && cd "$1"
    }

**Usage**::

    mkcd new-project

Find and Kill Process
~~~~~~~~~~~~~~~~~~~~~

::

    killport() {
        sudo kill -9 $(sudo lsof -t -i:$1)
    }

**Usage**::

    killport 8080

Troubleshooting
---------------

Alias Not Working
~~~~~~~~~~~~~~~~~

1. Check if alias is defined::

    alias alias_name

2. Verify ``.bashrc`` syntax - a typo can prevent the file from loading

3. Make sure you reloaded the configuration::

    source ~/.bashrc

Alias Not Persisting
~~~~~~~~~~~~~~~~~~~~

Ensure you added the alias to ``~/.bashrc`` not ``~/.bash_profile`` (which may not be loaded in all cases).

Conflict with Existing Command
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If an alias conflicts with a system command, use backslash to bypass the alias::

    \ls    # Uses the original ls command instead of any alias

Quick Reference
---------------

.. list-table:: Essential Alias Commands
   :header-rows: 1
   :widths: 40 60

   * - Command
     - Description
   * - ``alias name='command'``
     - Create temporary alias
   * - ``alias``
     - List all aliases
   * - ``alias name``
     - Show specific alias
   * - ``unalias name``
     - Remove alias
   * - ``source ~/.bashrc``
     - Reload bash configuration
   * - ``\command``
     - Bypass alias and use original command

Conclusion
----------

Aliases are powerful tools that can significantly improve your productivity. Start with a few essential aliases and gradually add more as you identify repetitive tasks in your workflow.

.. tip::
    Keep your alias list manageable. Too many aliases can be hard to remember. Focus on commands you use frequently.

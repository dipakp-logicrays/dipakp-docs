Git: First Time Configuration
==============================

When you install Git for the first time, it's important to configure your settings properly. This guide covers all essential Git configurations for initial setup.

.. note::
    Git configurations can be set at three levels:

    - **System level** (``--system``): Applies to all users on the system
    - **Global level** (``--global``): Applies to all repositories for the current user
    - **Repository level** (``--local``): Applies only to the current repository

Checking Your Settings
----------------------

View All Current Git Settings
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To see all your Git settings and where they are coming from::

    git config --list --show-origin

View Specific Configuration Level
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**View global settings**::

    git config --global --list

**View local repository settings**::

    git config --local --list

**View system settings**::

    git config --system --list

Configuring Your Identity
--------------------------

Your identity is the most important configuration. This information is used in every Git commit.

Set Username and Email (Repository Level)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

For the current repository only::

    git config user.name "Your Name"
    git config user.email "your.email@example.com"

Set Username and Email (Global Level)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

For all repositories on your system::

    git config --global user.name "Your Name"
    git config --global user.email "your.email@example.com"

.. important::
    Use your real name and email address. This information will be visible in your commits and on platforms like GitHub, GitLab, etc.

Verify Your Identity Configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Check configured username**::

    git config user.name

**Check configured email**::

    git config user.email

Configuring Your Editor
------------------------

Set your preferred text editor for Git commit messages and other text editing tasks.

Set Vim as Default Editor
~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    git config --global core.editor /usr/bin/vim

To exit Vim::

    Esc :wq

Set VS Code as Default Editor
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    git config --global core.editor "code --wait"

Set Nano as Default Editor
~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    git config --global core.editor nano

Set Sublime Text as Default Editor
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    git config --global core.editor "subl -n -w"

Set Other Editors
~~~~~~~~~~~~~~~~~

**Atom**::

    git config --global core.editor "atom --wait"

**Emacs**::

    git config --global core.editor emacs

**Notepad++ (Windows)**::

    git config --global core.editor "'C:/Program Files/Notepad++/notepad++.exe' -multiInst -notabbar -nosession -noPlugin"

Configuring Color Output
-------------------------

Enable colorized output in Git commands for better readability::

    git config --global color.ui auto
    git config --global color.branch auto
    git config --global color.diff auto
    git config --global color.interactive auto
    git config --global color.status auto
    git config --global color.grep auto

.. tip::
    You can also enable all colors at once with just::

        git config --global color.ui true

Configuring Default Branch Name
--------------------------------

Set the default branch name for new repositories::

    git config --global init.defaultBranch main

.. note::
    Modern Git best practice is to use ``main`` instead of ``master`` as the default branch name.

Configuring Line Endings
-------------------------

Line endings differ between operating systems. Configure Git to handle them properly.

For Windows
~~~~~~~~~~~

::

    git config --global core.autocrlf true

For macOS/Linux
~~~~~~~~~~~~~~~

::

    git config --global core.autocrlf input

Configuring Credential Storage
-------------------------------

Store credentials to avoid entering username and password repeatedly.

Cache Credentials (Temporary)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Cache credentials for 15 minutes (900 seconds)::

    git config --global credential.helper cache

Cache for custom duration (e.g., 1 hour = 3600 seconds)::

    git config --global credential.helper 'cache --timeout=3600'

Store Credentials Permanently
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Linux/macOS**::

    git config --global credential.helper store

**Windows**::

    git config --global credential.helper wincred

.. warning::
    The ``store`` helper saves credentials in plain text. Use with caution.

Configuring Merge Strategy
---------------------------

Set default merge behavior::

    git config --global pull.rebase false

Options:

- ``false``: Merge (default)
- ``true``: Rebase
- ``only``: Fast-forward only

Configuring Push Behavior
--------------------------

Set default push behavior::

    git config --global push.default simple

Options:

- ``simple``: Push current branch to its upstream branch (recommended)
- ``current``: Push current branch to a branch with the same name
- ``upstream``: Push current branch to its upstream branch
- ``matching``: Push all matching branches

Enable AutoCorrect
-------------------

Git can automatically correct typos in commands::

    git config --global help.autocorrect 1

The number represents tenths of a second. ``1`` = 0.1 seconds delay before executing the corrected command.

Example::

    $ git comit
    WARNING: You called a Git command named 'comit', which does not exist.
    Continuing in 0.1 seconds, assuming that you meant 'commit'.

Disable AutoCorrect
~~~~~~~~~~~~~~~~~~~

::

    git config --global help.autocorrect 0

Creating Git Aliases
---------------------

Aliases are shortcuts for frequently used Git commands.

Basic Aliases
~~~~~~~~~~~~~

**Common shortcuts**::

    git config --global alias.co checkout
    git config --global alias.br branch
    git config --global alias.ci commit
    git config --global alias.st status

Usage examples::

    git co feature-branch    # Instead of: git checkout feature-branch
    git st                   # Instead of: git status

Advanced Aliases
~~~~~~~~~~~~~~~~

**One-line log with graph**::

    git config --global alias.lol "log --oneline --graph --decorate --all"

Usage::

    git lol

**Pretty log format with graph**::

    git config --global alias.log-pretty-graph "log --graph --pretty=format:'%C(yellow)%h%Creset %C(red)%d%Creset %s - %C(cyan)%an <%ae>%Creset %C(green)(%ad)%Creset' --date=format:'%d-%m-%Y %I:%M:%S %p'"

Usage::

    git log-pretty-graph

**Pretty log format without graph**::

    git config --global alias.log-pretty "log --pretty=format:'%C(yellow)%h%Creset %C(red)%d%Creset %s - %C(cyan)%an <%ae>%Creset %C(green)(%ad)%Creset' --date=format:'%d-%m-%Y %I:%M:%S %p'"

Usage::

    git log-pretty

**Unstage files**::

    git config --global alias.unstage 'reset HEAD --'

Usage::

    git unstage file.txt    # Instead of: git reset HEAD -- file.txt

**View last commit**::

    git config --global alias.last 'log -1 HEAD'

Usage::

    git last

**Amend last commit**::

    git config --global alias.amend 'commit --amend --no-edit'

**List all aliases**::

    git config --global alias.aliases "config --get-regexp ^alias\."

Usage::

    git aliases

Additional Useful Configurations
---------------------------------

Show Branch in Terminal Prompt
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Add to your ``~/.bashrc`` or ``~/.zshrc``::

    parse_git_branch() {
        git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1)/'
    }
    PS1='${debian_chroot:+($debian_chroot)}\u@\h:\w$(parse_git_branch)\$ '

Configure Diff Tool
~~~~~~~~~~~~~~~~~~~

**Using vimdiff**::

    git config --global diff.tool vimdiff
    git config --global difftool.prompt false

**Using VS Code**::

    git config --global diff.tool vscode
    git config --global difftool.vscode.cmd 'code --wait --diff $LOCAL $REMOTE'

Configure Merge Tool
~~~~~~~~~~~~~~~~~~~~

**Using vimdiff**::

    git config --global merge.tool vimdiff
    git config --global mergetool.prompt false

**Using VS Code**::

    git config --global merge.tool vscode
    git config --global mergetool.vscode.cmd 'code --wait $MERGED'

Enable Reuse Recorded Resolution
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Git can remember how you've resolved merge conflicts::

    git config --global rerere.enabled true

Set Commit Template
~~~~~~~~~~~~~~~~~~~

Create a commit message template::

    git config --global commit.template ~/.gitmessage.txt

Ignore File Permissions Changes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    git config --global core.fileMode false

Configure Pager
~~~~~~~~~~~~~~~

**Disable pager for all commands**::

    git config --global core.pager ''

**Use specific pager**::

    git config --global core.pager 'less -RFX'

Getting Help
------------

Git provides built-in help for all commands.

View Command Help
~~~~~~~~~~~~~~~~~

**Method 1**::

    git help <command>

**Method 2**::

    git <command> --help

**Method 3**::

    man git-<command>

Examples
~~~~~~~~

::

    git help config
    git commit --help
    man git-log

Quick Option Reference
~~~~~~~~~~~~~~~~~~~~~~

For a quick list of available options::

    git <command> -h

Example::

    git commit -h

Complete Setup Script
---------------------

Here's a complete script to set up Git with recommended configurations:

.. code-block:: bash

    #!/bin/bash

    # User Identity
    git config --global user.name "Your Name"
    git config --global user.email "your.email@example.com"

    # Default Editor
    git config --global core.editor "code --wait"

    # Default Branch
    git config --global init.defaultBranch main

    # Color Output
    git config --global color.ui auto

    # Line Endings (Linux/Mac)
    git config --global core.autocrlf input

    # Credential Helper
    git config --global credential.helper cache

    # Pull Strategy
    git config --global pull.rebase false

    # Push Behavior
    git config --global push.default simple

    # AutoCorrect
    git config --global help.autocorrect 1

    # Common Aliases
    git config --global alias.co checkout
    git config --global alias.br branch
    git config --global alias.ci commit
    git config --global alias.st status
    git config --global alias.unstage 'reset HEAD --'
    git config --global alias.last 'log -1 HEAD'
    git config --global alias.lol "log --oneline --graph --decorate --all"

    # Rerere
    git config --global rerere.enabled true

    echo "Git configuration completed successfully!"
    git config --list --show-origin

Viewing and Editing Configuration
----------------------------------

View Configuration File
~~~~~~~~~~~~~~~~~~~~~~~

**Global configuration file location**::

    ~/.gitconfig

**Open in editor**::

    git config --global --edit

**View file content**::

    cat ~/.gitconfig

Remove Configuration
~~~~~~~~~~~~~~~~~~~~

**Remove specific setting**::

    git config --global --unset user.name

**Remove entire section**::

    git config --global --remove-section alias

Reset Configuration
~~~~~~~~~~~~~~~~~~~

To completely reset Git configuration, delete the config file::

    rm ~/.gitconfig

Verifying Your Setup
--------------------

After completing your setup, verify all configurations::

    git config --list

Check specific important settings::

    echo "Username: $(git config user.name)"
    echo "Email: $(git config user.email)"
    echo "Editor: $(git config core.editor)"
    echo "Default Branch: $(git config init.defaultBranch)"

Best Practices
--------------

1. **Always set your identity**: Make sure your name and email are configured before making any commits.

2. **Use global configurations**: Use ``--global`` flag for settings that apply to all your projects.

3. **Choose the right editor**: Select an editor you're comfortable with for commit messages.

4. **Enable colors**: Colored output makes Git commands easier to read.

5. **Create useful aliases**: Create aliases for commands you use frequently to save time.

6. **Use credential caching**: Avoid entering credentials repeatedly by using credential helpers.

7. **Set default branch to main**: Follow modern best practices by using ``main`` instead of ``master``.

8. **Enable rerere**: Let Git remember how you resolved conflicts to make future merges easier.

Troubleshooting
---------------

Configuration Not Working
~~~~~~~~~~~~~~~~~~~~~~~~~

Check configuration levels (local overrides global)::

    git config --list --show-origin

Wrong Editor Opening
~~~~~~~~~~~~~~~~~~~~

Verify editor configuration::

    git config core.editor

Set it explicitly::

    git config --global core.editor "your-preferred-editor"

Commits Showing Wrong Author
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Check your identity configuration::

    git config user.name
    git config user.email

Set them correctly::

    git config --global user.name "Correct Name"
    git config --global user.email "correct@email.com"

To fix previous commits, use::

    git commit --amend --reset-author

Git: Display Branch Name in Terminal
=====================================

Add the current branch name in the terminal to easily identify which Git branch you're working on.

Configuration Steps
-------------------

Follow these steps to display the Git branch name in your terminal prompt:

**Step 1: Open the Bash Configuration File**

Open the ``.bashrc`` file in the terminal::

    sudo nano ~/.bashrc

**Step 2: Add Branch Display Configuration**

Add the following code at the bottom of the file::

    # Display the git branch name
    function parse_git_branch () {
        git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1)/'
    }
    RED="\[\033[01;31m\]"
    YELLOW="\[\033[01;33m\]"
    GREEN="\[\033[01;32m\]"
    BLUE="\[\033[01;34m\]"
    NO_COLOR="\[\033[00m\]"

    # without host
    PS1="$GREEN\u$NO_COLOR:$BLUE\w$YELLOW\$(parse_git_branch)$NO_COLOR\$ "

    # with host (uncomment if you want to display hostname)
    # PS1="$GREEN\u@\h$NO_COLOR:$BLUE\w$YELLOW\$(parse_git_branch)$NO_COLOR\$ "

**Step 3: Save and Close the File**

Save the file (``Ctrl+X``, then ``Y``, then ``Enter`` in nano).

**Step 4: Apply the Changes**

Reload the bash configuration to apply changes::

    source ~/.bashrc

Result
------

After completing these steps, your terminal prompt will display:

- Username in **green**
- Current working directory in **blue**
- Git branch name in **yellow** (when inside a Git repository)

Example terminal prompt::

    username:/var/www/html/project(master)$

.. image:: images/display-git-branch-name.png
   :alt: Git branch name displayed in terminal
   :align: center

.. note::
    The branch name will only appear when you're inside a Git repository directory.

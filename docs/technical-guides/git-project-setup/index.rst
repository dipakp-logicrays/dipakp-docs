Project Setup Using GIT
=======================

You can setup git project using cli.

.. note:: 
    ``veritaspress`` is our project name that will setup in locally

Let's get started.

Automated Setup Using git_setup Script
---------------------------------------

We have created a global bash script ``git_setup`` that automates the git project setup process with interactive prompts.

.. note::
    The ``git_setup`` script is installed globally at ``/usr/bin/git_setup`` and can be executed from any directory.

Setup Steps
^^^^^^^^^^^

Follow these steps in sequence to set up the ``git_setup`` script:

**Step 1: Create the git_setup File**

Create a new file at ``/usr/bin/git_setup``::

    sudo nano /usr/bin/git_setup

**Step 2: Add Script Content**

Copy and paste the following script content into the file::

    #!/bin/bash

    # Git Setup Script - Interactive repository initialization
    # Usage: git_setup (run from any directory)

    set -e

    # Color codes for output
    GREEN='\033[0;32m'
    BLUE='\033[0;34m'
    YELLOW='\033[1;33m'
    RED='\033[0;31m'
    NC='\033[0m' # No Color

    echo ""
    echo "🚀 Git Repository Setup Script"
    echo "================================"
    echo ""

    # Check if already a git repository
    if [ -d ".git" ]; then
        echo -e "${YELLOW}⚠️  Warning: This directory is already a git repository!${NC}"
        read -p "Do you want to continue anyway? (y/n): " continue_choice
        if [[ ! $continue_choice =~ ^[Yy]$ ]]; then
            echo "❌ Aborted by user"
            exit 1
        fi
    fi

    # Prompt for Git URL
    echo -e "${BLUE}📡 Enter Git Repository URL:${NC}"
    read -p "URL: " git_url
    if [ -z "$git_url" ]; then
        echo -e "${RED}❌ Error: Git URL cannot be empty${NC}"
        exit 1
    fi

    # Prompt for Branch Name
    echo ""
    echo -e "${BLUE}🌿 Enter Branch Name:${NC}"
    read -p "Branch: " branch_name
    if [ -z "$branch_name" ]; then
        echo -e "${RED}❌ Error: Branch name cannot be empty${NC}"
        exit 1
    fi

    # Prompt for Git User Name
    echo ""
    echo -e "${BLUE}👤 Enter Git User Name:${NC}"
    read -p "Name: " git_user_name
    if [ -z "$git_user_name" ]; then
        echo -e "${RED}❌ Error: Git user name cannot be empty${NC}"
        exit 1
    fi

    # Prompt for Git User Email
    echo ""
    echo -e "${BLUE}📧 Enter Git User Email:${NC}"
    read -p "Email: " git_user_email
    if [ -z "$git_user_email" ]; then
        echo -e "${RED}❌ Error: Git user email cannot be empty${NC}"
        exit 1
    fi

    echo ""
    echo "🔧 Starting Git setup..."
    echo ""

    # Initialize git repository
    echo "📦 Initializing Git repository..."
    if [ ! -d ".git" ]; then
        git init
        echo -e "${GREEN}✅ Git repository initialized${NC}"
    else
        echo -e "${YELLOW}⚠️  Git repository already exists${NC}"
    fi

    # Add remote origin
    echo ""
    echo "🔗 Adding remote origin..."
    if git remote | grep -q "^origin$"; then
        echo -e "${YELLOW}⚠️  Remote 'origin' already exists, updating URL...${NC}"
        git remote set-url origin "$git_url"
    else
        git remote add origin "$git_url"
    fi
    echo -e "${GREEN}✅ Remote origin configured${NC}"

    # Fetch from remote
    echo ""
    echo "📥 Fetching from remote..."
    git fetch
    echo -e "${GREEN}✅ Fetch completed${NC}"

    # Checkout branch
    echo ""
    echo "🌿 Checking out branch '$branch_name'..."
    if git show-ref --verify --quiet "refs/heads/$branch_name"; then
        git checkout "$branch_name"
    else
        git checkout -b "$branch_name" "origin/$branch_name" 2>/dev/null || git checkout -b "$branch_name"
    fi
    echo -e "${GREEN}✅ Checked out branch '$branch_name'${NC}"

    # Configure user name
    echo ""
    echo "👤 Configuring Git user name..."
    git config user.name "$git_user_name"
    echo -e "${GREEN}✅ User name configured${NC}"

    # Configure user email
    echo ""
    echo "📧 Configuring Git user email..."
    git config user.email "$git_user_email"
    echo -e "${GREEN}✅ User email configured${NC}"

    # Display summary
    echo ""
    echo "════════════════════════════════════════"
    echo "✨ Git Setup Complete!"
    echo "════════════════════════════════════════"
    echo ""

    echo -e "${BLUE}📡 Remote Configuration:${NC}"
    git remote -v
    echo ""

    echo -e "${BLUE}👤 Git User Configuration:${NC}"
    echo "Name:  $(git config user.name)"
    echo "Email: $(git config user.email)"
    echo ""

    echo -e "${BLUE}🌿 Current Branch:${NC}"
    current_branch=$(git branch --show-current)
    echo "$current_branch"
    echo ""

    echo -e "${GREEN}🎉 All done! Your repository is ready to use.${NC}"
    echo ""

After adding the script content, save and close the file (``Ctrl+X``, then ``Y``, then ``Enter`` in nano).

**Step 3: Make the Script Executable**

Grant execute permissions to the script::

    sudo chmod +x /usr/bin/git_setup

**Step 4: Verify Installation**

Verify that the script is installed correctly by checking if it's executable::

    which git_setup
    # Should output: /usr/bin/git_setup

Usage
^^^^^

#. Go to ``/var/www/html``

#. Create your project directory::

    mkdir veritaspress
    cd veritaspress

#. Run the automated setup script::

    git_setup

#. The script will interactively prompt you for:

    - **Git Repository URL**: Enter your GitHub/GitLab repository URL
    - **Branch Name**: Enter the branch you want to checkout (e.g., ``master``, ``main``, ``develop``)
    - **Git User Name**: Enter your git username for commits
    - **Git User Email**: Enter your git email for commits

#. The script will automatically execute:

    - ``git init`` - Initialize git repository
    - ``git remote add origin <git_url>`` - Add remote origin
    - ``git fetch`` - Fetch all branches from remote
    - ``git checkout <branch_name>`` - Checkout specified branch
    - ``git config user.name <git_user_name>`` - Configure git user name
    - ``git config user.email <git_user_email>`` - Configure git user email

#. After completion, the script displays:

    - Remote configuration (``git remote -v``)
    - Git user configuration (name and email)
    - Current active branch

Features
^^^^^^^^

- Interactive prompts with validation
- Color-coded output with emojis for better readability
- Checks if directory is already a git repository
- Handles existing remote origins
- Automatic branch checkout with fallback to creating new branch
- Complete summary display at the end

Manual Setup Using GIT Commands
--------------------------------

If you prefer manual setup instead of using the automated script:

#. Go to ``/var/www/html``

#. Create directory: ``mkdir veritaspress``

#. Execute following commands::

    cd veritaspress
    git init
    git remote add origin <git_url>
    git fetch
    git checkout master
    git config user.name "Your Name"
    git config user.email "your.email@example.com"

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
        
        mysql -uroot -p  ## mysql username is root
        Enter password : secret ## Here my password is secret
    
    - Import db using SOURCE command::

        SET FOREIGN_KEY_CHECKS=0;
        use veritaspress;
        SOURCE cw_m2_LIVE_2022-06-09_09-27-25.sql;
        SET FOREIGN_KEY_CHECKS=1;

#. Update base_url in ``core_config_data`` table

#. Run all magento commands  and check functionality

#. Add pub/media directories

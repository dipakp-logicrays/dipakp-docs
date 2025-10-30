Bash Scripts for Service Management
====================================

Bash scripts provide an efficient way to automate repetitive tasks and manage system services. This comprehensive guide demonstrates how to create and deploy seven essential bash scripts for development workflows: service management (Apache, MySQL, Elasticsearch, Docker), Git repository setup, PHP version switching, and system information checking.

These scripts streamline daily development tasks, reduce errors, and improve productivity by automating complex multi-step processes into simple, single-command operations.

Overview
--------

This comprehensive guide covers creating seven essential bash scripts for development workflow automation:

**Service Management Scripts:**

1. **stop_services** - Stops Apache2, MySQL, and Elasticsearch
2. **start_services** - Starts Apache2, MySQL, and Elasticsearch
3. **start_docker** - Starts Docker daemon and related services
4. **stop_docker** - Stops Docker daemon and related services

**Development Utility Scripts:**

5. **git_setup** - Interactive Git repository setup with validation
6. **switch** - Automated PHP version switching for Apache and CLI
7. **check_system** - Interactive system information checker with 38+ options

All scripts will be installed as global commands, allowing you to run them from any directory.

Prerequisites
-------------

**General Requirements:**

- Ubuntu/Debian-based Linux system
- Bash shell (version 4.0 or higher)
- sudo privileges
- Text editor (nano, vim, or VS Code)

**Script-Specific Requirements:**

**For Service Management Scripts (1-4):**
- Apache2, MySQL, Elasticsearch (for web services scripts)
- Docker and containerd (for Docker scripts)

**For Git Setup Script (5):**
- Git installed (``sudo apt install git``)
- Network access to remote repositories
- SSH keys configured (for SSH-based repositories)

**For PHP Switching Script (6):**
- Multiple PHP versions installed
- Apache2 with PHP modules
- ``update-alternatives`` utility (usually pre-installed)

**For System Information Script (7):**
- Standard Linux utilities (pre-installed on most systems)
- Optional: inxi, hwinfo, lshw for detailed hardware info

.. note::
   You can install individual scripts based on your needs. Not all prerequisites are required if you only use specific scripts.

Script 1: Stop Web Services
----------------------------

This script stops Apache2, MySQL, and Elasticsearch services.

Create the Script
~~~~~~~~~~~~~~~~~

Create the script file in your working directory::

    cd /var/www/html
    touch stop_services.sh

Add Script Content
~~~~~~~~~~~~~~~~~~

Edit the file and add the following content:

.. code-block:: bash

    #!/bin/bash

    # This bash script is used to stop Apache2, MySQL, and Elasticsearch services.

    echo "Stopping Apache2..."
    sudo service apache2 stop
    echo  # Adds a line break

    echo "Stopping MySQL..."
    sudo service mysql stop
    echo  # Adds a line break

    echo "Stopping Elasticsearch..."
    sudo service elasticsearch stop
    echo  # Adds a line break

    echo "All services stopped successfully."

Make Executable
~~~~~~~~~~~~~~~

Grant execution permissions to the script::

    sudo chmod u+x stop_services.sh

Install Globally
~~~~~~~~~~~~~~~~

Move the script to ``/usr/bin`` to make it accessible from anywhere::

    sudo mv stop_services.sh /usr/bin/stop_services

Usage
~~~~~

Now you can run the command from any directory::

    stop_services

**Expected Output:**

.. code-block:: text

    Stopping Apache2...

    Stopping MySQL...

    Stopping Elasticsearch...

    All services stopped successfully.

Script 2: Start Web Services
-----------------------------

This script starts Apache2, MySQL, and Elasticsearch services.

Create the Script
~~~~~~~~~~~~~~~~~

Create the script file::

    cd /var/www/html
    touch start_services.sh

Add Script Content
~~~~~~~~~~~~~~~~~~

Edit the file and add the following content:

.. code-block:: bash

    #!/bin/bash

    # Starting Apache2, MySQL, and Elasticsearch services

    echo "Starting Apache2..."
    sudo service apache2 start
    echo  # Adds a line break

    echo "Starting MySQL..."
    sudo service mysql start
    echo  # Adds a line break

    echo "Starting Elasticsearch..."
    sudo service elasticsearch start
    echo  # Adds a line break

    echo "All services started successfully."

Make Executable and Install
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Grant permissions and move to ``/usr/bin``::

    sudo chmod u+x start_services.sh
    sudo mv start_services.sh /usr/bin/start_services

Usage
~~~~~

Run from anywhere::

    start_services

**Expected Output:**

.. code-block:: text

    Starting Apache2...

    Starting MySQL...

    Starting Elasticsearch...

    All services started successfully.

Script 3: Start Docker Services
--------------------------------

This script starts Docker daemon, docker.socket, and containerd services, and sets proper permissions.

Create the Script
~~~~~~~~~~~~~~~~~

Create the script file::

    cd /var/www/html
    touch start_docker.sh

Add Script Content
~~~~~~~~~~~~~~~~~~

Edit the file and add the following content:

.. code-block:: bash

    #!/bin/bash

    # This bash script starts the docker service and docker.socket.

    echo "✅ Enabling docker.socket..."
    sudo systemctl enable docker.service
    echo  # Adds a line break

    echo "🔌 Starting docker.socket..."
    sudo systemctl start docker.socket
    echo  # Adds a line break

    echo "🐳 Starting Docker..."
    sudo service docker start
    echo  # Adds a line break

    echo "✅ Enabling containerd.service..."
    sudo systemctl enable containerd.service
    echo  # Adds a line break

    echo "🐳 Starting containerd.service..."
    sudo systemctl start containerd.service
    echo  # Adds a line break

    echo "🔐 Set permission to /var/run/docker.sock..."
    sudo chmod 777 /var/run/docker.sock
    echo  # Adds a line break

    echo "✅ All docker services started successfully."

Make Executable and Install
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Grant permissions and move to ``/usr/bin``::

    sudo chmod u+x start_docker.sh
    sudo mv start_docker.sh /usr/bin/start_docker

Usage
~~~~~

Run from anywhere::

    start_docker

**Expected Output:**

.. code-block:: text

    ✅ Enabling docker.socket...

    🔌 Starting docker.socket...

    🐳 Starting Docker...

    ✅ Enabling containerd.service...

    🐳 Starting containerd.service...

    🔐 Set permission to /var/run/docker.sock...

    ✅ All docker services started successfully.

.. note::
    The script sets ``chmod 777`` on docker.sock to allow non-root users to run Docker commands. Consider using Docker group membership instead for better security in production environments.

Script 4: Stop Docker Services
-------------------------------

This script stops Docker daemon, docker.socket, and containerd services.

Create the Script
~~~~~~~~~~~~~~~~~

Create the script file::

    cd /var/www/html
    touch stop_docker.sh

Add Script Content
~~~~~~~~~~~~~~~~~~

Edit the file and add the following content:

.. code-block:: bash

    #!/bin/bash

    # This bash script stops the docker service and docker.socket.

    echo "🔌 Stopping docker.socket..."
    sudo systemctl stop docker.socket
    echo  # Adds a line break

    echo "🚫 Disabling docker.socket..."
    sudo systemctl disable docker.service
    echo  # Adds a line break

    echo "🐳 Stopping Docker..."
    sudo service docker stop
    echo  # Adds a line break

    echo "🐳 Stopping containerd.service..."
    sudo systemctl stop containerd.service
    echo  # Adds a line break

    echo "🚫 Disabling containerd.service..."
    sudo systemctl disable containerd.service
    echo  # Adds a line break

    echo "✅ All services stopped successfully."

Make Executable and Install
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Grant permissions and move to ``/usr/bin``::

    sudo chmod u+x stop_docker.sh
    sudo mv stop_docker.sh /usr/bin/stop_docker

Usage
~~~~~

Run from anywhere::

    stop_docker

**Expected Output:**

.. code-block:: text

    🔌 Stopping docker.socket...

    🚫 Disabling docker.socket...

    🐳 Stopping Docker...

    🐳 Stopping containerd.service...

    🚫 Disabling containerd.service...

    ✅ All services stopped successfully.

.. _script-5-git-repository-setup:

Script 5: Git Repository Setup
-------------------------------

This interactive bash script automates the git project setup process with color-coded prompts and validation.

.. seealso::
    For manual Git setup instructions and project-specific configuration, see :doc:`/git-knowledge/git-project-setup/index`

Create the Script
~~~~~~~~~~~~~~~~~

Create the script file directly in ``/usr/bin``::

    sudo nano /usr/bin/git_setup

Add Script Content
~~~~~~~~~~~~~~~~~~

Add the following content to the file:

.. code-block:: bash

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

Make Executable
~~~~~~~~~~~~~~~

Grant execute permissions to the script::

    sudo chmod +x /usr/bin/git_setup

Usage
~~~~~

Navigate to your project directory and run the script::

    cd /var/www/html
    mkdir myproject
    cd myproject
    git_setup

The script will interactively prompt you for:

1. **Git Repository URL**: Your GitHub/GitLab repository URL
2. **Branch Name**: The branch to checkout (e.g., ``master``, ``main``, ``develop``)
3. **Git User Name**: Your name for commits
4. **Git User Email**: Your email for commits

**Expected Output:**

.. code-block:: text

    🚀 Git Repository Setup Script
    ================================

    📡 Enter Git Repository URL:
    URL: https://github.com/username/repository.git

    🌿 Enter Branch Name:
    Branch: master

    👤 Enter Git User Name:
    Name: John Doe

    📧 Enter Git User Email:
    Email: john@example.com

    🔧 Starting Git setup...

    📦 Initializing Git repository...
    ✅ Git repository initialized

    🔗 Adding remote origin...
    ✅ Remote origin configured

    📥 Fetching from remote...
    ✅ Fetch completed

    🌿 Checking out branch 'master'...
    ✅ Checked out branch 'master'

    👤 Configuring Git user name...
    ✅ User name configured

    📧 Configuring Git user email...
    ✅ User email configured

    ════════════════════════════════════════
    ✨ Git Setup Complete!
    ════════════════════════════════════════

    📡 Remote Configuration:
    origin  https://github.com/username/repository.git (fetch)
    origin  https://github.com/username/repository.git (push)

    👤 Git User Configuration:
    Name:  John Doe
    Email: john@example.com

    🌿 Current Branch:
    master

    🎉 All done! Your repository is ready to use.

Features
~~~~~~~~

The git_setup script provides:

- **Interactive prompts**: User-friendly input validation
- **Color-coded output**: Visual feedback with emojis for better readability
- **Repository detection**: Checks if directory is already a git repository
- **Smart remote handling**: Updates existing remotes or creates new ones
- **Automatic branch checkout**: Creates new branch if it doesn't exist locally
- **Complete summary**: Displays all configuration after setup
- **Error handling**: Validates all inputs and provides clear error messages

What the Script Does
~~~~~~~~~~~~~~~~~~~~

The script automatically executes these git commands in sequence:

1. ``git init`` - Initialize git repository
2. ``git remote add origin <url>`` - Add remote origin
3. ``git fetch`` - Fetch all branches from remote
4. ``git checkout <branch>`` - Checkout specified branch
5. ``git config user.name`` - Configure git user name
6. ``git config user.email`` - Configure git user email

Verify Installation
~~~~~~~~~~~~~~~~~~~

Check if the script is installed correctly::

    which git_setup
    # Should output: /usr/bin/git_setup

.. _script-6-automated-php-version-switching:

Script 6: Automated PHP Version Switching
------------------------------------------

For web development environments with multiple PHP versions, this automated shell script simplifies switching between PHP versions for both Apache and CLI.

**Reference**: https://github.com/vinugawade/s-php/blob/master/s-php

.. seealso::
    For manual PHP version switching instructions, see :doc:`/linux-guides/switch-multiple-php/index`

Create the Script
~~~~~~~~~~~~~~~~~

Create the script file::

    cd /var/www/html
    touch switch.sh

Add Script Content
~~~~~~~~~~~~~~~~~~

Edit the file and add the following content:

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
    php_ver=("5.6" "7.0" "7.1" "7.2" "7.3" "7.4" "8.0" "8.1" "8.2" "8.3" "8.4")
    # php_ver=("7.1" "7.2" "7.3" "7.4" "8.0" "8.1" "8.2" "8.3" "8.4")


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

Make Executable and Install
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Grant permissions and move to ``/usr/bin``::

    sudo chmod u+x switch.sh
    sudo mv switch.sh /usr/bin/switch

Usage
~~~~~

After installation, switch PHP versions with a simple command:

**Switch to PHP 8.1**::

    switch 8.1

**Switch to PHP 7.4**::

    switch 7.4

**Switch to PHP 8.2**::

    switch 8.2

**View help**::

    switch --help

**View script version**::

    switch --version

**Expected Output:**

.. code-block:: text

    Disabling PHP versions.
    ---------------------------
    php5.6 x
    php7.0 x
    php7.1 x
    php7.2 x
    php7.3 x
    php7.4 x
    php8.0 x
    php8.1 x
    php8.2 x
    php8.3 x
    php8.4 x

    Activating PHP version. ✔
    ---------------------------
    php8.1 ✔

    Switch apache PHP version ✔
    ---------------------------

    Restart apache server ✔
    ---------------------------

    Current PHP version :-
    ---------------------------
    PHP 8.1.x (cli) (built: ...)

Features
~~~~~~~~

The automated PHP switching script provides:

- **Quick switching**: Single command to switch versions
- **Comprehensive**: Updates both Apache and CLI PHP versions
- **Safe**: Disables all other PHP versions automatically
- **Automatic restart**: Restarts Apache automatically after switching
- **Version verification**: Shows current PHP version after switching
- **Multiple versions supported**: PHP 5.6, 7.0, 7.1, 7.2, 7.3, 7.4, 8.0, 8.1, 8.2, 8.3, 8.4

.. note::
    To customize supported PHP versions, edit the ``php_ver`` array in ``/usr/bin/switch``.

.. _script-7-system-information-checker:

Script 7: System Information Checker
-------------------------------------

An interactive bash script that provides comprehensive system information through a menu-driven interface with 38+ checking options.

.. seealso::
    For detailed system information commands and usage examples, see :doc:`/linux-guides/system-information/index`

Create the Script
~~~~~~~~~~~~~~~~~

Create the script file::

    nano /var/www/html/check_system.sh

Or in your home directory::

    nano ~/check_system.sh

Add Script Content
~~~~~~~~~~~~~~~~~~

Add the following content to the file:

.. code-block:: bash

    #!/bin/bash

    # Colors
    RED='\033[0;31m'
    GREEN='\033[0;32m'
    BLUE='\033[1;34m'
    YELLOW='\033[1;33m'
    CYAN='\033[1;36m'
    NC='\033[0m' # No Color

    # Function to show help
    show_help() {
        echo -e "${YELLOW}Usage: check_system [OPTION]${NC}"
        echo ""
        echo "Options:"
        echo "  --help       Show this help message"
        echo ""
        echo "When run without arguments, presents a menu to check system information."
    }

    # Function to detect architecture & current logged in user
    detect_arch() {
        ARCH=$(uname -m)
        CURRENT_USER=$(whoami)
        echo -e "${BLUE}------------------------------------${NC}"
        echo -e "✅ ${CYAN}Current System Architecture:${NC} ${GREEN}$ARCH${NC}"
        echo ""
        echo -e "👤 ${CYAN}Current Logged In User:${NC} ${GREEN}$CURRENT_USER${NC}"
        echo -e "${BLUE}------------------------------------${NC}"
    }

    # Display menu
    show_menu() {
        echo -e "${YELLOW}Please select an option:${NC}"
        echo -e "${CYAN}[0]${NC} General system info - [${GREEN}uname -a${NC}]"
        echo -e "${CYAN}[1]${NC} Check host name - [${GREEN}hostname${NC}]"
        echo -e "${CYAN}[2]${NC} Linux OS info - [${GREEN}cat /etc/os-release${NC}]"
        echo -e "${CYAN}[3]${NC} Free and used memory info - [${GREEN}free -m${NC}]"
        echo -e "${CYAN}[4]${NC} Partition information - [${GREEN}fdisk -l${NC}]"
        echo -e "${CYAN}[5]${NC} File system disk usage - [${GREEN}df -h${NC}]"
        echo -e "${CYAN}[6]${NC} List PCI devices - [${GREEN}lspci${NC}]"
        echo -e "${CYAN}[7]${NC} List USB devices - [${GREEN}lsusb${NC}]"
        echo -e "${CYAN}[8]${NC} More info (lsdev) - [${GREEN}lsdev${NC}]"
        echo -e "${CYAN}[9]${NC} Gather disk information - [${GREEN}lsblk${NC}]"
        echo -e "${CYAN}[10]${NC} Display CPU information - [${GREEN}lscpu${NC}]"
        echo -e "${CYAN}[11]${NC} Total available memory - [${GREEN}/proc/meminfo${NC}]"
        echo -e "${CYAN}[12]${NC} All hardware info - [${GREEN}inxi / hwinfo / lshw${NC}]"
        echo -e "${CYAN}[13]${NC} Memory config - [${GREEN}dmidecode -t memory${NC}]"
        echo -e "${CYAN}[14]${NC} Save system info to file - [${GREEN}dmidecode > system_info_TIMESTAMP.txt${NC}]"
        echo -e "${CYAN}[15]${NC} Show uptime - [${GREEN}uptime${NC}]"
        echo -e "${CYAN}[16]${NC} Show who is logged in - [${GREEN}who${NC}]"
        echo -e "${CYAN}[17]${NC} Show running processes - [${GREEN}top -n 1${NC}]"
        echo -e "${CYAN}[18]${NC} Show network interfaces - [${GREEN}ip a${NC}]"
        echo -e "${CYAN}[19]${NC} Show open ports - [${GREEN}ss -tuln${NC}]"
        echo -e "${CYAN}[20]${NC} Show kernel version - [${GREEN}uname -r${NC}]"
        echo -e "${CYAN}[21]${NC} List loaded kernel modules - [${GREEN}lsmod${NC}]"
        echo -e "${CYAN}[22]${NC} Last 20 kernel messages - [${GREEN}dmesg | tail -20${NC}]"
        echo -e "${CYAN}[23]${NC} Last 20 system logs - [${GREEN}journalctl -n 20${NC}]"
        echo -e "${CYAN}[24]${NC} Environment variables - [${GREEN}env${NC}]"
        echo -e "${CYAN}[25]${NC} Show fstab - [${GREEN}cat /etc/fstab${NC}]"
        echo -e "${CYAN}[26]${NC} Inode usage - [${GREEN}df -i${NC}]"
        echo -e "${CYAN}[27]${NC} Pretty uptime - [${GREEN}uptime -p${NC}]"
        echo -e "${CYAN}[28]${NC} Current date/time - [${GREEN}date${NC}]"
        echo -e "${CYAN}[29]${NC} Current user - [${GREEN}whoami${NC}]"
        echo -e "${CYAN}[30]${NC} User groups - [${GREEN}groups${NC}]"
        echo -e "${CYAN}[31]${NC} Top 10 memory processes - [${GREEN}ps aux --sort=-%mem | head -10${NC}]"
        echo -e "${CYAN}[32]${NC} Top 10 CPU processes - [${GREEN}ps aux --sort=-%cpu | head -10${NC}]"
        echo -e "${CYAN}[33]${NC} Routing table - [${GREEN}ip r${NC}]"
        echo -e "${CYAN}[34]${NC} Show mounts - [${GREEN}mount${NC}]"
        echo -e "${CYAN}[35]${NC} Hostname details - [${GREEN}hostnamectl${NC}]"
        echo -e "${CYAN}[36]${NC} Check 32/64 bit system - [${GREEN}getconf LONG_BIT${NC}]"
        echo -e "${CYAN}[37]${NC} OS type - [${GREEN}uname -o${NC}]"
        echo -e "${CYAN}[q]${NC} Quit"
        echo ""
    }

    # Execute based on user input
    handle_choice() {
        case "$1" in
            0) uname -a ;;
            1) hostname ;;
            2) cat /etc/os-release || lsb_release -a ;;
            3) free -m ;;
            4) sudo fdisk -l ;;
            5) df -h ;;
            6) lspci ;;
            7) lsusb ;;
            8) lsdev || echo "lsdev not installed, run: sudo apt install procinfo" ;;
            9) lsblk ;;
            10) lscpu ;;
            11) cat /proc/meminfo ;;
            12) inxi -Fxz || hwinfo --short || lshw --short ;;
            13) sudo dmidecode -t memory | grep -i size || lshw -short -C memory ;;
            14)
                REPORT_DIR="$HOME/system_report"
                TIMESTAMP=$(date '+%Y-%m-%d_%H-%M-%S')
                REPORT_FILE="$REPORT_DIR/system_info_$TIMESTAMP.txt"

                mkdir -p "$REPORT_DIR"

                sudo dmidecode > "$REPORT_FILE"

                echo -e "✅ ${GREEN}System information saved to: $REPORT_FILE${NC}"
                ;;
            15) uptime ;;
            16) who ;;
            17) top -n 1 ;;
            18) ip a ;;
            19) ss -tuln ;;
            20) uname -r ;;
            21) lsmod ;;
            22) dmesg | tail -20 ;;
            23) journalctl -n 20 ;;
            24) env ;;
            25) cat /etc/fstab ;;
            26) df -i ;;
            27) uptime -p ;;
            28) date ;;
            29) whoami ;;
            30) groups ;;
            31) ps aux --sort=-%mem | head -10 ;;
            32) ps aux --sort=-%cpu | head -10 ;;
            33) ip r ;;
            34) mount ;;
            35) hostnamectl ;;
            36) getconf LONG_BIT ;;
            37) uname -o ;;
            q) echo "Exiting..."; exit 0 ;;
            *) echo -e "${RED}Invalid option. Exiting...${NC}"; exit 1 ;;
        esac
    }

    # Main execution
    if [[ "$1" == "--help" ]]; then
        show_help
        exit 0
    fi

    detect_arch
    show_menu
    read -rp "Enter your choice: " choice
    handle_choice "$choice"

Make Executable and Install
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Grant permissions and move to global location::

    chmod +x check_system.sh
    sudo mv check_system.sh /usr/local/bin/check_system

Or to ``/usr/bin``::

    sudo mv check_system.sh /usr/bin/check_system

Usage
~~~~~

Run the script from anywhere::

    check_system

**View help**::

    check_system --help

**Expected Output:**

.. code-block:: text

    ------------------------------------
    ✅ Current System Architecture: x86_64

    👤 Current Logged In User: john
    ------------------------------------
    Please select an option:
    [0] General system info - [uname -a]
    [1] Check host name - [hostname]
    [2] Linux OS info - [cat /etc/os-release]
    [3] Free and used memory info - [free -m]
    [4] Partition information - [fdisk -l]
    [5] File system disk usage - [df -h]
    ...
    [37] OS type - [uname -o]
    [q] Quit

    Enter your choice:

Features
~~~~~~~~

The check_system script provides:

- **38+ System Checks**: Comprehensive coverage of system information
- **Interactive Menu**: Easy-to-use numbered options
- **Color-coded Output**: Visual feedback for better readability
- **Architecture Detection**: Shows current system architecture
- **User Display**: Shows currently logged-in user
- **Help Option**: Built-in help documentation
- **Report Generation**: Option [14] saves complete system info to file with timestamp
- **Organized Categories**: System, CPU, memory, disk, network, hardware, logs

Available Information Categories
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The script covers these main categories:

**System Information**
- General system info, hostname, OS details, architecture

**Hardware Information**
- CPU, memory, PCI devices, USB devices, all hardware

**Storage Information**
- Disk usage, partitions, block devices, filesystem, inodes

**Network Information**
- Network interfaces, open ports, routing table

**System Status**
- Uptime, logged-in users, running processes, CPU/memory usage

**Logs and Monitoring**
- Kernel messages, system logs, kernel modules

**Configuration**
- Environment variables, fstab, mounts

Saving System Reports
~~~~~~~~~~~~~~~~~~~~~

Option [14] creates detailed system reports:

- Creates directory: ``~/system_report/``
- Files named: ``system_info_2025-10-29_14-23-45.txt``
- Contains complete dmidecode output
- Useful for documentation or support tickets

Managing Custom Scripts
------------------------

List Installed Scripts
~~~~~~~~~~~~~~~~~~~~~~

View all custom scripts in ``/usr/bin``::

    ls -l /usr/bin/{start_*,stop_*,git_setup,switch,check_system}

View Script Content
~~~~~~~~~~~~~~~~~~~

Display the content of an installed script::

    cat /usr/bin/start_services
    cat /usr/bin/git_setup

Edit Installed Script
~~~~~~~~~~~~~~~~~~~~~

To modify an installed script::

    sudo nano /usr/bin/start_services

Remove Script
~~~~~~~~~~~~~

To uninstall a script::

    sudo rm /usr/bin/start_services

Check Service Status
~~~~~~~~~~~~~~~~~~~~

After running start/stop scripts, verify service status:

**For systemd services:**

::

    sudo systemctl status apache2
    sudo systemctl status mysql
    sudo systemctl status elasticsearch
    sudo systemctl status docker

**For all services:**

::

    sudo service --status-all

Best Practices
--------------

Script Development
~~~~~~~~~~~~~~~~~~

1. **Error Handling**
   Add error checking to ensure services start/stop successfully:

   .. code-block:: bash

       if sudo service apache2 start; then
           echo "✅ Apache2 started successfully"
       else
           echo "❌ Failed to start Apache2"
           exit 1
       fi

2. **Status Verification**
   Check service status before and after operations:

   .. code-block:: bash

       sudo systemctl is-active apache2 && echo "Apache2 is running"

3. **Logging**
   Add logging to track script execution:

   .. code-block:: bash

       LOG_FILE="/var/log/service-scripts.log"
       echo "$(date): Starting services" >> "$LOG_FILE"

4. **Input Validation**
   Always validate user input in interactive scripts:

   .. code-block:: bash

       if [ -z "$user_input" ]; then
           echo "Error: Input cannot be empty"
           exit 1
       fi

Service Management
~~~~~~~~~~~~~~~~~~

1. **Service Dependencies**
   Start services in the correct order (database before web server):

   .. code-block:: bash

       # Start MySQL first
       sudo service mysql start
       # Wait for MySQL to be ready
       sleep 2
       # Then start Apache
       sudo service apache2 start

2. **Use Systemctl Commands**
   For modern systems, prefer ``systemctl`` over ``service``:

   .. code-block:: bash

       sudo systemctl start apache2
       sudo systemctl enable apache2

3. **Check Service Availability**
   Verify a service exists before attempting operations:

   .. code-block:: bash

       if systemctl list-unit-files | grep -q "^apache2.service"; then
           sudo systemctl start apache2
       fi

Security Considerations
~~~~~~~~~~~~~~~~~~~~~~~

1. **Sudo Credentials**
   - Use ``sudo -v`` to cache credentials at the start of scripts
   - Avoid storing passwords in scripts

2. **File Permissions**
   - Avoid ``chmod 777`` in production; use proper user groups
   - Set appropriate permissions: ``chmod 755`` for scripts

3. **Systemd Services**
   - Consider using systemd service files for complex setups
   - Use systemd timers instead of cron for scheduled tasks

4. **Docker Socket Permissions**
   - Instead of ``chmod 777``, add users to docker group:

   ::

       sudo usermod -aG docker $USER

Documentation
~~~~~~~~~~~~~

1. **Comment Your Scripts**
   Add clear comments explaining what each section does

2. **Include Usage Information**
   Add help messages and usage examples

3. **Version Control**
   Keep scripts in version control (Git) for tracking changes

4. **Document Dependencies**
   List required packages and services at the top of scripts

Troubleshooting
---------------

Script Permission Denied
~~~~~~~~~~~~~~~~~~~~~~~~

If you get "Permission denied" error::

    sudo chmod +x /usr/bin/script_name

Or recreate with proper permissions::

    sudo chmod u+x script_name.sh

Command Not Found
~~~~~~~~~~~~~~~~~

1. Verify script is in ``/usr/bin``::

    ls -l /usr/bin/stop_services

2. Check your PATH includes ``/usr/bin``::

    echo $PATH

3. If needed, add to PATH in ``~/.bashrc``::

    export PATH="/usr/bin:$PATH"

4. Reload your shell configuration::

    source ~/.bashrc

Service Fails to Start/Stop
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Check service status::

    sudo systemctl status service_name

2. View service logs::

    sudo journalctl -u service_name -n 50

3. Verify service is installed::

    which apache2
    which mysqld

4. Check for conflicting processes::

    sudo lsof -i:80  # Check if another process is using port 80

Script Runs But Services Not Affected
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Ensure you have sudo privileges and the services are properly installed. Test individual commands::

    sudo service apache2 status
    sudo systemctl status docker

Git Setup Issues
~~~~~~~~~~~~~~~~

If ``git_setup`` fails:

1. Verify Git is installed::

    git --version

2. Check network connectivity to remote repository::

    ping github.com

3. Verify repository URL is correct and accessible

4. Check SSH keys if using SSH URLs::

    ssh -T git@github.com

PHP Switching Issues
~~~~~~~~~~~~~~~~~~~~

If ``switch`` command doesn't work:

1. Verify PHP versions are installed::

    dpkg -l | grep php

2. Install required PHP modules::

    sudo apt install libapache2-mod-php8.1

3. Check Apache modules::

    apache2ctl -M | grep php

Quick Reference
---------------

.. list-table:: Installed Commands
   :header-rows: 1
   :widths: 30 70

   * - Command
     - Description
   * - ``start_services``
     - Start Apache2, MySQL, and Elasticsearch
   * - ``stop_services``
     - Stop Apache2, MySQL, and Elasticsearch
   * - ``start_docker``
     - Start Docker daemon and related services
   * - ``stop_docker``
     - Stop Docker daemon and related services
   * - ``git_setup``
     - Interactive Git repository setup with prompts
   * - ``switch <version>``
     - Switch PHP version for Apache and CLI
   * - ``check_system``
     - Interactive system information checker with 38+ options

.. list-table:: Service Management Commands
   :header-rows: 1
   :widths: 40 60

   * - Command
     - Description
   * - ``sudo systemctl start service``
     - Start a service
   * - ``sudo systemctl stop service``
     - Stop a service
   * - ``sudo systemctl restart service``
     - Restart a service
   * - ``sudo systemctl status service``
     - Check service status
   * - ``sudo systemctl enable service``
     - Enable service at boot
   * - ``sudo systemctl disable service``
     - Disable service at boot
   * - ``sudo journalctl -u service``
     - View service logs

Conclusion
----------

This comprehensive guide has covered seven essential bash scripts that streamline development workflows and system administration tasks. These scripts provide an efficient way to manage services, set up repositories, switch PHP versions, and gather system information.

Key Benefits
~~~~~~~~~~~~

**Time Savings**
- Eliminate repetitive command typing
- Automate complex multi-step processes
- Reduce human error in service management

**Consistency**
- Ensure commands are executed in the correct order
- Standardize operations across development team
- Maintain consistent configurations

**Productivity**
- Quick service management with single commands
- Interactive prompts reduce memorization burden
- Global installation allows execution from any directory

**Reliability**
- Built-in error handling and validation
- Status verification after operations
- Clear feedback with color-coded output

Next Steps
~~~~~~~~~~

1. **Install the Scripts**
   Start with the service management scripts you need most frequently

2. **Customize for Your Environment**
   Modify scripts to match your specific service stack and workflow

3. **Create Additional Scripts**
   Build on these examples to automate other repetitive tasks:

   - Database backup and restore scripts
   - Cache clearing and warm-up scripts
   - Development environment setup scripts
   - Log rotation and cleanup scripts
   - Deployment automation scripts
   - Testing and validation scripts

4. **Share with Your Team**
   Version control your scripts and share them with your development team

5. **Document Your Scripts**
   Add README files explaining what each script does and how to use it

Best Practices Summary
~~~~~~~~~~~~~~~~~~~~~~

- Always test scripts in development before production use
- Include error handling and status verification
- Add logging for troubleshooting
- Use version control for script management
- Document dependencies and prerequisites
- Follow security best practices (avoid hardcoded credentials, use proper permissions)
- Keep scripts simple and focused on single tasks
- Create wrapper scripts for complex workflows

Related Resources
~~~~~~~~~~~~~~~~~

- :doc:`/linux-guides/linux-alias/index` - Create command shortcuts
- :doc:`/linux-guides/system-information/index` - Learn system information commands
- :doc:`/linux-guides/switch-multiple-php/index` - Manual PHP version switching
- :doc:`/git-knowledge/git-project-setup/index` - Manual Git setup procedures

.. tip::
    Bookmark this guide for quick reference when creating new scripts or troubleshooting existing ones.

.. warning::
    Always test scripts in a development environment before deploying to production. Stopping critical services can affect running applications and user access. Ensure you have proper backups and rollback procedures.

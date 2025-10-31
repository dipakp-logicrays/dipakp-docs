Git: SSH Key Generation and Setup
====================================

SSH (Secure Shell) keys provide a secure way to authenticate with Git services like GitHub, GitLab, and Bitbucket without entering your password every time. This guide covers generating SSH keys and configuring them for use with Git.

.. note::
    SSH keys consist of a **key pair** - meaning TWO files are always generated:

    - **Private key**: Kept secret on your local machine (never share this)
    - **Public key**: Added to services like GitHub (safe to share)

    When you run ``ssh-keygen``, you get **BOTH** files automatically.

Why Use SSH Keys?
-----------------

**Benefits of SSH authentication**:

- **Security**: More secure than password authentication
- **Convenience**: No need to enter credentials for every Git operation
- **Automation**: Enables automated scripts and CI/CD pipelines
- **Multiple Keys**: Different keys for different services or machines

Prerequisites
-------------

Before generating SSH keys, ensure you have:

1. Git installed on your system
2. Access to a terminal or command line
3. A GitHub/GitLab/Bitbucket account (for adding the public key)

Generating SSH Keys
-------------------

Step 1: Navigate to Your Working Directory
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Navigate to your preferred working directory::

    cd ~/your-project-directory/

.. tip::
    You can generate the key in any directory, but it's common practice to generate it in your project directory and then move it to ``~/.ssh/`` for proper organization.

Step 2: Generate ED25519 SSH Key
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Generate a new SSH key using the ED25519 algorithm::

    ssh-keygen -t ed25519 -C "your.email@example.com"

**Real example**::

    ssh-keygen -t ed25519 -C "john.doe@acme.com"

**Command breakdown**:

- ``-t ed25519``: Specifies the key type (ED25519 is modern and secure)
- ``-C "your.email@example.com"``: Adds a comment (usually your email) to identify the key

**Interactive prompts**::

    Enter file in which to save the key:
    Enter passphrase (empty for no passphrase):
    Enter same passphrase again:

.. important::
    **Passphrase recommendations**:

    - Use a strong passphrase for additional security
    - Leave empty for automation/CI/CD (less secure)
    - Use a password manager to store the passphrase

Understanding SSH Key Naming
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

When ``ssh-keygen`` prompts you with ``Enter file in which to save the key:``, you need to understand how key naming works.

**IMPORTANT**: The key filename is **NOT automatically generated** from your email address. You must manually specify it.

**The -C Flag (Comment)**:

The ``-C "your.email@example.com"`` flag only adds a **comment** to your public key for identification purposes. It appears at the end of your ``.pub`` file but does **NOT** determine the filename.

**Example with placeholder**::

    ssh-keygen -t ed25519 -C "your.email@example.com"

**Example with actual email**::

    ssh-keygen -t ed25519 -C "john.doe@acme.com"

    # When prompted:
    Enter file in which to save the key (/home/user/.ssh/id_ed25519): johndoe-company
                                                                       ^^^^^^^^^^^^^^^
                                                                       YOU TYPE THIS

**What happens**:

1. You run the command with ``-C`` flag (sets the comment)
2. ssh-keygen prompts for filename
3. You type your chosen name (e.g., ``johndoe-company``)
4. Two files are created:

   - ``johndoe-company`` (private key)
   - ``johndoe-company.pub`` (public key with comment at the end)

**Public key structure**::

    ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAILongRandomString john.doe@company.com
                ^                    ^                      ^
                |                    |                      |
             Key Type            Key Data              Comment (from -C flag)

Choosing a Key Filename
~~~~~~~~~~~~~~~~~~~~~~~~

**Option 1: Use Default Name (Press Enter)**

If you press Enter without typing anything::

    Enter file in which to save the key (/home/user/.ssh/id_ed25519): [PRESS ENTER]

Default names:

- ``id_ed25519`` (for ED25519 keys)
- ``id_rsa`` (for RSA keys)

**Option 2: Specify Custom Name (Recommended)**

Type a descriptive name that helps you identify the key's purpose::

    Enter file in which to save the key: id_ed25519_work_github

Common Naming Patterns
~~~~~~~~~~~~~~~~~~~~~~

**Pattern 1: username-organization**

**Syntax**::

    <username>-<organization>

**Examples**::

    johndoe-acme            # User "johndoe" at "acme" (email: john.doe@acme.com)
    alice-techcorp          # User "alice" at "techcorp" (email: alice.smith@techcorp.com)
    bob-github              # User "bob" for "github" (email: bob.jones@gmail.com)

**Pattern 2: id_keytype_purpose**

**Syntax**::

    id_<keytype>_<purpose>

**Examples**::

    id_ed25519_work         # ED25519 key for work (email: john.doe@acme.com)
    id_ed25519_personal     # ED25519 key for personal (email: john.personal@gmail.com)
    id_rsa_github_work      # RSA key for work GitHub (email: alice.smith@techcorp.com)

**Pattern 3: service-purpose**

**Syntax**::

    <service>-<purpose>

**Examples**::

    github-work             # GitHub work account (email: john.doe@acme.com)
    gitlab-personal         # GitLab personal account (email: john.personal@gmail.com)
    bitbucket-project       # Bitbucket for specific project (email: dev@project.com)

**Pattern 4: machine-service**

**Syntax**::

    <machine>-<service>

**Examples**::

    laptop-github           # Laptop's key for GitHub (email: john.doe@acme.com)
    desktop-gitlab          # Desktop's key for GitLab (email: alice.smith@techcorp.com)
    server-bitbucket        # Server's key for Bitbucket (email: deploy@server.com)

**Pattern 5: organization-service-user**

**Syntax**::

    <organization>-<service>-<username>

**Examples**::

    acme-github-johndoe     # Acme organization, GitHub (email: john.doe@acme.com)
    techcorp-gitlab-alice   # TechCorp, GitLab (email: alice.smith@techcorp.com)
    personal-gitlab-bob     # Personal, GitLab (email: bob.personal@gmail.com)

Recommended Naming Strategy
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

For better organization and clarity, use this comprehensive naming pattern::

    id_<keytype>_<organization>_<service>_<purpose>

**Template Examples**::

    id_ed25519_<company>_github_work
    id_ed25519_personal_gitlab
    id_rsa_<company>_bitbucket_project

**Real Examples with Actual Emails**::

    # For work at Acme Corp
    id_ed25519_acme_github_work         # Email: john.doe@acme.com

    # For personal projects
    id_ed25519_personal_gitlab          # Email: john.personal@gmail.com

    # For TechCorp Bitbucket
    id_rsa_techcorp_bitbucket_project   # Email: alice.smith@techcorp.com

    # For freelance work
    id_ed25519_freelance_github         # Email: bob.freelance@gmail.com

**Benefits**:

- Easy to identify key type (ed25519, rsa)
- Clear purpose (work, personal, project, freelance)
- Service identification (github, gitlab, bitbucket)
- Organization context (acme, techcorp, company name, personal)

Quick Reference: Placeholder vs Actual Examples
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: Email and Key Name Examples
   :header-rows: 1
   :widths: 25 35 40

   * - **Use Case**
     - **Placeholder Format**
     - **Actual Example**
   * - Work Email
     - ``your.email@example.com``
     - ``john.doe@acme.com``
   * - Personal Email
     - ``your.email@example.com``
     - ``john.personal@gmail.com``
   * - Work Key Name
     - ``id_ed25519_company_github``
     - ``id_ed25519_acme_github_work``
   * - Personal Key Name
     - ``id_ed25519_personal_github``
     - ``id_ed25519_personal_github``
   * - Freelance Key
     - ``id_ed25519_freelance_service``
     - ``id_ed25519_freelance_gitlab``
   * - Multi-account Work
     - ``username-company``
     - ``johndoe-acme``

**When to use placeholders**: In documentation, templates, or when sharing examples publicly.

**When to use actual values**: In your actual SSH key generation commands on your local machine.

Complete Key Generation Example with Custom Name
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Full interactive session**::

    $ cd ~/projects/
    $ ssh-keygen -t ed25519 -C "john.doe@acme.com"

    Generating public/private ed25519 key pair.
    Enter file in which to save the key (/home/user/.ssh/id_ed25519): id_ed25519_acme_github
    Enter passphrase (empty for no passphrase): [type strong passphrase]
    Enter same passphrase again: [type same passphrase]

    Your identification has been saved in id_ed25519_acme_github
    Your public key has been saved in id_ed25519_acme_github.pub
    The key fingerprint is:
    SHA256:xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx john.doe@acme.com
    The key's randomart image is:
    +--[ED25519 256]--+
    |                 |
    |       ...       |
    +----[SHA256]-----+

**Files created**:

- ``id_ed25519_acme_github`` (private key, no extension)
- ``id_ed25519_acme_github.pub`` (public key, .pub extension)

**Public key content example**::

    ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIM8K7Qi5qT9W... john.doe@acme.com

Notice the email ``john.doe@acme.com`` appears at the end as a comment, but the filename is ``id_ed25519_acme_github`` (what you typed).

.. tip::
    **Best Practice**: Always use descriptive names that indicate:

    1. Key type (ed25519, rsa)
    2. Purpose (work, personal)
    3. Service (github, gitlab, bitbucket)
    4. Organization (company name, personal)

    This makes managing multiple keys much easier!

Real-World Example: Multiple Keys Setup
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Here's a practical example of setting up multiple SSH keys for different purposes:

**Scenario**: John works at Acme Corp, has personal projects, and does freelance work.

**Key 1: Work GitHub**::

    # Command with actual email
    ssh-keygen -t ed25519 -C "john.doe@acme.com"

    # When prompted for filename, enter:
    id_ed25519_acme_github

    # Result: Used for all Acme Corp work repositories

**Key 2: Personal GitLab**::

    # Command with actual email
    ssh-keygen -t ed25519 -C "john.personal@gmail.com"

    # When prompted for filename, enter:
    id_ed25519_personal_gitlab

    # Result: Used for personal side projects

**Key 3: Freelance Bitbucket**::

    # Command with actual email
    ssh-keygen -t ed25519 -C "john.freelance@gmail.com"

    # When prompted for filename, enter:
    id_ed25519_freelance_bitbucket

    # Result: Used for client projects

**All keys in ~/.ssh/ directory**::

    ~/.ssh/
    ├── id_ed25519_acme_github          (private key for work)
    ├── id_ed25519_acme_github.pub      (public key for work)
    ├── id_ed25519_personal_gitlab      (private key for personal)
    ├── id_ed25519_personal_gitlab.pub  (public key for personal)
    ├── id_ed25519_freelance_bitbucket  (private key for freelance)
    └── id_ed25519_freelance_bitbucket.pub (public key for freelance)

Alternative: Generate RSA SSH Key
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If your system doesn't support ED25519, use RSA::

    ssh-keygen -t rsa -b 4096 -C "your.email@example.com"

**Real example**::

    ssh-keygen -t rsa -b 4096 -C "alice.smith@techcorp.com"

**Command breakdown**:

- ``-t rsa``: Specifies RSA key type
- ``-b 4096``: Sets key size to 4096 bits (more secure than default 2048)
- ``-C "your.email@example.com"``: Adds identifying comment

.. note::
    **Key type comparison**:

    - **ED25519**: Modern, faster, smaller key size, more secure (recommended)
    - **RSA**: Widely supported, larger key size, older algorithm

Key Generation Output
~~~~~~~~~~~~~~~~~~~~~

After generating the key, you'll see output similar to::

    Your identification has been saved in your-key-name
    Your public key has been saved in your-key-name.pub
    The key fingerprint is:
    SHA256:xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx your.email@example.com

.. important::
    **ssh-keygen ALWAYS generates TWO files** - a key pair:

    1. **Private key** (no file extension)
    2. **Public key** (with ``.pub`` extension)

**Two files are created**:

- ``your-key-name``: **Private key** (keep secret, NEVER share)
- ``your-key-name.pub``: **Public key** (safe to share, add to Git services)

**Example with actual filenames**:

If you named your key ``id_ed25519_acme_github``, you'll get:

- ``id_ed25519_acme_github`` → Private key
- ``id_ed25519_acme_github.pub`` → Public key

Understanding the Key Pair
~~~~~~~~~~~~~~~~~~~~~~~~~~~

**How the two keys work together**::

    ┌─────────────────────────────────────────────────────────────┐
    │                    SSH Key Pair Generation                  │
    │                                                              │
    │  Command: ssh-keygen -t ed25519 -C "john.doe@acme.com"     │
    └─────────────────────────────────────────────────────────────┘
                                 │
                                 ▼
                    ┌────────────────────────┐
                    │   Generates TWO files  │
                    └────────────────────────┘
                                 │
                 ┌───────────────┴───────────────┐
                 │                               │
                 ▼                               ▼
    ┌────────────────────────┐      ┌────────────────────────┐
    │   PRIVATE KEY          │      │   PUBLIC KEY           │
    │   (No extension)       │      │   (.pub extension)     │
    ├────────────────────────┤      ├────────────────────────┤
    │ File: id_ed25519_acme  │      │ File: id_ed25519_acme  │
    │       _github          │      │       _github.pub      │
    ├────────────────────────┤      ├────────────────────────┤
    │ Location:              │      │ Location:              │
    │ - Keep on your machine │      │ - Add to GitHub        │
    │ - Never share          │      │ - Add to GitLab        │
    │ - Never commit to Git  │      │ - Add to Bitbucket     │
    │ - Store in ~/.ssh/     │      │ - Safe to share        │
    ├────────────────────────┤      ├────────────────────────┤
    │ Permissions: 600       │      │ Permissions: 644       │
    │ (Read/Write for owner) │      │ (Read for everyone)    │
    └────────────────────────┘      └────────────────────────┘

**Key Pair Relationship**:

- The **private key** stays on your computer
- The **public key** goes to GitHub/GitLab/Bitbucket
- They work as a **cryptographic pair** - messages encrypted with the public key can only be decrypted with the private key
- This is why you must **NEVER share** your private key

**What each file contains**:

**Private Key** (``id_ed25519_acme_github``)::

    -----BEGIN OPENSSH PRIVATE KEY-----
    b3BlbnNzaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAAAAAAAABAAAAMwAAAAtzc2gtZW
    [Many lines of encrypted data]
    -----END OPENSSH PRIVATE KEY-----

**Public Key** (``id_ed25519_acme_github.pub``)::

    ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAILongRandomString john.doe@acme.com

.. tip::
    **Easy way to remember**:

    - ``.pub`` = PUBlic = Share with GitHub/GitLab
    - No extension = PRIVate = Keep secret on your machine

Moving Keys to SSH Directory
-----------------------------

For proper organization and security, move your keys to the ``~/.ssh/`` directory.

Step 1: Create SSH Directory
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Create the ``.ssh`` directory if it doesn't exist::

    mkdir -p ~/.ssh

Step 2: Move Keys to SSH Directory
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Move both the private and public keys::

    mv ~/your-project-directory/your-key-name ~/.ssh/
    mv ~/your-project-directory/your-key-name.pub ~/.ssh/

**Real example** (moving both files)::

    # Move BOTH the private key AND public key
    mv ~/projects/id_ed25519_acme_github ~/.ssh/
    mv ~/projects/id_ed25519_acme_github.pub ~/.ssh/

.. important::
    You must move **BOTH files** (the private key and the .pub public key). Both are required for SSH authentication to work properly.

Step 3: Set Proper Permissions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Set secure permissions on **BOTH** keys::

    chmod 600 ~/.ssh/your-key-name
    chmod 644 ~/.ssh/your-key-name.pub

**Real example** (setting permissions on both files)::

    # Set permissions on PRIVATE key (more restrictive)
    chmod 600 ~/.ssh/id_ed25519_acme_github

    # Set permissions on PUBLIC key (less restrictive)
    chmod 644 ~/.ssh/id_ed25519_acme_github.pub

**Permission breakdown**:

- ``600`` (private key): Owner can read/write, no one else can access
- ``644`` (public key): Owner can read/write, others can only read

.. warning::
    **Security critical**: Private keys must have restrictive permissions (600). SSH will refuse to use keys with overly permissive permissions.

Adding Key to SSH Agent
------------------------

The SSH agent manages your SSH keys and remembers your passphrase during your session.

Step 1: Start SSH Agent
~~~~~~~~~~~~~~~~~~~~~~~~

Start the SSH agent in the background::

    eval "$(ssh-agent -s)"

**Expected output**::

    Agent pid 12345

.. tip::
    The agent is usually already running. This command is safe to run multiple times.

Step 2: Add Key to Agent
~~~~~~~~~~~~~~~~~~~~~~~~~

Add your private key to the SSH agent::

    ssh-add ~/.ssh/your-key-name

**If you set a passphrase**, you'll be prompted to enter it::

    Enter passphrase for ~/.ssh/your-key-name:

Step 3: Verify Key is Loaded
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

List all keys currently loaded in the agent::

    ssh-add -l

**Expected output**::

    256 SHA256:xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx your.email@example.com (ED25519)

Additional SSH Agent Commands
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**List all loaded keys with full public key**::

    ssh-add -L

**Remove specific key from agent**::

    ssh-add -d ~/.ssh/your-key-name

**Remove all keys from agent**::

    ssh-add -D

Adding Public Key to GitHub
----------------------------

Now that your SSH key is generated and loaded, add the public key to GitHub.

Step 1: Copy Public Key to Clipboard
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Linux (using xclip)**:

First, install xclip if not already installed::

    sudo apt install -y xclip

Copy the public key::

    xclip -selection clipboard < ~/.ssh/your-key-name.pub

**Linux (using cat)**::

    cat ~/.ssh/your-key-name.pub

Then manually copy the output.

**macOS**::

    pbcopy < ~/.ssh/your-key-name.pub

**Windows (Git Bash)**::

    clip < ~/.ssh/your-key-name.pub

Step 2: Add Key to GitHub
~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Open GitHub in your browser and log in
2. Click your profile photo (top-right) → **Settings**
3. In the left sidebar, click **SSH and GPG keys**
4. Click **New SSH key** or **Add SSH key**
5. In the "Title" field, add a descriptive label (e.g., "Work Laptop" or "Personal Desktop")
6. In the "Key" field, paste your public key (entire line starting with ``ssh-ed25519`` or ``ssh-rsa``)
7. Click **Add SSH key**
8. If prompted, confirm your GitHub password

.. important::
    **Public key format**: The key should be one long line starting with ``ssh-ed25519`` or ``ssh-rsa``, followed by the key data, and ending with your email comment.

Step 3: Test GitHub Connection
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Test your SSH connection to GitHub::

    ssh -T git@github.com

**First-time connection**: You'll see a message about host authenticity::

    The authenticity of host 'github.com (IP_ADDRESS)' can't be established.
    ED25519 key fingerprint is SHA256:xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx.
    Are you sure you want to continue connecting (yes/no/[fingerprint])?

Type ``yes`` and press Enter.

**Expected success message**::

    Hi username! You've successfully authenticated, but GitHub does not provide shell access.

.. note::
    The "does not provide shell access" message is normal and means your SSH key is working correctly.

Adding Public Key to GitLab
----------------------------

Step 1: Copy Public Key
~~~~~~~~~~~~~~~~~~~~~~~~

Copy your public key using one of the methods described in the GitHub section.

Step 2: Add Key to GitLab
~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Open GitLab in your browser and log in
2. Click your profile picture (top-right) → **Preferences**
3. In the left sidebar, click **SSH Keys**
4. Paste your public key in the "Key" text box
5. Add a descriptive title in the "Title" field
6. Optionally set an expiration date
7. Click **Add key**

Step 3: Test GitLab Connection
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Test your SSH connection to GitLab::

    ssh -T git@gitlab.com

**Expected success message**::

    Welcome to GitLab, @username!

Adding Public Key to Bitbucket
-------------------------------

Step 1: Copy Public Key
~~~~~~~~~~~~~~~~~~~~~~~~

Copy your public key using one of the methods described earlier.

Step 2: Add Key to Bitbucket
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Open Bitbucket in your browser and log in
2. Click your profile avatar (bottom-left) → **Personal settings**
3. In the left sidebar, click **SSH keys**
4. Click **Add key**
5. Paste your public key in the "Key" text box
6. Add a descriptive label
7. Click **Add key**

Step 3: Test Bitbucket Connection
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Test your SSH connection to Bitbucket::

    ssh -T git@bitbucket.org

**Expected success message**::

    authenticated via ssh key.
    You can use git to connect to Bitbucket.

Using SSH Keys with Git
-----------------------

Clone Repository with SSH
~~~~~~~~~~~~~~~~~~~~~~~~~~

When cloning a repository, use the SSH URL instead of HTTPS::

    git clone git@github.com:username/repository.git

Change Existing Repository to SSH
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If you already have a repository cloned with HTTPS, change it to SSH::

    git remote set-url origin git@github.com:username/repository.git

Verify the remote URL::

    git remote -v

**Expected output**::

    origin  git@github.com:username/repository.git (fetch)
    origin  git@github.com:username/repository.git (push)

Managing Multiple SSH Keys
---------------------------

If you have multiple SSH keys for different services or accounts, configure SSH to use the right key for each service.

Create SSH Config File
~~~~~~~~~~~~~~~~~~~~~~

Create or edit the SSH config file::

    nano ~/.ssh/config

Add Configuration for Each Service
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Example configuration**::

    # GitHub Work Account
    Host github.com-work
        HostName github.com
        User git
        IdentityFile ~/.ssh/id_ed25519_work
        IdentitiesOnly yes

    # GitHub Personal Account
    Host github.com-personal
        HostName github.com
        User git
        IdentityFile ~/.ssh/id_ed25519_personal
        IdentitiesOnly yes

    # GitLab
    Host gitlab.com
        HostName gitlab.com
        User git
        IdentityFile ~/.ssh/id_ed25519_gitlab
        IdentitiesOnly yes

    # Bitbucket
    Host bitbucket.org
        HostName bitbucket.org
        User git
        IdentityFile ~/.ssh/id_ed25519_bitbucket
        IdentitiesOnly yes

**Configuration explanation**:

- ``Host``: Alias you'll use in Git commands
- ``HostName``: Actual hostname of the service
- ``User``: Always ``git`` for Git services
- ``IdentityFile``: Path to your private key
- ``IdentitiesOnly``: Only use specified key (prevents trying other keys)

Using Different Keys
~~~~~~~~~~~~~~~~~~~~

Clone using specific host alias::

    git clone git@github.com-work:username/work-repo.git
    git clone git@github.com-personal:username/personal-repo.git

Set Proper Permissions on Config
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    chmod 600 ~/.ssh/config

Security Best Practices
-----------------------

1. **Never share private keys**

   - Private keys should never leave your machine
   - Don't email, message, or commit them to repositories

2. **Use strong passphrases**

   - Protect private keys with strong passphrases
   - Use a password manager to store passphrases

3. **Set correct permissions**

   - Private keys: ``chmod 600``
   - Public keys: ``chmod 644``
   - SSH directory: ``chmod 700 ~/.ssh``

4. **Use different keys for different purposes**

   - Separate keys for work and personal accounts
   - Different keys for different machines

5. **Regularly rotate keys**

   - Generate new keys periodically
   - Remove old keys from services when no longer needed

6. **Add expiration dates**

   - Some services allow setting expiration dates on SSH keys
   - Helps enforce key rotation policies

7. **Keep private keys secure**

   - Never store in cloud storage
   - Never commit to version control
   - Encrypt your disk/home directory

8. **Monitor key usage**

   - Regularly review authorized keys on services
   - Remove unused or unknown keys

Troubleshooting
---------------

Permission Denied (publickey)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Error**::

    git@github.com: Permission denied (publickey).

**Solutions**:

1. Verify SSH key is added to GitHub/GitLab/Bitbucket
2. Check SSH agent is running and key is loaded::

       ssh-add -l

3. Test SSH connection::

       ssh -T git@github.com

4. Ensure you're using SSH URL, not HTTPS::

       git remote -v

5. Check SSH key permissions::

       ls -la ~/.ssh/

Bad Permissions
~~~~~~~~~~~~~~~

**Error**::

    Permissions 0644 for '~/.ssh/id_ed25519' are too open.

**Solution**: Fix private key permissions::

    chmod 600 ~/.ssh/id_ed25519

Could Not Open a Connection to Your Authentication Agent
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Error**::

    Could not open a connection to your authentication agent.

**Solution**: Start SSH agent::

    eval "$(ssh-agent -s)"
    ssh-add ~/.ssh/your-key-name

Wrong Key Being Used
~~~~~~~~~~~~~~~~~~~~

**Problem**: SSH is using the wrong key for a service.

**Solution**: Create or update ``~/.ssh/config`` with specific ``IdentityFile`` directives (see "Managing Multiple SSH Keys" section).

Host Key Verification Failed
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Error**::

    Host key verification failed.

**Solution**: Remove the old host key and try again::

    ssh-keygen -R github.com
    ssh -T git@github.com

Type ``yes`` when prompted about host authenticity.

Key Not Loading on System Restart
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Problem**: SSH keys need to be added to agent after every restart.

**Solution**: Add to shell startup file (``~/.bashrc`` or ``~/.zshrc``)::

    # Start SSH agent and add keys
    if [ -z "$SSH_AUTH_SOCK" ]; then
        eval "$(ssh-agent -s)"
        ssh-add ~/.ssh/your-key-name
    fi

Frequently Asked Questions (FAQ)
---------------------------------

Does ssh-keygen generate both public and private keys?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Yes!** When you run ``ssh-keygen``, it **ALWAYS generates TWO files**:

1. **Private key** (no extension) - e.g., ``id_ed25519_acme_github``
2. **Public key** (with ``.pub`` extension) - e.g., ``id_ed25519_acme_github.pub``

You never have to generate them separately. One ``ssh-keygen`` command creates both.

Which key do I upload to GitHub/GitLab?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Upload the **PUBLIC key** (the file ending in ``.pub``).

**Example**::

    # Copy the PUBLIC key (the .pub file)
    cat ~/.ssh/id_ed25519_acme_github.pub

**NEVER** upload the private key (the one without ``.pub``).

What happens to the private key?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The **private key** stays on your computer in the ``~/.ssh/`` directory. You:

- Add it to ssh-agent: ``ssh-add ~/.ssh/your-key-name``
- Set permissions to 600: ``chmod 600 ~/.ssh/your-key-name``
- **NEVER** share it, upload it, or commit it to Git

Do I need both files for SSH to work?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Yes!** Both files must exist:

- **Private key**: On your local machine in ``~/.ssh/``
- **Public key**: On GitHub/GitLab/Bitbucket

They work as a **cryptographic pair**. If you delete either one, SSH authentication will fail.

Can I regenerate the public key from the private key?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Yes**, but it's not recommended. If you lose your ``.pub`` file, you can regenerate it::

    ssh-keygen -y -f ~/.ssh/your-private-key > ~/.ssh/your-private-key.pub

However, it's better to keep both original files from the initial generation.

How many key pairs can I have?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**As many as you want!** You can create separate key pairs for:

- Different services (GitHub, GitLab, Bitbucket)
- Different accounts (work, personal, freelance)
- Different machines (laptop, desktop, server)

Example: You might have::

    ~/.ssh/id_ed25519_work_github          (private)
    ~/.ssh/id_ed25519_work_github.pub      (public)
    ~/.ssh/id_ed25519_personal_gitlab      (private)
    ~/.ssh/id_ed25519_personal_gitlab.pub  (public)
    ~/.ssh/id_ed25519_freelance_bitbucket  (private)
    ~/.ssh/id_ed25519_freelance_bitbucket.pub (public)

That's **6 files** total (3 key pairs).

Listing All SSH Keys
--------------------

List All Keys in SSH Directory
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    ls -la ~/.ssh/

**Example output showing key pairs**::

    -rw------- 1 user user  464 Oct 31 10:00 id_ed25519_acme_github
    -rw-r--r-- 1 user user  103 Oct 31 10:00 id_ed25519_acme_github.pub
    -rw------- 1 user user  464 Oct 31 11:00 id_ed25519_personal_gitlab
    -rw-r--r-- 1 user user  103 Oct 31 11:00 id_ed25519_personal_gitlab.pub

Notice each key pair has two files (one with ``.pub``, one without).

View Public Key Content
~~~~~~~~~~~~~~~~~~~~~~~~

::

    cat ~/.ssh/your-key-name.pub

View Key Fingerprint
~~~~~~~~~~~~~~~~~~~~~

::

    ssh-keygen -lf ~/.ssh/your-key-name.pub

**Example output**::

    256 SHA256:xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx your.email@example.com (ED25519)

List Keys on GitHub
~~~~~~~~~~~~~~~~~~~

View your SSH keys on GitHub:

1. Go to GitHub → Settings → SSH and GPG keys
2. View all added keys with their titles and fingerprints

Removing SSH Keys
-----------------

Remove Key from SSH Agent
~~~~~~~~~~~~~~~~~~~~~~~~~~

**Remove specific key**::

    ssh-add -d ~/.ssh/your-key-name

**Remove all keys**::

    ssh-add -D

Delete Key Files
~~~~~~~~~~~~~~~~

::

    rm ~/.ssh/your-key-name
    rm ~/.ssh/your-key-name.pub

.. warning::
    Make sure the key is removed from all services (GitHub, GitLab, etc.) before deleting the files.

Remove Key from GitHub
~~~~~~~~~~~~~~~~~~~~~~~

1. Go to GitHub → Settings → SSH and GPG keys
2. Find the key you want to remove
3. Click **Delete**
4. Confirm deletion

Quick Reference Commands
------------------------

**Generate ED25519 key**::

    ssh-keygen -t ed25519 -C "your.email@example.com"

**Generate RSA key**::

    ssh-keygen -t rsa -b 4096 -C "your.email@example.com"

**Start SSH agent**::

    eval "$(ssh-agent -s)"

**Add key to agent**::

    ssh-add ~/.ssh/your-key-name

**List loaded keys**::

    ssh-add -l

**Copy public key (Linux)**::

    xclip -selection clipboard < ~/.ssh/your-key-name.pub

**Test GitHub connection**::

    ssh -T git@github.com

**Test GitLab connection**::

    ssh -T git@gitlab.com

**Test Bitbucket connection**::

    ssh -T git@bitbucket.org

**Change remote to SSH**::

    git remote set-url origin git@github.com:username/repository.git

**View remote URLs**::

    git remote -v

**Set key permissions**::

    chmod 600 ~/.ssh/your-key-name
    chmod 644 ~/.ssh/your-key-name.pub

Additional Resources
--------------------

Official Documentation
~~~~~~~~~~~~~~~~~~~~~~~

- **GitHub SSH Keys**: https://docs.github.com/en/authentication/connecting-to-github-with-ssh
- **GitLab SSH Keys**: https://docs.gitlab.com/ee/user/ssh.html
- **Bitbucket SSH Keys**: https://support.atlassian.com/bitbucket-cloud/docs/set-up-an-ssh-key/
- **OpenSSH Manual**: https://www.openssh.com/manual.html

Key Management Tools
~~~~~~~~~~~~~~~~~~~~

- **ssh-keygen**: Generate and manage SSH keys
- **ssh-agent**: Manage SSH keys and passphrases
- **ssh-add**: Add keys to SSH agent
- **keychain**: Manage SSH and GPG keys (advanced)

Best Practices Summary
----------------------

1. Use ED25519 keys (modern and secure)
2. Always protect private keys with strong passphrases
3. Set correct permissions (600 for private, 644 for public)
4. Use SSH agent to avoid entering passphrase repeatedly
5. Organize keys in ``~/.ssh/`` directory
6. Use descriptive names when adding keys to services
7. Create SSH config for multiple keys/services
8. Regularly audit and rotate SSH keys
9. Never commit private keys to version control
10. Test SSH connection after adding keys to services

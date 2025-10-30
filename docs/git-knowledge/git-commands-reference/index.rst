Git: Commands Reference Guide
==============================

Comprehensive reference guide for essential Git commands with examples and explanations for everyday Git operations.

.. contents:: Table of Contents
   :local:
   :depth: 2

Overview
--------

This guide covers Git commands organized by category, from basic operations to advanced techniques. Each command includes:

- Description of what it does
- Common usage examples
- Important flags and options
- Best practices and warnings

Git Basics
----------

Initialize Repository
~~~~~~~~~~~~~~~~~~~~~

**git init**

Create an empty Git repository in the specified directory. Run with no arguments to initialize the current directory as a git repository.

.. code-block:: bash

    # Initialize repository in current directory
    git init

    # Initialize repository in specific directory
    git init <directory>

Clone Repository
~~~~~~~~~~~~~~~~

**git clone**

Clone a repository located at the given URL onto your local machine. The original repository can be located on the local filesystem or on a remote machine via HTTP or SSH.

.. code-block:: bash

    # Clone using HTTPS
    git clone https://github.com/user/repo.git

    # Clone using SSH
    git clone git@github.com:user/repo.git

    # Clone into specific directory
    git clone https://github.com/user/repo.git my-project

    # Clone specific branch
    git clone -b branch-name https://github.com/user/repo.git

    # Clone with depth (shallow clone)
    git clone --depth 1 https://github.com/user/repo.git

Configuration
~~~~~~~~~~~~~

**git config**

Define configuration options for Git. Developers commonly use ``--global`` flag to set config options for the current user.

.. code-block:: bash

    # Set user name globally
    git config --global user.name "Your Name"

    # Set user email globally
    git config --global user.email "your.email@example.com"

    # Set user name for current repository only
    git config user.name "Your Name"

    # Create command alias
    git config --global alias.glog "log --graph --oneline"

    # Set default editor
    git config --global core.editor "vim"
    git config --global core.editor "code --wait"  # VS Code

    # Edit global configuration
    git config --global --edit

    # List all configuration
    git config --list

    # List global configuration
    git config --global --list

Working with Files
------------------

Stage Changes
~~~~~~~~~~~~~

**git add**

Stage changes in the working directory for the next commit. Replace ``<directory>`` with a ``<file>`` to change a specific file.

.. code-block:: bash

    # Stage specific file
    git add file.txt

    # Stage all changes in current directory
    git add .

    # Stage all changes recursively
    git add -A

    # Stage specific directory
    git add directory/

    # Interactive staging (choose what to stage)
    git add -i

    # Stage only modified files (not new files)
    git add -u

    # Stage with patch mode (interactive)
    git add -p

Commit Changes
~~~~~~~~~~~~~~

**git commit**

Record changes to the repository. The commit command is used to save your staged changes to the repository.

.. code-block:: bash

    # Commit with message
    git commit -m "Your commit message"

    # Commit with detailed message
    git commit -m "Title" -m "Detailed description"

    # Amend last commit (change message or add files)
    git commit --amend

    # Amend last commit with new message
    git commit --amend -m "New message"

    # Amend last commit and add staged files
    git add forgotten-file.txt
    git commit --amend --no-edit

    # Amend last commit message only (no changes)
    git commit --amend -m "Updated commit message"

    # Amend last commit and change author
    git commit --amend --author="Name <email@example.com>"

    # Amend last commit and change date
    git commit --amend --date="2024-01-01 12:00:00"

    # Amend last commit without changing commit date
    git commit --amend --no-edit --no-verify

    # Skip hooks (use with caution)
    git commit --no-verify -m "Message"

Check Status
~~~~~~~~~~~~

**git status**

Show the working tree status. Lists which files are staged, unstaged, and untracked.

.. code-block:: bash

    # Show status
    git status

    # Short format
    git status -s

    # Show branch information
    git status -b

View Differences
~~~~~~~~~~~~~~~~

**git diff**

Show changes between commits, commit and working tree, etc.

.. code-block:: bash

    # Show unstaged changes
    git diff

    # Show staged changes
    git diff --cached
    git diff --staged

    # Show all changes (staged + unstaged)
    git diff HEAD

    # Show differences for specific file
    git diff file.txt

    # Show differences between commits
    git diff commit1 commit2

    # Show differences between branches
    git diff branch1 branch2

    # Show file differences between commits
    git diff commit1:file.txt commit2:file.txt

    # Show word-level diff
    git diff --word-diff

View History
------------

**git log**

Display commit history with various formatting options.

.. code-block:: bash

    # Show commit history
    git log

    # Show last N commits
    git log -5

    # One line per commit
    git log --oneline

    # Show full diff for each commit
    git log -p

    # Show file statistics
    git log --stat

    # Show graph
    git log --graph

    # Show decorated graph
    git log --graph --decorate --oneline

    # Show commits by author
    git log --author="John Doe"

    # Search commit messages
    git log --grep="search term"

    # Show commits for specific file
    git log -- file.txt

    # Show commits since date
    git log --since="2 weeks ago"

    # Show commits between dates
    git log --since="2024-01-01" --until="2024-12-31"

    # Show commits between commits/branches
    git log commit1..commit2
    git log branch1..branch2

    # Show only merge commits
    git log --merges

    # Show commits not in remote
    git log origin/main..HEAD

Branching
---------

List Branches
~~~~~~~~~~~~~

**git branch**

List, create, or delete branches.

.. code-block:: bash

    # List local branches
    git branch

    # List all branches (local + remote)
    git branch -a

    # List remote branches
    git branch -r

    # Show current branch with last commit
    git branch -v

    # Show merged branches
    git branch --merged

    # Show unmerged branches
    git branch --no-merged

Create Branch
~~~~~~~~~~~~~

.. code-block:: bash

    # Create new branch
    git branch branch-name

    # Create branch from specific commit
    git branch branch-name commit-hash

    # Create branch from remote branch
    git branch branch-name origin/remote-branch

Switch Branch
~~~~~~~~~~~~~

**git checkout**

Switch branches or restore working tree files.

.. code-block:: bash

    # Switch to existing branch
    git checkout branch-name

    # Create and switch to new branch
    git checkout -b new-branch

    # Create branch from specific commit
    git checkout -b new-branch commit-hash

    # Create branch from remote branch
    git checkout -b local-branch origin/remote-branch

    # Switch to previous branch
    git checkout -

    # Discard changes in working directory
    git checkout -- file.txt

    # Restore file from specific commit
    git checkout commit-hash -- file.txt

**git switch** (Newer alternative to checkout)

.. code-block:: bash

    # Switch to branch
    git switch branch-name

    # Create and switch to new branch
    git switch -c new-branch

Rename Branch
~~~~~~~~~~~~~

.. code-block:: bash

    # Rename current branch
    git branch -m new-name

    # Rename specific branch
    git branch -m old-name new-name

    # Push renamed branch and delete old remote branch
    git push origin new-name
    git push origin --delete old-name

Delete Branch
~~~~~~~~~~~~~

.. code-block:: bash

    # Delete merged branch (safe)
    git branch -d branch-name

    # Force delete branch (unsafe)
    git branch -D branch-name

    # Delete remote branch
    git push origin --delete branch-name
    git push origin :branch-name  # Alternative syntax

Merging
-------

**git merge**

Join two or more development histories together.

.. code-block:: bash

    # Merge branch into current branch
    git merge branch-name

    # Merge with no fast-forward (always creates merge commit)
    git merge --no-ff branch-name

    # Merge with fast-forward only (fails if not possible)
    git merge --ff-only branch-name

    # Merge with commit message
    git merge -m "Merge message" branch-name

    # Abort merge
    git merge --abort

Remote Repositories
-------------------

Manage Remotes
~~~~~~~~~~~~~~

**git remote**

Manage set of tracked repositories.

.. code-block:: bash

    # List remotes
    git remote

    # List remotes with URLs
    git remote -v

    # Show remote URL
    git remote show origin

    # Add remote
    git remote add origin https://github.com/user/repo.git

    # Add remote with custom name
    git remote add upstream https://github.com/original/repo.git

    # Remove remote
    git remote remove origin

    # Rename remote
    git remote rename old-name new-name

    # Update remote URL
    git remote set-url origin https://new-url.git

Fetch
~~~~~

**git fetch**

Download objects and refs from another repository.

.. code-block:: bash

    # Fetch from default remote
    git fetch

    # Fetch from specific remote
    git fetch origin

    # Fetch specific branch
    git fetch origin branch-name

    # Fetch all remotes
    git fetch --all

    # Fetch with tags
    git fetch --tags

    # Fetch and prune (remove deleted remote branches)
    git fetch --prune

Pull
~~~~

**git pull**

Fetch and integrate changes from a remote repository.

.. code-block:: bash

    # Pull from default remote
    git pull

    # Pull from specific remote and branch
    git pull origin main

    # Pull with merge (explicit)
    git pull --no-rebase origin main

    # Pull with rebase instead of merge
    git pull --rebase origin main

    # Pull with rebase by default
    git config --global pull.rebase true

    # Pull with merge by default
    git config --global pull.rebase false

Push
~~~~

**git push**

Update remote refs along with associated objects.

.. code-block:: bash

    # Push to default remote
    git push

    # Push to specific remote and branch
    git push origin branch-name

    # Push and set upstream
    git push -u origin branch-name

    # Push all branches
    git push --all origin

    # Push all tags
    git push --tags origin

    # Force push (use with caution!)
    git push --force origin branch-name

    # Force push with lease (safer)
    git push --force-with-lease origin branch-name

    # Delete remote branch
    git push origin --delete branch-name

Undoing Changes
---------------

Reset
~~~~~

**git reset**

Reset current HEAD to the specified state.

.. code-block:: bash

    # Unstage all files (keep changes)
    git reset

    # Unstage specific file
    git reset file.txt

    # Reset to commit (keep changes in working directory)
    git reset commit-hash

    # Reset to commit (keep changes staged)
    git reset --soft commit-hash

    # Reset to commit (discard all changes)
    git reset --hard commit-hash

    # Reset to previous commit
    git reset HEAD~1

    # Reset to remote branch state
    git reset --hard origin/main

Revert
~~~~~~

**git revert**

Create a new commit that undoes changes made in a specified commit.

.. code-block:: bash

    # Revert last commit
    git revert HEAD

    # Revert specific commit
    git revert commit-hash

    # Revert without creating commit (stage only)
    git revert -n commit-hash

    # Revert multiple commits
    git revert commit1 commit2

Clean
~~~~~

**git clean**

Remove untracked files from working directory.

.. code-block:: bash

    # Show what would be removed (dry run)
    git clean -n

    # Remove untracked files
    git clean -f

    # Remove untracked files and directories
    git clean -fd

    # Remove untracked files and ignored files
    git clean -fX

    # Remove everything (tracked + untracked)
    git clean -fdX

Restore
~~~~~~~

**git restore** (Git 2.23+)

Restore working tree files or staged files.

.. code-block:: bash

    # Discard changes in working directory
    git restore file.txt

    # Discard all changes
    git restore .

    # Unstage file
    git restore --staged file.txt

    # Restore file from specific commit
    git restore --source=commit-hash file.txt

Rewriting History
-----------------

Amend
~~~~~

**git commit --amend**

Modify the last commit. Useful for fixing mistakes or adding forgotten files.

.. code-block:: bash

    # Amend last commit (opens editor to change message)
    git commit --amend

    # Amend last commit with new message
    git commit --amend -m "New message"

    # Amend last commit and add staged files
    git add forgotten-file.txt
    git commit --amend --no-edit

    # Amend last commit message only (no changes)
    git commit --amend -m "Updated commit message"

    # Amend last commit and change author
    git commit --amend --author="Name <email@example.com>"

    # Amend last commit and change date
    git commit --amend --date="2024-01-01 12:00:00"

    # Amend without changing commit date
    git commit --amend --no-edit --no-verify

.. warning::
   Never amend commits that have been pushed to a shared repository. This rewrites history and can cause issues for other developers.

Rebase
~~~~~~

**git rebase**

Reapply commits on top of another base tip.

.. code-block:: bash

    # Rebase current branch onto another branch
    git rebase main

    # Interactive rebase (last N commits)
    git rebase -i HEAD~3

    # Interactive rebase from commit
    git rebase -i commit-hash

    # Continue rebase after resolving conflicts
    git rebase --continue

    # Abort rebase
    git rebase --abort

    # Skip current commit during rebase
    git rebase --skip

    # Rebase with autosquash
    git rebase -i --autosquash HEAD~3

Rebase Operations
~~~~~~~~~~~~~~~~~

During interactive rebase, you can use these commands:

- ``pick`` - Use the commit
- ``reword`` - Use commit, but edit the message
- ``edit`` - Use commit, but stop for amending
- ``squash`` - Use commit, but meld into previous commit
- ``fixup`` - Like squash, but discard commit message
- ``drop`` - Remove commit

Reflog
~~~~~~

**git reflog**

Reference logs, or "reflogs", record when the tips of branches and other references were updated in the local repository.

.. code-block:: bash

    # Show reflog
    git reflog

    # Show reflog with dates
    git reflog --date=relative

    # Show reflog for specific branch
    git reflog show branch-name

    # Restore from reflog
    git checkout HEAD@{2}

Stashing
--------

**git stash**

Temporarily save changes without committing.

.. code-block:: bash

    # Stash changes
    git stash

    # Stash with message
    git stash save "Message"

    # Stash including untracked files
    git stash -u

    # List stashes
    git stash list

    # Show stash content
    git stash show

    # Show stash diff
    git stash show -p

    # Apply stash (keeps stash)
    git stash apply

    # Apply specific stash
    git stash apply stash@{1}

    # Pop stash (removes stash)
    git stash pop

    # Pop specific stash
    git stash pop stash@{1}

    # Delete stash
    git stash drop

    # Delete all stashes
    git stash clear

Tags
----

**git tag**

Create, list, delete, or verify tags.

.. code-block:: bash

    # List tags
    git tag

    # Create lightweight tag
    git tag v1.0.0

    # Create annotated tag
    git tag -a v1.0.0 -m "Release version 1.0.0"

    # Tag specific commit
    git tag v1.0.0 commit-hash

    # Show tag information
    git show v1.0.0

    # Delete local tag
    git tag -d v1.0.0

    # Push tag to remote
    git push origin v1.0.0

    # Push all tags
    git push --tags

    # Delete remote tag
    git push origin --delete v1.0.0
    git push origin :refs/tags/v1.0.0

Useful Commands
---------------

Show Information
~~~~~~~~~~~~~~~~

.. code-block:: bash

    # Show commit details
    git show commit-hash

    # Show file at specific commit
    git show commit-hash:file.txt

    # Show current branch
    git branch --show-current

    # Show remote URL
    git remote get-url origin

    # Show last commit info
    git log -1

    # Show who changed what and when
    git blame file.txt

    # Count commits
    git rev-list --count HEAD

    # Find large files
    git rev-list --objects --all | git cat-file --batch-check='%(objecttype) %(objectname) %(objectsize) %(rest)' | awk '/^blob/ {print substr($0,6)}' | sort --numeric-sort --key=2 | tail -10

Search
~~~~~~

.. code-block:: bash

    # Search in code
    git grep "search term"

    # Search in specific path
    git grep "search term" -- path/

    # Search with case insensitive
    git grep -i "search term"

    # Search through history
    git log -S "search term"

    # Find when file was deleted
    git log --diff-filter=D --summary

Bisect
~~~~~~

**git bisect**

Use binary search to find the commit that introduced a bug.

.. code-block:: bash

    # Start bisect
    git bisect start

    # Mark commit as bad
    git bisect bad

    # Mark commit as good
    git bisect good commit-hash

    # Mark current commit as good/bad
    git bisect good
    git bisect bad

    # Auto bisect with script
    git bisect run ./test-script.sh

    # Reset bisect
    git bisect reset

Cherry-Pick
~~~~~~~~~~~

**git cherry-pick**

Apply changes from one or more commits to current branch.

.. code-block:: bash

    # Cherry-pick commit
    git cherry-pick commit-hash

    # Cherry-pick range
    git cherry-pick commit1..commit2

    # Cherry-pick without commit
    git cherry-pick -n commit-hash

    # Cherry-pick with editing
    git cherry-pick -e commit-hash

Submodules
----------

.. code-block:: bash

    # Add submodule
    git submodule add https://github.com/user/repo.git path/to/submodule

    # Initialize submodules
    git submodule init

    # Update submodules
    git submodule update

    # Clone with submodules
    git clone --recursive https://github.com/user/repo.git

    # Update all submodules
    git submodule update --remote

Advanced Operations
-------------------

Worktree
~~~~~~~~

**git worktree**

Manage multiple working trees attached to the same repository.

.. code-block:: bash

    # List worktrees
    git worktree list

    # Create new worktree
    git worktree add ../feature-branch feature-branch

    # Remove worktree
    git worktree remove ../feature-branch

    # Prune worktrees
    git worktree prune

Patch
~~~~~

.. code-block:: bash

    # Create patch from commits
    git format-patch -1 HEAD

    # Create patch from range
    git format-patch commit1..commit2

    # Apply patch
    git apply patch-file.patch

    # Apply patch with commit
    git am patch-file.patch

Archive
~~~~~~~

.. code-block:: bash

    # Create archive
    git archive --format=zip HEAD > archive.zip

    # Create archive from specific directory
    git archive --format=tar HEAD -- path/ > archive.tar

Common Workflows
----------------

Feature Branch Workflow
~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

    # Create feature branch
    git checkout -b feature/new-feature

    # Make changes and commit
    git add .
    git commit -m "feat: add new feature"

    # Push to remote
    git push -u origin feature/new-feature

    # Create pull request (on GitHub/GitLab)
    # After merge, clean up
    git checkout main
    git pull
    git branch -d feature/new-feature

Initial Setup Workflow
~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

    # Configure Git
    git config --global user.name "Your Name"
    git config --global user.email "your.email@example.com"

    # Initialize repository
    git init

    # Add files
    git add .

    # First commit
    git commit -m "Initial commit"

    # Add remote
    git remote add origin https://github.com/user/repo.git

    # Push to remote
    git push -u origin main

Updating from Remote
~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

    # Fetch latest changes
    git fetch origin

    # Merge remote changes
    git merge origin/main

    # Or use pull (fetch + merge)
    git pull origin main

    # Or use pull with rebase
    git pull --rebase origin main

Quick Reference
---------------

Essential Commands
~~~~~~~~~~~~~~~~~~

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Command
     - Description
   * - ``git init``
     - Initialize repository
   * - ``git clone <url>``
     - Clone repository
   * - ``git add .``
     - Stage all changes
   * - ``git commit -m "msg"``
     - Commit changes
   * - ``git status``
     - Show status
   * - ``git log``
     - Show history
   * - ``git diff``
     - Show changes
   * - ``git branch``
     - List branches
   * - ``git checkout -b <name>``
     - Create and switch branch
   * - ``git merge <branch>``
     - Merge branch
   * - ``git push``
     - Push to remote
   * - ``git pull``
     - Pull from remote

Useful Aliases
~~~~~~~~~~~~~~

Add these to your Git config for shortcuts:

.. code-block:: bash

    git config --global alias.st status
    git config --global alias.co checkout
    git config --global alias.br branch
    git config --global alias.ci commit
    git config --global alias.unstage 'reset HEAD --'
    git config --global alias.last 'log -1 HEAD'
    git config --global alias.visual '!gitk'
    git config --global alias.lg "log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --date=relative"
    git config --global alias.glog "log --graph --oneline --all --decorate"

See Also
--------

- :doc:`../git-first-time-setup/index` - First time Git configuration
- :doc:`../git-commit-messages/index` - Commit message guide
- :doc:`../git-stash/index` - Git stash guide
- :doc:`../git-branch-name/index` - Display branch name in terminal
- `Git Official Documentation <https://git-scm.com/doc>`_
- `Atlassian Git Tutorials <https://www.atlassian.com/git/tutorials>`_


Git: GitHub Releases Guide
===========================

Complete guide for creating and managing GitHub releases using Git tags. Learn how to tag your releases and publish them on GitHub.

.. contents:: Table of Contents
   :local:
   :depth: 2

Overview
--------

GitHub releases allow you to package and share software versions with your team and users. This guide covers the complete workflow from initializing a repository to creating and pushing release tags to GitHub.

Prerequisites
-------------

Before creating a GitHub release, ensure you have:

- Git installed on your system
- A GitHub account
- Access to the repository (owner or collaborator)
- Basic understanding of Git commands

GitHub Release Workflow
-----------------------

Complete step-by-step workflow for creating and releasing tags on GitHub:

Step 1: Initialize Repository
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

    # Initialize a Git repository
    git init

    # Add files
    git add .

    # Initial commit
    git commit -m "Initial commit"

Step 2: Create GitHub Repository
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Go to `GitHub <https://github.com/>`_
2. Click the "+" icon in the top right corner
3. Select "New repository"
4. Enter repository name (e.g., ``magento2-module-sentimate``)
5. Choose visibility (public or private)
6. Click "Create repository"

**Note**: Do NOT initialize with README, .gitignore, or license if you already have local files.

Step 3: Link Local Repository to GitHub
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

    # Add remote origin
    git remote add origin https://github.com/your-username/magento2-module-sentimate.git

    # Verify remote was added
    git remote -v

    # Expected output:
    # origin  https://github.com/your-username/magento2-module-sentimate.git (fetch)
    # origin  https://github.com/your-username/magento2-module-sentimate.git (push)

**Alternative: Using SSH**

.. code-block:: bash

    # Add remote using SSH
    git remote add origin git@github.com:your-username/magento2-module-sentimate.git

Step 4: Push Code to GitHub
~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

    # Push to main branch (GitHub default)
    git push -u origin main

    # Or for older repositories using master
    git push -u origin master

    # The -u flag sets upstream tracking for future pushes

Step 5: Create and Push Tag
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

There are three ways to create tags:

Option A: Lightweight Tag
^^^^^^^^^^^^^^^^^^^^^^^^^^

Lightweight tags are simple pointers to a specific commit. They don't store additional metadata.

.. code-block:: bash

    # Create lightweight tag
    git tag 1.0.0

    # Push tag to GitHub
    git push origin 1.0.0

    # Push all tags at once
    git push --tags

**When to use**: For local references or temporary tags.

Option B: Annotated Tag (Recommended)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Annotated tags are recommended for releases as they store author, date, and message information.

.. code-block:: bash

    # Create annotated tag with single-line message
    git tag -a 1.0.0 -m "Release version 1.0.0"

    # Create annotated tag with multi-line message
    git tag -a 1.0.1 -m "Release 1.0.1

    Changelog:
    - Different ways to get product data by ID in magento 2
    - Get Order Information by Order ID & Increment ID"

    # Push tag to GitHub
    git push origin 1.0.1

**When to use**: For all production releases and important milestones.

Option C: Multi-line Tag Message
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Use multiple ``-m`` flags to create structured release notes. Each ``-m`` becomes a separate paragraph.

.. code-block:: bash

    # Create tag with multiple -m options (each becomes a paragraph)
    git tag -a 1.0.2 \
        -m "Release 1.0.2" \
        -m "Changelog:" \
        -m "- Feature: Added new functionality" \
        -m "- Fix: Resolved bug in checkout" \
        -m "- Improvement: Enhanced performance"

    # Push tag
    git push origin 1.0.2

**When to use**: For releases requiring detailed changelogs or release notes.

Complete Release Workflow Example
----------------------------------

Full example workflow from commit to release:

.. code-block:: bash

    # 1. Make sure all changes are committed
    git add .
    git commit -m "feat: add new features for v1.0.0"

    # 2. Push changes to GitHub
    git push origin main

    # 3. Create annotated tag
    git tag -a v1.0.0 -m "Release version 1.0.0" -m "Major features and improvements"

    # 4. Push tag to GitHub
    git push origin v1.0.0

    # 5. GitHub will automatically create a release from the tag
    # Optionally, create release via GitHub web interface with additional notes

Managing Tags
-------------

List Tags
~~~~~~~~~

.. code-block:: bash

    # List all tags
    git tag

    # List tags matching pattern
    git tag -l "v1.0.*"

    # List tags sorted by version
    git tag -l --sort=-v:refname

View Tag Information
~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

    # Show tag information
    git show v1.0.0

    # Show tag message only
    git tag -l -n1 v1.0.0

    # Show all tags with messages
    git tag -l -n

Delete Tags
~~~~~~~~~~~

.. code-block:: bash

    # Delete local tag
    git tag -d v1.0.0

    # Delete remote tag
    git push origin --delete v1.0.0

    # Alternative syntax for deleting remote tag
    git push origin :refs/tags/v1.0.0

Tag Specific Commits
~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

    # Tag a specific commit
    git tag -a v1.0.0 commit-hash -m "Release message"

    # Tag previous commit
    git tag -a v1.0.0 HEAD~1 -m "Release message"

Creating GitHub Releases
-------------------------

After pushing a tag, GitHub automatically creates a release. You can enhance it via the web interface:

1. Go to your GitHub repository
2. Click on "Releases" in the right sidebar
3. Click "Draft a new release"
4. Select the tag you pushed
5. Add release title and description
6. Upload release assets (binaries, archives, etc.)
7. Mark as pre-release if needed
8. Click "Publish release"

API Method
~~~~~~~~~~

You can also create releases using GitHub API:

.. code-block:: bash

    # Create release using GitHub CLI (gh)
    gh release create v1.0.0 --title "Release v1.0.0" --notes "Release notes"

    # Create release with file assets
    gh release create v1.0.0 file1.zip file2.tar.gz --title "Release v1.0.0"

Semantic Versioning
-------------------

Follow semantic versioning (SemVer) for your tags:

Format: ``MAJOR.MINOR.PATCH``

- **MAJOR**: Incompatible API changes
- **MINOR**: Backward-compatible functionality additions
- **PATCH**: Backward-compatible bug fixes

Examples:

.. code-block:: bash

    git tag -a v1.0.0 -m "Initial release"
    git tag -a v1.0.1 -m "Bug fixes"
    git tag -a v1.1.0 -m "New features"
    git tag -a v2.0.0 -m "Breaking changes"

Pre-release Versions
~~~~~~~~~~~~~~~~~~~~

For pre-release versions:

.. code-block:: bash

    # Alpha release
    git tag -a v1.0.0-alpha.1 -m "Pre-release alpha"

    # Beta release
    git tag -a v1.0.0-beta.1 -m "Pre-release beta"

    # Release candidate
    git tag -a v1.0.0-rc.1 -m "Release candidate"

Best Practices
--------------

Tagging Best Practices
~~~~~~~~~~~~~~~~~~~~~~

- **Use semantic versioning**: Follow `v1.0.0`, `v1.0.1`, `v2.0.0` format
- **Use annotated tags**: Annotated tags store more information (author, date, message)
- **Write descriptive messages**: Include changelog or release notes in tag message
- **Tag at release points**: Tag stable, tested code only
- **Push tags explicitly**: Tags are not pushed automatically with commits
- **Signed tags**: Use `-s` flag for signed tags in production environments
- **Tag from main/master**: Create release tags from stable branches

Release Workflow Best Practices
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- **Test before tagging**: Ensure code is tested and stable
- **Update changelog**: Document changes in tag message
- **Create release notes**: Use GitHub release notes feature
- **Tag regularly**: Don't wait too long between releases
- **Use CI/CD**: Automate release process when possible
- **Communicate releases**: Notify team/users about new releases

Common Workflows
----------------

Feature Release Workflow
~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

    # 1. Complete feature development
    git checkout -b feature/new-feature
    git add .
    git commit -m "feat: add new feature"
    git push origin feature/new-feature

    # 2. Merge to main
    git checkout main
    git pull origin main
    git merge feature/new-feature
    git push origin main

    # 3. Create release tag
    git tag -a v1.1.0 -m "Release v1.1.0: New feature"
    git push origin v1.1.0

Hotfix Release Workflow
~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

    # 1. Create hotfix branch
    git checkout -b hotfix/critical-bug main

    # 2. Fix the bug
    git add .
    git commit -m "fix: resolve critical bug"
    git push origin hotfix/critical-bug

    # 3. Merge to main
    git checkout main
    git merge hotfix/critical-bug
    git push origin main

    # 4. Create patch release
    git tag -a v1.0.1 -m "Hotfix v1.0.1: Critical bug fix"
    git push origin v1.0.1

Troubleshooting
---------------

Tag Not Appearing on GitHub
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

    # Verify tag exists locally
    git tag -l

    # Push tag explicitly
    git push origin tag-name

    # Push all tags
    git push --tags

    # Check remote tags
    git ls-remote --tags origin

Cannot Push Tag
~~~~~~~~~~~~~~~

.. code-block:: bash

    # Verify you have push permissions
    git push origin tag-name

    # Check remote configuration
    git remote -v

    # Re-authenticate if needed
    git credential approve

Tag Already Exists
~~~~~~~~~~~~~~~~~~

.. code-block:: bash

    # Delete local tag
    git tag -d v1.0.0

    # Delete remote tag
    git push origin --delete v1.0.0

    # Create tag again
    git tag -a v1.0.0 -m "Release message"
    git push origin v1.0.0

See Also
--------

- :doc:`../git-commands-reference/index` - Complete Git commands reference
- :doc:`../git-project-setup/index` - Project setup using Git
- :doc:`../git-commit-messages/index` - Commit message guide
- `GitHub Releases Documentation <https://docs.github.com/en/repositories/releasing-projects-on-github>`_
- `Semantic Versioning <https://semver.org/>`_


Git Stash Guide
===============

The ``git stash`` command takes your uncommitted changes (both staged and unstaged), saves them away for later use, and then reverts them from your working copy. This is useful when you need to quickly switch context and work on something else without committing half-done work.

.. note::
    **Reference Documentation:**

    - `Atlassian Git Stash Tutorial <https://www.atlassian.com/git/tutorials/saving-changes/git-stash>`_
    - `Git Stash Guide <https://opensource.com/article/21/4/git-stash>`_
    - `Official Documentation <https://docs.google.com/document/d/1LS2irQzU0Qj1vnSR8DUNBduZvoatMVSWpaNCo_jp2Ps/edit>`_

What Gets Stashed?
------------------

By default, running ``git stash`` will stash:

- Changes that have been added to your index (staged changes)
- Changes made to files that are currently tracked by Git (unstaged changes)

But it will **not** stash:

- New files in your working copy that have not yet been staged
- Files that have been ignored

Stashing Changes
----------------

Basic Stash Commands
~~~~~~~~~~~~~~~~~~~~

**Save your current changes**::

    git stash

**Save with a descriptive message**::

    git stash save "your descriptive message"

Stashing Untracked Files
~~~~~~~~~~~~~~~~~~~~~~~~~

To include untracked files in your stash, use the ``-u`` or ``--include-untracked`` option::

    git stash --include-untracked
    # or
    git stash -u

Stashing All Files (Including Ignored)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To stash everything, including ignored files::

    git stash --all
    # or
    git stash -a

Viewing Stashes
---------------

List All Stashes
~~~~~~~~~~~~~~~~

View all stashed changes::

    git stash list

Output example::

    stash@{0}: WIP on master: 5002d47 our new homepage
    stash@{1}: WIP on master: 5002d47 feat: add new feature
    stash@{2}: WIP on master: 5002d47 fix: resolve bug

Show Latest Stash
~~~~~~~~~~~~~~~~~

**View the latest stash summary**::

    git stash show

**View the latest stash with full diff**::

    git stash show -p

**View the latest stash including untracked files**::

    git stash show -u
    # or
    git stash show --include-untracked

**View full diff with untracked files**::

    git stash show -p -u

**View only untracked files in latest stash**::

    git stash show -p --only-untracked

Show Specific Stash
~~~~~~~~~~~~~~~~~~~

Replace ``stash@{1}`` with your desired stash reference:

**View specific stash summary**::

    git stash show stash@{1}

**View specific stash with full diff**::

    git stash show stash@{1} -p

**View specific stash including untracked files**::

    git stash show stash@{1} -u
    # or
    git stash show stash@{1} --include-untracked

**View only untracked files in specific stash**::

    git stash show stash@{1} --only-untracked

Re-applying Stashed Changes
----------------------------

Git Stash Pop
~~~~~~~~~~~~~

Reapply the most recent stash and **remove it** from the stash list::

    git stash pop

.. important::
    ``git stash pop`` removes the changes from your stash and reapplies them to your working copy.

**Pop a specific stash**::

    git stash pop stash@{1}

Git Stash Apply
~~~~~~~~~~~~~~~

Reapply stashed changes but **keep them** in the stash list::

    git stash apply

This is useful when you want to apply the same stashed changes to multiple branches.

**Apply a specific stash**::

    git stash apply stash@{1}

**Apply stash and restore staged state**::

    git stash apply --index

Deleting Stashes
----------------

Drop a Single Stash
~~~~~~~~~~~~~~~~~~~

Remove a specific stash from the stash list::

    git stash drop stash@{2}

**Drop the latest stash**::

    git stash drop

Clear All Stashes
~~~~~~~~~~~~~~~~~

Remove all stashed entries::

    git stash clear

.. warning::
    This action cannot be undone. All stashed changes will be permanently deleted.

Creating a Branch from Stash
-----------------------------

When you want to create a new branch and apply your stashed changes to it:

**Create a branch from the latest stash**::

    git stash branch <branch_name>

**Create a branch from a specific stash**::

    git stash branch <branch_name> stash@{1}

This is particularly useful when:

- You stashed work on the wrong branch
- You need to create a feature branch from stashed changes
- You want to isolate stashed work into its own branch

Advanced Usage
--------------

Stash with Patch Mode
~~~~~~~~~~~~~~~~~~~~~

Interactively select which changes to stash::

    git stash push -p
    # or
    git stash save -p

Stash Specific Files
~~~~~~~~~~~~~~~~~~~~

Stash only specific files::

    git stash push -m "message" path/to/file1 path/to/file2

Stash with Keep Index
~~~~~~~~~~~~~~~~~~~~~~

Stash changes but keep staged files in the index::

    git stash --keep-index

View Stash as Diff
~~~~~~~~~~~~~~~~~~

View the difference between current state and a stash::

    git diff stash@{0}

Common Workflows
----------------

**Scenario 1: Quick Context Switch**::

    # You're working on a feature but need to fix a bug urgently
    git stash save "WIP: feature in progress"
    git checkout -b hotfix/urgent-bug
    # Fix the bug and commit
    git checkout feature-branch
    git stash pop

**Scenario 2: Testing Changes on Different Branches**::

    # You have changes you want to test on multiple branches
    git stash save "experimental changes"
    git checkout branch1
    git stash apply
    # Test changes
    git checkout branch2
    git stash apply
    # Test again
    # When done, clean up
    git stash drop

**Scenario 3: Cleaning Working Directory**::

    # Save all changes including untracked files
    git stash -u
    # Now you have a clean working directory
    # Later restore everything
    git stash pop

Quick Reference Cheat Sheet
----------------------------

Stashing Commands
~~~~~~~~~~~~~~~~~

.. list-table::
   :header-rows: 1
   :widths: 40 60

   * - Command
     - Description
   * - ``git stash``
     - Stash tracked changes
   * - ``git stash save "message"``
     - Stash with descriptive message
   * - ``git stash -u``
     - Stash including untracked files
   * - ``git stash -a``
     - Stash including ignored files
   * - ``git stash push -p``
     - Interactively stash changes

Viewing Commands
~~~~~~~~~~~~~~~~

.. list-table::
   :header-rows: 1
   :widths: 40 60

   * - Command
     - Description
   * - ``git stash list``
     - List all stashes
   * - ``git stash show``
     - Show latest stash summary
   * - ``git stash show -p``
     - Show latest stash with full diff
   * - ``git stash show stash@{1}``
     - Show specific stash
   * - ``git stash show -u``
     - Show with untracked files

Applying Commands
~~~~~~~~~~~~~~~~~

.. list-table::
   :header-rows: 1
   :widths: 40 60

   * - Command
     - Description
   * - ``git stash pop``
     - Apply latest stash and remove it
   * - ``git stash apply``
     - Apply latest stash and keep it
   * - ``git stash apply stash@{1}``
     - Apply specific stash
   * - ``git stash apply --index``
     - Apply and restore staged state

Deleting Commands
~~~~~~~~~~~~~~~~~

.. list-table::
   :header-rows: 1
   :widths: 40 60

   * - Command
     - Description
   * - ``git stash drop``
     - Delete latest stash
   * - ``git stash drop stash@{2}``
     - Delete specific stash
   * - ``git stash clear``
     - Delete all stashes

Branch Commands
~~~~~~~~~~~~~~~

.. list-table::
   :header-rows: 1
   :widths: 40 60

   * - Command
     - Description
   * - ``git stash branch <name>``
     - Create branch from latest stash
   * - ``git stash branch <name> stash@{1}``
     - Create branch from specific stash

Best Practices
--------------

1. **Use Descriptive Messages**: Always use ``git stash save "descriptive message"`` to make it easier to identify stashes later.

2. **Don't Accumulate Stashes**: Clean up old stashes regularly with ``git stash drop`` or ``git stash clear``.

3. **Be Careful with Pop**: Use ``git stash apply`` if you're not sure you want to remove the stash yet.

4. **Stash Before Pulling**: If you have uncommitted changes and need to pull, stash first to avoid conflicts.

5. **Review Before Applying**: Always use ``git stash show -p`` to review changes before applying them.

6. **Use Branches for Long-term Storage**: Stashes are meant for temporary storage. For longer-term work, create a branch instead.

Troubleshooting
---------------

Stash Pop Conflicts
~~~~~~~~~~~~~~~~~~~

If ``git stash pop`` results in conflicts:

1. Resolve the conflicts manually
2. Stage the resolved files: ``git add <file>``
3. The stash will be automatically dropped after resolution

If you want to keep the stash::

    git stash apply
    # Resolve conflicts
    git add <resolved-files>
    # Stash is still available

Lost Stash Recovery
~~~~~~~~~~~~~~~~~~~

If you accidentally dropped a stash, you might be able to recover it using::

    git fsck --unreachable | grep commit | cut -d ' ' -f3 | xargs git log --merges --no-walk

Then inspect the commits to find your lost stash and apply it::

    git stash apply <commit-hash>

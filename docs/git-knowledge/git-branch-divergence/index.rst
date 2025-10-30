Git: Branch Divergence Guide
=============================

Understanding Git branch divergence, how to detect it, resolve it, and prevent it in your daily workflow.

.. contents:: Table of Contents
   :local:
   :depth: 2

Overview
--------

Git branch divergence occurs when your local branch and the remote tracking branch (e.g., ``origin/branch``) point to different commits because they have evolved separately. This is a common scenario in collaborative development and understanding how to handle it is crucial for effective Git workflow.

What is Git Branch Divergence?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Branch divergence happens when:

- Your local branch has commits that are not on the remote branch
- The remote branch has commits that are not on your local branch
- Both branches have unique commits that the other doesn't have

This creates a "fork" in the commit history where the branches have diverged from their common ancestor.

Key Causes of Divergence
-------------------------

Understanding why branches diverge helps prevent and resolve these situations:

1. **Concurrent Development**
   - You made local commits without pushing
   - Someone else pushed new commits to the remote branch
   - This is the most common scenario in team environments

2. **Rebasing or Amending Commits**
   - You rebased or amended commits locally
   - This rewrites commit history
   - Remote branch still has the old commits

3. **Force Pushing**
   - Someone force-pushed to the remote branch
   - This overwrites remote history
   - Your local branch now points to non-existent commits

4. **Incorrect Pull Strategy**
   - Pulled remote changes incorrectly
   - Mixed up branches during merge/rebase
   - Configuration issues with pull behavior

5. **Working on Stale Branch**
   - Started work on an outdated branch
   - Remote branch was updated in the meantime
   - Your commits are based on old history

How Git Shows Divergence
-------------------------

Using git status
~~~~~~~~~~~~~~~~

The simplest way to check divergence:

.. code-block:: bash

    git status

**Output Examples:**

Branches in sync:

.. code-block:: bash

    On branch feature-branch
    Your branch is up to date with 'origin/feature-branch'.

Local ahead:

.. code-block:: bash

    Your branch is ahead of 'origin/feature-branch' by 2 commits.

Local behind:

.. code-block:: bash

    Your branch is behind 'origin/feature-branch' by 3 commits.

Fully diverged:

.. code-block:: bash

    Your branch and 'origin/feature-branch' have diverged,
    and have 2 and 3 different commits each, respectively.

Using git log
~~~~~~~~~~~~~

View branch positions with log commands:

.. code-block:: bash

    git log --oneline --graph --decorate --all

**Output Example:**

.. code-block:: text

    * c67f89a (HEAD -> feature-branch) Local commit 2
    * a12b3c4 Local commit 1
    | * b98d7f6 (origin/feature-branch) Remote commit 2
    | * f34e67d Remote commit 1
    |/
    * 537c1ad Common ancestor commit

Branch Divergence Scenarios
----------------------------

Here's a detailed explanation of how local and remote branches diverge and how to fix each scenario.

1️⃣ When Local and Remote Branches Are in Sync
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: text

    commit 537c1ad (HEAD -> feature-branch, origin/feature-branch)

**Meaning:**

- HEAD points to your local branch ``feature-branch``
- ``origin/feature-branch`` points to the same commit
- Local and remote are perfectly synced
- No action needed

2️⃣ When Local is Ahead of Remote
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Scenario:** You made new commits locally but haven't pushed yet.

.. code-block:: text

    commit a12b3c4 (HEAD -> feature-branch)
    commit 537c1ad (origin/feature-branch)

**Meaning:**

- Your local branch has commits not present in the remote branch
- Running ``git status`` will show:

.. code-block:: bash

    Your branch is ahead of 'origin/feature-branch' by 1 commit.

**🔧 Fix:**

Push changes to sync:

.. code-block:: bash

    git push origin feature-branch

3️⃣ When Local is Behind Remote
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Scenario:** The remote branch has new commits that you haven't pulled.

.. code-block:: text

    commit b98d7f6 (origin/feature-branch)
    commit 537c1ad (HEAD -> feature-branch)

**Meaning:**

- Your local branch is missing commits from remote
- ``git status`` shows:

.. code-block:: bash

    Your branch is behind 'origin/feature-branch' by 1 commit and can be fast-forwarded.

**🔧 Fix:**

Pull updates:

.. code-block:: bash

    git pull origin feature-branch

4️⃣ When Local and Remote Have Diverged
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Scenario:** Both local and remote have unique commits.

.. code-block:: text

    commit c67f89a (HEAD -> feature-branch)
    commit b98d7f6 (origin/feature-branch)

**Meaning:**

- Your local branch has commits remote doesn't
- Remote branch also has commits local doesn't
- ``git status`` shows:

.. code-block:: bash

    Your branch and 'origin/feature-branch' have diverged,
    and have 1 and 1 different commits each, respectively.

**🔧 Fix:**

You need to merge or rebase:

.. code-block:: bash

    git pull --rebase origin feature-branch   # Preferred (linear history)
    # or
    git merge origin/feature-branch           # Merge commit will be created

5️⃣ Detached HEAD (No Branch)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Scenario:** If you checkout a specific commit.

.. code-block:: text

    commit 537c1ad (HEAD detached from origin/main)

**Meaning:**

- You are not on any branch, just on a commit
- Any new commits will not belong to a branch unless you create one

**🔧 Fix:**

Create a new branch to save your work:

.. code-block:: bash

    git checkout -b new-branch

Resolving Branch Divergence
----------------------------

When branches have fully diverged (scenario 4️⃣), you need to choose a resolution strategy:

Strategy 1: Merge (Preserves History)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**When to use:**

- You want to preserve complete history
- Working in a collaborative environment
- Feature branch with shared work

**Command:**

.. code-block:: bash

    git pull origin feature-branch
    # or explicitly
    git fetch origin
    git merge origin/feature-branch

**Pros:**

- Complete history preservation
- Safe for shared branches
- Clear merge points

**Cons:**

- Creates merge commits (can clutter history)
- Non-linear history
- May require conflict resolution

Strategy 2: Rebase (Linear History)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**When to use:**

- You want clean, linear history
- Working on personal feature branch
- Commits haven't been pushed yet

**Command:**

.. code-block:: bash

    git pull --rebase origin feature-branch
    # or explicitly
    git fetch origin
    git rebase origin/feature-branch

**Pros:**

- Clean, linear history
- Easier to read log
- Professional commit history

**Cons:**

- Rewrites commit history
- Not safe for shared branches
- May require conflict resolution at each commit

**Important Warning:**

.. warning::

    Never rebase commits that have been pushed to a shared branch unless you're absolutely sure no one else is working on it. Rewriting shared history causes problems for other developers.

Strategy 3: Force Push (Dangerous)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**When to use:**

- You intentionally rewrote history (rebased)
- Working alone on the branch
- Absolutely sure no one else is using the branch

**Command:**

.. code-block:: bash

    git push --force-with-lease origin feature-branch

**Use ``--force-with-lease`` instead of ``--force``:**

- Safer alternative to ``--force``
- Checks if remote branch has changed
- Prevents overwriting others' work

.. danger::

    Force pushing overwrites remote history. This can:

    - Cause loss of work for other developers
    - Break others' branches
    - Create difficult recovery situations

    Always communicate with your team before force pushing!

Resolving Conflicts
-------------------

When merging or rebasing diverged branches, conflicts may occur.

During Merge
~~~~~~~~~~~~

**Steps:**

1. Start the merge:

   .. code-block:: bash

       git merge origin/feature-branch

2. If conflicts occur, Git will notify you:

   .. code-block:: bash

       CONFLICT (content): Merge conflict in file.txt
       Automatic merge failed; fix conflicts and then commit the result.

3. View conflicted files:

   .. code-block:: bash

       git status

4. Open and resolve conflicts in your editor

5. Mark conflicts as resolved:

   .. code-block:: bash

       git add file.txt

6. Complete the merge:

   .. code-block:: bash

       git commit

During Rebase
~~~~~~~~~~~~~

**Steps:**

1. Start the rebase:

   .. code-block:: bash

       git rebase origin/feature-branch

2. If conflicts occur, resolve them in your editor

3. Stage resolved files:

   .. code-block:: bash

       git add file.txt

4. Continue the rebase:

   .. code-block:: bash

       git rebase --continue

5. Repeat steps 2-4 for each conflicted commit

**Abort if needed:**

.. code-block:: bash

    git rebase --abort

Visualizing Divergence
----------------------

Custom Git Alias
~~~~~~~~~~~~~~~~

Add this alias to your Git configuration for better visualization:

.. code-block:: bash

    git config --global alias.log-diverge "log --graph --oneline --decorate --all --pretty=format:'%C(yellow)%h%Creset %C(red)%d%Creset %s %C(cyan)- %an%Creset %C(green)(%ad)%Creset' --date=format:'%d-%m-%Y %I:%M:%S %p'"

**Alias Breakdown:**

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Option
     - Description
   * - ``--graph``
     - Draws ASCII graph showing branch structure and merges
   * - ``--oneline``
     - One line per commit (compact view)
   * - ``--decorate``
     - Shows branch/tag names (HEAD, origin, etc.)
   * - ``--all``
     - Includes all branches (local + remote)
   * - ``%h``
     - Short commit hash (yellow)
   * - ``%d``
     - Branch/tag info (red)
   * - ``%s``
     - Commit message
   * - ``%an``
     - Author name (cyan)
   * - ``%ad``
     - Date with time (green) formatted as DD-MM-YYYY HH:MM:SS AM/PM

**Usage:**

.. code-block:: bash

    git log-diverge

**Example Output:**

.. code-block:: text

    * c67f89a (HEAD -> feature-branch) Add user authentication - John Doe (30-10-2025 02:30:15 PM)
    | * b98d7f6 (origin/feature-branch) Fix login bug - Jane Smith (30-10-2025 01:15:45 PM)
    | * f34e67d Update dependencies - Jane Smith (30-10-2025 11:20:30 AM)
    |/
    * 537c1ad (origin/main, main) Initial commit - John Doe (29-10-2025 10:00:00 AM)

Preventing Branch Divergence
-----------------------------

Best practices to minimize divergence issues.

Standard Git Workflow
~~~~~~~~~~~~~~~~~~~~~

Follow this workflow to prevent most divergence issues:

1. Update local branch:

   .. code-block:: bash

       git checkout feature-branch
       git pull --rebase origin feature-branch

2. Make changes and commit:

   .. code-block:: bash

       git add .
       git commit -m "feat: add new feature"

3. Update again before pushing:

   .. code-block:: bash

       git pull --rebase origin feature-branch

4. Push to remote:

   .. code-block:: bash

       git push origin feature-branch

Best Practices
~~~~~~~~~~~~~~

**Regular Updates:**

- Fetch regularly: ``git fetch origin``
- Pull before starting work
- Pull before pushing

**Communication:**

- Coordinate with team members
- Communicate before rebasing shared branches
- Use pull requests for code review
- Agree on branching strategy

**Short-Lived Branches:**

- Keep feature branches short-lived
- Merge frequently to main/develop
- Delete branches after merging

Troubleshooting Common Issues
------------------------------

Issue 1: Can't Push Due to Divergence
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Error:**

.. code-block:: bash

    ! [rejected]        feature-branch -> feature-branch (non-fast-forward)
    error: failed to push some refs to 'origin'

**Solution:**

1. Pull with rebase:

   .. code-block:: bash

       git pull --rebase origin feature-branch

2. Resolve any conflicts

3. Push again:

   .. code-block:: bash

       git push origin feature-branch

Issue 2: Accidentally Worked on Wrong Branch
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Solution:**

1. Stash your changes:

   .. code-block:: bash

       git stash

2. Switch to correct branch:

   .. code-block:: bash

       git checkout correct-branch

3. Apply stashed changes:

   .. code-block:: bash

       git stash pop

Issue 3: Merge Conflicts Too Complex
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Solution:**

1. Abort current operation:

   .. code-block:: bash

       git merge --abort
       # or
       git rebase --abort

2. Consider alternative strategy:

   .. code-block:: bash

       # If you were merging, try rebasing
       git rebase origin/feature-branch

       # If you were rebasing, try merging
       git merge origin/feature-branch

Issue 4: Lost Commits After Rebase
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Solution:**

1. Find lost commits using reflog:

   .. code-block:: bash

       git reflog

2. Reset to previous state:

   .. code-block:: bash

       git reset --hard HEAD@{n}

   Replace ``n`` with the number from reflog where your branch was before the rebase.

Configuration Tips
------------------

Configure Pull Behavior
~~~~~~~~~~~~~~~~~~~~~~~

Set default pull strategy:

.. code-block:: bash

    # Use rebase by default
    git config --global pull.rebase true

    # Or preserve merges during rebase
    git config --global pull.rebase merges

Configure Push Behavior
~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

    # Push only current branch
    git config --global push.default current

    # Refuse to push if would create divergence
    git config --global push.default simple

Summary
-------

Key Takeaways
~~~~~~~~~~~~~

1. Branch divergence is normal in collaborative development
2. Regular fetching and pulling prevents most divergence issues
3. Choose merge vs rebase based on your workflow and team preferences
4. Communication is crucial when dealing with shared branches
5. Use visualization tools to understand branch relationships

Quick Reference Commands
~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

    # Check divergence
    git status
    git fetch origin
    git log --oneline --graph --all

    # Resolve divergence (merge)
    git pull origin branch-name

    # Resolve divergence (rebase)
    git pull --rebase origin branch-name

    # Visualize divergence
    git log-diverge

    # Safe force push
    git push --force-with-lease origin branch-name

    # Abort operations
    git merge --abort
    git rebase --abort

See Also
--------

- :doc:`../git-commands-reference/index` - Git commands reference
- :doc:`../git-commit-messages/index` - Git commit messages guide
- :doc:`../git-stash/index` - Git stash guide
- :doc:`../git-branch-name/index` - Git branch naming conventions
- `Git Documentation - Branches <https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell>`_
- `Git Documentation - Rebasing <https://git-scm.com/book/en/v2/Git-Branching-Rebasing>`_

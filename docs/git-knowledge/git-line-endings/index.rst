Git: Fix Line Ending Issues (CRLF/LF)
======================================

This guide helps you resolve Git issues when a single file shows "entire file modified" due to line ending differences between CRLF (Windows) and LF (Unix/Linux).

Understanding the Problem
--------------------------

When Git shows that every line in a file has changed, but you only made minor edits, the issue is usually caused by line ending differences:

- **CRLF** (Carriage Return + Line Feed): Windows line endings (``\r\n``)
- **LF** (Line Feed): Unix/Linux/Mac line endings (``\n``)

**The Problem**: Your repository copy uses CRLF, but your edited copy uses LF (or vice versa). Git interprets this as every line being modified.

Detect Line Ending Issues
--------------------------

Check What Git Sees
~~~~~~~~~~~~~~~~~~~

Use the following command to check line endings for a specific file:

.. code-block:: bash

    git ls-files --eol -- path/to/your/file.js

**Understanding the Output:**

- ``i/crlf`` = File in the index (repository) has CRLF
- ``i/lf`` = File in the index (repository) has LF
- ``w/crlf`` = File in working tree (your local copy) has CRLF
- ``w/lf`` = File in working tree (your local copy) has LF

**Example**: ``i/crlf w/lf`` means the repository has CRLF, but your local file has LF.

Verify Line Endings in Files
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Compare the committed file with your working tree file:

.. code-block:: bash

    # Navigate to your project root
    cd /var/www/html/your-project/

    # Show committed file (check for \r which indicates CRLF)
    git show HEAD:path/to/file.js | sed -n l | head

    # Show working tree file (no \r means LF)
    sed -n l path/to/file.js | head

.. note::
    If you see ``\r$`` at the end of lines in the output, the file uses CRLF. If you only see ``$``, it uses LF.

Fix Line Ending Issues
-----------------------

Choose the appropriate fix based on what line endings your repository uses.

Option 1: Convert Local File to CRLF
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If the repository uses CRLF and you want to convert your edited file to CRLF:

.. code-block:: bash

    # Normalize to CRLF safely (keeps your code edits)
    perl -i -pe 's/\r?\n/\r\n/g' path/to/file.js

This command:

- Preserves your code changes
- Only changes line endings to CRLF
- Works even if some lines already have CRLF

Option 2: Convert Local File to LF
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If the repository uses LF and your file has CRLF:

.. code-block:: bash

    # Normalize to LF
    perl -i -pe 's/\r\n/\n/g' path/to/file.phtml

This command:

- Removes carriage returns (``\r``)
- Converts CRLF to LF
- Preserves your actual code changes

Verify the Fix
~~~~~~~~~~~~~~

After applying the fix, verify that the line endings are now correct:

.. code-block:: bash

    # Check line endings again
    git ls-files --eol -- path/to/file.js

    # Check the diff (should now only show your real edits)
    git diff -- path/to/file.js

The diff should now only display your actual code changes, not every line as modified.

Prevent Future Issues
---------------------

Use .gitattributes
~~~~~~~~~~~~~~~~~~

Create a ``.gitattributes`` file in your repository root to enforce consistent line endings:

.. code-block:: text
    :caption: .gitattributes

    # Auto detect text files and normalize to LF
    * text=auto

    # Force LF for these file types
    *.js text eol=lf
    *.php text eol=lf
    *.css text eol=lf
    *.html text eol=lf
    *.xml text eol=lf
    *.json text eol=lf
    *.md text eol=lf
    *.sh text eol=lf

    # Force CRLF for Windows scripts
    *.bat text eol=crlf
    *.cmd text eol=crlf

Configure Git Settings
~~~~~~~~~~~~~~~~~~~~~~

Set Git to handle line endings automatically:

.. code-block:: bash

    # Linux/Mac - Convert CRLF to LF on commit
    git config --global core.autocrlf input

    # Windows - Convert LF to CRLF on checkout, LF on commit
    git config --global core.autocrlf true

Real-World Examples
-------------------

Here are complete examples using actual files from a Magento 2 project, showing when and how to convert line endings.

When to Convert: Decision Guide
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Convert to CRLF when**:
- Your repository uses CRLF (``i/crlf``) and your local file has LF (``w/lf``)
- You're matching the existing repository standard (usually legacy Windows projects)

**Convert to LF when**:
- Your repository uses LF (``i/lf``) and your local file has CRLF (``w/crlf``)
- You're following modern development standards (recommended for most projects)

.. important::
    **Best Practice**: Always match your local file to the repository's line ending format, not the other way around. This ensures consistency across the team.

Example 1: Converting Local File to CRLF
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Scenario**: Repository uses CRLF, but your local file was saved with LF.

**Project root**: ``/var/www/html/ci244p2/``

**File**: ``app/code/Cellularisrael/Order/view/adminhtml/web/js/order/view/post-wrapper.js``

**Step 1: Detect the Issue**

.. code-block:: bash

    git ls-files --eol -- /var/www/html/ci244p2/app/code/Cellularisrael/Order/view/adminhtml/web/js/order/view/post-wrapper.js

**Output**: ``i/crlf w/lf`` → Repository has CRLF, your local file has LF

**Step 2: Verify Line Endings**

Navigate to your Magento root and check both versions:

.. code-block:: bash

    # Go to Magento root
    cd /var/www/html/ci244p2/

    # Show committed file (\r at end means CRLF in repo)
    git show HEAD:app/code/Cellularisrael/Order/view/adminhtml/web/js/order/view/post-wrapper.js | sed -n l | head

    # Show working tree (\r missing means LF locally)
    sed -n l /var/www/html/ci244p2/app/code/Cellularisrael/Order/view/adminhtml/web/js/order/view/post-wrapper.js | head

**Expected output**:

- Committed file: Lines ending with ``\r$`` (CRLF)
- Working tree: Lines ending with ``$`` only (LF)

**Step 3: Convert Local File to CRLF**

Since the repository uses CRLF, convert your local file to match:

.. code-block:: bash

    # Normalize to CRLF safely (keeps your code edits, only changes line endings)
    perl -i -pe 's/\r?\n/\r\n/g' \
      /var/www/html/ci244p2/app/code/Cellularisrael/Order/view/adminhtml/web/js/order/view/post-wrapper.js

.. note::
    The ``\r?\n`` pattern works even if some lines already have CRLF, preventing double conversion.

**Step 4: Verify the Fix**

.. code-block:: bash

    # Check line endings again (should now show i/crlf w/crlf)
    git ls-files --eol -- /var/www/html/ci244p2/app/code/Cellularisrael/Order/view/adminhtml/web/js/order/view/post-wrapper.js

    # Check the diff (should now only show your real edits, not every line)
    git diff -- /var/www/html/ci244p2/app/code/Cellularisrael/Order/view/adminhtml/web/js/order/view/post-wrapper.js

**Result**: The diff now shows only your actual code changes, not the entire file as modified.

Example 2: Converting Local File to LF
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Scenario**: Repository uses LF, but your local file was saved with CRLF (common when editing on Windows).

**Project root**: ``/var/www/html/ci244p2/``

**File**: ``app/code/Cellularisrael/Order/view/adminhtml/templates/order/status/hold_popup.phtml``

**Step 1: Detect the Issue**

.. code-block:: bash

    git ls-files --eol -- /var/www/html/ci244p2/app/code/Cellularisrael/Order/view/adminhtml/templates/order/status/hold_popup.phtml

**Output**: ``i/lf w/crlf`` → Repository has LF, your local file has CRLF

**Step 2: Verify Line Endings**

.. code-block:: bash

    # Go to Magento root
    cd /var/www/html/ci244p2/

    # Show committed file (no \r means LF in repo)
    git show HEAD:app/code/Cellularisrael/Order/view/adminhtml/templates/order/status/hold_popup.phtml | sed -n l | head

    # Show working tree (\r present means CRLF locally)
    sed -n l /var/www/html/ci244p2/app/code/Cellularisrael/Order/view/adminhtml/templates/order/status/hold_popup.phtml | head

**Expected output**:

- Committed file: Lines ending with ``$`` only (LF)
- Working tree: Lines ending with ``\r$`` (CRLF)

**Step 3: Convert Local File to LF**

Since the repository uses LF (modern standard), convert your local file to match:

.. code-block:: bash

    # Normalize to LF (removes \r, converts CRLF to LF)
    perl -i -pe 's/\r\n/\n/g' \
      /var/www/html/ci244p2/app/code/Cellularisrael/Order/view/adminhtml/templates/order/status/hold_popup.phtml

.. note::
    This is the recommended conversion for most modern projects. LF is the standard for web development.

**Step 4: Verify the Fix**

.. code-block:: bash

    # Check line endings again (should now show i/lf w/lf)
    git ls-files --eol -- /var/www/html/ci244p2/app/code/Cellularisrael/Order/view/adminhtml/templates/order/status/hold_popup.phtml

    # Check the diff (should now only show your real edits)
    git diff -- /var/www/html/ci244p2/app/code/Cellularisrael/Order/view/adminhtml/templates/order/status/hold_popup.phtml

**Result**: The diff now shows only your actual code changes.

Quick Reference
~~~~~~~~~~~~~~~

+-----------------+------------------+---------------------------+
| Repository Uses | Your Local File  | Command to Use            |
+=================+==================+===========================+
| CRLF (i/crlf)   | LF (w/lf)        | Convert to CRLF           |
|                 |                  | ``perl -i -pe             |
|                 |                  | 's/\r?\n/\r\n/g' file``   |
+-----------------+------------------+---------------------------+
| LF (i/lf)       | CRLF (w/crlf)    | Convert to LF             |
|                 |                  | ``perl -i -pe             |
|                 |                  | 's/\r\n/\n/g' file``      |
+-----------------+------------------+---------------------------+

.. tip::
    **Remember**: Always convert your local file to match the repository, not the other way around. This maintains consistency across the entire project and team.

Common Scenarios
----------------

Scenario 1: Cloned Repository on Different OS
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Problem**: You cloned a Windows repository on Linux (or vice versa).

**Solution**:

1. Check if the repository has a ``.gitattributes`` file
2. If not, create one (see above)
3. Normalize the repository:

   .. code-block:: bash

       git add --renormalize .
       git commit -m "Normalize line endings"

Scenario 2: Multiple Developers on Different OS
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Problem**: Team members use different operating systems.

**Solution**:

1. Add a ``.gitattributes`` file to the repository
2. Have all team members run:

   .. code-block:: bash

       git rm --cached -r .
       git reset --hard

3. Configure Git settings consistently across the team

Best Practices
--------------

- **Use .gitattributes**: Always define line ending rules in your repository
- **Be Consistent**: Choose one line ending style for your project (usually LF)
- **Configure Git**: Set ``core.autocrlf`` appropriately for your OS
- **Editor Settings**: Configure your code editor to use the correct line endings
- **Pre-commit Hooks**: Consider using pre-commit hooks to enforce line endings

.. tip::
    Modern development typically uses LF (Unix-style) line endings for all text files, regardless of the operating system. This is the recommended standard for most projects.

Troubleshooting
---------------

Issue: Normalization Doesn't Work
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If ``git add --renormalize .`` doesn't fix the issue:

.. code-block:: bash

    # Remove all files from Git index
    git rm --cached -r .

    # Re-add all files (Git will apply .gitattributes rules)
    git add .

    # Check what changed
    git diff --cached

Issue: Files Keep Showing as Modified
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Check your Git configuration:

   .. code-block:: bash

       git config --list | grep autocrlf

2. Ensure ``.gitattributes`` is properly configured
3. Try refreshing the index:

   .. code-block:: bash

       git add --renormalize .

References
----------

- **Git Documentation**: https://git-scm.com/docs/gitattributes
- **GitHub Line Endings Guide**: https://docs.github.com/en/get-started/getting-started-with-git/configuring-git-to-handle-line-endings

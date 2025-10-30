Linux: Nano Text Editor Guide
=============================

Nano is a simple, user-friendly command-line text editor for Unix and Linux systems. This guide covers installation, shortcuts, and advanced usage.

.. contents:: Table of Contents
   :local:
   :depth: 2

Introduction
------------

Nano is a lightweight text editor that runs in the terminal, making it ideal for:

- Quick file editing on servers
- Editing configuration files
- Working in environments without a GUI
- Beginners who find vi/vim too complex

**Key Features:**

- Easy to use with on-screen help
- Syntax highlighting for many languages
- Search and replace functionality
- Multiple file buffers
- Undo/redo support

**Official Reference:** `Nano Editor Cheatsheet <https://www.nano-editor.org/dist/latest/cheatsheet.html>`_

Installation
------------

Install on Debian/Ubuntu
~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

    sudo apt-get update
    sudo apt-get install nano

Install on RHEL/CentOS/Fedora
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

    sudo yum install nano
    # or on newer versions
    sudo dnf install nano

Verify Installation
~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

    nano --version

Basic Usage
-----------

Opening Files
~~~~~~~~~~~~~

.. code-block:: bash

    # Open a file
    nano filename.txt

    # Create a new file
    nano newfile.txt

    # Open file at specific line
    nano +10 filename.txt

    # Open file in read-only mode
    nano -v filename.txt

Understanding the Interface
~~~~~~~~~~~~~~~~~~~~~~~~~~~

When you open nano, you'll see:

- **Top line:** Nano version and filename
- **Main area:** File content (editable)
- **Bottom two lines:** Available shortcuts (help menu)

The ``^`` symbol represents the ``Ctrl`` key, and ``M-`` represents the ``Alt`` key.

Keyboard Shortcuts Reference
-----------------------------

File Handling
~~~~~~~~~~~~~

.. list-table::
   :header-rows: 1
   :widths: 20 80

   * - Shortcut
     - Description
   * - ``Ctrl+S``
     - Save current file
   * - ``Ctrl+O``
     - Offer to write file ("Save as")
   * - ``Ctrl+R``
     - Insert a file into current one
   * - ``Ctrl+X``
     - Close buffer, exit from nano

Editing Operations
~~~~~~~~~~~~~~~~~~

.. list-table::
   :header-rows: 1
   :widths: 20 80

   * - Shortcut
     - Description
   * - ``Ctrl+K``
     - Cut current line into cutbuffer
   * - ``Alt+6``
     - Copy current line into cutbuffer
   * - ``Ctrl+U``
     - Paste contents of cutbuffer
   * - ``Alt+T``
     - Cut until end of buffer
   * - ``Ctrl+]``
     - Complete current word (auto-complete)
   * - ``Alt+3``
     - Comment/uncomment line or region
   * - ``Alt+U``
     - Undo last action
   * - ``Alt+E``
     - Redo last undone action

Search and Replace
~~~~~~~~~~~~~~~~~~

.. list-table::
   :header-rows: 1
   :widths: 20 80

   * - Shortcut
     - Description
   * - ``Ctrl+W``
     - Start forward search
   * - ``Ctrl+Q``
     - Start backward search
   * - ``Alt+W``
     - Find next occurrence forward
   * - ``Alt+Q``
     - Find next occurrence backward
   * - ``Alt+R``
     - Start a replacing session (search and replace)

Deletion
~~~~~~~~

.. list-table::
   :header-rows: 1
   :widths: 20 80

   * - Shortcut
     - Description
   * - ``Ctrl+H``
     - Delete character before cursor (Backspace)
   * - ``Ctrl+D``
     - Delete character under cursor
   * - ``Alt+Backspace``
     - Delete word to the left
   * - ``Ctrl+Delete``
     - Delete word to the right
   * - ``Alt+Delete``
     - Delete current line

Navigation
~~~~~~~~~~

**Character and Line Movement:**

.. list-table::
   :header-rows: 1
   :widths: 20 80

   * - Shortcut
     - Description
   * - ``Ctrl+B``
     - One character backward
   * - ``Ctrl+F``
     - One character forward
   * - ``Ctrl+←``
     - One word backward
   * - ``Ctrl+→``
     - One word forward
   * - ``Ctrl+A``
     - To start of line
   * - ``Ctrl+E``
     - To end of line
   * - ``Ctrl+P``
     - One line up
   * - ``Ctrl+N``
     - One line down

**Page and Block Movement:**

.. list-table::
   :header-rows: 1
   :widths: 20 80

   * - Shortcut
     - Description
   * - ``Ctrl+Y``
     - One page up
   * - ``Ctrl+V``
     - One page down
   * - ``Ctrl+↑``
     - To previous block
   * - ``Ctrl+↓``
     - To next block
   * - ``Alt+/``
     - To end of buffer

**Special Navigation:**

.. list-table::
   :header-rows: 1
   :widths: 20 80

   * - Shortcut
     - Description
   * - ``Alt+G``
     - Go to specified line number
   * - ``Alt+]``
     - Go to complementary bracket
   * - ``Alt+↑``
     - Scroll viewport up (without moving cursor)
   * - ``Alt+↓``
     - Scroll viewport down (without moving cursor)
   * - ``Alt+<``
     - Switch to preceding buffer
   * - ``Alt+>``
     - Switch to succeeding buffer

Advanced Operations
~~~~~~~~~~~~~~~~~~~

.. list-table::
   :header-rows: 1
   :widths: 20 80

   * - Shortcut
     - Description
   * - ``Ctrl+T``
     - Execute some command (spell checker, etc.)
   * - ``Ctrl+J``
     - Justify paragraph or region
   * - ``Alt+J``
     - Justify entire buffer
   * - ``Alt+B``
     - Run a syntax check
   * - ``Alt+F``
     - Run a formatter/fixer/arranger
   * - ``Alt+:``
     - Start/stop recording of macro
   * - ``Alt+;``
     - Replay macro

Information and Help
~~~~~~~~~~~~~~~~~~~~

.. list-table::
   :header-rows: 1
   :widths: 20 80

   * - Shortcut
     - Description
   * - ``Ctrl+C``
     - Report cursor position
   * - ``Alt+D``
     - Report line/word/character count
   * - ``Ctrl+G``
     - Display help text

View and Display Options
~~~~~~~~~~~~~~~~~~~~~~~~~

.. list-table::
   :header-rows: 1
   :widths: 20 80

   * - Shortcut
     - Description
   * - ``Alt+A``
     - Turn the mark on/off (for selecting text)
   * - ``Tab``
     - Indent marked region
   * - ``Shift+Tab``
     - Unindent marked region
   * - ``Alt+V``
     - Enter next keystroke verbatim
   * - ``Alt+N``
     - Turn line numbers on/off
   * - ``Alt+P``
     - Turn visible whitespace on/off
   * - ``Alt+X``
     - Hide or unhide the help lines
   * - ``Ctrl+L``
     - Refresh the screen

Common Tasks
------------

How to Save and Exit
~~~~~~~~~~~~~~~~~~~~

**Save and continue editing:**

1. Press ``Ctrl+S`` or ``Ctrl+O``
2. Confirm filename (press Enter)

**Save and exit:**

1. Press ``Ctrl+X``
2. Press ``Y`` when asked to save
3. Confirm filename (press Enter)

**Exit without saving:**

1. Press ``Ctrl+X``
2. Press ``N`` when asked to save

How to Cut, Copy, and Paste
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Cut a line:**

1. Position cursor on the line
2. Press ``Ctrl+K``

**Copy a line:**

1. Position cursor on the line
2. Press ``Alt+6``

**Paste:**

1. Move cursor to desired location
2. Press ``Ctrl+U``

**Cut/Copy multiple lines:**

1. Move cursor to start of selection
2. Press ``Alt+A`` to set mark
3. Move cursor to end of selection
4. Press ``Ctrl+K`` to cut or ``Alt+6`` to copy

How to Search and Replace
~~~~~~~~~~~~~~~~~~~~~~~~~~

**Search:**

1. Press ``Ctrl+W``
2. Type search term
3. Press Enter
4. Press ``Alt+W`` to find next occurrence

**Search and replace:**

1. Press ``Alt+R``
2. Enter search term, press Enter
3. Enter replacement term, press Enter
4. Press ``Y`` to replace, ``N`` to skip, or ``A`` to replace all

How to Go to a Specific Line
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Press ``Alt+G``
2. Enter line number
3. Press Enter

Configuration
-------------

Nano Configuration File
~~~~~~~~~~~~~~~~~~~~~~~~

Nano can be customized using a configuration file located at:

- System-wide: ``/etc/nanorc``
- User-specific: ``~/.nanorc``

Creating Custom Configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Create or edit your personal configuration file:

.. code-block:: bash

    nano ~/.nanorc

**Common configuration options:**

.. code-block:: text

    # Enable syntax highlighting
    include /usr/share/nano/*.nanorc

    # Show line numbers
    set linenumbers

    # Enable mouse support
    set mouse

    # Auto-indent new lines
    set autoindent

    # Convert tabs to spaces
    set tabstospaces

    # Set tab size to 4 spaces
    set tabsize 4

    # Enable soft wrapping
    set softwrap

    # Backup files
    set backup
    set backupdir "~/.nano/backups"

    # Smooth scrolling
    set smooth

Useful Command-Line Options
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

    # Open with line numbers
    nano -l filename.txt

    # Open with mouse support
    nano -m filename.txt

    # Open with auto-indent
    nano -i filename.txt

    # Open in read-only mode
    nano -v filename.txt

    # Create backup of original file
    nano -B filename.txt

    # Set tab width to 4
    nano -T 4 filename.txt

Tips and Best Practices
------------------------

Essential Tips
~~~~~~~~~~~~~~

1. **Always use Ctrl+X to exit** - This ensures you're prompted to save changes
2. **Enable line numbers** - Helps with debugging and referencing code (``Alt+N``)
3. **Use search instead of scrolling** - Faster for large files (``Ctrl+W``)
4. **Master undo/redo** - ``Alt+U`` and ``Alt+E`` can save you from mistakes
5. **Use marks for selecting** - ``Alt+A`` to start selecting, then navigate to select text

Syntax Highlighting
~~~~~~~~~~~~~~~~~~~

Nano automatically detects file types and applies syntax highlighting. To manually set syntax:

.. code-block:: bash

    # View available syntax definitions
    ls /usr/share/nano/

    # Open with specific syntax
    nano -Y python script.txt

Working with Multiple Files
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

    # Open multiple files
    nano file1.txt file2.txt file3.txt

    # Switch between buffers
    # Use Alt+< (previous) and Alt+> (next)

Troubleshooting
---------------

Common Issues
~~~~~~~~~~~~~

**Nano not found:**

.. code-block:: bash

    # Install nano
    sudo apt-get install nano  # Debian/Ubuntu
    sudo yum install nano      # RHEL/CentOS

**Shortcuts not working:**

- Check if your terminal emulator is capturing the key combinations
- Try using the ``Esc`` key instead of ``Alt`` (e.g., ``Esc`` then ``U`` instead of ``Alt+U``)

**No syntax highlighting:**

.. code-block:: bash

    # Install syntax highlighting files
    sudo apt-get install nano-syntax-highlighting

    # Add to ~/.nanorc
    include /usr/share/nano/*.nanorc

**Can't save file (Permission denied):**

.. code-block:: bash

    # Edit file with sudo
    sudo nano /path/to/protected/file

Conclusion
----------

Nano is an excellent text editor for beginners and experienced users who need a straightforward, efficient editing experience in the terminal. With this guide, you should be able to:

- Navigate and edit files efficiently
- Use advanced features like search/replace and macros
- Customize nano to fit your workflow
- Troubleshoot common issues

**Additional Resources:**

- `Official Nano Documentation <https://www.nano-editor.org/docs.php>`_
- `Nano FAQ <https://www.nano-editor.org/dist/latest/faq.html>`_
- `Nano Cheatsheet <https://www.nano-editor.org/dist/latest/cheatsheet.html>`_
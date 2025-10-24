Linux Commands Reference Guide
===============================

This comprehensive guide covers essential Linux commands with their options and practical examples for everyday system administration and development tasks.

.. contents:: Table of Contents

File System Navigation
----------------------

pwd (Print Working Directory)
------------------------------

Displays the current working directory path.

**Syntax**::

    pwd [OPTIONS]

**Common Options**:

* ``-L`` - Print the logical path (follows symbolic links)
* ``-P`` - Print the physical path (resolves symbolic links)

**Examples**::

    # Show current directory
    pwd

    # Show physical path (without symlinks)
    pwd -P

ls (List Directory Contents)
-----------------------------

Lists files and directories in the specified location.

**Syntax**::

    ls [OPTIONS] [FILE/DIRECTORY]

**Common Options**:

* ``-a`` - Show all files including hidden files (starting with .)
* ``-l`` - Long format with detailed information
* ``-h`` - Human-readable file sizes (with -l)
* ``-t`` - Sort by modification time, newest first
* ``-r`` - Reverse order
* ``-R`` - Recursive listing of subdirectories
* ``-S`` - Sort by file size, largest first
* ``-d`` - List directories themselves, not their contents
* ``-i`` - Print inode number of each file
* ``-1`` - List one file per line

**Examples**::

    # Basic listing
    ls

    # List all files including hidden
    ls -a

    # Long format with human-readable sizes
    ls -lh

    # Sort by modification time
    ls -lt

    # List files recursively
    ls -R

    # List only directories
    ls -d */

    # Combination: detailed, all files, human-readable
    ls -lah

    # Sort by size, largest first
    ls -lhS

cd (Change Directory)
---------------------

Changes the current working directory.

**Syntax**::

    cd [DIRECTORY]

**Special Paths**:

* ``~`` - Home directory
* ``-`` - Previous directory
* ``..`` - Parent directory
* ``.`` - Current directory
* ``/`` - Root directory

**Examples**::

    # Go to home directory
    cd
    cd ~

    # Go to specific directory
    cd /var/www/html

    # Go to parent directory
    cd ..

    # Go back to previous directory
    cd -

    # Go up two levels
    cd ../..

    # Relative path
    cd documents/work

tree
----

Displays directory structure in a tree format.

**Syntax**::

    tree [OPTIONS] [DIRECTORY]

**Common Options**:

* ``-a`` - Show all files including hidden
* ``-d`` - List directories only
* ``-L [level]`` - Maximum display depth
* ``-h`` - Print file sizes in human-readable format
* ``-p`` - Print file permissions
* ``-u`` - Print file owner/group

**Examples**::

    # Show tree of current directory
    tree

    # Show only 2 levels deep
    tree -L 2

    # Show directories only
    tree -d

    # Show with file sizes and permissions
    tree -hp

.. note::
   If tree is not installed, install it using: ``sudo apt-get install tree``

File Operations
---------------

cp (Copy)
---------

Copies files and directories.

**Syntax**::

    cp [OPTIONS] SOURCE DESTINATION

**Common Options**:

* ``-r`` or ``-R`` - Copy directories recursively
* ``-i`` - Interactive mode (prompt before overwrite)
* ``-v`` - Verbose mode
* ``-u`` - Copy only when source is newer
* ``-p`` - Preserve file attributes
* ``-a`` - Archive mode (preserve all attributes)
* ``-n`` - No overwrite

**Examples**::

    # Copy file
    cp file.txt backup.txt

    # Copy directory recursively
    cp -r /source/dir /destination/dir

    # Copy with confirmation
    cp -i file.txt backup.txt

    # Copy preserving attributes
    cp -p file.txt backup.txt

    # Copy multiple files to directory
    cp file1.txt file2.txt file3.txt /destination/

    # Archive mode (preserve everything)
    cp -a /source/ /backup/

mv (Move)
---------

Moves or renames files and directories.

**Syntax**::

    mv [OPTIONS] SOURCE DESTINATION

**Common Options**:

* ``-i`` - Interactive mode (prompt before overwrite)
* ``-v`` - Verbose mode
* ``-u`` - Move only when source is newer
* ``-n`` - No overwrite
* ``-f`` - Force overwrite

**Examples**::

    # Rename file
    mv oldname.txt newname.txt

    # Move file to directory
    mv file.txt /destination/

    # Move multiple files
    mv file1.txt file2.txt /destination/

    # Move with confirmation
    mv -i file.txt /destination/

    # Rename directory
    mv old_directory new_directory

rm (Remove)
-----------

Removes files and directories.

**Syntax**::

    rm [OPTIONS] FILE/DIRECTORY

**Common Options**:

* ``-r`` or ``-R`` - Remove directories recursively
* ``-i`` - Interactive mode (prompt before removal)
* ``-f`` - Force removal without prompts
* ``-v`` - Verbose mode
* ``-d`` - Remove empty directories

**Examples**::

    # Remove file
    rm file.txt

    # Remove directory recursively
    rm -r directory/

    # Remove with confirmation
    rm -i file.txt

    # Force remove without confirmation
    rm -f file.txt

    # Remove multiple files
    rm file1.txt file2.txt file3.txt

    # Remove all .log files
    rm *.log

.. warning::
   Use ``rm -rf`` with extreme caution. This will permanently delete files without confirmation.

mkdir (Make Directory)
----------------------

Creates new directories.

**Syntax**::

    mkdir [OPTIONS] DIRECTORY

**Common Options**:

* ``-p`` - Create parent directories as needed
* ``-v`` - Verbose mode
* ``-m`` - Set permissions

**Examples**::

    # Create single directory
    mkdir new_folder

    # Create nested directories
    mkdir -p path/to/new/folder

    # Create with specific permissions
    mkdir -m 755 new_folder

    # Create multiple directories
    mkdir folder1 folder2 folder3

touch
-----

Creates empty files or updates file timestamps.

**Syntax**::

    touch [OPTIONS] FILE

**Common Options**:

* ``-a`` - Change access time only
* ``-m`` - Change modification time only
* ``-c`` - Do not create file if it doesn't exist
* ``-t`` - Use specified time instead of current

**Examples**::

    # Create empty file
    touch newfile.txt

    # Create multiple files
    touch file1.txt file2.txt file3.txt

    # Update timestamp
    touch existing_file.txt

    # Create file with specific time
    touch -t 202301011200 file.txt

File Viewing and Editing
------------------------

cat (Concatenate)
-----------------

Displays file contents, concatenates files, and creates files.

**Syntax**::

    cat [OPTIONS] [FILE]

**Common Options**:

* ``-n`` - Number all output lines
* ``-b`` - Number non-empty lines
* ``-s`` - Squeeze multiple blank lines
* ``-A`` - Show all characters including non-printing
* ``-E`` - Display $ at end of each line
* ``-T`` - Display tabs as ^I

**Examples**::

    # Display file contents
    cat file.txt

    # Display multiple files
    cat file1.txt file2.txt

    # Display with line numbers
    cat -n file.txt

    # Concatenate files into new file
    cat file1.txt file2.txt > combined.txt

    # Append to file
    cat file1.txt >> existing.txt

    # Create new file (Ctrl+D to save)
    cat > newfile.txt

    # Show non-printing characters
    cat -A file.txt

less
----

Views file contents one page at a time with backward navigation.

**Syntax**::

    less [OPTIONS] FILE

**Common Options**:

* ``-N`` - Show line numbers
* ``-S`` - Chop long lines
* ``-i`` - Case-insensitive search
* ``-X`` - Don't clear screen on exit
* ``-F`` - Quit if entire file fits on screen

**Navigation Keys**:

* ``Space`` or ``f`` - Forward one page
* ``b`` - Backward one page
* ``d`` - Forward half page
* ``u`` - Backward half page
* ``g`` - Go to start of file
* ``G`` - Go to end of file
* ``/pattern`` - Search forward
* ``?pattern`` - Search backward
* ``n`` - Next search match
* ``N`` - Previous search match
* ``q`` - Quit

**Examples**::

    # View file
    less file.txt

    # View with line numbers
    less -N file.txt

    # View without line wrapping
    less -S file.txt

    # Case-insensitive search
    less -i file.txt

    # View command output
    ls -la | less

head
----

Displays the first part of files.

**Syntax**::

    head [OPTIONS] [FILE]

**Common Options**:

* ``-n [NUM]`` - Print first NUM lines (default 10)
* ``-c [NUM]`` - Print first NUM bytes
* ``-q`` - Quiet mode (no headers)
* ``-v`` - Verbose mode (always show headers)

**Examples**::

    # Show first 10 lines (default)
    head file.txt

    # Show first 20 lines
    head -n 20 file.txt

    # Short form
    head -20 file.txt

    # Show first 100 bytes
    head -c 100 file.txt

    # Multiple files
    head -n 5 file1.txt file2.txt

    # View first lines of command output
    ls -la | head -5

tail
----

Displays the last part of files.

**Syntax**::

    tail [OPTIONS] [FILE]

**Common Options**:

* ``-n [NUM]`` - Print last NUM lines (default 10)
* ``-c [NUM]`` - Print last NUM bytes
* ``-f`` - Follow file (monitor for changes)
* ``-F`` - Follow file with retry
* ``-q`` - Quiet mode (no headers)
* ``--pid=[PID]`` - With -f, terminate after process PID dies

**Examples**::

    # Show last 10 lines (default)
    tail file.txt

    # Show last 20 lines
    tail -n 20 file.txt

    # Short form
    tail -20 file.txt

    # Monitor file in real-time
    tail -f /var/log/apache2/error.log

    # Follow with retry (useful for log rotation)
    tail -F /var/log/syslog

    # Show last 100 bytes
    tail -c 100 file.txt

    # Show all lines from line 50 onwards
    tail -n +50 file.txt

Text Processing
---------------

grep (Global Regular Expression Print)
---------------------------------------

Searches for patterns in files.

**Syntax**::

    grep [OPTIONS] PATTERN [FILE]

**Common Options**:

* ``-i`` - Case-insensitive search
* ``-v`` - Invert match (show non-matching lines)
* ``-r`` or ``-R`` - Recursive search
* ``-n`` - Show line numbers
* ``-c`` - Count matching lines
* ``-l`` - List filenames only
* ``-w`` - Match whole words
* ``-A [NUM]`` - Show NUM lines after match
* ``-B [NUM]`` - Show NUM lines before match
* ``-C [NUM]`` - Show NUM lines before and after match
* ``-E`` - Extended regex (same as egrep)
* ``-o`` - Print only matched parts
* ``--color`` - Highlight matches

**Examples**::

    # Basic search
    grep "error" logfile.txt

    # Case-insensitive
    grep -i "error" logfile.txt

    # Search recursively in directory
    grep -r "function" /var/www/html/

    # Show line numbers
    grep -n "error" logfile.txt

    # Count matches
    grep -c "error" logfile.txt

    # Invert match
    grep -v "success" logfile.txt

    # Whole word match
    grep -w "log" file.txt

    # Multiple patterns
    grep -e "error" -e "warning" logfile.txt

    # Show context (2 lines before and after)
    grep -C 2 "error" logfile.txt

    # Search in multiple files
    grep "pattern" *.txt

    # With color highlighting
    grep --color "error" logfile.txt

    # List only filenames
    grep -l "pattern" *.txt

sed (Stream Editor)
-------------------

Performs text transformations on files.

**Syntax**::

    sed [OPTIONS] 'COMMAND' FILE

**Common Options**:

* ``-i`` - Edit files in-place
* ``-e`` - Add script to commands
* ``-n`` - Suppress automatic printing
* ``-r`` or ``-E`` - Extended regex

**Common Commands**:

* ``s/pattern/replacement/`` - Substitute
* ``d`` - Delete
* ``p`` - Print
* ``a`` - Append
* ``i`` - Insert

**Examples**::

    # Replace first occurrence in each line
    sed 's/old/new/' file.txt

    # Replace all occurrences (global)
    sed 's/old/new/g' file.txt

    # Replace in-place (modify original file)
    sed -i 's/old/new/g' file.txt

    # Delete lines containing pattern
    sed '/pattern/d' file.txt

    # Delete empty lines
    sed '/^$/d' file.txt

    # Delete lines 5-10
    sed '5,10d' file.txt

    # Print only lines 5-10
    sed -n '5,10p' file.txt

    # Replace only on specific lines
    sed '5,10s/old/new/g' file.txt

    # Multiple operations
    sed -e 's/old/new/g' -e 's/foo/bar/g' file.txt

    # Case-insensitive replace
    sed 's/old/new/gi' file.txt

    # Add line after match
    sed '/pattern/a New line text' file.txt

    # Insert line before match
    sed '/pattern/i New line text' file.txt

    # Replace with backreference
    sed 's/\([0-9]*\)/Number: \1/' file.txt

Compression and Archives
------------------------

tar
---

Archives and extracts files.

**Syntax**::

    tar [OPTIONS] FILE

**Common Options**:

* ``-c`` - Create archive
* ``-x`` - Extract archive
* ``-v`` - Verbose mode
* ``-f`` - Specify filename
* ``-z`` - Compress with gzip (.tar.gz)
* ``-j`` - Compress with bzip2 (.tar.bz2)
* ``-J`` - Compress with xz (.tar.xz)
* ``-t`` - List archive contents
* ``-r`` - Append to archive
* ``-u`` - Update archive
* ``-C`` - Change to directory

**Examples**::

    # Create tar archive
    tar -cvf archive.tar directory/

    # Create gzip compressed archive
    tar -cvzf archive.tar.gz directory/

    # Create bzip2 compressed archive
    tar -cvjf archive.tar.bz2 directory/

    # Extract tar archive
    tar -xvf archive.tar

    # Extract gzip archive
    tar -xvzf archive.tar.gz

    # Extract to specific directory
    tar -xvzf archive.tar.gz -C /destination/path/

    # List archive contents
    tar -tvf archive.tar

    # Extract specific file
    tar -xvf archive.tar file.txt

    # Append files to existing archive
    tar -rvf archive.tar newfile.txt

    # Extract single file from archive
    tar -xvzf archive.tar.gz path/to/file

gzip
----

Compresses or decompresses files.

**Syntax**::

    gzip [OPTIONS] FILE

**Common Options**:

* ``-d`` - Decompress (same as gunzip)
* ``-k`` - Keep original file
* ``-r`` - Recursive compression
* ``-v`` - Verbose mode
* ``-[1-9]`` - Compression level (1=fastest, 9=best)
* ``-l`` - List compressed file information
* ``-c`` - Write to stdout

**Examples**::

    # Compress file
    gzip file.txt

    # Compress and keep original
    gzip -k file.txt

    # Decompress file
    gzip -d file.txt.gz
    gunzip file.txt.gz

    # Compress with best compression
    gzip -9 file.txt

    # Compress recursively
    gzip -r directory/

    # View compressed file info
    gzip -l file.txt.gz

    # Compress to stdout
    gzip -c file.txt > file.txt.gz

zip/unzip
---------

Creates and extracts ZIP archives.

**zip Syntax**::

    zip [OPTIONS] archive.zip FILE

**zip Common Options**:

* ``-r`` - Recursive
* ``-e`` - Encrypt with password
* ``-q`` - Quiet mode
* ``-v`` - Verbose mode
* ``-[0-9]`` - Compression level
* ``-u`` - Update existing archive
* ``-d`` - Delete files from archive

**zip Examples**::

    # Create zip archive
    zip archive.zip file.txt

    # Create zip with multiple files
    zip archive.zip file1.txt file2.txt

    # Zip directory recursively
    zip -r archive.zip directory/

    # Zip with password protection
    zip -e -r secure.zip directory/

    # Add files to existing archive
    zip -u archive.zip newfile.txt

    # Best compression
    zip -9 -r archive.zip directory/

**unzip Syntax**::

    unzip [OPTIONS] archive.zip

**unzip Common Options**:

* ``-l`` - List archive contents
* ``-d`` - Extract to directory
* ``-o`` - Overwrite without prompting
* ``-q`` - Quiet mode
* ``-v`` - Verbose mode

**unzip Examples**::

    # Extract zip archive
    unzip archive.zip

    # Extract to specific directory
    unzip archive.zip -d /destination/

    # List archive contents
    unzip -l archive.zip

    # Extract specific file
    unzip archive.zip file.txt

    # Extract without prompting
    unzip -o archive.zip

System Information
------------------

uname
-----

Displays system information.

**Syntax**::

    uname [OPTIONS]

**Common Options**:

* ``-a`` - All information
* ``-s`` - Kernel name
* ``-n`` - Network node hostname
* ``-r`` - Kernel release
* ``-v`` - Kernel version
* ``-m`` - Machine hardware name
* ``-o`` - Operating system

**Examples**::

    # Show all information
    uname -a

    # Show kernel version
    uname -r

    # Show operating system
    uname -o

    # Show machine hardware
    uname -m

top
---

Displays real-time system processes and resource usage.

**Syntax**::

    top [OPTIONS]

**Interactive Commands**:

* ``q`` - Quit
* ``k`` - Kill process
* ``r`` - Renice process
* ``h`` - Help
* ``M`` - Sort by memory usage
* ``P`` - Sort by CPU usage
* ``1`` - Show individual CPU cores
* ``c`` - Show full command path

**Common Options**:

* ``-d [SEC]`` - Update delay in seconds
* ``-u [USER]`` - Show specific user
* ``-p [PID]`` - Monitor specific process
* ``-n [NUM]`` - Number of iterations

**Examples**::

    # Start top
    top

    # Update every 2 seconds
    top -d 2

    # Show processes for specific user
    top -u username

    # Monitor specific process
    top -p 1234

    # Run 5 iterations then exit
    top -n 5

htop
----

Interactive process viewer (enhanced top).

**Syntax**::

    htop [OPTIONS]

**Interactive Commands**:

* ``F1`` - Help
* ``F2`` - Setup
* ``F3`` - Search
* ``F4`` - Filter
* ``F5`` - Tree view
* ``F6`` - Sort by
* ``F9`` - Kill process
* ``F10`` - Quit
* ``Space`` - Tag process
* ``U`` - Show specific user
* ``/`` - Search

**Examples**::

    # Start htop
    htop

    # Show specific user processes
    htop -u username

    # Sort by memory
    htop -s PERCENT_MEM

.. note::
   If htop is not installed, install it using: ``sudo apt-get install htop``

df (Disk Free)
--------------

Reports file system disk space usage.

**Syntax**::

    df [OPTIONS] [FILE/DIRECTORY]

**Common Options**:

* ``-h`` - Human-readable sizes
* ``-a`` - Include all file systems
* ``-T`` - Show file system type
* ``-i`` - Show inode information
* ``-t [TYPE]`` - Show only specified type
* ``-x [TYPE]`` - Exclude specified type
* ``--total`` - Show grand total

**Examples**::

    # Show disk usage
    df

    # Human-readable format
    df -h

    # Show file system types
    df -hT

    # Show inode usage
    df -i

    # Show specific file system type
    df -t ext4

    # Exclude file system type
    df -x tmpfs

    # Show with total
    df -h --total

    # Check specific directory
    df -h /var/www/html

du (Disk Usage)
---------------

Estimates file and directory space usage.

**Syntax**::

    du [OPTIONS] [FILE/DIRECTORY]

**Common Options**:

* ``-h`` - Human-readable sizes
* ``-s`` - Summary (total size only)
* ``-a`` - Include files
* ``-c`` - Show grand total
* ``-d [NUM]`` - Max depth
* ``--max-depth=[NUM]`` - Max depth
* ``-x`` - Skip different file systems
* ``--exclude=[PATTERN]`` - Exclude pattern

**Examples**::

    # Show current directory usage
    du -h

    # Show summary only
    du -sh

    # Show with grand total
    du -ch

    # Limit depth to 1 level
    du -h --max-depth=1

    # Sort by size
    du -h | sort -h

    # Show top 10 largest directories
    du -h | sort -rh | head -10

    # Exclude pattern
    du -h --exclude="*.log"

    # Check specific directory
    du -sh /var/www/html

    # Show all files and directories
    du -ah

free
----

Displays memory usage information.

**Syntax**::

    free [OPTIONS]

**Common Options**:

* ``-h`` - Human-readable format
* ``-b`` - Bytes
* ``-k`` - Kilobytes
* ``-m`` - Megabytes
* ``-g`` - Gigabytes
* ``-s [SEC]`` - Update every SEC seconds
* ``-c [NUM]`` - Number of updates
* ``-t`` - Show total line
* ``-w`` - Wide mode

**Examples**::

    # Show memory usage
    free

    # Human-readable format
    free -h

    # Show in megabytes
    free -m

    # Show in gigabytes
    free -g

    # Update every 2 seconds
    free -h -s 2

    # Show 5 updates
    free -h -s 2 -c 5

    # Show with total line
    free -ht

    # Wide mode (separate buffers/cache)
    free -hw

Search and Find
---------------

find
----

Searches for files in directory hierarchy.

**Syntax**::

    find [PATH] [OPTIONS] [EXPRESSION]

**Common Options**:

* ``-name [PATTERN]`` - Search by name
* ``-iname [PATTERN]`` - Case-insensitive name
* ``-type [TYPE]`` - File type (f=file, d=directory, l=link)
* ``-size [SIZE]`` - File size
* ``-mtime [DAYS]`` - Modified days ago
* ``-user [USER]`` - Owner
* ``-perm [MODE]`` - Permissions
* ``-exec [CMD] {} \;`` - Execute command on results
* ``-delete`` - Delete found files
* ``-maxdepth [NUM]`` - Maximum depth

**Examples**::

    # Find files by name
    find /path -name "*.txt"

    # Case-insensitive search
    find /path -iname "*.TXT"

    # Find directories only
    find /path -type d

    # Find files only
    find /path -type f

    # Find files larger than 100MB
    find /path -size +100M

    # Find files smaller than 10KB
    find /path -size -10k

    # Find files modified in last 7 days
    find /path -mtime -7

    # Find files modified more than 30 days ago
    find /path -mtime +30

    # Find and delete
    find /path -name "*.tmp" -delete

    # Find and execute command
    find /path -name "*.log" -exec rm {} \;

    # Find with permissions
    find /path -perm 644

    # Limit search depth
    find /path -maxdepth 2 -name "*.txt"

    # Find empty files
    find /path -type f -empty

    # Find by owner
    find /path -user username

Permissions
-----------

chown (Change Owner)
--------------------

Changes file owner and group.

**Syntax**::

    chown [OPTIONS] USER[:GROUP] FILE

**Common Options**:

* ``-R`` - Recursive
* ``-v`` - Verbose
* ``-c`` - Report only changes
* ``--reference=[FILE]`` - Use reference file

**Examples**::

    # Change owner
    chown username file.txt

    # Change owner and group
    chown username:groupname file.txt

    # Change recursively
    chown -R username:groupname directory/

    # Change group only
    chown :groupname file.txt

    # Verbose mode
    chown -v username file.txt

    # Use reference file
    chown --reference=ref.txt file.txt

chmod (Change Mode)
-------------------

Changes file permissions.

**Syntax**::

    chmod [OPTIONS] MODE FILE

**Permission Numbers**:

* ``4`` - Read (r)
* ``2`` - Write (w)
* ``1`` - Execute (x)

**Permission Format**: ``[owner][group][others]``

Example: ``755`` = rwxr-xr-x

**Common Options**:

* ``-R`` - Recursive
* ``-v`` - Verbose
* ``-c`` - Report only changes

**Symbolic Mode**:

* ``u`` - User/owner
* ``g`` - Group
* ``o`` - Others
* ``a`` - All
* ``+`` - Add permission
* ``-`` - Remove permission
* ``=`` - Set exact permission

**Examples**::

    # Numeric mode - full permissions
    chmod 777 file.txt

    # Numeric mode - read/write for owner, read for others
    chmod 644 file.txt

    # Numeric mode - executable
    chmod 755 script.sh

    # Recursive
    chmod -R 755 directory/

    # Symbolic - add execute
    chmod +x script.sh

    # Symbolic - remove write from others
    chmod o-w file.txt

    # Symbolic - set exact permissions
    chmod u=rwx,g=rx,o=r file.txt

    # Add read for all
    chmod a+r file.txt

    # Remove execute from group
    chmod g-x file.txt

    # Make directory and contents readable
    chmod -R a+rX directory/

Networking
----------

ping
----

Tests network connectivity.

**Syntax**::

    ping [OPTIONS] DESTINATION

**Common Options**:

* ``-c [NUM]`` - Number of packets to send
* ``-i [SEC]`` - Interval between packets
* ``-s [SIZE]`` - Packet size
* ``-t [TTL]`` - Time to live
* ``-W [SEC]`` - Timeout in seconds
* ``-q`` - Quiet mode

**Examples**::

    # Ping host
    ping google.com

    # Send 5 packets
    ping -c 5 google.com

    # Set interval to 2 seconds
    ping -i 2 google.com

    # Set packet size
    ping -s 1024 google.com

    # Ping IP address
    ping 8.8.8.8

    # Quiet mode (summary only)
    ping -c 10 -q google.com

curl
----

Transfers data from or to a server.

**Syntax**::

    curl [OPTIONS] URL

**Common Options**:

* ``-X [METHOD]`` - HTTP method (GET, POST, PUT, DELETE)
* ``-d [DATA]`` - HTTP POST data
* ``-H [HEADER]`` - Custom header
* ``-o [FILE]`` - Output to file
* ``-O`` - Save with remote filename
* ``-L`` - Follow redirects
* ``-i`` - Include headers
* ``-I`` - Show headers only
* ``-u [USER:PASS]`` - Authentication
* ``-s`` - Silent mode
* ``-v`` - Verbose mode

**Examples**::

    # Simple GET request
    curl https://example.com

    # Download file
    curl -O https://example.com/file.zip

    # Save to specific filename
    curl -o output.html https://example.com

    # Follow redirects
    curl -L https://example.com

    # POST request with data
    curl -X POST -d "param1=value1&param2=value2" https://api.example.com

    # POST JSON data
    curl -X POST -H "Content-Type: application/json" -d '{"key":"value"}' https://api.example.com

    # Custom headers
    curl -H "Authorization: Bearer token" https://api.example.com

    # Show response headers
    curl -i https://example.com

    # Show only headers
    curl -I https://example.com

    # Basic authentication
    curl -u username:password https://example.com

    # Upload file
    curl -F "file=@/path/to/file" https://example.com/upload

wget
----

Downloads files from the web.

**Syntax**::

    wget [OPTIONS] URL

**Common Options**:

* ``-O [FILE]`` - Save to specific filename
* ``-c`` - Continue partial download
* ``-b`` - Background download
* ``-q`` - Quiet mode
* ``-v`` - Verbose mode
* ``-r`` - Recursive download
* ``-np`` - No parent directories
* ``-l [NUM]`` - Maximum recursion depth
* ``--limit-rate=[RATE]`` - Limit download speed
* ``--user=[USER]`` - Username
* ``--password=[PASS]`` - Password

**Examples**::

    # Download file
    wget https://example.com/file.zip

    # Save with different name
    wget -O newname.zip https://example.com/file.zip

    # Continue interrupted download
    wget -c https://example.com/largefile.iso

    # Background download
    wget -b https://example.com/file.zip

    # Download multiple files
    wget https://example.com/file1.zip https://example.com/file2.zip

    # Recursive download
    wget -r https://example.com/directory/

    # Limit download speed
    wget --limit-rate=500k https://example.com/file.zip

    # Quiet mode
    wget -q https://example.com/file.zip

    # Authentication
    wget --user=username --password=password https://example.com/file.zip

ssh (Secure Shell)
------------------

Connects to remote servers securely.

**Syntax**::

    ssh [OPTIONS] [USER@]HOST [COMMAND]

**Common Options**:

* ``-p [PORT]`` - Specify port
* ``-i [KEY]`` - Identity file (private key)
* ``-v`` - Verbose mode
* ``-C`` - Enable compression
* ``-L [PORT:HOST:HOSTPORT]`` - Local port forwarding
* ``-R [PORT:HOST:HOSTPORT]`` - Remote port forwarding
* ``-N`` - No remote command
* ``-f`` - Background mode

**Examples**::

    # Connect to server
    ssh username@hostname

    # Connect to specific port
    ssh -p 2222 username@hostname

    # Use specific key file
    ssh -i ~/.ssh/id_rsa username@hostname

    # Execute remote command
    ssh username@hostname 'ls -la'

    # Local port forwarding
    ssh -L 8080:localhost:80 username@hostname

    # Copy SSH key to server
    ssh-copy-id username@hostname

    # Verbose mode (debugging)
    ssh -v username@hostname

scp (Secure Copy)
-----------------

Securely copies files between hosts.

**Syntax**::

    scp [OPTIONS] SOURCE DESTINATION

**Common Options**:

* ``-r`` - Recursive (for directories)
* ``-P [PORT]`` - Specify port
* ``-i [KEY]`` - Identity file
* ``-v`` - Verbose mode
* ``-C`` - Enable compression
* ``-p`` - Preserve file attributes
* ``-q`` - Quiet mode

**Examples**::

    # Copy file to remote server
    scp file.txt username@hostname:/path/to/destination/

    # Copy file from remote server
    scp username@hostname:/path/to/file.txt /local/path/

    # Copy directory recursively
    scp -r directory/ username@hostname:/path/to/destination/

    # Specify port
    scp -P 2222 file.txt username@hostname:/path/

    # Use specific key
    scp -i ~/.ssh/id_rsa file.txt username@hostname:/path/

    # Copy multiple files
    scp file1.txt file2.txt username@hostname:/path/

    # Copy between two remote hosts
    scp user1@host1:/path/file.txt user2@host2:/path/

    # Preserve file attributes
    scp -p file.txt username@hostname:/path/

    # With compression
    scp -C largefile.zip username@hostname:/path/

Process Management
------------------

nohup
-----

Runs commands immune to hangups, with output to a non-tty.

**Syntax**::

    nohup COMMAND [ARGS] &

**Examples**::

    # Run command in background
    nohup ./script.sh &

    # Run with custom output file
    nohup ./script.sh > output.log 2>&1 &

    # Run long process
    nohup python long_script.py &

    # Check process
    jobs
    ps aux | grep script.sh

    # View nohup output
    tail -f nohup.out

.. note::
   By default, output is written to ``nohup.out`` in the current directory.

Package Management
------------------

dpkg
----

Debian package manager (low-level).

**Syntax**::

    dpkg [OPTIONS] PACKAGE

**Common Options**:

* ``-i`` - Install package
* ``-r`` - Remove package
* ``-P`` - Purge package
* ``-l`` - List installed packages
* ``-L`` - List files installed by package
* ``-s`` - Show package status
* ``-S`` - Search for file owner

**Examples**::

    # Install package
    sudo dpkg -i package.deb

    # Remove package
    sudo dpkg -r package-name

    # Purge package (remove including config)
    sudo dpkg -P package-name

    # List all installed packages
    dpkg -l

    # List specific package
    dpkg -l | grep package-name

    # Show package information
    dpkg -s package-name

    # List files from package
    dpkg -L package-name

    # Find package that owns file
    dpkg -S /path/to/file

    # Reconfigure package
    sudo dpkg-reconfigure package-name

snap
----

Universal Linux package manager.

**Syntax**::

    snap [COMMAND] [OPTIONS]

**Common Commands**:

* ``install`` - Install snap
* ``remove`` - Remove snap
* ``list`` - List installed snaps
* ``find`` - Find snaps in store
* ``refresh`` - Update snaps
* ``info`` - Show snap information

**Examples**::

    # Install snap
    sudo snap install package-name

    # Install from specific channel
    sudo snap install package-name --channel=edge

    # Install classic snap
    sudo snap install package-name --classic

    # Remove snap
    sudo snap remove package-name

    # List installed snaps
    snap list

    # Search for snaps
    snap find package-name

    # Update all snaps
    sudo snap refresh

    # Update specific snap
    sudo snap refresh package-name

    # Show snap info
    snap info package-name

    # Disable snap
    sudo snap disable package-name

    # Enable snap
    sudo snap enable package-name

systemctl
---------

Controls the systemd system and service manager.

**Syntax**::

    systemctl [COMMAND] [SERVICE]

**Common Commands**:

* ``start`` - Start service
* ``stop`` - Stop service
* ``restart`` - Restart service
* ``reload`` - Reload configuration
* ``enable`` - Enable service at boot
* ``disable`` - Disable service at boot
* ``status`` - Show service status
* ``is-active`` - Check if active
* ``is-enabled`` - Check if enabled
* ``list-units`` - List units

**Examples**::

    # Start service
    sudo systemctl start apache2

    # Stop service
    sudo systemctl stop apache2

    # Restart service
    sudo systemctl restart apache2

    # Reload configuration
    sudo systemctl reload apache2

    # Enable service at boot
    sudo systemctl enable apache2

    # Disable service at boot
    sudo systemctl disable apache2

    # Check service status
    systemctl status apache2

    # Check if service is active
    systemctl is-active apache2

    # Check if service is enabled
    systemctl is-enabled apache2

    # List all services
    systemctl list-units --type=service

    # List running services
    systemctl list-units --type=service --state=running

    # Show failed services
    systemctl --failed

    # Reboot system
    sudo systemctl reboot

    # Shutdown system
    sudo systemctl poweroff

Database Operations
-------------------

Create Database
---------------

**Syntax**::

    GRANT ALL PRIVILEGES ON <database_name>.* TO '<mysql_username>'@'localhost';

**Example**:

Here, ``root`` is **username** of ``mysql``::

    mysql -uroot -p
    CREATE DATABASE m2demo;
    GRANT ALL PRIVILEGES ON m2demo.* TO 'root'@'localhost';
    FLUSH PRIVILEGES;

Import Database
---------------

**Examples**::

    # Method 1: Command line
    mysql -u <username> -p <your_database_name> < database_file_name.sql

    # Method 2: Inside MySQL
    mysql -uroot -p
    SET FOREIGN_KEY_CHECKS=0;
    use database_name;
    SOURCE database_file_name.sql;
    SET FOREIGN_KEY_CHECKS=1;

Export Database
---------------

**Example**::

    mysqldump -u <username> -p <your_database_name> > database_file_name.sql

    # Export with compression
    mysqldump -u <username> -p <your_database_name> | gzip > database_file_name.sql.gz

Remove Definer
--------------

**Example**::

    # Find DEFINER statements
    grep "DEFINER" db_bkp_01042022.sql -rsn

    # Remove DEFINER from SQL file
    sed -i 's/DEFINER=`[^`]*`@`[^`]*`//g' your_database_name.sql

    # Alternative with find
    find . -name "your_database_name.sql" -type f -exec sed -i 's/DEFINER=`root`@`localhost`/ /g' {} +

Additional Examples
-------------------

Create .tar File
----------------

**Examples**::

    # Create tar archive
    tar -cvf archive.tar directory/

    # Create compressed tar.gz
    tar -cvzf code.tar.gz app/code/

    # Create tar.bz2 (better compression)
    tar -cvjf code.tar.bz2 app/code/

Extract .tar File
-----------------

**Examples**::

    # Extract tar
    tar -xvf archive.tar

    # Extract tar.gz
    tar -xvzf code.tar.gz

    # Extract to specific directory
    tar -xvzf code.tar.gz -C /destination/path/

Create .zip File
----------------

**Examples**::

    # Create zip file
    zip archive.zip file.txt

    # Create zip recursively
    zip -r code.zip app/code/

    # Create with password
    zip -e -r secure.zip app/code/

Extract .zip File
-----------------

**Examples**::

    # Extract zip
    unzip file_name.zip

    # Extract to specific directory
    unzip file_name.zip -d /destination/

    # List contents without extracting
    unzip -l file_name.zip

SCP File Transfer
-----------------

**Complete Example**:

#. Create tar files in ``Server A``::

    cd /var/www/html/
    tar -cvzf mage245.tar.gz mage245/

#. Transfer file Server A to B

   .. important:: Login Server B using SSH.

#. Go to destination path where you want the copied file in Server B

   **Example**: ``cd /home/plugincardknox/public_html``

#. Execute below command in ``Server B``::

    scp root@197.280.111.178:/var/www/html/mage245.tar.gz .

   .. note::
      The ``.`` at the end means current directory

#. Extract the transferred file::

    tar -xvzf mage245.tar.gz

Quick Reference
---------------

**File Operations**::

    pwd                    # Print working directory
    ls -lah                # List all files with details
    cd /path               # Change directory
    cp -r source dest      # Copy recursively
    mv old new             # Move/rename
    rm -rf directory/      # Remove directory
    mkdir -p path/to/dir   # Create nested directories
    touch file.txt         # Create empty file

**File Viewing**::

    cat file.txt           # Display file
    less file.txt          # View file (paginated)
    head -n 20 file.txt    # First 20 lines
    tail -f log.txt        # Monitor file
    grep "pattern" file    # Search in file

**System Info**::

    uname -a               # System information
    df -h                  # Disk usage
    free -h                # Memory usage
    top                    # Process monitor
    htop                   # Better process monitor

**Networking**::

    ping google.com        # Test connectivity
    curl https://api.com   # HTTP request
    wget url/file.zip      # Download file
    ssh user@host          # Remote connection
    scp file user@host:    # Secure copy

**Permissions**::

    chmod 755 file         # Change permissions
    chown user:group file  # Change owner
    chmod +x script.sh     # Make executable

**Archives**::

    tar -czf file.tar.gz dir/      # Create tar.gz
    tar -xzf file.tar.gz           # Extract tar.gz
    zip -r archive.zip dir/        # Create zip
    unzip archive.zip              # Extract zip

**System Services**::

    systemctl start service        # Start service
    systemctl stop service         # Stop service
    systemctl restart service      # Restart service
    systemctl status service       # Check status
    systemctl enable service       # Enable at boot

See Also
--------

* `Linux Command Line Basics <https://www.gnu.org/software/bash/manual/>`_
* `Advanced Bash Scripting Guide <https://tldp.org/LDP/abs/html/>`_
* `Linux Journey <https://linuxjourney.com/>`_

.. tip::
   Use ``man <command>`` or ``<command> --help`` to get detailed help for any command.

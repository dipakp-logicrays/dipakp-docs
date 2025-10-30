Linux: System Information Commands
==================================

A comprehensive guide to collecting system and hardware information on Linux using command-line tools. Learn how to check CPU, memory, disk, network, and other system details.

.. contents:: Table of Contents
   :local:
   :depth: 2

Overview
--------

Understanding your Linux system's hardware and software configuration is essential for system administration, troubleshooting, and optimization. This guide covers various commands to gather detailed system information.

Why Check System Information?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- **Troubleshooting**: Identify hardware or software issues
- **Performance Monitoring**: Track resource usage and bottlenecks
- **System Inventory**: Document hardware specifications
- **Compatibility**: Verify system requirements before installation
- **Security Audits**: Review system configuration and users
- **Capacity Planning**: Monitor resource utilization trends

Basic System Information Commands
----------------------------------

General System Information
~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Display Complete System Information**

Show operating system name, system node name, OS release, version, hardware name, and processor type::

    uname -a

**Example Output**::

    Linux logicrays-Latitude-5590 5.15.0-157-generic #167-Ubuntu SMP Wed Sep 17 21:35:53 UTC 2025 x86_64 x86_64 x86_64 GNU/Linux

**Check Hostname**

Display the system's hostname::

    hostname

**Example Output**::

    myserver.example.com
    logicrays-Latitude-5590

**Get Detailed Hostname Information**

Show static and transient hostname with additional details::

    hostnamectl

**Example Output**::

    Static hostname: logicrays-Latitude-5590
    Icon name: computer-laptop
    Chassis: laptop
    Machine ID: e7d0df732b0649e49e97a4d764308014
    Boot ID: f04e8165d4194c6ca3e0175bb8b470ab
    Operating System: Linux Mint 21.3
    Kernel: Linux 5.15.0-157-generic
    Architecture: x86-64
    Hardware Vendor: Dell Inc.
    Hardware Model: Latitude 5500

Operating System Information
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Get Complete Linux OS Information**

Display detailed OS information including version, ID, and URLs::

    cat /etc/os-release

**Example Output**::

    NAME="Linux Mint"
    VERSION="21.3 (Virginia)"
    ID=linuxmint
    ID_LIKE="ubuntu debian"
    PRETTY_NAME="Linux Mint 21.3"
    VERSION_ID="21.3"
    HOME_URL="https://www.linuxmint.com/"
    SUPPORT_URL="https://forums.linuxmint.com/"
    BUG_REPORT_URL="http://linuxmint-troubleshooting-guide.readthedocs.io/en/latest/"
    PRIVACY_POLICY_URL="https://www.linuxmint.com/"
    VERSION_CODENAME=virginia
    UBUNTU_CODENAME=jammy

**Alternative OS Information Command**::

    lsb_release -a

**Example Output**::

    Distributor ID: Ubuntu
    Description:    Ubuntu 22.04.3 LTS
    Release:        22.04
    Codename:       jammy

**Check Kernel Version**::

    uname -r

**Example Output**::

    5.15.0-157-generic

**Check OS Type**::

    uname -o

**Example Output**::

    GNU/Linux

Architecture Information
~~~~~~~~~~~~~~~~~~~~~~~~

**Check System Architecture**

Determine if your system is x64, ARM64, or other architecture::

    uname -m

**Common Outputs**:

- ``x86_64`` - 64-bit Intel/AMD (also called AMD64 or x64)
- ``aarch64`` - 64-bit ARM (ARM64)
- ``armv7l`` - 32-bit ARM
- ``i686`` - 32-bit x86

**Alternative Architecture Command**::

    arch

**Check if System is 32-bit or 64-bit**::

    getconf LONG_BIT

**Example Output**::

    64

CPU Information
---------------

Display CPU Details
~~~~~~~~~~~~~~~~~~~

**Using lscpu Command**

Get detailed CPU architecture information::

    lscpu

**Example Output**::

    Architecture:            x86_64
    CPU op-mode(s):          32-bit, 64-bit
    Byte Order:              Little Endian
    Address sizes:           39 bits physical, 48 bits virtual
    CPU(s):                  8
    Thread(s) per core:      2
    Core(s) per socket:      4
    Socket(s):               1
    Vendor ID:               GenuineIntel
    Model name:              Intel(R) Core(TM) i7-8550U CPU @ 1.80GHz
    CPU MHz:                 800.057
    CPU max MHz:             4000.0000
    CPU min MHz:             400.0000

**Using /proc/cpuinfo**

Display raw CPU information::

    cat /proc/cpuinfo

**Get CPU Model Only**::

    cat /proc/cpuinfo | grep "model name" | head -1

**Example Output**::

    model name      : Intel(R) Core(TM) i7-8550U CPU @ 1.80GHz

**Using lshw for CPU**

Display CPU information using lshw::

    lshw -C cpu

or in short format::

    lshw -C cpu -short

**Count CPU Cores**::

    nproc

**Example Output**::

    8

Memory Information
------------------

Display Memory Usage
~~~~~~~~~~~~~~~~~~~~

**Show Free and Used Memory**

Display memory in megabytes::

    free -m

**Example Output**::

                  total        used        free      shared  buff/cache   available
    Mem:          31906        15264        9855       1859        6786       14326
    Swap:          5119        03232        1887

**Display Memory in Gigabytes**::

    free -g

**Human-Readable Memory Display**::

    free -h

**Example Output**::

                  total        used        free      shared  buff/cache   available
    Mem:           31Gi        15Gi       9.5Gi       1.8Gi       6.6Gi        13Gi
    Swap:         5.0Gi       3.2Gi       1.8Gi

**Display Total Available Memory**

View detailed memory information::

    cat /proc/meminfo

**Get Total Memory Only**::

    cat /proc/meminfo | grep MemTotal

**Example Output**::

    MemTotal:       32672444 kB

Memory Hardware Information
~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Show Memory Size and Configuration**

Using dmidecode::

    sudo dmidecode -t memory | grep -i size

**Example Output**::

    Size: 16 GB
    Non-Volatile Size: None
    Volatile Size: 16 GB
    Cache Size: None
    Logical Size: None
    Size: 16 GB
    Non-Volatile Size: None
    Volatile Size: 16 GB
    Cache Size: None
    Logical Size: None

**Using lshw for Memory**::

    lshw -short -C memory

**Detailed Memory Information**::

    sudo dmidecode -t memory

Disk and Storage Information
-----------------------------

Disk Usage Commands
~~~~~~~~~~~~~~~~~~~

**Display File System Disk Space Usage**

Show disk usage in human-readable format::

    df -h

**Example Output**::

    Filesystem      Size  Used Avail Use% Mounted on
    /dev/sda1       457G  123G  311G  29% /
    /dev/sda2       1.8T  856G  849G  51% /home

**Show Disk Usage with SI Units**::

    df -H

**Display Inode Usage**::

    df -i

**Example Output**::

    Filesystem      Inodes  IUsed   IFree IUse% Mounted on
    /dev/sda1      30474240 456789 30017451    2% /

Partition Information
~~~~~~~~~~~~~~~~~~~~~

**List All Partitions**

Display partition table::

    sudo fdisk -l

**Example Output**::

    Disk /dev/sda: 465.76 GiB, 500107862016 bytes, 976773168 sectors
    Device     Boot   Start       End   Sectors   Size Id Type
    /dev/sda1  *       2048 976771071 976769024 465.8G 83 Linux

**Show Mounted Filesystems**::

    mount

**Display /etc/fstab Configuration**::

    cat /etc/fstab

Disk Block Devices
~~~~~~~~~~~~~~~~~~

**Gather Disk Information**

List block devices::

    lsblk

**Example Output**::

    NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
    sda      8:0    0 465.8G  0 disk
    ├─sda1   8:1    0   512M  0 part /boot/efi
    ├─sda2   8:2    0   450G  0 part /
    └─sda3   8:3    0  15.3G  0 part [SWAP]

**Show Filesystem Type**::

    lsblk -f

**Example Output**::

    NAME   FSTYPE LABEL UUID                                 MOUNTPOINT
    sda
    ├─sda1 vfat         1234-5678                            /boot/efi
    ├─sda2 ext4         12345678-1234-1234-1234-123456789abc /
    └─sda3 swap         87654321-4321-4321-4321-210987654321 [SWAP]

Hardware Information
--------------------

PCI Devices
~~~~~~~~~~~

**List PCI Devices**

Display all PCI devices::

    lspci

**Example Output**::

    00:00.0 Host bridge: Intel Corporation Coffee Lake HOST and DRAM Controller (rev 0c)
    00:02.0 VGA compatible controller: Intel Corporation WhiskeyLake-U GT2 [UHD Graphics 620] (rev 02)
    00:04.0 Signal processing controller: Intel Corporation Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor Thermal Subsystem (rev 0c)
    00:08.0 System peripheral: Intel Corporation Xeon E3-1200 v5/v6 / E3-1500 v5 / 6th/7th/8th Gen Core Processor Gaussian Mixture Model
    00:12.0 Signal processing controller: Intel Corporation Cannon Point-LP Thermal Controller (rev 30)
    00:14.0 USB controller: Intel Corporation Cannon Point-LP USB 3.1 xHCI Controller (rev 30)
    00:14.2 RAM memory: Intel Corporation Cannon Point-LP Shared SRAM (rev 30)
    00:14.3 Network controller: Intel Corporation Cannon Point-LP CNVi [Wireless-AC] (rev 30)
    00:15.0 Serial bus controller: Intel Corporation Cannon Point-LP Serial IO I2C Controller #0 (rev 30)
    00:15.1 Serial bus controller: Intel Corporation Cannon Point-LP Serial IO I2C Controller #1 (rev 30)
    00:16.0 Communication controller: Intel Corporation Cannon Point-LP MEI Controller #1 (rev 30)
    00:16.3 Serial controller: Intel Corporation Cannon Point-LP Keyboard and Text (KT) Redirection (rev 30)
    00:19.0 Serial bus controller: Intel Corporation Cannon Point-LP Serial IO I2C Host Controller (rev 30)
    00:1c.0 PCI bridge: Intel Corporation Cannon Point-LP PCI Express Root Port #1 (rev f0)
    00:1c.4 PCI bridge: Intel Corporation Cannon Point-LP PCI Express Root Port #5 (rev f0)
    00:1d.0 PCI bridge: Intel Corporation Cannon Point-LP PCI Express Root Port #13 (rev f0)
    00:1f.0 ISA bridge: Intel Corporation Cannon Point-LP LPC Controller (rev 30)
    00:1f.3 Audio device: Intel Corporation Cannon Point-LP High Definition Audio Controller (rev 30)
    00:1f.4 SMBus: Intel Corporation Cannon Point-LP SMBus Controller (rev 30)
    00:1f.5 Serial bus controller: Intel Corporation Cannon Point-LP SPI Controller (rev 30)
    00:1f.6 Ethernet controller: Intel Corporation Ethernet Connection (6) I219-LM (rev 30)
    01:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS525A PCI Express Card Reader (rev 01)
    02:00.0 PCI bridge: Intel Corporation JHL6340 Thunderbolt 3 Bridge (C step) [Alpine Ridge 2C 2016] (rev 02)
    03:00.0 PCI bridge: Intel Corporation JHL6340 Thunderbolt 3 Bridge (C step) [Alpine Ridge 2C 2016] (rev 02)
    03:01.0 PCI bridge: Intel Corporation JHL6340 Thunderbolt 3 Bridge (C step) [Alpine Ridge 2C 2016] (rev 02)
    03:02.0 PCI bridge: Intel Corporation JHL6340 Thunderbolt 3 Bridge (C step) [Alpine Ridge 2C 2016] (rev 02)
    04:00.0 System peripheral: Intel Corporation JHL6340 Thunderbolt 3 NHI (C step) [Alpine Ridge 2C 2016] (rev 02)
    3a:00.0 USB controller: Intel Corporation JHL6340 Thunderbolt 3 USB 3.1 Controller (C step) [Alpine Ridge 2C 2016] (rev 02)
    3b:00.0 Non-Volatile memory controller: MAXIO Technology (Hangzhou) Ltd. NVMe SSD Controller MAP1202 (rev 01)

**Detailed PCI Information**::

    lspci -v

**Show Specific Device (e.g., Network)**::

    lspci | grep -i network

USB Devices
~~~~~~~~~~~

**List USB Devices**

Display all USB devices::

    lsusb

**Example Output**::

    Bus 004 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
    Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
    Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
    Bus 001 Device 004: ID 0a5c:5842 Broadcom Corp. 58200
    Bus 001 Device 003: ID 0c45:6a09 Microdia Integrated_Webcam_HD
    Bus 001 Device 002: ID 046d:c077 Logitech, Inc. M105 Optical Mouse
    Bus 001 Device 005: ID 8087:0aaa Intel Corp. Bluetooth 9460/9560 Jefferson Peak (JfP)
    Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

**Detailed USB Information**::

    lsusb -v

**Show USB Device Tree**::

    lsusb -t

All Hardware Information
~~~~~~~~~~~~~~~~~~~~~~~~

**Using inxi**

Display comprehensive hardware information::

    inxi -Fxz

.. note::
   Install inxi if not available: ``sudo apt install inxi``

**Using hwinfo**

Show short hardware summary::

    hwinfo --short

**Detailed Hardware Information**::

    hwinfo

.. note::
   Install hwinfo if not available: ``sudo apt install hwinfo``

**Using lshw**

Display hardware information in short format::

    lshw -short

**Detailed Hardware Listing**::

    sudo lshw

**Output to HTML File**::

    sudo lshw -html > hardware.html

**Using lsdev**

List all device drivers::

    lsdev

.. note::
   Install lsdev if not available: ``sudo apt install procinfo``

**Using dmidecode**

Get all DMI/SMBIOS information::

    sudo dmidecode

**Save System Information to File**::

    sudo dmidecode > systeminfo.txt

System Status and Monitoring
-----------------------------

System Uptime
~~~~~~~~~~~~~

**Display System Uptime**

Show how long the system has been running::

    uptime

**Example Output**::

    18:08:34 up 2 days,  7:30,  1 user,  load average: 0.67, 0.80, 1.28

**Pretty Uptime Format**::

    uptime -p

**Example Output**::

    up 2 days, 7 hours, 30 minutes

Date and Time
~~~~~~~~~~~~~

**Display Current Date and Time**::

    date

**Example Output**::

    Wednesday 29 October 2025 06:09:17 PM IST

**Show Date in Specific Format**::

    date '+%Y-%m-%d %H:%M:%S'

**Example Output**::

    2025-10-29 18:09:33

User Information
~~~~~~~~~~~~~~~~

**Show Current User**::

    whoami

**Example Output**::

    john

**Show Current User's Groups**::

    groups

**Example Output**::

    logicrays adm cdrom sudo dip plugdev lpadmin sambashare www-data docker

**Show Who is Logged In**::

    who

**Example Output**::

    john     pts/0        2025-10-29 10:15 (192.168.1.100)
    jane     pts/1        2025-10-29 12:30 (192.168.1.105)

**Show Last Logged In Users**::

    last

**Show Login History**::

    lastlog

Process Information
-------------------

View Running Processes
~~~~~~~~~~~~~~~~~~~~~~

**Show Running Processes (Interactive)**::

    top

**Take One Snapshot**::

    top -n 1

**Show All Processes**::

    ps aux

**Top 10 Memory-Consuming Processes**::

    ps aux --sort=-%mem | head -10

**Example Output**::

    USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
    mysql     1234  2.5 15.3 2847564 2456432 ?     Ssl  Oct28  23:15 /usr/sbin/mysqld
    www-data  5678  1.8 8.2  1234567 1312456 ?     S    Oct28  15:42 php-fpm: pool www

**Top 10 CPU-Consuming Processes**::

    ps aux --sort=-%cpu | head -10

Network Information
-------------------

Network Interfaces
~~~~~~~~~~~~~~~~~~

**Show All Network Interfaces**

Display IP addresses and network interfaces::

    ip a

or::

    ip address show

**Example Output**::

    1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536
        inet 127.0.0.1/8 scope host lo
    2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500
        inet 192.168.1.100/24 brd 192.168.1.255 scope global eth0

**Show Specific Interface**::

    ip a show eth0

**Show Only IP Addresses**::

    hostname -I

Network Connections
~~~~~~~~~~~~~~~~~~~

**Show Open Ports and Connections**

Display all TCP and UDP listening ports::

    ss -tuln

**Example Output**::

    Netid State  Recv-Q Send-Q Local Address:Port  Peer Address:Port
    tcp   LISTEN 0      128    0.0.0.0:22           0.0.0.0:*
    tcp   LISTEN 0      80     0.0.0.0:80           0.0.0.0:*
    tcp   LISTEN 0      128    0.0.0.0:443          0.0.0.0:*

**Show All Connections**::

    ss -tuna

**Alternative: Using netstat**::

    netstat -tuln

.. note::
   Install net-tools if netstat is not available: ``sudo apt install net-tools``

Routing Information
~~~~~~~~~~~~~~~~~~~

**Show Routing Table**::

    ip r

or::

    ip route show

**Example Output**::

    default via 192.168.1.1 dev eth0 proto dhcp metric 100
    192.168.1.0/24 dev eth0 proto kernel scope link src 192.168.1.100

**Show Default Gateway**::

    ip route | grep default

Kernel and Module Information
------------------------------

Kernel Information
~~~~~~~~~~~~~~~~~~

**Display Kernel Version**::

    uname -r

**Example Output**::

    5.15.0-157-generic

**Show Kernel Details**::

    uname -a

Kernel Modules
~~~~~~~~~~~~~~

**List Loaded Kernel Modules**::

    lsmod

**Example Output**::

    Module                  Size  Used by
    btrfs                1392640  0
    xor                    24576  1 btrfs
    raid6_pq              114688  1 btrfs

**Show Specific Module Information**::

    modinfo module_name

**Example**::

    modinfo e1000e

Kernel Messages
~~~~~~~~~~~~~~~

**View Last Kernel Messages**::

    dmesg | tail -20

**View All Kernel Messages**::

    dmesg

**Search Kernel Messages**::

    dmesg | grep -i error

System Logs
-----------

View System Logs
~~~~~~~~~~~~~~~~

**View Recent System Logs**

Show last 20 system log entries::

    journalctl -n 20

**Follow System Logs in Real-Time**::

    journalctl -f

**View Logs Since Boot**::

    journalctl -b

**View Logs for Specific Service**::

    journalctl -u apache2

**View Logs for Specific Time Range**::

    journalctl --since "2025-10-29 10:00:00" --until "2025-10-29 12:00:00"

**View Logs with Priority**

Show only error messages::

    journalctl -p err

Environment and Configuration
-----------------------------

Environment Variables
~~~~~~~~~~~~~~~~~~~~~

**Display All Environment Variables**::

    env

**Show Specific Variable**::

    echo $PATH

**Example Output**::

    /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

**Display Shell Variables**::

    set

System Configuration Files
~~~~~~~~~~~~~~~~~~~~~~~~~~

**View Important Configuration Files**

- ``/etc/os-release`` - OS information
- ``/etc/hostname`` - System hostname
- ``/etc/hosts`` - Host name mapping
- ``/etc/fstab`` - Filesystem mount configuration
- ``/etc/network/interfaces`` - Network configuration (Debian/Ubuntu)
- ``/etc/resolv.conf`` - DNS configuration

System Information Script
-------------------------

Interactive System Information Tool
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

For convenient access to all these system information commands, use the ``check_system`` bash script.

.. seealso::
    For installation instructions and the complete script, see :ref:`script-7-system-information-checker`

The automated script provides:

- Interactive menu with 38+ checking options
- Color-coded output for better readability
- Architecture and current user detection
- Organized command categories (System, CPU, Memory, Disk, Network, Hardware, Logs)
- Report generation with timestamp
- Help documentation

Quick Example
^^^^^^^^^^^^^

After installing the script from the bash service scripts guide::

    check_system

The script will display an interactive menu where you can select from 38+ options to view different system information.

**Example Output:**

.. code-block:: text

    ------------------------------------
    ✅ Current System Architecture: x86_64

    👤 Current Logged In User: john
    ------------------------------------
    Please select an option:
    [0] General system info - [uname -a]
    [1] Check host name - [hostname]
    [2] Linux OS info - [cat /etc/os-release]
    ...
    [37] OS type - [uname -o]
    [q] Quit

    Enter your choice:

Quick Reference
---------------

Essential Commands
~~~~~~~~~~~~~~~~~~

**System Information**::

    uname -a                  # Complete system info
    hostname                  # System hostname
    hostnamectl               # Detailed hostname info
    cat /etc/os-release       # OS details
    uname -m                  # System architecture
    getconf LONG_BIT          # 32 or 64 bit

**CPU**::

    lscpu                     # CPU information
    nproc                     # Number of processors
    cat /proc/cpuinfo         # Detailed CPU info

**Memory**::

    free -h                   # Memory usage
    cat /proc/meminfo         # Detailed memory info
    sudo dmidecode -t memory  # Memory hardware info

**Disk**::

    df -h                     # Disk usage
    lsblk                     # Block devices
    sudo fdisk -l             # Partition information
    df -i                     # Inode usage

**Hardware**::

    lspci                     # PCI devices
    lsusb                     # USB devices
    lshw -short               # Hardware summary
    sudo dmidecode            # DMI/SMBIOS info

**Network**::

    ip a                      # Network interfaces
    ss -tuln                  # Open ports
    ip r                      # Routing table
    hostname -I               # IP addresses

**System Status**::

    uptime                    # System uptime
    top                       # Process monitor
    who                       # Logged in users
    ps aux                    # All processes

**Logs**::

    journalctl -n 20          # Recent logs
    dmesg | tail -20          # Kernel messages

Common Use Cases
----------------

Server Inventory
~~~~~~~~~~~~~~~~

Collect complete server specifications::

    echo "=== Server Inventory ===" > server_info.txt
    echo "Hostname: $(hostname)" >> server_info.txt
    echo "OS: $(cat /etc/os-release | grep PRETTY_NAME | cut -d'"' -f2)" >> server_info.txt
    echo "Kernel: $(uname -r)" >> server_info.txt
    echo "CPU: $(lscpu | grep 'Model name' | cut -d':' -f2 | xargs)" >> server_info.txt
    echo "Memory: $(free -h | grep Mem | awk '{print $2}')" >> server_info.txt
    echo "Disk: $(df -h / | tail -1 | awk '{print $2}')" >> server_info.txt
    cat server_info.txt

Performance Monitoring
~~~~~~~~~~~~~~~~~~~~~~

Check system performance metrics::

    echo "CPU Usage:"
    top -bn1 | grep "Cpu(s)" | awk '{print $2}' | cut -d'%' -f1

    echo "Memory Usage:"
    free | grep Mem | awk '{printf("%.2f%%\n", $3/$2 * 100.0)}'

    echo "Disk Usage:"
    df -h / | tail -1 | awk '{print $5}'

Troubleshooting
~~~~~~~~~~~~~~~

Gather diagnostic information::

    echo "System Diagnostics" > diagnostics.txt
    echo "==================" >> diagnostics.txt
    echo "" >> diagnostics.txt
    echo "Uptime:" >> diagnostics.txt
    uptime >> diagnostics.txt
    echo "" >> diagnostics.txt
    echo "Top Memory Processes:" >> diagnostics.txt
    ps aux --sort=-%mem | head -6 >> diagnostics.txt
    echo "" >> diagnostics.txt
    echo "Recent Errors:" >> diagnostics.txt
    journalctl -p err -n 10 >> diagnostics.txt

Resources
---------

Official Documentation
~~~~~~~~~~~~~~~~~~~~~~

- **Linux Man Pages**: https://linux.die.net/man/
- **Ubuntu Documentation**: https://help.ubuntu.com/
- **Red Hat System Administration**: https://www.redhat.com/sysadmin/

Useful Tutorials
~~~~~~~~~~~~~~~~

- TecMint: https://www.tecmint.com/commands-to-collect-system-and-hardware-information-in-linux/
- Red Hat SysAdmin: https://www.redhat.com/sysadmin/linux-system-info-commands
- Baeldung Linux: https://www.baeldung.com/linux/cli-hardware-info
- Opensource.com: https://opensource.com/article/19/9/linux-commands-hardware-information

Related Guides
~~~~~~~~~~~~~~

- :doc:`../linux-commands/index` - General Linux command reference
- :doc:`../package-management/index` - Linux package management
- :doc:`../lamp-stack/index` - LAMP stack setup

Best Practices
--------------

Regular Monitoring
~~~~~~~~~~~~~~~~~~

#. **Check system resources regularly**: Monitor CPU, memory, and disk usage
#. **Review logs periodically**: Check for errors and warnings
#. **Document your system**: Keep hardware and software inventory updated
#. **Monitor performance trends**: Track resource usage over time
#. **Set up alerts**: Use monitoring tools for proactive issue detection

Security Considerations
~~~~~~~~~~~~~~~~~~~~~~~

#. **Limit information exposure**: Don't share detailed system info publicly
#. **Secure sensitive files**: Protect configuration and log files
#. **Monitor unauthorized access**: Check who commands and logs
#. **Regular audits**: Review system users and processes
#. **Keep systems updated**: Apply security patches promptly

.. warning::
   Some commands like ``dmidecode``, ``fdisk``, and ``lshw`` require root/sudo access and may expose sensitive hardware information. Use caution when sharing output from these commands.

Conclusion
----------

Understanding how to gather system information is fundamental for Linux system administration. The commands and tools covered in this guide provide comprehensive insights into your system's hardware, software, and performance characteristics.

Key takeaways:

- Use appropriate commands for specific information needs
- Combine commands to create useful reports
- Automate information gathering with scripts
- Monitor systems regularly for optimal performance
- Keep documentation updated with system changes

The provided ``check_system`` script offers a convenient way to access all major system information commands through an interactive menu, making system administration tasks more efficient.

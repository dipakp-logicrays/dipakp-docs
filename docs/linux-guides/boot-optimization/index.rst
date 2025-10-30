Linux: Boot Speed Optimization Guide
====================================

A comprehensive guide to analyze and optimize Linux boot time, reduce system startup delays, and improve overall system performance. Learn safe techniques to speed up your Linux system without compromising stability.

.. contents:: Table of Contents
   :local:
   :depth: 2

Overview
--------

What is Boot Optimization?
~~~~~~~~~~~~~~~~~~~~~~~~~~

Boot optimization involves analyzing and reducing the time it takes for your Linux system to start up from power-on to a fully operational desktop environment. A typical Linux system takes 30-60 seconds to boot, but with proper optimization, this can be reduced to 10-20 seconds.

Why Optimize Boot Time?
~~~~~~~~~~~~~~~~~~~~~~~~

- **Faster System Access**: Get to your desktop and applications quicker
- **Improved Productivity**: Less waiting time, especially for frequent reboots
- **Better Resource Management**: Identify unnecessary services consuming resources
- **System Health**: Detect problematic services causing delays
- **Energy Efficiency**: Faster boot means less power consumption during startup

Understanding Boot Process
---------------------------

Boot Stages
~~~~~~~~~~~

Linux boot process consists of several stages:

#. **Firmware (BIOS/UEFI)**: Hardware initialization (~10-15 seconds)
#. **Bootloader**: OS selection and loading (~3-10 seconds)
#. **Kernel**: Linux kernel loading and initialization (~3-5 seconds)
#. **Userspace**: System services and desktop environment (~20-40 seconds)

**Example Boot Time Breakdown**::

    Startup finished in 12.268s (firmware) + 3.567s (loader) + 4.219s (kernel) + 26.927s (userspace) = 46.983s

Most optimization happens in the **userspace** stage where system services start.

Analyzing Boot Performance
---------------------------

Check Boot Time
~~~~~~~~~~~~~~~

**View Overall Boot Time**

Display total boot time and breakdown by stage::

    systemd-analyze time

**Example Output**::

    Startup finished in 12.268s (firmware) + 3.567s (loader) + 4.219s (kernel) + 26.927s (userspace) = 46.983s
    graphical.target reached after 26.918s in userspace

**Interpretation**:

- **Firmware (12.2s)**: BIOS/UEFI initialization - hard to optimize
- **Loader (3.5s)**: Bootloader - generally optimal
- **Kernel (4.2s)**: Kernel loading - generally optimal
- **Userspace (26.9s)**: System services - **main optimization target**

Identify Slow Services
~~~~~~~~~~~~~~~~~~~~~~

**List Services by Boot Time**

Show which services take longest to start::

    systemd-analyze blame

**Example Output**::

    2min 32.052s fstrim.service
         45.246s plocate-updatedb.service
         17.023s elasticsearch.service
          6.663s snapd.seeded.service
          6.659s snapd.service
          6.608s NetworkManager-wait-online.service
          3.930s rabbitmq-server.service
          3.594s mysql.service
          1.898s systemd-udev-settle.service
          1.827s fwupd.service

This shows the biggest offenders consuming boot time.

Generate Boot Timeline
~~~~~~~~~~~~~~~~~~~~~~~

**Create Visual Boot Chain**

Generate an SVG visualization of the boot process::

    systemd-analyze plot > boot-timeline.svg

Open the SVG file in a browser to see a visual timeline of all services.

**Create Critical Chain Analysis**::

    systemd-analyze critical-chain

**Example Output**::

    graphical.target @26.918s
    └─multi-user.target @26.917s
      └─mysql.service @23.322s +3.594s
        └─network.target @23.319s
          └─NetworkManager.service @23.224s +94ms

This shows the critical path of services blocking the boot.

Safe Boot Optimizations
------------------------

Critical Fix: fstrim Service
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Problem**: ``fstrim.service`` takes 2+ minutes at boot

The fstrim service performs SSD trimming, which should run weekly via timer, not at boot.

**Solution - Disable Boot-time fstrim**::

    # Disable fstrim at boot
    sudo systemctl disable fstrim.service

    # Enable weekly timer (recommended)
    sudo systemctl enable fstrim.timer
    sudo systemctl start fstrim.timer

**Verify Timer is Active**::

    systemctl status fstrim.timer

**Example Output**::

    ● fstrim.timer - Discard unused blocks once a week
         Loaded: loaded
         Active: active (waiting)
        Trigger: Mon 2025-11-03 00:00:00 IST

**Expected Savings**: ~2.5 minutes ✅

.. important::
   This optimization alone can save **2+ minutes** from your boot time! The fstrim operation will still run weekly in the background via the timer.

Fix plocate Database Updates
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Problem**: ``plocate-updatedb.service`` takes 45+ seconds at boot

This service updates the file search database (used by ``locate`` command).

**Solution - Run via Timer Only**::

    # Disable at boot (will still run daily via timer)
    sudo systemctl mask plocate-updatedb.service

    # Verify the daily timer is active
    systemctl list-timers | grep plocate

**Example Output**::

    NEXT                        LEFT     LAST                        PASSED  UNIT
    Wed 2025-10-30 00:00:00 IST 4h left  Tue 2025-10-29 00:00:00 IST 20h ago plocate-updatedb.timer

**Expected Savings**: ~45 seconds ✅

Disable NetworkManager-wait-online
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Problem**: ``NetworkManager-wait-online.service`` waits 6+ seconds for network

This service delays boot until network is fully connected. Most systems work fine without it.

**Solution - Disable Waiting**::

    sudo systemctl disable NetworkManager-wait-online.service

.. note::
   Your network will still work normally. This only removes the requirement to wait for network before continuing boot.

**Expected Savings**: ~6-7 seconds ✅

Optional Service Optimizations
-------------------------------

Optimize Development Services
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If you're running development services (Elasticsearch, RabbitMQ, Redis, MySQL), consider starting them manually when needed instead of at boot.

**Elasticsearch**

If you don't need search indexing immediately::

    # Disable automatic start
    sudo systemctl disable elasticsearch.service

    # Start manually when needed
    sudo systemctl start elasticsearch.service

**Expected Savings**: ~17 seconds

**RabbitMQ**

If you don't use message queuing at boot::

    sudo systemctl disable rabbitmq-server.service

**Expected Savings**: ~4 seconds

**Redis**

If you don't need caching immediately::

    sudo systemctl disable redis-server.service

**Expected Savings**: ~0.2 seconds

**MySQL/MariaDB**

If you don't need database at boot::

    sudo systemctl disable mysql.service

**Expected Savings**: ~3.6 seconds

.. tip::
   **Auto-start on demand**: These services can be configured with socket activation to start automatically when first accessed. See ``systemd.socket`` documentation.

Manage Snap Services
~~~~~~~~~~~~~~~~~~~~~

Snap packages can slow boot time. Each snap mounts a loop device.

**Check Installed Snaps**::

    snap list

**Remove Unused Snaps**::

    sudo snap remove <package-name>

**Example - Remove Unused Applications**::

    # Remove Figma if not used
    sudo snap remove figma-linux

    # Remove old GNOME versions
    sudo snap remove gnome-3-28-1804

.. note::
   Removing unused snaps reduces boot time and frees disk space.

Optimize Docker
~~~~~~~~~~~~~~~

Docker service takes ~1.2 seconds. If you don't need containers immediately::

    sudo systemctl disable docker.service
    sudo systemctl disable containerd.service

Start Docker when needed::

    sudo systemctl start docker.service

Performance Enhancement Tools
------------------------------

Install Preload
~~~~~~~~~~~~~~~

Preload monitors frequently used applications and preloads them into RAM.

**Installation**::

    sudo apt update
    sudo apt install preload

**Enable and Start**::

    sudo systemctl enable --now preload

**How It Works**:

- Monitors which applications you use most
- Preloads them into memory during idle time
- Speeds up application launch times
- Uses ~50-100MB RAM

.. tip::
   Preload learns your usage patterns over time. Allow 1-2 weeks for optimal performance.

**Expected Impact**: Faster application launch (not boot time)

Install TLP (Laptops)
~~~~~~~~~~~~~~~~~~~~~

TLP provides advanced power management for laptops, optimizing battery life without manual configuration.

**What is TLP?**

TLP is a feature-rich power management tool that applies power-saving settings automatically:

- CPU frequency scaling
- PCIe Active State Power Management (ASPM)
- USB autosuspend
- Disk power management
- Battery charge thresholds
- Better battery life

.. note::
   TLP is specifically designed for **laptops**. Desktop users may not see significant benefits.

**Installation Steps**

**Step 1: Install TLP**::

    sudo apt update
    sudo apt install tlp tlp-rdw

.. tip::
   ``tlp-rdw`` provides Radio Device Wizard support for WiFi and Bluetooth power management.

**Step 2: Start TLP Service**

Manually start TLP to apply power-saving settings immediately::

    sudo tlp start

✅ **Safe**: This command applies power-saving settings (CPU scaling, PCIe ASPM, USB autosuspend, etc.) without permanent kernel changes.

**Step 3: Check TLP Status**

Verify TLP is running correctly::

    sudo tlp-stat -s

**Example Output**::

    --- TLP 1.5.0 --------------------------------------------

    +++ System Info
    System         = Dell Inc. Latitude 5500
    BIOS           = 1.20.0
    Release        = Linux Mint 21.3
    Kernel         = 5.15.0-157-generic #167-Ubuntu SMP x86_64
    /proc/cmdline  = BOOT_IMAGE=/boot/vmlinuz-5.15.0-157-generic

    +++ TLP Status
    State          = enabled
    Last run       = 18:30:15,   5432 sec(s) ago
    Mode           = battery
    Power source   = battery

✅ **Safe**: This is a read-only command that displays status without changing system state.

**Enable TLP at Boot (Optional)**

TLP usually enables itself automatically during installation, but you can verify::

    sudo systemctl enable tlp
    sudo systemctl status tlp

**Verify Auto-start**::

    systemctl is-enabled tlp

**Example Output**::

    enabled

**View Detailed Configuration**

To see all TLP settings and current values::

    sudo tlp-stat

This shows comprehensive information about:

- Power source detection
- CPU settings
- Disk settings
- PCIe settings
- USB settings
- Battery status and thresholds

**Reverting TLP (If Needed)**

If you experience issues or want to remove TLP:

**Stop TLP Service**::

    sudo systemctl stop tlp

**Disable TLP at Boot**::

    sudo systemctl disable tlp

**Completely Remove TLP**::

    sudo apt remove --purge tlp tlp-rdw
    sudo apt autoremove

**Verify Removal**::

    dpkg -l | grep tlp

Should return no results after removal.

**Safety Considerations**

✅ **TLP is Safe Because**:

- No permanent kernel modifications
- Can be stopped/removed anytime
- Settings revert when service stops
- Widely used and well-tested
- Official Ubuntu/Debian packages

⚠️ **Rare Edge Cases**:

- Some older hardware may have compatibility issues
- Gaming laptops may see slight performance reduction on battery
- Can be easily disabled if any issues occur

**Expected Impact**:

- Significantly better battery life (20-40% improvement typical)
- Slight performance optimization
- Automatic power profile switching
- No impact on boot time

Install apt-fast
~~~~~~~~~~~~~~~~

apt-fast speeds up package downloads using parallel connections.

**Installation**::

    sudo add-apt-repository ppa:apt-fast/stable
    sudo apt update
    sudo apt install apt-fast

**Usage**::

    # Use apt-fast instead of apt
    sudo apt-fast install package-name
    sudo apt-fast update
    sudo apt-fast upgrade

**How It Works**:

- Uses aria2c for parallel downloads
- Downloads packages faster with multiple connections
- Compatible with apt command syntax

**Expected Impact**: Faster package installation (not boot time)

Manual Step-by-Step Guide
--------------------------

If you prefer manual optimization, follow these steps:

Step 1: Analyze Current Boot Time
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    # Check overall boot time
    systemd-analyze time

    # Identify slow services
    systemd-analyze blame | head -20

Step 2: Fix fstrim Service
~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    sudo systemctl disable fstrim.service
    sudo systemctl enable fstrim.timer
    sudo systemctl start fstrim.timer
    systemctl status fstrim.timer

Step 3: Optimize plocate
~~~~~~~~~~~~~~~~~~~~~~~~~

::

    sudo systemctl mask plocate-updatedb.service
    systemctl list-timers | grep plocate

Step 4: Disable Network Wait
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    sudo systemctl disable NetworkManager-wait-online.service

Step 5: Reboot and Verify
~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    sudo reboot

    # After reboot
    systemd-analyze time
    systemd-analyze blame

Monitoring and Maintenance
---------------------------

Regular Boot Time Checks
~~~~~~~~~~~~~~~~~~~~~~~~

**Create Monitoring Script**

.. code-block:: bash
   :caption: check-boot-time.sh

   #!/bin/bash

   echo "=== Boot Time Report ==="
   echo ""
   echo "Overall Boot Time:"
   systemd-analyze time
   echo ""
   echo "Top 10 Slowest Services:"
   systemd-analyze blame | head -10
   echo ""
   echo "Critical Chain:"
   systemd-analyze critical-chain

**Run Periodically**::

    chmod +x check-boot-time.sh
    ./check-boot-time.sh

Compare Boot Times
~~~~~~~~~~~~~~~~~~

**Track Improvements**::

    # Before optimization
    systemd-analyze time > boot-time-before.txt

    # After optimization
    systemd-analyze time > boot-time-after.txt

    # Compare
    diff boot-time-before.txt boot-time-after.txt

Troubleshooting
---------------

Common Issues
~~~~~~~~~~~~~

**Boot Slower After Optimization**

If boot time increased:

#. Check which service is now slower::

       systemd-analyze blame

#. Review recent changes::

       systemctl list-unit-files --state=masked
       systemctl list-unit-files --state=disabled

#. Re-enable critical service if needed::

       sudo systemctl unmask service-name.service
       sudo systemctl enable service-name.service

**Service Fails to Start**

Check service status::

    systemctl status service-name.service
    journalctl -u service-name.service

**fstrim Not Running**

Verify timer is active::

    systemctl list-timers | grep fstrim
    systemctl status fstrim.timer

Rollback Optimizations
~~~~~~~~~~~~~~~~~~~~~~~

**Restore Previous State**

If you saved backups with the optimization script::

    cd ~/boot-optimization-backup/
    cat enabled-services-*.txt

Re-enable services::

    sudo systemctl enable service-name.service
    sudo systemctl unmask service-name.service

Best Practices
--------------

Do's
~~~~

✅ **Always backup before optimizing**

- List enabled services before changes
- Document what you disable
- Test after each major change

✅ **Start with safe optimizations**

- Fix fstrim timer first (biggest impact)
- Disable NetworkManager-wait-online (safe)
- Optimize plocate database updates

✅ **Monitor boot time regularly**

- Run ``systemd-analyze`` monthly
- Check for new slow services
- Review system logs for issues

✅ **Test thoroughly**

- Reboot after each optimization
- Verify all applications work
- Check network connectivity
- Test database connections

Don'ts
~~~~~~

❌ **Don't disable critical services**

- Network Manager
- systemd-logind
- dbus
- udev

❌ **Don't disable without understanding**

- Research service purpose first
- Check dependencies
- Test in safe environment

❌ **Don't optimize firmware/BIOS time**

- Firmware optimization is risky
- Minimal benefit
- Can brick system

Security Considerations
~~~~~~~~~~~~~~~~~~~~~~~

- Disabling services may affect security updates
- Some services provide security monitoring
- Keep ``apparmor`` and ``ufw`` enabled
- Don't disable ``systemd-resolved``

.. warning::
   Never disable security-related services like ``apparmor``, ``fail2ban``, or ``ufw`` for boot optimization.

Expected Results
----------------

Benchmark Comparison
~~~~~~~~~~~~~~~~~~~~

**Before Optimization**::

    Startup finished in 12.268s (firmware) + 3.567s (loader) + 4.219s (kernel) + 26.927s (userspace) = 46.983s

**After Safe Optimizations**::

    Startup finished in 12.268s (firmware) + 3.567s (loader) + 4.219s (kernel) + 8.500s (userspace) = 28.554s

**Improvement**: ~18 seconds faster (39% reduction)

**With Optional Service Disabling**::

    Startup finished in 12.268s (firmware) + 3.567s (loader) + 4.219s (kernel) + 4.500s (userspace) = 24.554s

**Improvement**: ~22 seconds faster (47% reduction)

Service-by-Service Savings
~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. list-table::
   :header-rows: 1
   :widths: 40 20 20 20

   * - Optimization
     - Time Saved
     - Safety
     - Recommended
   * - fstrim.service → timer
     - 152s
     - ✅ Safe
     - ✅ Yes
   * - plocate-updatedb → mask
     - 45s
     - ✅ Safe
     - ✅ Yes
   * - NetworkManager-wait-online
     - 7s
     - ✅ Safe
     - ✅ Yes
   * - Elasticsearch disable
     - 17s
     - ⚠️ Optional
     - If unused
   * - RabbitMQ disable
     - 4s
     - ⚠️ Optional
     - If unused
   * - MySQL disable
     - 3.6s
     - ⚠️ Optional
     - If unused
   * - Docker disable
     - 1.2s
     - ⚠️ Optional
     - If unused

Resources
---------

Official Documentation
~~~~~~~~~~~~~~~~~~~~~~

- **systemd Documentation**: https://www.freedesktop.org/wiki/Software/systemd/
- **systemd-analyze Man Page**: https://www.freedesktop.org/software/systemd/man/systemd-analyze.html
- **Ubuntu Boot Optimization**: https://wiki.ubuntu.com/BootSpeed

Useful Tutorials
~~~~~~~~~~~~~~~~

- It's FOSS Boot Speed Guide: https://itsfoss.com/speed-up-ubuntu-1310/
- Arch Linux Boot Optimization: https://wiki.archlinux.org/title/Improving_performance/Boot_process
- Red Hat Performance Tuning: https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/

Related Guides
~~~~~~~~~~~~~~

- :doc:`../system-information/index` - System information commands
- :doc:`../linux-commands/index` - General Linux commands
- :doc:`../package-management/index` - Package management

Quick Reference
---------------

Essential Commands
~~~~~~~~~~~~~~~~~~

**Analysis**::

    systemd-analyze time              # Overall boot time
    systemd-analyze blame             # Service-by-service breakdown
    systemd-analyze critical-chain    # Critical path analysis
    systemd-analyze plot > boot.svg   # Visual timeline

**Safe Optimizations**::

    # Fix fstrim
    sudo systemctl disable fstrim.service
    sudo systemctl enable fstrim.timer

    # Fix plocate
    sudo systemctl mask plocate-updatedb.service

    # Disable network wait
    sudo systemctl disable NetworkManager-wait-online.service

**Service Management**::

    systemctl list-unit-files         # List all services
    systemctl is-enabled service      # Check if enabled
    systemctl status service          # Service status
    systemctl disable service         # Disable service
    systemctl enable service          # Enable service
    systemctl mask service            # Mask service
    systemctl unmask service          # Unmask service

Conclusion
----------

Boot time optimization can significantly improve your Linux experience by reducing startup delays and identifying resource-intensive services. By following the safe optimizations in this guide, you can typically reduce boot time by 40-50%.

Key takeaways:

- Use ``systemd-analyze`` to identify bottlenecks
- Fix fstrim service for immediate 2+ minute improvement
- Disable services you don't need at boot
- Use timers for maintenance tasks instead of boot-time execution
- Monitor boot time regularly
- Always backup before making changes
- Test thoroughly after optimizations

Remember: **A faster boot doesn't mean better system performance**. Focus on services that delay boot without providing immediate value, but keep essential services enabled for system stability and functionality.

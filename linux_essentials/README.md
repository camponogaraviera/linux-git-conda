<!-- Header: -->
<div align="center"> 
  <a href="https://www.linux.org/">
    <img align="center" src="https://www.linux.org/images/logo.png" alt="linux" />
  </a>
  <h1> Linux Essentials </h1>
</div>

Check out [explainshell.com](https://explainshell.com/) for an interactive alternative to Linux man pages that enables you to quick parse queried commands.

# Table of Contents

- [Terminal Keyboard Shortcuts](#terminal-keyboard-shortcuts)
- [Ubuntu Preliminaries](#ubuntu-preliminaries)
- [Package Management](#package-management)
- [TAR-based Files](#tar-based-files)
- [Shell Scripts (.sh files)](#shell-scripts-sh-files)
- [Debian Packages](#debian-packages)
- [Directory Operations](#directory-operations)
- [File Operations](#file-operations)
- [System Information](#system-information)
- [Process Management](#process-management)
- [Disk & Partition Management](#disk--partition-management)
    
# Terminal Keyboard Shortcuts

For QWERTY-based keyboard layouts on Linux systems.

- `Ctrl+Shift+C`: Copy selection (Windows: `Ctrl+C`).
- `Ctrl+Shift+V`: Paste selection (Windows: `Ctrl+V`).
- `Ctrl+Shift+T`: Open a new tab.
- `Ctrl+PgUp`: Switch to the previous tab.
- `Ctrl+PgDn`: Switch to the next tab.
- `Ctrl+Shift+W`: Close the current tab.
- `Ctrl+R`: Search command history.
- `Ctrl+G`: Exit command history search mode.
- `Ctrl+I` / `Tab`: Trigger command line suggestions.
- `Ctrl+A` / `Home`: Move to the beginning of the command line.
- `Ctrl+E` / `End`: Move to the end of the command line.
- `Ctrl+W` / `Alt+Backspace`: Delete an entire word before the cursor.
- `Alt+D`: Delete an entire word after the cursor.
- `Ctrl+U`: Delete the entire command.
- `Ctrl+C`: Send a SIGINT signal to terminate the current process.

<!--- ############################################################################################################################################### -->

## Ubuntu Preliminaries

**Note:** Angle brackets (`<>`) indicate placeholders, not special characters.

- **Check Ubuntu version:**
  ```bash
  lsb_release -a
  ```
- **Current user information:**
  ```bash
  who
  ```
- **Display manual page for a command:**
  ```bash
  man <command>
  ```
- **Brief description of a command:**
  ```bash
  whatis <command>
  ```
- **Open GNOME file manager:**
  ```bash
  nautilus .
  ```
- **Switch to root user:**
  ```bash
  sudo su
  ```
- **Locate command files:**
  ```bash
  whereis <command>
  ```
- **Find the path of a command:**
  ```bash
  which <command>
  ```

<!--- ############################################################################################################################################### -->

## Package Management

- **Add an external repository:**
  ```bash
  sudo add-apt-repository <repository>
  ```
- **Update package list:**
  ```bash
  sudo apt-get update
  ```
- **Install a package:**
  ```bash
  sudo apt-get install <package-name>
  ```
- **Uninstall a package:**
  ```bash
  sudo apt-get purge --auto-remove <package-name>
  sudo apt-get clean  # Remove aptitude cache
  ```
- **List installed packages:**
  ```bash
  dpkg --list # Type `q` to exit
  apt list --installed
  apt list -a <package_name>
  ```

<!--- ############################################################################################################################################### -->

## TAR-based Files

- **Extract files:**
  ```bash
  tar -xvzf <filename>.tar.gz    # For .gz files
  tar -xvjf <filename>.tar.bz2   # For .bz2 files
  tar -xf <filename>.tar.xz      # For .xz files
  gunzip <filename>.gz           # For .gz files
  ```
- **Install extracted package:**
  ```bash
  ./configure && make && sudo make install
  ```

<!--- ############################################################################################################################################### -->

## Shell Scripts (.sh Files)

- **Grant execute permission:**
  ```bash
  chmod +x <filename>.sh
  ```
- **Run script:**
  ```bash
  ./<filename>.sh
  ```

<!--- ############################################################################################################################################### -->

## Debian Packages

- **Install a package:**
  ```bash
  sudo dpkg -i package.deb
  ```
- **Remove a package:**
  ```bash
  sudo dpkg -r package.deb
  ```

<!--- ############################################################################################################################################### -->

## Directory Operations

- **Print current directory path:** `pwd`
- **Create a directory:** `mkdir <dir-name>`
- **Remove an empty directory:** `rmdir <dir-name>`
- **Remove a non-empty directory:** `rm -rf <dir-name>`
- **Switch to directory:** `cd <dir-name>`
- **Go up one level:** `cd ..`
- **Go to the previous directory:** `cd -`
- **Go to the root directory:** `cd /`
- **Go to the home directory:** `cd ~`

<!--- ############################################################################################################################################### -->

## File Operations

- **List files:**
  ```bash
  ls     # Show basic list
  ll     # Show hidden files
  ls -l  # Show detailed list
  ls -s  # Show allocated size of each file in blocks
  ```
- **Find a file:**
  ```bash
  find <filename>      # List a specific file
  ```
  ```bash
  find . -name "*.jpg" # List all files in the current directory with extension .jpg
  ```
- **Check file properties:**
  ```bash
  stat <filename>
  ```
- **Read a file:**
  ```bash
  less <filename>
  nano <filename>
  gedit <filename>
  evince <filename.pdf>
  ```
- **Create a file:**
  ```bash
  cat > <filename>.txt
  ```
  ```bash
  echo "This is a string" > <filename>.txt
  ```
- **Append to a file:**
  ```bash
  echo "New content" >> <filename>.txt
  ```
- **Copy a file:**
  ```bash
  cp <filename> <destination>
  ```
- **Move/Rename a file:**
  ```bash
  mv <filename> <new-filename>
  ```
- **Delete a file:**
  ```bash
  rm <filename>
  ```

<!--- ############################################################################################################################################### -->

## System Information

- **Sys/Kernel/Dist version:**
  ```bash
  uname -a                      # System info
  uname -srmv                   # Kernel version 
  uname -m && cat /etc/*release # Distribution info
  ```
- **CPU info:**
  ```bash
  lscpu
  Note: total threads = CPU core * threads per core.
  ```
- **RAM information:**
  ```bash
  sudo inxi -m
  sudo inxi -F
  sudo lshw -short -C memory
  free -h
  ```
  ```bash
  'free' = wasted memory (not being used)
  'available' = memory for allocation
  'buff/cache' = used memory for cache (Data has been read) and buffer (data is being written)
  'free' + 'buff/cache' = 'available'
  ```
- **List PCI devices (e.g., GPU, network card):**
  ```bash
  lspci -v
  lspci -v -s <id>
  lshw
  sudo lshw -C display
  ```
- **Check NVIDIA GPU status:**
  ```bash
  nvidia-smi
  ```

<!--- ############################################################################################################################################### -->

## Process Management

- **Show running processes:** `top`
- **List all processes:** `ps -A`
- **Find a process:** `ps aux | grep <process>`
- **Display process PID:** `pgrep <process>`
- **Kill a process:** `sudo kill -9 <PID>`

<!--- ############################################################################################################################################### -->

## Disk & Partition Management

- **List partitions:**
  ```bash
  sudo fdisk -l
  ```
- **Show mounted drives:**
  ```bash
  df -h
  ```
- **Mount a partition:**
  ```bash
  sudo mount /dev/sdbX
  ```

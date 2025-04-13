# **Linux Fundamental Commands with Examples**

## **Basic Navigation & File Operations**

1. **`clear`** - Clears the terminal screen  
   ```bash
   clear
   ```

2. **`echo`** - Prints text to the terminal  
   ```bash
   echo "Hello Dosto"
   ```

3. **`pwd`** - Prints current working directory  
   ```bash
   pwd
   ```

4. **`mkdir`** - Creates a new directory  
   ```bash
   mkdir devops
   ```

5. **`ls`** - Lists directory contents  
   ```bash
   ls
   ls -l      # Detailed list
   ls -a      # Show hidden files
   ```

6. **`touch`** - Creates an empty file  
   ```bash
   touch my-file.txt
   ```

7. **`cd`** - Changes directory  
   ```bash
   cd devops/      # Enter directory
   cd ..           # Go up one level
   cd ~            # Go to home directory
   cd /            # Go to root directory
   ```

## **File Management**

8. **`mv`** - Moves or renames files  
   ```bash
   mv my-file.txt devops/      # Move file
   mv old.txt new.txt          # Rename file
   ```

9. **`cp`** - Copies files  
   ```bash
   cp demo.txt devops/
   cp -r dir1/ dir2/          # Copy directory recursively
   ```

10. **`rm`** - Removes files  
    ```bash
    rm demo.txt               # Delete file
    rm -r demo/               # Delete directory recursively
    rm -v file.txt            # Verbose deletion
    ```

11. **`rmdir`** - Removes empty directory  
    ```bash
    rmdir demo/
    ```

## **System Information**

12. **`whoami`** - Shows current user  
    ```bash
    whoami
    ```

13. **`hostname`** - Shows system hostname  
    ```bash
    hostname
    ```

14. **`man`** - Shows command manual  
    ```bash
    man ls
    man mkdir
    ```

15. **`cat`** - Displays file contents  
    ```bash
    cat commands.txt
    cat /etc/passwd          # View system users
    ```

## **Text Editors**

16. **`vim`** - Powerful text editor  
    ```bash
    vim commands.txt
    ```

17. **`nano`** - Simple text editor  
    ```bash
    nano demo-file.txt
    ```

## **Package Management (Ubuntu/Debian)**

18. **`apt-get`** - Package manager commands  
    ```bash
    sudo apt-get update              # Update package list
    sudo apt-get upgrade             # Upgrade packages
    sudo apt-get install nginx       # Install package
    ```

## **Process & Service Management**

19. **`systemctl`** - Controls system services  
    ```bash
    systemctl status nginx     # Check service status
    sudo systemctl stop nginx  # Stop service
    sudo systemctl start nginx # Start service
    ```

## **User Management**

20. **`useradd`** - Creates new user  
    ```bash
    sudo useradd -m username -s /bin/bash
    ```

21. **`passwd`** - Sets user password  
    ```bash
    sudo passwd username
    ```

22. **`su`** - Switch user  
    ```bash
    su username               # Switch to user
    exit                      # Return to previous user
    ```

## **Network Commands**

23. **`ifconfig`** - Network interface info  
    ```bash
    ifconfig
    ```

24. **`ping`** - Test network connection  
    ```bash
    ping google.com
    ```

## **Special Directories**

25. **Exploring system directories**  
    ```bash
    cd /var/www/html/        # Web server files
    cd /etc/                 # Configuration files
    cd /tmp/                 # Temporary files
    cd /home/                # User directories
    ```

## **Useful Shortcuts**

26. **`Ctrl+C`** - Cancel current command  
27. **`Ctrl+L`** - Clear screen (alternative to `clear`)
28. **`Tab`** - Auto-complete filenames/commands
29. **`Up/Down`** - Navigate command history

## **Recommended Learning Resource**
For a complete Linux tutorial, watch:  
👉 **[Linux for Beginners (Full Course)](https://www.youtube.com/watch?v=e01GGTKmtpc&t=6876s)**  

Practice these commands daily to become proficient in Linux! 🐧

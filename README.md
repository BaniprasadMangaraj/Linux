# DevOps Engineer's Common Linux Commands

Welcome to the Linux Command Encyclopedia – your ultimate one-stop repository for mastering Linux from fundamentals to advanced levels! This repo is meticulously curated to cover everything from A to Z about Linux commands, concepts, and best practices.

## File System Operations

### `ls` - List directory contents
```bash
$ ls -l
total 12
drwxr-xr-x 2 user user 4096 Jan 10 10:00 dir1
-rw-r--r-- 1 user user  220 Jan 10 09:30 file1.txt
-rwxr-xr-x 1 user user 1234 Jan 10 09:35 script.sh
```

### `cd` - Change directory
```bash
$ cd /var/log
$ pwd
/var/log
```

### `mkdir` - Make directories
```bash
$ mkdir new_directory
$ ls
new_directory file1.txt
```

### `rm` - Remove files/directories
```bash
$ rm file1.txt
$ ls
new_directory
```

### `cp` - Copy files/directories
```bash
$ cp file1.txt file1_backup.txt
$ ls
file1.txt file1_backup.txt
```

### `mv` - Move/rename files
```bash
$ mv file1.txt renamed_file.txt
$ ls
renamed_file.txt
```

## File Viewing/Editing

### `cat` - Concatenate and display file content
```bash
$ cat config.yml
server:
  port: 8080
  host: 0.0.0.0
```

### `less` - View file content interactively
```bash
$ less large_log_file.log
[file content displayed interactively]
```

### `tail` - Display last part of file
```bash
$ tail -f /var/log/syslog
Jan 10 10:00:01 server CRON[1234]: (root) CMD (command)
Jan 10 10:01:01 server systemd[1]: Started Daily apt upgrade and clean.
```

### `grep` - Search text using patterns
```bash
$ grep "error" /var/log/syslog
Jan 10 09:45:22 server kernel: [123.456] ERROR: Something went wrong
```

## System Monitoring

### `top` - Display Linux processes
```bash
$ top
top - 10:00:00 up 30 days,  2:30,  1 user,  load average: 0.15, 0.10, 0.05
Tasks: 120 total,   2 running, 118 sleeping,   0 stopped,   0 zombie
%Cpu(s):  2.3 us,  1.0 sy,  0.0 ni, 96.7 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
MiB Mem :   7986.8 total,   1024.2 free,   4096.0 used,   2866.6 buff/cache
MiB Swap:   2048.0 total,   2048.0 free,      0.0 used.   3240.8 avail Mem
```

### `htop` - Interactive process viewer
```bash
$ htop
[Interactive process viewer with color and mouse support]
```

### `df` - Disk space usage
```bash
$ df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        50G   15G   33G  32% /
/dev/sdb1       200G   50G  150G  25% /data
```

### `free` - Memory usage
```bash
$ free -m
              total        used        free      shared  buff/cache   available
Mem:           7986        4096        1024         123        2866        3240
Swap:          2048           0        2048
```

## Network Operations

### `ping` - Test network connectivity
```bash
$ ping google.com
PING google.com (172.217.0.46) 56(84) bytes of data.
64 bytes from lga25s59-in-f14.1e100.net (172.217.0.46): icmp_seq=1 ttl=115 time=12.3 ms
```

### `netstat` - Network statistics
```bash
$ netstat -tulnp
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      1234/sshd
tcp6       0      0 :::80                   :::*                    LISTEN      5678/nginx
```

### `ss` - Socket statistics
```bash
$ ss -tuln
Netid  State   Recv-Q  Send-Q   Local Address:Port    Peer Address:Port
tcp    LISTEN  0       128      0.0.0.0:22           0.0.0.0:*
tcp    LISTEN  0       128      [::]:80              [::]:*
```

### `curl` - Transfer data from/to server
```bash
$ curl -I example.com
HTTP/1.1 200 OK
Content-Type: text/html; charset=UTF-8
Server: nginx/1.18.0
Date: Mon, 10 Jan 2022 10:00:00 GMT
```

## Package Management

### `apt` (Debian/Ubuntu)
```bash
$ apt update
Hit:1 http://archive.ubuntu.com/ubuntu focal InRelease
Get:2 http://archive.ubuntu.com/ubuntu focal-updates InRelease [114 kB]
...
```

### `yum` (RHEL/CentOS)
```bash
$ yum install nginx
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * base: mirror.rackspace.com
 * extras: mirror.rackspace.com
 * updates: mirror.rackspace.com
Resolving Dependencies
--> Running transaction check
---> Package nginx.x86_64 1:1.20.1-1.el7 will be installed
```

## Process Management

### `ps` - Process status
```bash
$ ps aux | grep nginx
root      1234  0.0  0.1 123456  7890 ?        Ss   10:00   0:00 nginx: master process
www-data  5678  0.0  0.0 123456  1234 ?        S    10:00   0:00 nginx: worker process
```

### `kill` - Terminate processes
```bash
$ kill -9 1234
[Process 1234 terminated]
```

### `systemctl` - Control systemd services
```bash
$ systemctl status nginx
● nginx.service - A high performance web server and a reverse proxy server
   Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset: enabled)
   Active: active (running) since Mon 2022-01-10 10:00:00 UTC; 5min ago
```

## Permissions

### `chmod` - Change file permissions
```bash
$ chmod 755 script.sh
$ ls -l script.sh
-rwxr-xr-x 1 user user 1234 Jan 10 10:00 script.sh
```

### `chown` - Change file owner
```bash
$ chown www-data:www-data /var/www/html
$ ls -ld /var/www/html
drwxr-xr-x 2 www-data www-data 4096 Jan 10 10:00 /var/www/html
```

## Text Processing

### `awk` - Pattern scanning and processing
```bash
$ awk '{print $1}' access.log
192.168.1.1
10.0.0.1
192.168.1.2
```

### `sed` - Stream editor
```bash
$ sed 's/foo/bar/g' file.txt
[file content with all 'foo' replaced by 'bar']
```

### `sort` - Sort lines of text
```bash
$ sort -u access.log | head -3
10.0.0.1 - - [10/Jan/2022:10:00:01 +0000] "GET / HTTP/1.1" 200 1234
192.168.1.1 - - [10/Jan/2022:10:00:02 +0000] "GET /about HTTP/1.1" 200 5678
192.168.1.2 - - [10/Jan/2022:10:00:03 +0000] "POST /login HTTP/1.1" 302 -
```

## Compression/Archiving

### `tar` - Tape archive
```bash
$ tar -czvf archive.tar.gz directory/
directory/
directory/file1.txt
directory/file2.txt
```

### `gzip` - Compression
```bash
$ gzip file.txt
$ ls
file.txt.gz
```

## SSH

### `ssh` - Secure shell client
```bash
$ ssh user@remote-server
user@remote-server's password: 
Last login: Mon Jan 10 09:30:00 2022 from 192.168.1.1
user@remote-server:~$
```

### `scp` - Secure copy
```bash
$ scp file.txt user@remote-server:/home/user/
user@remote-server's password: 
file.txt                                  100% 1234     1.2MB/s   00:00
```

## Version Control (Git)

### `git clone` - Clone repository
```bash
$ git clone https://github.com/user/repo.git
Cloning into 'repo'...
remote: Enumerating objects: 100, done.
remote: Counting objects: 100% (100/100), done.
remote: Compressing objects: 100% (80/80), done.
Receiving objects: 100% (100/100), 123.45 KiB | 1.23 MiB/s, done.
Resolving deltas: 100% (20/20), done.
```

### `git status` - Show working tree status
```bash
$ git status
On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
```

## Containerization

### `docker ps` - List containers
```bash
$ docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED       STATUS       PORTS                  NAMES
a1b2c3d4e5f6   nginx:latest   "/docker-entrypoint.…"   2 hours ago   Up 2 hours   0.0.0.0:80->80/tcp     webserver
```

### `docker images` - List images
```bash
$ docker images
REPOSITORY   TAG       IMAGE ID       CREATED        SIZE
nginx        latest    abc123def456   2 weeks ago    133MB
ubuntu       20.04     def456abc123   3 weeks ago    72.9MB
```


## **🎥 Recommended YouTube Resource**  
For a **detailed Linux tutorial**, watch:  
👉 **[Linux for Beginners (Full Course)](https://www.youtube.com/watch?v=e01GGTKmtpc&t=6876s)**  



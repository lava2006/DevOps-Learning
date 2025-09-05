# Linux Commands for DevOps Engineer

## Introduction

Linux forms the backbone of modern cloud and DevOps infrastructures. Mastering essential Linux commands empowers DevOps professionals to manage servers, automate workflows, troubleshoot issues, and maintain robust CI/CD pipelines effectively.

---

## Basic File and Directory Commands

- ls  
  Lists files and directories.  
  *Example:* ls -la lists all files including hidden ones with detailed info.

- cd  
  Changes the current directory.  
  *Example:* cd /var/log navigates to the system log directory.

- pwd  
  Prints the present working directory path.

- mkdir  
  Creates directories.  
  *Example:* mkdir my_project

- rm  
  Deletes files/directories (use with caution).  
  *Example:* rm file.txt or rm -r folder for recursive deletion.

---

## File Viewing and Editing

- cat  
  Displays file content.  
  *Example:* cat /etc/passwd

- less / more  
  View long files page by page.  
  *Example:* less /var/log/syslog

- head / tail  
  Show start/end of files.  
  *Example:* tail -f /var/log/nginx/access.log (live log output).

- nano / vim  
  Command-line editors for file modification.

---

## Process Management

- ps  
  Lists running processes.  
  *Example:* ps aux | grep nginx

- top / htop  
  Interactive process viewer.

- kill  
  Stops a process by PID.  
  *Example:* kill 1234

- systemctl  
  Controls systemd services.  
  *Example:* sudo systemctl restart nginx

---

## Networking Commands

- ping  
  Tests network connectivity.  
  *Example:* ping google.com

- netstat / ss  
  Shows network connections and listening ports.

- curl / wget  
  Makes HTTP requests or downloads files.

- ifconfig / ip  
  Displays or configures network interfaces.  
  *Example:* ip a

---

## Disk and Storage

- df  
  Shows disk space usage.  
  *Example:* df -h

- du  
  Displays directory space usage.  
  *Example:* du -sh /var/log

- mount / umount  
  Mount and unmount filesystems.

---

## User and Permissions Management

- chmod  
  Changes file permissions.  
  *Example:* chmod 755 script.sh

- chown  
  Changes file ownership.  
  *Example:* sudo chown user:user file.txt

- useradd / userdel  
  Adds or deletes users.

---

## Package Management

- Debian/Ubuntu:  
  sudo apt update && sudo apt install package-name

- RHEL/CentOS:  
  sudo yum install package-name

---

## Shell Scripting Essentials

Automate tasks with scripts. Example:
#!/bin/bash
echo "Deploying application..."
git pull origin main
docker-compose up -d
echo "Deployment done!"

---

## Logs and Monitoring

- journalctl  
  View system logs.  
  *Example:* journalctl -u nginx

- tail -f  
  Follow log updates live.

---

## Useful Resources
  
- [Linux Tutorial for Beginners (YouTube)](https://www.youtube.com/watch?v=ivdITTVGCe8)  
- [The Bash Guide](https://guide.bash.academy/)  
- [GitHub Learning Lab](https://lab.github.com/)  

---

This document is part of my DevOps learning documentation and will be continuously updated.

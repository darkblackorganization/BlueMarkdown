### Introduction

Linux is a powerful open-source operating system widely used in servers, cloud platforms, and DevOps environments. Whether you're managing servers, deploying applications, or automating workflows, Linux commands are the backbone of daily operations.



#  Linux Basics

### Show current directory path
```bash
pwd
````

### List files and directories

```bash
ls
```

### List all files (including hidden)

```bash
ls -la
```

### Change directory

```bash
cd /path/to/folder
```

### Create new directory

```bash
mkdir folder_name
```

### Remove file or directory

```bash
rm -rf file_or_folder
```

### Copy files or directories

```bash
cp -r source destination
```

### Move or rename

```bash
mv old_name new_name
```

### Create empty file

```bash
touch file.txt
```

### View file content

```bash
cat file.txt
```

### Edit file

```bash
nano file.txt
```

### Change permissions

```bash
chmod 755 file
```

### Change ownership

```bash
chown user:group file
```

---

#  Process Management

### Show running processes

```bash
ps aux
```

### Real-time process monitor

```bash
top
```

### Interactive monitor

```bash
htop
```

### Kill process by PID

```bash
kill PID
```

### Force kill process

```bash
kill -9 PID
```

### Kill by process name

```bash
killall process_name
```

### Start process with priority

```bash
nice -n 10 command
```

### Change process priority

```bash
renice -n 5 PID
```

---

#  Package Management (Ubuntu/Debian)

### Update package list

```bash
apt update
```

### Upgrade packages

```bash
apt upgrade
```

### Install package

```bash
apt install package_name
```

### Remove package

```bash
apt remove package_name
```

### Remove with config

```bash
apt purge package_name
```

### Remove unused packages

```bash
apt autoremove
```

---

#  Networking

### Show IP address

```bash
ip a
```

### Show routing table

```bash
ip route
```

### Check connectivity

```bash
ping google.com
```

### Show active connections

```bash
ss -tulnp
```

### Download file

```bash
wget url
```

### Make API request

```bash
curl -X GET url
```

---

#  Disk & File System

### Show disk usage

```bash
df -h
```

### Show folder size

```bash
du -sh *
```

### List block devices

```bash
lsblk
```

### Mount filesystem

```bash
mount /dev/sdb1 /mnt
```

### Unmount filesystem

```bash
umount /mnt
```

---

#  Users & Permissions

### Show current user

```bash
whoami
```

### Show user details

```bash
id
```

### Create user

```bash
useradd username
```

### Set password

```bash
passwd username
```

### Switch user

```bash
su - username
```

### Run as admin

```bash
sudo command
```

---

#  Archive & Compression

### Create archive

```bash
tar -cvf file.tar folder/
```

### Extract archive

```bash
tar -xvf file.tar
```

### Compress archive

```bash
tar -czvf file.tar.gz folder/
```

### Extract compressed archive

```bash
tar -xzvf file.tar.gz
```

### Compress file

```bash
gzip file
```

### Decompress file

```bash
gunzip file.gz
```

---

#  Git (Version Control)

### Initialize repository

```bash
git init
```

### Clone repository

```bash
git clone url
```

### Check status

```bash
git status
```

### Stage changes

```bash
git add .
```

### Commit changes

```bash
git commit -m "message"
```

### Push changes

```bash
git push origin main
```

### Pull changes

```bash
git pull origin main
```

### List branches

```bash
git branch
```

### Create branch

```bash
git branch new-branch
```

### Switch branch

```bash
git checkout branch_name
```

---

#  Docker

### Build image

```bash
docker build -t app .
```

### Pull image

```bash
docker pull nginx
```

### Run container

```bash
docker run -d -p 80:80 nginx
```

### List containers

```bash
docker ps
```

### List all containers

```bash
docker ps -a
```

### List images

```bash
docker images
```

### Stop container

```bash
docker stop container_id
```

### Remove container

```bash
docker rm container_id
```

### Access container

```bash
docker exec -it container_id bash
```

---

#  Kubernetes (kubectl)

### List pods

```bash
kubectl get pods
```

### List services

```bash
kubectl get svc
```

### List nodes

```bash
kubectl get nodes
```

### Apply config

```bash
kubectl apply -f file.yaml
```

### Delete resources

```bash
kubectl delete -f file.yaml
```

### Pod details

```bash
kubectl describe pod pod_name
```

### View logs

```bash
kubectl logs pod_name
```

### Access pod

```bash
kubectl exec -it pod_name -- bash
```

---

#  CI/CD & System

### Start service

```bash
systemctl start service
```

### Stop service

```bash
systemctl stop service
```

### Restart service

```bash
systemctl restart service
```

### Service status

```bash
systemctl status service
```

### View logs

```bash
journalctl -u service
```

---

#  Monitoring & Logs

### Memory usage

```bash
free -m
```

### System uptime

```bash
uptime
```

### Performance stats

```bash
vmstat
```

### Disk I/O stats

```bash
iostat
```

### Live logs

```bash
tail -f logfile
```

### Search text

```bash
grep "text" file
```

---

#  Bonus One-Liners

### Find large files

```bash
du -ah / | sort -rh | head -20
```

### Find process using port

```bash
lsof -i :8080
```

### Watch command output

```bash
watch -n 1 "df -h"
```

---

#  Final Note

This cheat sheet is created to help developers and DevOps engineers quickly access important commands in real-world scenarios.

 Visit: **bluemd.in**
 Practice daily and level up your DevOps skills!


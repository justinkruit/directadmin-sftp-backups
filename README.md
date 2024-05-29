<p align="center"><a href="https://directadmin.com"><img src="https://directadmin.com/img/logo/logo_directadmin.svg" alt="Directadmin" width="440px"/></a></p>

## Description

A set of patched scripts to allow Directadmin to 

- store
- list
- download

backups over SSH using SFTP.

## Author of patches

Alex Grebenschikov, Poralix, (www.poralix.com), 2018-2023

## Version

- Last modified: Thu Dec  7 18:54:17 +07 2023
- Version: 1.2.poralix.3 $ Thu Dec  7 18:54:17 +07 2023
- Repository URL: https://github.com/poralix/directadmin-sftp-backups
- Report issues to URL: https://github.com/poralix/directadmin-sftp-backups/issues
- Home page: www.poralix.com

## History of versions

- Version: 0.1.poralix $ Tue Jan 30 12:43:50 +07 2018
- Version: 1.2.poralix $ Thu Sep 12 23:55:18 +07 2019: Updated per changes in https://www.directadmin.com/features.php?id=2488
- Version: 1.2.poralix.2 $ Wed Dec 11 20:30:29 +07 2019: Recursive creation of FTP folders on remote server
- Version: 1.2.poralix.3 $ Thu Dec  7 18:54:17 +07 2023: ZST support added

## Requirements

**For Debian servers**:

```
apt-get install sshpass
```

**For CentOS**:

```
yum install sshpass git -y
```

## Installation

```
cd /usr/local/directadmin/scripts/custom/
git clone https://github.com/justinkruit/directadmin-sftp-backups.git
cp -f directadmin-sftp-backups/ftp_download.php ./
cp -f directadmin-sftp-backups/ftp_list.php ./
cp -f directadmin-sftp-backups/ftp_upload.php ./
chmod 700 ftp_*.php
chown diradmin:diradmin ftp_*.php
```

If you are using a ssh key you need to change the user with which the script is being run to the owner of the ssh key (see: https://www.directadmin.com/features.php?id=2854).

## Usage

Go to directadmin `Admin login -> Admin Backup/Transfer` and set:

- Username: **real ssh username**
- Password: **real ssh password or full to SSH RSA key**
- Remote Path: **full path to a backup directory from a remote server**
- Port: **22**

The script will detect the specified port **22** and will use SFTP to connect to SSH port. 
If you want FTP/FTPS just change port to 21 and update other credentials (the same script 
can be used for FTP/FTPS/SSH/SFTP).

If you run sFTP, SSH on a different port modify the scripts and your port to the line:

```
SSH_PORTS="22 2200 22022";
```

The line exists in all 3 files:

- ftp_download.php
- ftp_list.php
- ftp_upload.php

Backup files in DirectAdmin might be named in the following formats depending on settings:

Without encryption:

- zstd=1 & backup_gzip=2 & encryption=0 => `admin.root.admin.tar.zst`
- zstd=0 & backup_gzip=1 & encryption=0 => `admin.root.admin.tar.gz`
- zstd=0 & backup_gzip=0 & encryption=0 => `admin.root.admin.tar`

With encryption:

- zstd=1 & backup_gzip=2 & encryption=1 => `admin.root.admin.tar.zst.enc`
- zstd=0 & backup_gzip=1 & encryption=1 => `admin.root.admin.tar.gz.enc`
- zstd=0 & backup_gzip=0 & encryption=1 => `admin.root.admin.tar.enc`



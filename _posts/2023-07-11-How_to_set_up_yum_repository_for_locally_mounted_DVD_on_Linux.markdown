---
title: "How to set up yum repository for locally-mounted DVD on Linux"
layout: post
date: 2023-07-11 20:16
image: /assets/images/markdown.jpg
headerImage: false
tag:
- linux
- yum
- repository
category: blog
author: marmojezz
description: Learn to set up yum repository for locally-mounted DVD on Linux
---

# How to set up yum repository for locally-mounted DVD on Linux


1. Download the Linux ISO from your linux distribuction that contains yum. (e.g.: Rocky Linux, Red Hat, CentOS, etc...)
2. Get superuser permission, e.g.:
    ```console
    [foo@bar ~]$ su
    Password: <type your password>
    [root@bar foo]#
    ```
3. Mount the Linux Binary DVD ISO to a directory like as /mnt/disc, e.g.:
    ```console
    [root@bar foo]# mkdir -p  /mnt/disc
    [root@bar foo]# mount -o loop Rocky-9.2-x86_64-dvd.iso /mnt/disc
    ```
4. If you use DVD media , you can mount it as showed below,
    ```console
    [root@bar foo]# mkdir -p  /mnt/disc
    [root@bar foo]# mount /run/media/foo/<unit_name>  /mnt/disc
    ```
5. Create the repository file with the correct path of DVD or ISO is mounted,
    ```console
    [root@bar foo]# vi /etc/yum.repos.d/new_media_dvd.repo
    ```
    Now, press <INSERT> and type the following text:
    ```
    [BaseOS]
    name=My Wonderfull BaseOS
    metadata_expire=-1
    gpgcheck=1
    enabled=1
    baseurl=file:///mnt/disc/BaseOS/
    gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release
    
    [AppStream]
    name=My Wonderfull AppStream
    metadata_expire=-1
    gpgcheck=1
    enabled=1
    baseurl=file:///mnt/disc/AppStream/
    gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release
    ```

6. Clear the cache,
    ```console
    [root@bar foo]# yum clean all
    ```


7, Check whether you are able to get the packages from this DVD repository
    ```console
    [root@bar foo]# yum repolist
    ```


If are no errors, then you can go ahead to install or update a package, e.g:
  ```console
  [root@bar foo]# yum check-update 
  [root@bar foo]# yum update 
  [root@bar foo]# yum install <Package-Name>
  ```

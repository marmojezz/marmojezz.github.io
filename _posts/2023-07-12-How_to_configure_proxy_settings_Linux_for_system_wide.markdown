---
title: "How to configure proxy settings Linux for system wide"
layout: post
date: 2023-07-12 09:08
image: /assets/images/markdown.jpg
headerImage: false
tag:
- linux
- proxy
- vi
category: blog
author: marmojezz
description: Learn how to configure proxy settings Linux Client
---

# How to configure proxy settings Linux for system wide

1. Get superuser permission, e.g.:
    ```console
    [foo@bar ~]$ su
    Password: <type your password>
    [root@bar foo]#
    ```
2. Create new bash script file in the path /etc/profile.d/, as below:
    ```console
    [root@bar foo]# vi /etc/profile.d/proxy.sh
    ```

3. Type the following text:
    ```
    MY_PROXY_URL="prox.srv.world:3128"

    HTTP_PROXY=$MY_PROXY_URL
    HTTPS_PROXY=$MY_PROXY_URL
    FTP_PROXY=$MY_PROXY_URL
    http_proxy=$MY_PROXY_URL
    https_proxy=$MY_PROXY_URL
    ftp_proxy=$MY_PROXY_URL

    export HTTP_PROXY HTTPS_PROXY FTP_PROXY http_proxy https_proxy ftp_proxy
    ```

4. Finally, type:
    ```console
    [root@bar foo]# source /etc/profile.d/proxy.sh
    ```

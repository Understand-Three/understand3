---
title: 安装 git
aliases:
  - 安装 git
draft: true
---

```bash
opkg update  
# 安装Git  
opkg remove git  
opkg install git-http  
opkg install ca-bundle  
# 安装SSH  
opkg install openssh-client openssh-keygen openssh-sftp-server
```

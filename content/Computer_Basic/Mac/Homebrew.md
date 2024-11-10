---
title: 安装 brew
aliases:
  - 安装 brew
draft: true
---
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

# 常用命令
```bash
#安装软件
brew install name
#桌面端软件
brew cask install name
#联网搜索软件是否存在brew中
brew search name
#更新软件
brew upgrade name 
#卸载软件
brew unistall name
#重新安装软件
brew reinstall name
#查看软件安装地址
brew info name
#清理缓存
brew cleanup
#查看建议，例如升级等
brew doctor
```
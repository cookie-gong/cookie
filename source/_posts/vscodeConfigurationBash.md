---
title: vscode 配置 bash 为默认终端
date: 2022-05-27 22:36:11
author: cookie
img: ../images/26.jpg
top: false
cover: false # 表示该文章是否需要加入到首页轮播封面中
coverImg: ../images/26.jpg # 表示该文章在首页轮播封面需要显示的图片路径，如果没有，则默认使用文章的特色图片
toc: true
mathjax: false
summary: vscode
categories: vscode
tags:
  - vscode
---

### 解决方案

1、打开设置

2、搜索 shell windows

3、编辑配置

```json
"terminal.integrated.profiles.windows": {
    "GitBash": {
      "path": "F:\\git\\Git\\bin\\bash.exe" // 计算机配置git的位置
    }
  },
  "terminal.integrated.defaultProfile.windows": "GitBash"
```

4、重启生效

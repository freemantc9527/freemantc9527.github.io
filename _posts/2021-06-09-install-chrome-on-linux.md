---
layout: post
title: Linux安装chrome
category: develop
tags: [chrome, linux]
---

> 在centos上安装chrome浏览器，并以headless方式供其他程序调用

## 下载 chrome

![](/assets/images/linux-chrome/chrome_download.png)

## 安装 chrome

```bash
# 将rpm文件上传至服务器，并切换到对应目录
yum install ./google-chrome-stable_current_x86_64.rpm
```

安装过程中会增加一些依赖的安装
![](/assets/images/linux-chrome/chrome_install.png)

安装完毕后，检查是否成功
```bash
google-chrome --version
# Google Chrome 91.0.4472.77
```

## 安装 chromedriver

```bash
# 上传至服务器，解压缩
unzip chromedriver_linux64.zip

# 移动文件
mv chromedriver /usr/bin/

# 给予执行权限
chmod +x /usr/bin/chromedriver
```

*经过以上步骤，程序就可以调用`chrome`浏览器来工作了。*

***但是，浏览器现在是没有办法正常显示中文的，所以……👇***

## 安装中文字体

```bash
# 查看已安装的中文字体
fc-list :lang=zh

# 创建自己的字体目录
mkdir -p /usr/share/fonts/my_fonts

# 上传字体文件到 my_fonts 目录

# 生成字体索引
cd /usr/share/fonts/my_fonts
mkfontscale # 没有该命令，需自行安装 yum install mkfontscale

# 刷新字体缓存
fc-cache -fv # 没有该命令，需自行安装 yum install fontconfig

# 再次查看
fc-list :lang=zh
```

## 使用当中的问题

- unknown error: DevToolsActivePort file doesn‘t exist
    > 增加启动参数：no-sandbox

- 无窗口运行
    > 增加启动参数：headless

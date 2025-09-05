---
title: "OneDrive Couldn't Start. Please restart your computer and try again. Error codes: -93"
author: CYandYUE
index_img: 
date: 2025-09-05 14:07:41
tags:
- DEBUG
categories:
- DEBUG
---

## 1. Bug describe
我在Mac上安装Onedrive时，出现了登陆之后一直选定不了文件夹的情况

输出如下
```txt
OneDrive Couldn't Start
Please restart your computer and try again.
Error codes: -93
```

最后在网上查到了解决方法

## 2. Solution
不同平台的解决方法可以查阅[这里](https://support.microsoft.com/en-us/office/reset-onedrive-34701e00-bf7b-42db-b960-84905399050c#id0ebbh=mac)

我在Mac上的解决方法如下：
```txt
Select the OneDrive cloud icon in the top tray, then select Preferences > Pause > Quit OneDrive.

Find OneDrive in your Applications folder.

Control-click OneDrive and select Show Package Contents.

Navigate to the Contents > Resources folder.

Double-click ResetOneDriveApp.command (or ResetOneDriveAppStandalone.command, if you're using the standalone app).

Start OneDrive and finish the setup process.
```

## 3. Reference
[Reset OneDrive----Macrosoft](https://support.microsoft.com/en-us/office/reset-onedrive-34701e00-bf7b-42db-b960-84905399050c#id0ebbh=mac)
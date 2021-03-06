# Windows 工作环境部署

## 文档说明
- 文档名称：Windows 工作环境部署
- 文档作者：Ztj
- 作者邮箱：ztj1993#gmail.com
- 创建日期：2019-06-21
- 更新日期：2020-01-07
- 文档状态：定版

## 基本说明
- 安装 windows 10 enterprise ltsc 2019
- 推荐的计算机名称：windows, pc, job
- 以下命令需要在 PowerShell 管理员模式下执行

## 下载安装系统
- 下载地址 http://msdn.itellyou.cn/
- Windows 10 Enterprise LTSC 2019 (x64)
- Office Professional Plus 2016 (x86 and x64)
- Visio Professional 2016 (x86 and x64)
- Project Professional 2016 (x86 and x64)

## 激活系统
```
$sys32="${env:windir}/system32"
$lic16="${env:ProgramFiles(x86)}/Microsoft Office/root/Licenses16"
$off16="${env:ProgramFiles(x86)}/Microsoft Office/Office16"

# 激活系统
cscript //nologo "${sys32}/slmgr.vbs" /ipk M7XTQ-FN8P6-TTKYV-9D4CC-J462D
cscript //nologo "${sys32}/slmgr.vbs" /skms kms.03k.org
cscript //nologo "${sys32}/slmgr.vbs" /ato
cscript //nologo "${sys32}/slmgr.vbs" /dlv

# 激活 Office 2016
cscript //nologo "${sys32}/slmgr.vbs" /ilc "${lic16}/ProPlusVL_KMS_Client-ppd.xrm-ms"
cscript //nologo "${sys32}/slmgr.vbs" /ilc "${lic16}/ProPlusVL_KMS_Client-ul.xrm-ms"
cscript //nologo "${sys32}/slmgr.vbs" /ilc "${lic16}/ProPlusVL_KMS_Client-ul-oob.xrm-ms"

cscript //nologo "${sys32}/slmgr.vbs" /ilc "${lic16}/ProjectProVL_KMS_Client-ppd.xrm-ms"
cscript //nologo "${sys32}/slmgr.vbs" /ilc "${lic16}/ProjectProVL_KMS_Client-ul-oob.xrm-ms"
cscript //nologo "${sys32}/slmgr.vbs" /ilc "${lic16}/ProjectProVL_KMS_Client-ul.xrm-ms"

cscript //nologo "${sys32}/slmgr.vbs" /ilc "${lic16}/VisioProVL_KMS_Client-ppd.xrm-ms"
cscript //nologo "${sys32}/slmgr.vbs" /ilc "${lic16}/VisioProVL_KMS_Client-ul-oob.xrm-ms"
cscript //nologo "${sys32}/slmgr.vbs" /ilc "${lic16}/VisioProVL_KMS_Client-ul.xrm-ms"

cscript //nologo "${sys32}/slmgr.vbs" /ilc "${lic16}/client-issuance-bridge-office.xrm-ms"
cscript //nologo "${sys32}/slmgr.vbs" /ilc "${lic16}/client-issuance-root.xrm-ms"
cscript //nologo "${sys32}/slmgr.vbs" /ilc "${lic16}/client-issuance-root-bridge-test.xrm-ms"
cscript //nologo "${sys32}/slmgr.vbs" /ilc "${lic16}/client-issuance-stil.xrm-ms"
cscript //nologo "${sys32}/slmgr.vbs" /ilc "${lic16}/client-issuance-ul.xrm-ms"
cscript //nologo "${sys32}/slmgr.vbs" /ilc "${lic16}/client-issuance-ul-oob.xrm-ms"
cscript //nologo "${sys32}/slmgr.vbs" /ilc "${lic16}/pkeyconfig-office.xrm-ms"

cscript //nologo "${off16}/OSPP.VBS" /inpkey:XQNVK-8JYDB-WJ9W3-YJ8YR-WFG99
cscript //nologo "${off16}/OSPP.VBS" /inpkey:PD3PC-RHNGV-FXJ29-8JK7D-RJRJK
cscript //nologo "${off16}/OSPP.VBS" /inpkey:YG9NW-3K39V-2T3HJ-93F3Q-G83KT

cscript //nologo "${off16}/OSPP.VBS" /act
```

## 初始配置
```
# 允许执行远程脚本
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Force
```

## Scoop (用于安装便携软件)
```
# 配置 Scoop 目录
$env:SCOOP='D:\Scoop'
[Environment]::SetEnvironmentVariable('SCOOP', $env:SCOOP, 'User')

# 安装 Scoop
iwr -useb get.scoop.sh | iex

# 必须工具
scoop install sudo
scoop install aria2
scoop install git
scoop install openssh
scoop install curl

# 添加 extras
scoop bucket add extras

# 安装 VC++ 运行库
scoop install vcredist2005
scoop install vcredist2008
scoop install vcredist2010
scoop install vcredist2012
scoop install vcredist2013
scoop install vcredist2015
scoop install vcredist2017

# 安装常用软件
scoop install chromium
scoop install bandizip
scoop install notepadplusplus
scoop install beyondcompare
scoop install pdf-xchange-editor
scoop install pdfsam

# 安装系统工具
scoop install rufus

# 开发编程
scoop install jetbrains-toolbox
scoop install putty
scoop install postman
scoop install winscp
scoop install filezilla
scoop install sourcetree
scoop install switchhosts
```

## Choco (用于安装系统软件)
```
# 安装环境
$env:ChocolateyInstall="D:\Choco"
iwr -useb https://chocolatey.org/install.ps1 | iex

# 安装 JDK8
choco install -y jdk8

# 安装远程控制
choco install -y teamviewer

# 安装 TortoiseGit
choco install -y TortoiseGit

# 安装 VirtualBox(不兼容 Hyper-V)
choco install -y virtualbox

# 安装 VMware Workstation(不兼容 Hyper-V)
choco install -y vmwareworkstation

# 安装 Docker Toolbox
choco install -y docker-toolbox
```

## 环境安装
```
# 网站环境
scoop install nginx
scoop install apache

# 数据库环境
scoop install mysql
scoop install mongodb

# 安装 python 环境
scoop install python

# 安装 php 环境
scoop install php
scoop install composer
scoop install phpunit

# 安装 go 环境
scoop install go
scoop install protobuf
```

## 应用配置
```
# 配置 composer 源
composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/

# Notepad++ 简体中文
Settings -> Preferences... -> General -> Localization -> 中文简体
# Notepad++ Tab 转 空格
设置 -> 首选项... -> 语言 -> 制表符设置 -> 替换为空格(勾选)
```

## 推荐目录结构
```
mkdir Backup
mkdir Code
mkdir Data
mkdir Documents
mkdir Game
mkdir History
mkdir Share
mkdir Software
mkdir Temp
mkdir Virtual
```

## 常用命令
```
# 添加 VPN 客户端
iex(new-object net.webclient).downloadstring('https://dwz.cn/CxHFkLgw')

# 启用 Hyper-V, Containers
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All
Enable-WindowsOptionalFeature -Online -FeatureName Containers

# 设置端口转发
netsh interface portproxy add v4tov4 listenaddress=0.0.0.0 listenport=7379 connectaddress=127.0.0.1 connectport=6379
# 删除端口转发
netsh interface portproxy del v4tov4 listenport=7379 listenaddress=0.0.0.0
# 查看端口转发
netsh interface portproxy show v4tov4
```

## 软件命令

### Scoop
```
# 更新
scoop update <app>

# 重置
scoop reset <app>

# 卸载
scoop uninstall <app>
```

### Choco
```
# 卸载
Remove-Item -Recurse -Force "$env:ChocolateyBinRoot" -WhatIf
Remove-Item -Recurse -Force "$env:ChocolateyToolsRoot" -WhatIf
[System.Environment]::SetEnvironmentVariable("ChocolateyBinRoot", $null, 'User')
[System.Environment]::SetEnvironmentVariable("ChocolateyToolsLocation", $null, 'User')
```

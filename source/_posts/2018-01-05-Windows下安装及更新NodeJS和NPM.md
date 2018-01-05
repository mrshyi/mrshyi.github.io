---
title: Windows下安装及更新NodeJS和NPM
date: 2018-01-05 14:08:17
categories: FE
tags: [nodejs,npm]
---
## nodejs

1. 安装nodejs，直接通过官网的msi安装包安装即可；

2. 升级nodejs，直接重新下载新版本，安装会覆盖更新。

3. `node -v`


// 注意：设置npm镜像，不要使用cnpm

npm config set registry https://registry.npm.taobao.org --global

npm config set disturl https://npm.taobao.org/dist --global




## npm

1.安装npm，默认包含在nodejs的安装包中，通过安装nodejs实现安装npm\(可能版本不是最新\)；

2.更新npm，通过使用第三方包管理更新 `npm-windows-upgrade` [链接](https://github.com/felixrieseberg/npm-windows-upgrade\)


升级注意：only use this tool to upgrade npm, do not attempt to run npm install npm



`PowerShell as Administrator`

a. Set-ExecutionPolicy Unrestricted -Scope CurrentUser -Force

b. npm install --global --production npm-windows-upgrade

c. npm-windows-upgrade 或 npm-windows-upgrade --npm-version latest

d. `npm -v`


## ncu - npm-check-updates

检查\`package.json\`依赖库的最新版本



## nrm

[nrm](https://github.com/Pana/nrm) can help you easy and fast switch between different npm registries, now include: npm, cnpm, taobao, nj(nodejitsu), rednpm.

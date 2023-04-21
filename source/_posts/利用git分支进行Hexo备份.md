---
title: 利用git分支进行Hexo备份
date: 2023-04-22 03:49:02
tags: 
  - Hexo
categories: Hexo
---
# 创建分支
![创建分支.jpg](https://s2.loli.net/2023/04/22/GhsnguvADzC85B9.jpg)
在Hexo博客根目录下创建.git，最新版的Hexo在初始化之后是没有.git目录的，通过_config.yml里面的deploy参数生成.deploy_git目录，并在通过该目录进行push操作。
将Github部署的博客整个克隆下来，然后复制其中的.git目录到Hexo的根目录下。

```
git branch -a    # 查看所有分支

git branch    # 查看当前使用分支

git checkout hexo   # 切换到 hexo 分支上，若不存在则创建该分支并切换到该分支
```
# 创建.gitignore
直接在Hexo根目录下创建.gitignore排除剩下的不需要备份的文件。
```
.DS_Store
Thumbs.db
db.json
*.log
node_modules/
public/
.deploy*/
_multiconfig.yml
```
**注意：如果要连同主题文件一起备份，那么需要查看主题文件夹中是否有.git文件夹，如果有需要删除**
# 提交备份
```
git add .     # 添加当前目录

git commit -m "backup"    # 添加commit，引号内的内容随意

git push origin hexo     # 将本地数据推送到 hexo 分支中
```
远程仓库有两个分支，必须指定分支hexo，不能直接git push。

推送完成即备份完毕

# 迁移与复原
新环境重新安装Node.js，Hexo,以及主题相关依赖，插件。
```
npm install -g hexo-cli
hexo init
```
## 安装Hexo-deployer-git
```shell
npm install hexo-deployer-git --save
```

## 克隆备份分支
将原来的source，package.json，theme主题等文件克隆到Hexo根目录下
```
git clone -b hexo_backup git@github.com:[username]/[username].github.io.git
npm install   # npm i
```
## 渲染推送
```
hexo cl
hexo g
hexo d
# 生成新的页面并推送至主分支
```
主分支会利用Hexo自身集成的git组件进行推送。
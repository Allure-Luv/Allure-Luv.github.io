---
title: 博客搭建（hexo+github）
date: 2024-05-09 21:21:26
categories: 
- 博客搭建
tags: 
- hexo
- github
---

## 博客搭建基本流程（hexo + github）

### hexo环境搭建

hexo环境搭建需要下载node.js、git，下载之后在cmd中输入下面命令检查node、npm、git是否安装成功

``` bash
> node -v

> npm -v

> git -v
```

确认node.js、git安装无误后，使用git bash进行hexo的安装

``` bash
$ npm install -g hexo-cli
```

安装完成之后，创建一个博客文件夹，在git bash中输入如下命令进行初始化和本地预览

``` bash
$ hexo init                           # 初始化
$ hexo install                        # 安装组件

$ hexo generate                       # 生成页面 （可以简写为 hexo g ）
$ hexo server                         # 预览 （默认端口为4000，若被占用可以通过 -p 更换端口）
```

此时访问"localhost:4000"即可预览博客

博客文件夹目录结构：

```
- _config.yml                          # 站点配置信息  
- package.json                         # 应用程序信息  
- scaffolds                            # 模板文件  
- source                               # 存放用户源文件  
- themes                               # 存放主题文件  
- public                               # 静态网站文件
```

### 部署到github

在部署之前要确保主机通过ssh密钥域github连接，可通过如下命令进行检查

```
> ssh -T git@github.com
```

连接成功后在github中新建博客仓库，仓库名称为"username.github.io"，username为github用户名  
创建完成之后对`_config.yml`文件中的deploy部分进行如下修改，将博客部署在main分支

```
deploy:
  type: git
  repository: git@github.com:Allure-Luv/Allure-Luv.github.io.git
  branch: main
```

修改完成后，运行如下命令进行部署

``` bash
$ hexo cl
$ hexo g
$ hexo d
```

部署之后可以访问`username.github.io`来查看部署情况

## 跨设备移植博客
根据上述步骤，博客部署在main分支，利用git分支机制，将源码推送至另一分支，即可实现源码的保存  
在更换设备后，仅需要搭建hexo环境，从github中拉取源码即可，具体步骤如下：  
a. 在github中创建新的分支，这里为`gh-pages`，并将其设置为默认分支，为了每次方便上传源码  
b. 在本地拉取新创建的新分支  
c. 将文件夹中除`.git`文件之外所有文件均删除  
d. 将博客源码除`.deploy_git`文件复制到拉取的文件夹中（注意要有.gitignore文件）  
e. 将本地仓库推送至远端仓库  
注：因为git不支持嵌套，因此在github中拉取的主题中的.git文件需要删除  

## 博客资源管理
通常在 `source/images` 文件夹下可以存放文章所引用的图片，但当资源较多时，可以启用资源管理文件夹实现分组管理  
在 `_config.yml` 文件中置 `post_asset_folder` 选项为true，这样在进行博客创建的时候，会自动创建一个与文章同名的文件夹用于放置文章引用的资源  
在这种方式下，图片、链接等无法使用`markdown`语法链接，具体链接方式为：  
```
{% asset_path slug %}
{% asset_img slug [title] %}
{% asset_link slug [title] %}
```
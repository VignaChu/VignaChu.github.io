---
title: Hugo初学

cover: ./cover/Hugo1.png
date: 2025-08-26T20:12:52+08:00
lastmod: 2025-08-26T20:12:52+08:00

tags:
  - Hugo
  - Study
categories:
  - Study

math: true
mermaid: true

---

## 开头
今日我初步学习了Hugo这一博客引擎，并使用拔剑大佬制作的主题，成功搭建了自己的博客。

从今日开始我会把每天所学的内容与做出的成果都记录在这个博客里，并发布一些自己的碎碎念，
反正这里没人认识我(捏嘿嘿)。
 
## 安装
 
（本文不是教程,只是单纯的日记，全是吐槽。想看教程去下面参考资料中的网站 **‾ω‾** ）

我首先尝试使用`go install github.com/gohugoio/hugo@latest`命令安装Hugo，由于我提前安装了Go环境(五一的时候学了一点)，所以顺利安装成功。
但是在安装主题的时候，我遇到了一些问题，所以我参考了[hugo-theme-reimu主题文档](https://github.com/D-Sketon/hugo-theme-reimu?tab=readme-ov-file)
发现该主题需要扩展版的Hugo，所以我使用包管理工具中下载。但又发现需要下载TDM-GCC-64, 加环境变量后但发现无法识别，最后只能直接用编译好的extended版本*（反正总算安装完了）*直接去官方github下载后解压放到对应的文件夹(直接替换上条命令的hugo.exe即可,获取其位置可以使用用cmd命令`where hugo`)。安装完成后记得通过`hugo version`检查是否安装完成哟。

## 部署

首先创建一个文件夹，然后在该文件夹下打开命令行，输入`hugo new site myblog`命令创建站点。

之后切换到创建好的博客目录中，输入`git init`命令初始化仓库，便于主题的安装以及后续的版本管理。

然后要准备下载主题，可以从网上找一个好看的主题，我这里以官方教程的主题为例`git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke`
 
之后修改hugo.toml文件，将theme改为ananke(你主题的名称)，教程直接用的`echo "theme = 'ananke'" >> hugo.toml`指令，我这里会报错，用vscode打开看了一下发现写入的内容变乱码了，不知道为什么，于是手动修改成正确的theme = 'ananke'，就正常了。

在之后就要写页面的内容了，按照你主题的要求写md文档就行，如果没要求就直接放到content/post文件夹里就行

最上面*三个减号*之间包围的区域要写一些参数，例如写作日期失效日期，是否为草稿之类的，看官方文档就行。

之后在命令行输入`hugo server`命令启动本地服务器，然后在浏览器中输入`http://localhost:1313/`就可以看到你的博客啦。

## 配置主题

(由于我第一次看这么复杂的项目结构，所以我看了好久才看明白呜呜呜)

### 修改头像与名称

将你的头像放到static\avatar文件夹中，再修改config\_default\params.yml中的` avatar: "avatar.webp"`为你头像的名称。

修改params.yml文件中的
```yml
author: XXX
email: XXX@XXX.com
```
为你自己的名称与邮箱即可，其他自定义内容也在该文件中修改。

### 添加文章

直接在content\post 文件夹添加新的markdown文档即可，记得将模板中的_index.md复制进来，之后也要添加about.md与friend.md中的内容。
如果不指定封面图就会在data\covers.yml中随机选择一张。

### 添加页面底部一些功能

同样在params.yml中修改

### 导入网易云歌单

在params.yml中的player:中修改，修改下面的meting可以导入网易云歌单

## 部署到GitHub Pages

*不写了，明天再写，睡了Zzz*

## 参考资料
- [Hugo官网](https://gohugo.io/)
- [hugo-theme-reimu主题文档](https://github.com/D-Sketon/hugo-theme-reimu?tab=readme-ov-file)
- [Hugo｜30分钟搭建完整的个人博客](https://blog.csdn.net/weixin_35891787/article/details/145103961)
- [利用hugo从零开始建立自己的博客(本地版)](https://zhuanlan.zhihu.com/p/25223045625)
- [使用 Hugo 构建静态网站](https://blog.icytown.com/posts/web/hugo/)
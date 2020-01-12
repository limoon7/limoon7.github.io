---
title: 使用Github+hexo搭建博客
date: 2018-07-18
category: 工具
tag: 工具
author: lemon
---

#### 1、配置 Node.js 和配置 Node.js 环境
#### 2、安装Git和配置Git环境
&ensp;&ensp;&ensp;&ensp;注：本篇主要写搭建博客，工具类的不再赘述
#### 3、github配置
- 我们假设你已经有了一个 github 账号，你需要添加一个新的 new repository。点击创建一个新的 repository ，你需要将你的 Repository name 设置为 `** 账户名.github.io **` ，这一步至关重要。

- 在建好的项目右侧有个settings按钮，点击它，向下拉到GitHub Pages，你会看到一个 http://账户名.github.io 的网址，这样，你已经有一个属于自己的博客啦。
#### 4、hexo 配置
- 首先找一个合适的位置创建一个文件夹，通过 git 进入到该文件夹下
- 输入 `npm install hexo -g`，开始安装Hexo
- 输入 `hexo -v`，检查hexo是否安装成功
- 输入 `hexo init`，初始化该文件夹。看到 `** “Start blogging with Hexo！” **` 即成功
- 输入 `npm install`,安装所需组件
- 输入 `hexo g`,对文件进行编译
- 输入 `hexo s`,输入`hexo s`，开启服务器，访问该网址，正式体验Hexo。
&ensp;&ensp;&ensp;&ensp;我的默认端口是4000，如果你的页面一直无法跳转，可能是端口号被占用，可以通过 `hexo server -p 端口号` 进行修改。
#### 5、将Hexo与Github page联系起来
- 设置Git的user name和email（对于第一次设置的童鞋）
```
    git config --global user.name "xxx"
    git config --global user.email "xxx@gmail.com"
```
- 输入cd ~/.ssh，检查是否有.ssh的文件夹，输入ls，列出该文件下的内容。如果有`id_rsa,id_rsa_pub,known_hosts`,则说明存在。
- 输入 `ssh-keygen -t rsa -C "你的github邮箱地址" `,连续三个回车，生成密钥，也会自动生成两个文件：`id_rsa和id_rsa.pub`（默认存储路径是：`C:\Users\Administrator\.ssh`）
- 输入`eval "$(ssh-agent -s)"`，添加密钥到 ssh-agent
- 输入`ssh-add ~/.ssh/id_rsa`，添加生成的 SSH key 到 ssh-agent
- 登录Github，点击头像下的settings，点击 SSH and GPG keys，点击 右侧的 new SSH key，用VS Code打开id_rsa，ctrl + A 全部复制粘贴到新建的 SSH key 中。
- 输入ssh -T git@github.com，测试添加ssh是否成功。如果看到Hi后面是你的用户名，就说明成功了。
- 配置Deployment，在其文件夹中，找到_config.yml文件，修改repo值（在末尾）,配置成如下效果。
```
deploy:
  type: git
  repo: git@github.com:limoon7/limoon7.github.io.git
  branch: master
```
- 新建一篇博客，在git下执行命令：hexo new post “博客名”，这时候在文件夹_posts目录下将会看到已经创建的文件。
- 在生成以及部署文章之前，需要安装一个扩展：`npm install hexo-deployer-git --save`
- 使用编辑器编好文章，那么就可以使用命令：`hexo d g`，生成以及部署了
- 部署成功后访问你的地址：http://用户名.github.io,就可以看到你的文章啦
- 在实际的使用中，可以修改过文件后可以先在本地预览预览，通过` hexo s ` 命令
- 个人一般使用的顺序为： `hexo clean` ,`hexo g` ,`hexo s`, `hexo d`

#### 6、配置主题

&ensp;&ensp;&ensp;&ensp;是不是觉得配置好的不是很美观，那就来一个优雅大方的主题吧！
>参考资料:
- [一个简洁优雅的hexo主题 A simple and elegant theme for hexo.](https://github.com/litten/hexo-theme-yilia)
- [配置 next 主题](http://forsigner.com/fexo/)

#### 7、遇到的一些问题
- [git 连接 github 超时问题](https://www.jianshu.com/p/83fbb1828453)
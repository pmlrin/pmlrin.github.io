---
title: Hexo 博客搭建
mathjax: true
date: 2019-10-03 18:28:18
tags: 
 - Hexo
categories: 
 - Hexo
bgimg: https://cdn.jsdelivr.net/gh/Yurchiu/PicGo/mobileqq_card_pic_1699031751455.jpg
height: 20em
---

# 1. 安装 git & Node.js

请自行下载。

<https://gitforwindows.org/>

<https://nodejs.org/en/download/>

<!-- more -->

# 2. 安装 Hexo

先创建一个文件夹 blog，在这个文件夹下右键打开 git bash。如果 npm 不好用，使用 yarn。

```bash
npm install -g hexo-cli
```

初始化 Hexo。

```bash
hexo init
npm install
```

打开 Hexo 的服务，

```bash
hexo g
hexo server
```

在浏览器输入 `localhost:4000` 就可以看到你生成的博客了。

Ctrl+C 关闭。

# 3. GitHub 创建个人仓库

你先要有一个 GitHub 账户，去[注册一个吧](https://github.com/)。

创建一个和你用户名相同的仓库，**后面加 `.github.io`**

![](https://cdn.jsdelivr.net/gh/yz-hs/PicGo/%E6%90%ADhexo%20(1).png)

![](https://cdn.jsdelivr.net/gh/yz-hs/PicGo/%E6%90%ADhexo%20(2).png)

点击 create repository。

# 4. 生成 SSH 添加到 GitHub

回到 git bash 中，

```bash
git config --global user.name "yourname"
git config --global user.email "youremail"
```

这里的 yourname 输入你的 GitHub 用户名，youremail 输入你 GitHub 的邮箱。

可以用以下两条，检查一下你有没有输对。

```bash
git config user.name
git config user.email
```

然后创建 SSH,一路回车。
```bash
ssh-keygen -t rsa -C "youremail"
```

这个时候它会告诉你已经生成了 .ssh 的文件夹。在你的电脑中找到这个文件夹。

ssh，简单来讲，就是一个秘钥，其中，id_rsa 是你这台电脑的私人秘钥，不能给别人看的，id_rsa.pub 是公共秘钥，可以随便给别人看。把这个公钥放在 GitHub 上，这样当你链接 GitHub 自己的账户时，它就会根据公钥匹配你的私钥，当能够相互匹配时，才能够顺利的通过 git 上传你的文件到 GitHub 上。

而后在 GitHub 的 setting 中，找到 SSH keys 的设置选项，点击 New SSH key 把你的 id_rsa.pub 里面的信息复制进去。

```bash
ssh -T git@github.com
```
如果出现让你写 yes 或 no,写 yes。

# 5. 将 Hexo 部署到 GitHub

这一步，我们就可以将 Hexo 和 GitHub 关联起来，也就是将 Hexo 生成的文章部署到 GitHub 上，打开站点配置文件 `_config.yml`，翻到最后，修改为 YourName 就是你的 GitHub 账户

```yml
deploy:
  type: git
  repository: git@github.com:YourName/YourName.github.io.git
  branch: master
```

安装 deploy-git，也就是部署的命令,这样你才能用命令部署到 GitHub。

```bash
npm install hexo-deployer-git --save
```

然后

```bash
hexo clean
hexo generate
hexo deploy
```

其中 hexo clean 清除了你之前生成的东西，也可以不加。 hexo generate 顾名思义，生成静态文章，可以用 hexo g 缩写；hexo deploy 部署文章，可以用 hexo d 缩写

出现 `INFO  Deploy done: git` 就说明部署成功了，过一会儿就可以在 `http://yourname.github.io` 这个网站看到你的博客了。

# 6. 博客备份

为了保证我们写的文章不丢失、快速迁移博客，都需要备份我们的 blog。

1. 博客根目录，执行 `git init` 创建 git 仓库。

2. 在 github 创建仓库并和本地仓库建立联系。

3. 在`~/.bashrc` 文件中添加以下内容：

   ```
   alias hs='hexo clean && hexo g && hexo s'
   alias hd='hexo clean && hexo g && hexo d && git add . && git commit -m "update" && git push -f'
   ```

这样，执行`hs`即可启动本地服务；执行 `hd` 进行部署博客时，就一同将博客进行备份了。

# 7. 参考

https://zhuanlan.zhihu.com/p/44213627

接下来就要你自己配置了。
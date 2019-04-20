---
title: Hexo运维的那些事
date: 2019-04-20 20:20:10
tags:
	- Hexo
	- 运维
	- 博客
categories :
	- 运维
---

![view](https://user-gold-cdn.xitu.io/2019/4/20/16a3ab573ea2dc44?w=2048&h=1366&f=jpeg&s=2868013)

不轻言放弃，年轻就是要拼搏 ~ ~ 本就是一无所有，又害怕失去什么？
<!-- more -->

## Github维护Hexo
怎么把Hexo从一台服务器迁移至另一台服务器。hexo官方给了一些迁移的方法，但是我觉得最好的还是放在Github上面，这样又可以保证万无一失了。

具体思路：将Hexo博客系统中有用的一部分放在Github上面保存即可。

|   文件（夹）   |   说明   |
| ----          | ----             |
|   scaffolds/   |  博客文章的模版    |
|   themes/   |   网站的主题   |
|    source/ |    网站的页面资源    |
|  .gitignore    |  在push时需要忽略的文件和文件夹    |
|   _config.yml  |  站点配置文件    |
|    package.json  |   依赖包的名称和版本号   |


### Git操作

如果使用的主题是从GitHub克隆的，那么主题文件夹下有Git管理文件，需要将它们移除，我使用的是hexo-next，需要移除的文件如下

`rm -R themes/next/.git`

克隆gitHub上面生成的静态文件到本地

`git clone https://github.com/yourname/hexo-test.github.io.git`


创建一个叫hexo的分支

`git checkout -b hexo`

把克隆到本地的文件除了git的文件都删掉，找不到git的文件的话就到删了吧。不要用hexo init初始化。

`rm -r hexo-test.github.io`

回到本地的博客文件夹里。将上述的关键文件夹放进来，然后提交到Git上面
```shell
git add -A
git commit -m '创建hexo分支'
git push
```
效果如下: 

![文件目录](https://user-gold-cdn.xitu.io/2019/4/20/16a3ac91d1f5225a?w=1251&h=397&f=png&s=24322)

### 迁移
将hexo分支克隆下来

`git clone -b hexo https://github.com/liaohengrui/liaohengrui.github.io.git`

然后安装Hexo依赖

`npm install`

这样就可以简单的将Hexo博客迁移到任何电脑上了 : )

只是每次发表新文章要输入很多命令和密码 : (


## Hexo配置git钩子

在服务器上安装git，通过git的钩子，自动将博客部署指定目录上，让写博客更加轻松！
![架构](http://www.cnscarb.com/blog/post/323/hexo-git-hook.png)
1. 安装 git ：

	`$ sudo apt-get install git`

2. 创建一个 git 用户，用来运行 git 服务：

	`sudo adduser git`

3. 创建证书登录，将自己电脑的公钥 ~/.ssh/id_rsa.pub 文件里的内容添加到服务器的 /home/git/.ssh/authorized_keys 文件中

	Windows：C:\Users\XXX\.ssh\ XXX为用户名
4. 初始化 Git 仓库，这里将其放在 /var/repo/blog.git 目录下的：

	```shell
	sudo mkdir /var/repo
	cd /var/repo
	sudo git init --bare blog.git
	```
	使用 --bare 参数，Git 会创建一个裸仓库，裸仓库没有工作区，只为共享而存在。
	
5.  新建部署目录 /var/www/html 存储部署的内容 

	```shell
	cd /var/
	sudo mkdir www
	cd www
	sudo mkdir html
	```
	在push的时候可能会有权限问题，更改目录权限
	```shell
	cd /var/
	sudo chmod -R 777 /www
	cd www
	sudo chmod -R 777 /html
	```
	
6. 这里使用 post-receive ，这个 hook 会在整个 git 操作过程完结以后被运行。

	在 blog.git/hooks 目录下新建一个 post-receive 文件：
	
	```shell
	cd /var/repo/blog.git/hooks
	sudo vim post-receive
	```
	在 `post-receive` 文件中写入如下内容：
	```shelll
	git --work-tree=/var/www/html --git-dir=/var/repo/blog.git checkou -f
	```
	注意将 /var/www/html 换成自己的部署目录。

	上面的 git 命令可在每次 push 之后，把博客最新状态更新到部署目录中，达到自动部署的目的。

	为 post-receive 文件设置可执行权限：
	`chmod +x post-receive`
7. 本地配置
	配置 hexo 博客可以自动 deploy 到服务器上

	修改 hexo 目录下的` _config.yml `文件，找到 [deploy] 条目，并修改为：
	```
	deploy:
      type: git
      repo: git@服务器地址:/var/repo/blog.git
      branch: master
	```
8. 远程提交
	```
	hexo clean& hexo g -d
	```

[参考](https://calton007.github.io/2018/05/08/n-deploy-vps/)
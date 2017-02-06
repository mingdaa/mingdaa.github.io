---
title: Hexo + Github搭建个人独立博客  
date: 2017-02-05 20:30:18   
tags: Hexo  
---

# Hexo + Github搭建个人静态博客

- hexo出自台湾大学生tommy351之手，是一个基于Node.js的静态博客程序，其编译上百篇文字只需要几秒。hexo生成的静态网页可以直接放到GitHub Pages，BAE，SAE等平台上。
- 搭建过程你或许觉得有那么点小繁琐，但一旦搭建完成，写文章是极简单，极舒服的。
- 只需要几个简单命令，你就可以完成一切。
```
hexo n #写文章
hexo g #生成
hexo d #部署到github # 可与hexo g合并为 hexo d -g
```

---

## 环境准备
- **安装Node**  
官网[Node.js](https://nodejs.org/en/)下载相应平台的最新版本，一路安装即可。    
可参考[Node.js 安装配置](http://www.runoob.com/nodejs/nodejs-install-setup.html)  
  
- **安装Git**  
下载地址：http://git-scm.com/download/  
下载下来设置一下环境变量即可，Git_HOME，%Git_HOME%\bin之类的。  


## GitHub配置
Github官网：http://www.github.com/    
- **创建GitHub仓库**  
注册GitHub账号，创建一个以”用户名.github.io”命名的仓库，如我的用户名为mingdaa,那我的仓库名为：mingdaa.github.io。

- **配置Git**  
设置Git的用户名和邮件地址（邮箱就是你注册Github时候的邮箱），打开Git Bash,键入：  

```
$ git config --global user.name "username" # username填写Git的用户名
$ git config --global user.email "email@example.com" # email@example.com填写注册Github的邮箱
```

- **本地Git与GitHub建立联系**  
配置SSH，先检查电脑是否已经有SSH  

```
$ ls -al ~/.ssh
```
如果不存在就没有关系，如果存在的话，直接删除.ssh文件夹里面所有文件。  
输入以下指令后，一路回车就好：

```
$ ssh-keygen -t rsa -C "emailt@example.com" 
```
然后键入以下指令：

```
$ ssh-agent -s
$ ssh-add ~/.ssh/id_rsa
```

如果出现这个错误:Could not open a connection to your authentication agent，则先执行如下命令即可：

```
$ ssh-agent bash
```
再重新输入指令：

```
$ ssh-add ~/.ssh/id_rsa
```
到了这一步，就可以添加SSH key到你的Github账户了。键入以下指令，拷贝Key（先拷贝了，等一下可以直接粘贴）：

```
$ clip < ~/.ssh/id_rsa.pub
```
在github右上角点击头像–>Settings–>SSH and GPG keys–>New SSH key
Title自己随便取，然后这个Key就是刚刚拷贝的，你直接粘贴就好（也可以文本打开id_rsa.pub复制其内容），最后Add SSH key。  
最后测试一下吧，键入命令：

```
$ ssh -T git@github.com
```
设置成功应该是会显示成功提示，如下：  
![image](http://okxlor1n5.bkt.clouddn.com/ssh-T.png)


## Hexo 配置
- **初始化hexo文件夹**  
先在本地自定义一个文件夹存放Hexo相关的文件，我例如我在D盘创建了一个文件夹myBlog。  
github仓库默有master分支，用于托管生成的静态文件，再新建一个develop(名字自定)分支，用于托管后台文件，方便以后换电脑时后台文件不会丢失。  
到GitHub的用户名.github.io仓库下，复制里面的HTTPS地址。
在myBlog目录下，右键Git Bash Here: 键入git clone -b develop <刚复制HTTPS地址>

```
$ cd /d/ 
$ mkdir myBlog
$ cd myBlog
$ git clone -b develop https://github.com/mingdaa/mingdaa.github.io.git

```

- **安装Hexo**  
在Git Bash继续键入命令：  

```
$ mkdir hexo # 再创建一个hexo文件夹，安装hexo
$ cd hexo
$ npm install -g hexo
$ hexo init
$ hexo g # 或者hexo generate
$ hexo s # 或者hexo server，可以在http://localhost:4000/查看

```
注意在使用npm安装hexo的时候，如果在Git Bash中出现  

```
"sh.exe": npm: command not found
```

那么需要右击Git Bash以管理员身份运行，再次在Git Bash中输入npm install -g hexo即可。

装好之后你可以用 hexo -v 命令查看hexo的相关信息，我的hexo如下所示：
![image](http://okxlor1n5.bkt.clouddn.com/hexo-v.png)

现在已经可以本地预览博客，执行下列命令,然后到浏览器输入localhost:4000查看。

```
$ hexo g # 生成
$ hexo s # 部署到本地，启动服务
```


## Hexo配置Next主题
Next主题官网：http://theme-next.iissnan.com/  
其他相关主题配置可浏览Hexo官网上的推荐：https://hexo.io/themes/
- **复制主题**  
在hexo根目录打开Git Bash，键入：
```
$ hexo clean # 清除缓存
$ git clone https://github.com/iissnan/hexo-theme-next themes/next # 下载Next主题

```
- **启用主题**  
修改Hexo根目录下的_config.yml配置文件中的theme属性，将其设置为next。

```
theme: next
```
到此，NexT 主题安装完成。下一步我们将验证主题是否正确启用。在切换主题之后、验证之前， 我们最好使用 hexo clean 来清除 Hexo 的缓存。  

- **预览配置好的主题**  
执行下列命令,然后到浏览器输入localhost:4000查看效果了。

```
$ hexo g #生成
$ hexo s #部署到本地，启动服务
```

- **配置git仓库路径**

修改Hexo根目录下的_config.yml配置文件，找到并配置：

```
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  repo: https://git@github.com:mingdaa/mingdaa.github.io.git #仓库路径https地址
  branch: master
```
- **完成部署**
最后一步，部署到github上，键入指令：

```
$ npm install hexo-deployer-git --save
$ hexo generate
$ hexo deploy
```

输入弹出框的用户名与密码(首次使用git会弹出)。  
OK，博客已经完全搭建起来了，在浏览器输入https://mingdaa.github.io/（你的github配置的地址），就可以愉快的浏览了

最后，每次写文章输入一下命令就可以了：

```
hexo n #写文章
hexo g #生成
hexo d #部署到github # 可与hexo g合并为 hexo d -g
```

## 日常操作
- **写文章**
执行new命令，生成指定名称的文章至 \hexo\source\\_posts\文章标题.md 。

```
$ hexo new [layout] "文章标题" # 新建文章
```

然后用编辑器打开“文章标题.md”按照Markdown语法书写文章。  
其中layout是可选参数，默认值为post。到 source 目录下查看现有的layout。当然你可以添加自己的layout，
同时你也可以编辑现有的layout。

```
---
title: 文章标题 
date: 2017-01-19 16:13:10   # 日期时间
categories: 分类
tags: 标签 
---
```

- **提交**  
每次在本地对博客进行修改后，先执行下列命令提交网站相关的文件。

```
$ git add .
$ git commit -m "..."
$ git push origin develop
```

然后才执行hexo generate -d发布网站到master分支上

```
$ hexo generate -d
```

- **本地仓库丢失**  
当你想在其他电脑工作，或电脑重装系统后，安装Git与Node.js后，可以使用下列步骤：

```
# 拷贝仓库到本地
$ git clone -b develop https://github.com/mingdaa/mingdaa.github.io.git

# 配置Hexo
$ npm install -g hexo-cli
$ npm install hexo
$ npm install
$ npm install hexo-deployer-git --save

```


- **Hexo常用的几个命令**  

```
hexo new "postName" # 新建文章
hexo new page "pageName" # 新建页面
hexo generate # 生成静态页面至public目录
hexo server # 开启预览访问端口（默认端口4000，'ctrl + c'关闭server）
hexo deploy # 将.deploy目录部署到GitHub
hexo help  # 查看帮助
hexo version  # 查看Hexo的版本
hexo deploy -g  # 生成加部署
hexo server -g  # 生成加预览

#命令的简写
hexo n == hexo new
hexo g == hexo generate
hexo s == hexo server
hexo d == hexo deploy
```
---
title: 从零开始搭建Hexo博客
tags: hexo blog
---

[TOC]



# 1. What Hexo

---

> "Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 [Markdown](https://hexo.io)（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。"

最好了解一个产品的方法就是阅读__[官方文档](https://hexo.io)__，但不论是官方还是各路教程，都会遇到一些卡壳的地方导致浪费大量时间去排错，本文将逐步记录如何在Mac OS下方便快捷且__无坑__的搭建个人博客。

# 2. Why Hexo
---

### Hexo 、Jelly、Wordpress、Hugo 优势劣势、简单说明



# 3. How Hexo
---

##  前置安装

### 安装Homebrew

  __[Hombrew](https://brew.sh/)__可以方便的管理各种包以及版本管理，一个你迟早会安的软件，早安早享受，晚安没折扣。

  ```ruby
  /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
  ```

  检查

  ```shell
  brew --version
  # Homebrew 2.2.2
  # Homebrew/homebrew-core (git revision 4710; last commit 2019-12-23)
  # Homebrew/homebrew-cask (git revision dc32a; last commit 2019-12-24)
  ```

  

### 安装Xcode

前往Appstore，安装Xcode最新版，安装完成后

```shell
sudo xcode-select --switch /Applications/Xcode.app/Contents/Developer
sudo xcodebuild -runFirstLaunch
```

正常来说这是最新版的路径，如果想要切换不同版本的Xcode，需要用相应的路径替换。

### 安装NodeJs

__[NodeJs](https://nodejs.org/zh-cn/)__是Hexo依赖的环境，可以__[官网](https://nodejs.org/zh-cn/)__下载安装包，或使用Homebrew直接安装

```shell
brew install node
```

检查

```shell
node -v
# v13.4.0
npm -v
# 6.13.4  
```

### 安装Git

Git是当前最流行的版本管理工具，前往**[官网](https://git-scm.com/download/)**下载安装，或使用Homebrew直接安装

```shell
brew install git
```

检查

```shell
git --version
# git version 2.21.0 (Apple Git-122.2)
```

所有你搞不定的编译型软件安装都可以用Homebrewo迅速搞定，你还在等什么？

## 安装Hexo

基础环境已经搭建完成，终于可以开心的进入正片了，安装Hexo只需要一条Npm命令即可搞定。

```shell
npm install -g hexo-cli
```

检查

```shell
hexo version
# hexo-cli: 3.1.0
# os: Darwin 19.2.0 darwin x64
# node: 13.4.0
# v8: 7.9.317.25-node.23
# uv: 1.34.0
# zlib: 1.2.11
# brotli: 1.0.7
# ares: 1.15.0
# modules: 79
# nghttp2: 1.40.0
# napi: 5
# llhttp: 2.0.1
# openssl: 1.1.1d
# cldr: 35.1
# icu: 64.2
# tz: 2019a
# unicode: 12.1
```



- `npm install ...` 是npm的安装命令
- `hexo-cli` 表示被安装的是hexo的命令行管理工具
- `-g`表示全局安装

> 使用`npm`在正常的国内环境中下载速度会非常的慢，需要使用某些方法来解决。
>
> 1. 使用**[cnpm](https://npm.taobao.org/)**，是又淘宝团队维护的一个npm源，每十分钟更新一次。
> 2. 在`.npmrc`文件中配置国内的镜像源
> 3. 使用**[smart-npm](https://github.com/qiu8310/smart-npm)**,
> 4. 使用科学且政治正确的上网方式

具体应该使用那种加点方式呢？我推荐主4副3，1看似简单好用，但实际使用的是时候会发现有些项目结构用两种命令是不一致的，2不支持很多原生命令如`npm publish`等。

所以只有在科学的环境下，我们能体验原汁原味的npm，偶尔有波动的情况再依附源替换的方式，为了看看世界有多大，头秃的猿/媛子们，也是操碎了心。

## 建站

目前我使用的`hexo-cli`为`V 3.1.0`使用几条简单的命令即可完成建站操作

```shell
# 在当前目录下新建一个名为hexo_blog的文件夹，初始化文件结构，并自动执行npm install命令
~ hexo init hexo_blog
```

如果有发现诸如`npm ERROR`的字样，请参考之前的4种方式，搭建好后

```shell
~ cd hexo_blog
~/hexo_blog npm install
```

安装成功后执行

```shell
~/hexo_blog hexo server # 开启本地的博客服务，方便本地预览
# INFO  Start processing
# INFO  Hexo is running at http://localhost:4000 . Press Ctrl+C to stop.
```

请勿关闭终端，任意浏览器打开以上地址，回车。

Enjoy it.

## Github Page配置

既然你看到了这里，那我相信你一定不满足于自己写的东西只有自己可以看到，想用最少的代价让全世界的人都可以随意的浏览你写的文章，在当下只有我们的**[Github Pages](https://pages.github.com/)**莫属。

我会用尽可能简单的方式去讲解它的基本使用。

1. 首先，你需要有一个**[Github](https://github.com/)**账号，并登陆。

2. **[新建](https://github.com/new)**一个仓库，仓库名必须为

   `<用户名>.github.io`

   假如你的用户名是codesign，那仓库的名字应该为codesign.github.io，Github为每个用户提供了用户仓库，也就是所谓的User Page，而另一种随处可见的仓库则是Organization Page，区别方式就是通过仓库名。

3. 将你的hexo_blog文件夹上传到刚刚新建的仓库

   ```shell
   # 进入博客本地目录
   ~ cd hexo_blog
   # 在本路径进行git初始化，方便未来推送管理
   ~/hexo_blog git init
   # 将博客的推送目录设置为刚刚新建的User Page的仓库
   ~/hexo_blog git remote add origin https://github.com/your-user-name/your-user-name.github.io.git
   # 添加所有博客内容准备上传
   ~/hexo_blog git add .
   # 填写修改说明
   ~/hexo_blog git commit -m "my first commit for hexo blog"
   # 将本地博客推送到远程的master分支
   ~/hexo_blog git push -u origin master
   ```
   **【接下来的步骤至关重要】**
   
   ```shell
   # 新建一个本地分支hexo-source并推送到git，用来真正存放blog的代码
   git checkout -b hexo-source
   ~/hexo_blog git push -u origin hexo-source
   ```
   
   为什么这么做？因为官网的说明有坑，官网的思路是master存放博客代码，build出来的网页放在gh-pages分支，但Github Pages的规定是，用户页面必须存放在master分支，也就是说实际现实的博客网页应该存放在master分支，博客源代码放在另一个分支去维护，具体怎么做马上说明。

### Travis自动化打包部署（官网有坑）

对于Bloger来说，我们只关心增删查改自己的博客，而并不想每次写完博客以后，还需要`hexo generate`生成网页，再把网页push到我们的用户页面，所以我们需要一个自动化打包并部署的工具来帮我们完成这些操作，我们每次只需要修改博客的Markdown文件，并push到git，这个工具就会自动帮我们把博客页面生成好并放在用户页面。

接下来就介绍一位极其具有Geek范儿的嘉宾，**[Travis](https://travis-ci.org/)**

>  Travis是一个自动化工具，能方便的在几分钟里，全自动实现同步git代码、打包、测试、部署程序的功能。目前支持34种编程语言。

使用Travis极大程度的减轻了开发者的负担，显著延缓了发际线升高的速度，不要问我为什么知道。我们马上就来介绍如何让Travis为我们的博客工作。

4. 只需轻轻一点，即可将**[Travis CI](https://github.com/marketplace/travis-ci)**添加到你的Git账号中。

5. 在Github中**[配置Travis CI的权限](https://github.com/settings/installations)**，点击`Configure`，根据权限最小化原则，选择`Only select repositories` >> `Select repositories` >> `<your-username>.github.io` >> `Save`。

6. 正常来说你会被重定向到Travis CI的页面，或者你可以**[自行前往](https://travis-ci.com/)**。

7. 在浏览器新建一个标签页，前往 GitHub [新建 Personal Access Token](https://github.com/settings/tokens)，点击`Generate new token`，填写备注，只勾选 `repo` 的权限并点击`Generate token`按钮，生成一个新的 Token，请复制并保存好，只要拥有这个Token就代表拥有了修改你repos的权限。

8. 回到 Travis CI，前往你的 repository 的设置页面，在 `Environment Variables` 下新建一个环境变量，`Name` 为 `GH_TOKEN`，`Value` 为刚才你在 GitHub 生成的 Token。确保 `DISPLAY VALUE IN BUILD LOG` 保持 **不被勾选** 避免你的 Token 泄漏。点击 `Add` 保存。（照抄官网）

9. 在你的 Hexo 站点文件夹中新建一个 `.travis.yml` 文件（**这是官网版本，千万别用！**）：

   ```yaml
   # 这是官网版本，千万别用
   sudo: false
   language: node_js
   node_js:
     - 10 # use nodejs v10 LTS
   cache: npm
   branches:
     only:
       - master # build master branch only
   script:
     - hexo generate # generate static files
   deploy:
     provider: pages
     skip-cleanup: true
     github-token: $GH_TOKEN
     keep-history: true
     on:
       branch: master
     local-dir: public
   ```

   如果你不想知道为什么，只想赶快开始，请直接使用以下版本，并直接进入步骤10。

   ```yaml
   sudo: false
   language: node_js
   # use nodejs v10 LTS
   node_js:
     - 10 
   cache: npm
   branches:
   # build [hexo-source] branch only
     only:
       - hexo-source 
   # generate static files
   script:
     - hexo generate 
   deploy:
     provider: pages
     skip-cleanup: true
     github-token: $GH_TOKEN
     keep-history: true
     # generate static files to master, github pages must release to master.
     target_branch: master 
     on:
       branch: hexo-source
     local-dir: public
   ```

   这里我会稍微讲解一下为什么官网的版本无法配置，不敢兴趣的话可以直接进行下一步。

   首先我们来逐步讲解一下每一行的命令是在做什么

   - `sudo: false` Travis实际是运行了一个Docker，这条命令告诉Travis在容器内不要使用管理员权限
   - `language: node_js` 表示我们本次使用的语言是NodeJs
   - `node_js:` 表明了此次Docker中将会安装Node的哪个版本
   - `cache` 重复的安装依赖会浪费很多时间，使用npm的缓存可以极大的减少项目构建时间
   - `branches:` 表明对仓库分支的一些操作
   - `only:hexo-source` 表示Travis只对hexo-source这条分支进行构建
   - `script:` 表示安装完依赖后应该执行什么构建命令
   - `hexo generate` 是hexo的命令，执行后会在当前目录生成一个`public`文件夹，用来存放博客的静态页面
   - `deploy:`在这里对项目构建后的部署操作进行设置
   - `provider:pages` 设置Travis支持的特定项目的部署方式，pages表明将部署方式设定为Github Pages，所有支持的`provider`可以在**[这里](https://docs.travis-ci.com/user/deployment/)**查阅。
   - `skip-cleanup: true`字面意思，跳过清除步骤，否则Travis CI将删除在构建期间创建的所有文件，就会删除我们build出来想要上传的文件。
   - `github-token: $GH_TOKEN`设置Github仓库的权限密钥，就是我们之前生成的那一串字符。$GH_TOKEN是获取环境变量，也就是我们在Travis中的Environment Variables中配置的Name。
   - `keep-history: true`提交的时候是增量提交而不是默认的强制提交
   - `target_branch: master` **将local_dir内容推送到到master分支，默认为gh-pages。**
   - `on:branch: hexo-source`官方也没说，我理解为设置源码是在那个分支上。
   - `local-dir: public`**执行`hexo generate`命令后会在当前目录生成一个public文件夹，而`local-dir`是指定一个文件夹待会儿上传到target_branch。**

   解释完每个命令的意思，我们再回看官方文档的示例配置和我修改的配置就知道为什么说官网有坑了。

   >  **官网是把hexo的源码放在master分支，`hexo generate`生成的静态博客放在gh-pages分支。**

   > **Github Pages要求静态网页必须放在master分支。**

   这就是你跟着官网教程一步步配置后，访问`https://<your-username>.github.io`时**404 Not Found**的根本原因。

   我们做的是

   >  **增删修改博客都在本地的hexo_blog文件夹，完成后直接通过git工具push到hexo-source分支**

   >  **Travis接受到push请求，开始自动同步代码，安装依赖最近进行编译，并将生成的静态博客网页推送到master分支。**

   >  **Github Pages服务会根据master分支下的内容自动生成一个网页，所有人通过访问`<your-username>.githb.io`即可看到你写的**

10. 将 `.travis.yml` 推送到 repository 中。Travis CI 检测到有push提交，会自动开始运行，并将生成的文件推送到同一 repository 下的 `mater` 分支下

11. 前往 `https://<your-username>.github.io` 查看你的站点是否可以访问，Travis打包上传、Github Pages打包静态网页都要一定时间，请耐心等待2分钟。

### next主题








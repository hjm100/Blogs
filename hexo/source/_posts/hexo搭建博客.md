---
layout: github
title: hexo搭建博客
date: 2017-09-29 10:14:22
author: 鸿基梦
categories: web
tags: web开发技术
---

手把手教你 hexo + github搭建自己的博客以及个人主页

网上有很多这样的资料素材，但是没有一个系统化的教程

使你除了搜怎么搭建个人主页外，还要搜hexo使用教程

况且中间还可能遇到多种多样的坑

本篇文章，告诉你怎么使用github提供的空间，以及搭建自己的博客

本人亲身检测，绿色无公害；

一、环境准备

1.安装Git 下载地址：https://git-scm.com/downloads

2.安装Node.js  下载地址：https://nodejs.org/en/

3.安装hexo 

利用 npm 命令即可安装。（在任意位置点击鼠标右键，选择Git bash）

``` bash
npm install -g hexo
```
hexo安装中问题：

npm ERR! registry error parsing json 错误

可能需要设置npm代理,执行命令

``` bash
npm config set registry http://registry.cnpmjs.org
```

hexo:command not found

删除刚刚安装的npm目录，重新执行命令npm install -g hexo安装hexo， -g为全局安装

二、初始化hexo项目

1.创建hexo文件夹

安装完成后，在你喜爱的文件夹下（如H:\hexo），

执行以下指令(在H:\hexo内点击鼠标右键，选择Git bash)，

Hexo 即会自动在目标文件夹建立网站所需要的所有文件。

hexo init（初始化hexo项目）

2.安装依赖包

npm install（安装npm依赖包）

现在我们已经搭建起本地的hexo博客了

hexo命令行使用

常用命令：

``` bash
hexo help                #查看帮助
hexo init                #初始化一个目录
hexo new "postName"      #新建文章
hexo new page "pageName" #新建页面
hexo generate            #生成网页，可以在 public 目录查看整个网站的文件
hexo server              #本地预览，'Ctrl+C'关闭
hexo deploy              #部署.deploy目录
hexo clean               #清除缓存，**强烈建议每次执行命令前先清理缓存，每次部署前先删除 .deploy 文件夹**

简写（常用）：
hexo n == hexo new
hexo g == hexo generate
hexo s == hexo server
hexo d == hexo deploy
``` 
3.本地预览

执行一下命令：

hexo generate 生成网页

hexo server   本地预览

到浏览器输入localhost:4000可以看到（系统再带的博客页面）。

三、更换模板

可能系统自带的模板不满足你的需求，没关系hexo提供了很多模板供你选择

访问：https://hexo.io/themes/选择自己喜欢的模板吧！

本人选择的模板是MiHo 主题地址 http://blog.minhow.com/2017/08/01/blog/installation-configuration/

1、搭建自己喜欢的模板

1.1 安装主题

删除hexo自带的themes文件夹在hexo下clone MiHo 主题
``` bash
$ git clone https://github.com/WongMinHo/hexo-theme-miho.git themes/miho
``` 
MiHo 主题需要Hexo 3.0或以上版本，请先升级。

1.2 更新主题（提供技术支持）
``` bash
cd themes/miho
```
git pull

1.3 依赖安装

生成站点文章静态数据，用于站内搜索。
``` bash
npm install hexo-generator-json-content --save
``` 
1.4 配置主题

此处需要理解：

与themes文件同级的_config.yml文件是hexo的项目配置文件（以下定义为‘主配置’）

在themes/miho文件中的_config.yml文件是主题的配置文件（以下定义为‘主题配置’）

注：可以在_config.yml中定义变量在模板中<%- config.userurl %>引入

在主配置下找到theme属性将其定义为theme: miho即可

主配置文件属性注释：
``` bash
# Hexo Configuration
## Docs: http://hexo.io/docs/configuration.html
## Source: https://github.com/hexojs/hexo/
# Site #站点信息
title:  #标题
subtitle:  #副标题
description:  #站点描述，给搜索引擎看的
author:  #作者
email:  #电子邮箱
language: zh-CN #语言
# URL #链接格式
url:  #网址
root: / #根目录
permalink: :year/:month/:day/:title/ #文章的链接格式
tag_dir: tags #标签目录
archive_dir: archives #存档目录
category_dir: categories #分类目录
code_dir: downloads/code
permalink_defaults:
# Directory #目录
source_dir: source #源文件目录
public_dir: public #生成的网页文件目录
# Writing #写作
new_post_name: :title.md #新文章标题
default_layout: post #默认的模板，包括 post、page、photo、draft（文章、页面、照片、草稿）
titlecase: false #标题转换成大写
external_link: true #在新选项卡中打开连接
filename_case: 0
render_drafts: false
post_asset_folder: false
relative_link: false
highlight: #语法高亮
  enable: true #是否启用
  line_number: true #显示行号
  tab_replace:
# Category & Tag #分类和标签
default_category: uncategorized #默认分类
category_map:
tag_map:
# Archives
2: 开启分页
1: 禁用分页
0: 全部禁用
archive: 2
category: 2
tag: 2
# Server #本地服务器
port: 4000 #端口号
server_ip: localhost #IP 地址
logger: false
logger_format: dev
# Date / Time format #日期时间格式
date_format: YYYY-MM-DD #参考http://momentjs.com/docs/#/displaying/format/
time_format: H:mm:ss
# Pagination #分页
per_page: 10 #每页文章数，设置成 0 禁用分页
pagination_dir: page
# Disqus #Disqus评论，替换为多说
disqus_shortname:
# Extensions #拓展插件
theme: landscape-plus #主题
exclude_generator:
plugins: #插件，例如生成 RSS 和站点地图的
- hexo-generator-feed
- hexo-generator-sitemap
# Deployment #部署，将 lmintlcx 改成用户名
deploy:
  type: git
  repo: github创库地址.git （需要使用ssh）
  branch: master
```
不要担心主题配置文件有中文注释，根据提示走就可以轻松搞定

注意：主配置文件中的 url ，root配置
url: https://hjm100.github.io/Blogs
root: /Blogs

如果你想要通过https://hjm100.github.io去访问你的博客root: /
因为我的https://hjm100.github.io用来装自己的主页，所以我的博客地址架构如上

虽然选择了自己想要的主题，但是主题中显示有关主体信息，以及博客信息，看着就不舒服

特别是网页底部版权那块，教你怎么改：

修改模板标签(用于一般模板不满足个人需求)
步骤：
用文本编辑器打开 Hexo 所在的目录
打开 themes 目录
打开你想要编辑的主题所在的目录中的 layout 目录
打开 layout 目录下的 _partial 目录
打开 _partial 目录下的 footer.ejs 文件修改底部链接
post/copyright.ejs用于修改文章页脚用户链接

好了，至此，本地博客已经搭建起来了，只是本地哦，别人看不到的。下面，我们要部署到Github。


四、外网部署（为的就是省钱--哈哈）：

github为我们提供了一个放置静态资源的空间，空间不大但是足以满足你博客以及个人主页的部署

如果有后台就不行了（不过可以选择自己租服务器，一个月就50多，不差钱的同鞋可以考虑一下）

以我的为例：github放置个人主页以及博客

1.申请账号，设置公钥这些老生常谈的话题就不用多说了（直接进入主题）

2.创建代码仓库
2.1 点击加号穿件仓库New repository
2.2仓库名字格式必须为: yourname.github.io （yourname为你的账号名）
2.3进入新建的项目点击Settings设置项目找到GitHub Pages 点击change theme选择模板
这时你的项目中就有了生成文件（但是这是系统创建的）
2.4 不要删除_config.yml文件直接引入你的个人主页项目即可，默认打开index.html

ok此时你的个人主页已经搭建好了

Blogs的搭建，你可以新建一个代码仓库（把这个代码仓库设置为html）

在设置中的GitHub Pages 选择Source 中的下拉框为master branch做法与上一样！

3.仓库分析（yourname.github.io放个人主页，Blogs存放博客）

4.Blogs上传：
将主配置中的deploy属性添加一下代码，
deploy:
  type: git
  repo: 你github上的Blogs的SSH地址（注意ssh必须是系统最先生成的）
  branch: master

运行命令行
 hexo g 编译文件
 hexo d 提交文件即可

 4.发布博文
 在hexo\source\_posts文件夹下新建一个MD文件类型的文档
 或者命令行 hexo new 博文创建
``` bash
---
title: 博文  （博文标题）
date: 2017-09-27 14:49:15 （博文时间）
categories: hexo #文章文类
tags: web开发技术  （ 文章标签）
cover_picture: images/exploit.jpg(图片格式)
---
这里正常写文章即可
# 可以理解为h1(但是#后面一定要有空格)
``` bash（代码要写在这里面）
$ console.log('Hello hjm100') //这里写代码
```
``` 
注意：博文写好之后一定要先在本地查看后在提交！！！！！！
  ```bash
  语法：{{express | 过滤器名:补充说明}}（一定要放在bash中）
  ```
五、域名的配置（将github提供的二级域名与自己购买的域名绑定）：

1.可以前往腾讯购买一个域名，一般cn域名一年就20多块钱

2.点击 Github 上项目的 Settings，GitHub Pages，

提示Your site is published at http://hjm100.cn (这是我买的域名)

Custom domain下面的对话框填写你的域名即可

将独立域名与GitHub Pages的空间绑定

方法一：在站点source目录下面，新建一个名为CNAME的文本文件，

        里面写入你要绑定的域名，比如hjm100.cn

方法二：在Repository的根目录下面，新建一个名为CNAME的文本文件，

        里面写入你要绑定的域名，比如hjm100.cn

在github上面添加好自己的域名后，不要着急，此时你的域名还没有与博客完全绑定

打开cmd命令行，使用ping hjm100.github.io 查看到git对应的ip地址

前往你购买域名的平台进行ipv4域名解析，输入你ping到的域名即可，

域名解析后，去浏览器访问一下你的域名吧！就是这么神奇！！


至此你的博客已经搭建完毕了，不要感谢我，本人博客预览hjm100.cn 

域名https添加（让你的域名更加安全）

第一步首先注册一个属于自己的域名，可以选择cn域名，不贵一年就20多元
我的域名是hjm100.cn

第二步域名https添加，

1.登录这个网站并注册：https://www.cloudflare.com/（直接使用邮箱注册）

2.注册完毕后登录，如果你之前没有用过，则系统会直接显示
Add a website对话框，再次填写hjm100.cn(你的域名)点击scan DNS Records即可，
系统会自动扫描你的域名（扫描需要等待一定时间）

3.扫描完毕后点击Continue(继续)

4.添加DNS Records 
typt:CNAME类型 name：www Value:

附件小妙招：

怎么换一台电脑仍然可以使用hexo（亲测有用）

1.在Blogs这个项目中创建hexo分支用来储存开发环境（master分支用来存储生成的静态资源）

git branch hexo（新建一个hexo分支）

2.将hexo分支发布在github上(这个时候分支中可能有master分支的文件)

git push origin hexo(将代码提交到hexo分支上)

3.切换到hexo分支上（如果有文件就清空分支中的内容除了.git文件）

git checkout hexo（切换到hexo分支上）

4.整理你的开发环境hexo,修改hexo下面的.gitignore(限制git上传)文件

``` bash
db.json
*.log
node_modules/
public/
.deploy*/
```
5.删除themes-->miho文件中的 .git文件以及.gitignore

6.将你上述修改的hexo文件提交到hexo分支里面（不要改错奥）
在hexo分之下即可
git add .
git commit .
git push origin hexo

7.当你换电脑的时候，配置公钥以及全局安装npm install -g hexo（请参考以上说明）
下载的分支默认显示的是master分支，请切换到hexo分支，
cd hexo（进入到hexo文件）执行npm install 安装node模块，按照以上写博客提交博客即可同步

8.切结，修改过hexo文件中的内容后记得提交hexo分支，以免你再次换电脑的时候使用

建议使用最新的git版本以及Node版本，如有问题请留言！！！！
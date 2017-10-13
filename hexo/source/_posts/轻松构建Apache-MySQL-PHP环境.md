---
title: 轻松构建Apache+MySQL+PHP环境
date: 2017-10-13 14:01:08
author: 鸿基梦
categories: 开发
tags: 开发技术
---

||--如何使用集成工具调试你的php项目，以及搭建你的数据库--||

**本人选用的工具是：（好用如此简单）**

  |--> XAMPP（Apache+MySQL+PHP+PERL）是一个功能强大的建站集成软件包。
  |--> Navicat for MySQL是一套管理和开发MySQL或MariaDB的理想解决方案，支持单一程序，可同时连接到MySQL和MariaDB。
  |--> 这两个软件非常容易得到：Navicat(下载的都是试用版-->我们可以使用破解工具对其破解)
    |-->破解工具（PatchNavicat.exe）的使用：
    |-->安装Navicat for MySQL成功后（记着安装的目录，破解有用）
    |-->打开PatchNavicat.exe
    |-->选择D:\nv\Navicat for MySQL\navicat.exe
    |-->打开即可（不要怀疑就是如此简单）
    |-->中文破解版Navicat for MySQL百度云分享地址:http://pan.baidu.com/s/1mi3etny 密码：vgig
    |-->附加PatchNavicat.exe奥 Y(^_^)Y

一、配置XAMPP：（本人默认将其安装到D:\xampp文件夹下）

  1.将需要运行的项目放在D:\xampp\htdocs文件夹下
  2.配置Apache服务：（注意：在httpd.conf文件中 #后面的为注释）
  -->（1）打开D:\xampp\apache\conf\httpd.conf这个文件
  -->（2）在57行左右 --> 可以添加多端口 --> Listen 80(默认是80端口)多个端口是为了运行多个项目
  -->（3）在250行左右-->可以修改默认的运行文件地址即（D:/xampp/htdocs）
          |-->DocumentRoot "D:/xampp/htdocs"
          |--><Directory "D:/xampp/htdocs">
          |-->如果你的文件都存放在D:/work目录下文件少的话还可以复制拷贝，如果文件太多的话文件迁移也是个麻烦事
          |-->所以你可以自己修改运行文件地址(将上面的两处如下修改即可) |--> 【注意：如果是从地址栏直接拷贝的话需要将反斜杠变为斜杠】
          |-->DocumentRoot "D:/work"
          |--><Directory "D:/work">
  -->（4）配置服务：在文件的最后添加我们的代码（切记不要随意修改文件）两种配置方式
          |-->（1）#配置同域名多端口使用（同域名即为127.0.0.1）
                 |-> 例子：配置127.0.0.1:8080用来访问D:\xampp\htdocs\sharkItOff的项目
                 |->（默认会找www文件下的index.html或者index.php）
                 |-><virtualhost *:8080>
                 |->    ServerName localhost
                 |->    DocumentRoot D:\xampp\htdocs\sharkItOff
                 |-></virtualhost>

          |-->（2）#配置多域名(需要配合C:\Windows\System32\drivers\etc\hosts文件使用)
                 |->（hosts用来配置本机的域名）
                 |-> 例子：配置angular.hjm.com用来访问D:\xampp\htdocs\webnotes\Angular2的项目
                 |-> # Angular2 #
                 |-><virtualhost *:80>
                 |->    ServerName angular.hjm.com
                 |->    DocumentRoot D:\xampp\htdocs\webnotes\Angular2
                 |-></virtualhost>
  3.重启apache服务后即可使用上述域名访问我们的项目了

备注：（巧妙使用hosts文件）
    --> 配置文件地址：C:\Windows\System32\drivers\etc\hosts文件(本机域名配置)
    -->使用：notepad++编辑器打开这个文件（也可以使用笔记本-->保存的时候可能要管理员）但是
    -->使用notepad++就不需要了，直接可以保存，就是这么神奇，在hosts文件最后面添加自己设置的域名
    -->配置案例：127.0.0.1 angular.hjm.com (尝试一下吧在浏览器输入angular.hjm.com即可访问Angular2这个项目了)

Y(^_^)Y 就是这么简单，项目就这样可以运行了 Y(^_^)Y

二、Navicat for MySQL创建数据库(如果php项目中有数据库本地数据库的访问需要先打开XAMPP的MySQl->连接->打开数据库)
  1. --> 打开Navicat for MySQL这个软件
     --> 点击链接
     --> 填写连接名（主机以及端口，用户名，密码==>都不填）
     --> 点击链接测试
     --> 成功后点击确定
  2.在生成的链接下新建一个数据库 
     --> 数据名自起
     --> 字符集选择utf8 -- UTF-8 Unicode（如果不选会乱码）
     --> 排序规则选择utf8_general_ci
  3.如果没有数据库文件就直接新建表（建表一定要有主键：详细内容不过多描述）
  4.如果有sql文件就可以导入
     -->（点绿数据库）右键 
     --> 选择运行SQL文件 
     --> 在文件后面选择我们要运行的文件就可以了

总结一下数据库有关操作（待定） 

三、起动XAMPP的Apache和MySQl
     --> 打开XAMPP
     --> XAMPP Control Panel这个运行文件
     --> 点击Apache后面的Start（start开始：stop停止）等到Apache背景变绿色-->开启成功
     --> 点击MySQl后面的Start（start开始：stop停止）等到MySQl背景变绿色-->开启成功

注意：（看书百遍，不如动手）
使用中可能会遇到多种问题，可以查找相关资料解决，或者留言给我，我们共同解决这些问题！